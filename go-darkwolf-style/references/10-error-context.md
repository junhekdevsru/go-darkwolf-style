# DW-10: Sentinels and error context

- Name recognizable states ErrXExist, ErrXNotExist, or ErrXUnchanged and use errors.Is or errors.As.
- Translate adapter errors at the adapter; wrap useful operation context with %w.
- Use concise English messages such as cannot convert … and failed to update …. Propagate directly when another wrapper adds no context.

```go
import (
	"context"
	"errors"
	"fmt"
)

var ErrRecordNotExist = errors.New("record does not exist")

func (r *RecordReadRepository) Get(ctx context.Context, id RecordID) (*Record, error) {
	record, err := r.storage.Load(ctx, id)
	if errors.Is(err, ErrNoRows) {
		return nil, ErrRecordNotExist
	}
	if err != nil {
		return nil, fmt.Errorf("failed to load record: %w", err)
	}
	return record, nil
}
```
