# DW-20: Repository update callbacks

- Use a named XUpdateFunc func(*X) error and an Update(ctx, id, updateFn) method.
- Own the lock or concurrency check and transaction in the adapter. Read, clone, call updateFn, validate, compare, then persist.
- Keep begin/commit/rollback in the transaction helper. Return ErrXUnchanged according to the repository contract.

```go
import (
	"context"
	"errors"
)

type RecordUpdateFunc func(record *Record) error

func (r *RecordWriteRepository) Update(ctx context.Context, id RecordID, updateFn RecordUpdateFunc) error {
	if id.IsZero() {
		return errors.New("zero id")
	}
	if updateFn == nil {
		return errors.New("nil updateFn")
	}
	return RunTransaction(r.db, ctx, func(tx Transaction) error {
		record, err := tx.GetRecordForUpdate(ctx, id)
		if err != nil {
			return err
		}
		before := record.Clone()
		if err := updateFn(record); err != nil {
			return err
		}
		if err := record.Validate(); err != nil {
			return err
		}
		if record.Equal(before) {
			return ErrRecordUnchanged
		}
		return tx.SaveRecord(ctx, record)
	})
}
```
