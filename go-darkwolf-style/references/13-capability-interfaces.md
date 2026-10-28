# DW-13: Read, write, and event capabilities

- Declare read and write repository capabilities separately and embed them in the full repository.
- Depend on the capability actually used: read for queries, write for commands, Publisher for producers, Subscriber for subscriptions.

```go
import "context"

type RecordReadRepository interface {
	Get(ctx context.Context, id RecordID) (*Record, error)
	List(ctx context.Context, query RecordQuery) (Records, error)
	Count(ctx context.Context, query RecordQuery) (int, error)
}

type RecordWriteRepository interface {
	Create(ctx context.Context, record *Record) error
	Update(ctx context.Context, id RecordID, updateFn RecordUpdateFunc) error
	Delete(ctx context.Context, id RecordID) error
}

type RecordRepository interface {
	RecordReadRepository
	RecordWriteRepository
}
```
