# DW-12: Interface and implementation declarations

- Use an exported capability interface and a private implementation; keep the compile-time assertion beside the implementation.
- Return the useful interface or the established concrete type from NewX. Concrete adapter types may be exported.

```go
import "context"

type Indexer interface {
	Run(ctx context.Context) error
}

var _ Indexer = (*indexer)(nil)

type indexer struct{ store Store }

func (i *indexer) Run(ctx context.Context) error {
	return i.store.Rebuild(ctx)
}
```
