# DW-21: Old and new event snapshots

- Capture old state before mutation and new state afterward. Use independent application DTOs in the payload.
- Publish after the repository update succeeds; wrap publication errors with the event name.
- Preserve the application's retry and delivery contract; write followed by publish does not itself provide an atomic delivery guarantee.

```go
import (
	"context"
	"fmt"
)

type RecordRenamed struct{ OldRecord, NewRecord *RecordView }

func (h *renameRecordHandler) Handle(ctx context.Context, command *RenameRecord) error {
	var oldRecord, newRecord *RecordView
	if err := h.recordRepository.Update(ctx, command.ID, func(record *Record) error {
		oldRecord = NewRecordViewFromDomain(record.Clone())
		if err := NewRecordMutator(record).SetName(command.Name).Mutate(); err != nil {
			return err
		}
		newRecord = NewRecordViewFromDomain(record.Clone())
		return nil
	}); err != nil {
		return fmt.Errorf("failed to rename record: %w", err)
	}
	if err := h.eventBus.Publish(ctx, &RecordRenamed{
		OldRecord: oldRecord,
		NewRecord: newRecord,
	}); err != nil {
		return fmt.Errorf("failed to publish RecordRenamed event: %w", err)
	}
	return nil
}
```
