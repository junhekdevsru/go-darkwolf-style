# DW-23: Names, receivers, and files

- Use domain nouns for models, plural nouns for collections, and action names for commands.
- Spell dependencies by role: recordRepository, eventBus, logger. Use short receivers b, m, h, r, and s for those established roles.
- Use snake_case filenames with purpose suffixes such as record_builder.go and record_read_repository.go. Follow the target project's comment language.

```go
import "context"

type RenameRecord struct {
	ID   RecordID
	Name string
}
type Records []*Record

type renameRecordHandler struct {
	recordRepository RecordWriteRepository
	eventBus         Publisher
}

func (h *renameRecordHandler) Handle(ctx context.Context, command *RenameRecord) error {
	return h.recordRepository.Rename(ctx, command.ID, command.Name)
}
```
