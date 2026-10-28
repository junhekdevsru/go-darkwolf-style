# DW-15: Command and query declarations

- Keep the input type, typed handler interface, private implementation, constructor, and Handle method together.
- Name commands by action and queries GetX, ListX, or CountX. Put ctx first in Handle.
- Use the existing generic handler contract when present; preserve the same declaration shape with an ordinary interface otherwise.

```go
import (
	"context"
	"fmt"
)

type GetRecord struct{ ID RecordID }

type GetRecordHandler interface {
	Handle(ctx context.Context, query *GetRecord) (*RecordView, error)
}

type getRecordHandler struct{ recordRepository RecordReadRepository }

func (h *getRecordHandler) Handle(ctx context.Context, query *GetRecord) (*RecordView, error) {
	record, err := h.recordRepository.Get(ctx, query.ID)
	if err != nil {
		return nil, fmt.Errorf("failed to get record: %w", err)
	}
	return NewRecordViewFromDomain(record), nil
}
```
