# DW-19: Typed query construction

- Express filtering and ordering with the domain query fields; keep storage column names in the adapter.
- Build queries with chained Where, OrderBy, WithOffset, and WithLimit calls. Prepare repeated queries using the existing PrepareQuery contract.
- Extend the query vocabulary already present in the target code.

```go
import (
	"context"
	"fmt"
)

func (h *listRecordsHandler) Handle(ctx context.Context, query *ListRecords) (Records, error) {
	recordQuery := NewRecordQuery().
		Where(RecordQueryNode.Enabled.Equals(true)).
		OrderBy(RecordQueryNode.ID.Asc()).
		WithOffset(query.Offset).
		WithLimit(query.Limit)
	records, err := h.recordRepository.List(ctx, recordQuery)
	if err != nil {
		return nil, fmt.Errorf("failed to list records: %w", err)
	}
	return records, nil
}
```
