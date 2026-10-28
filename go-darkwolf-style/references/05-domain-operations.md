# DW-05: Named domain operations

- Use verbs such as Enable(), Disable(), and MakeProcessed(); keep transition checks on the entity.
- Return a named sentinel for a recognizable invalid transition. Check before assigning state.
- Update the relevant timestamp as part of the successful transition.

```go
import (
	"errors"
	"time"
)

var ErrRecordEnabled = errors.New("record already enabled")

type Record struct {
	enabled   bool
	updatedAt time.Time
}

func (r *Record) Enable() error {
	if r.enabled {
		return ErrRecordEnabled
	}
	r.enabled = true
	r.updatedAt = time.Now().UTC()
	return nil
}
```
