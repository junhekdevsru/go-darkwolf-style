# DW-06: Named IDs and closed statuses

- Use distinct named types; name conversions NewXFromString or NewXFromInt64.
- Provide the relevant IsZero, Equal, String, and primitive conversion methods. Check lossy numeric conversions.
- Represent statuses with a private slug, named values, a checked conversion, and IsX predicates. Extend an existing enum registry when present.

```go
import (
	"errors"
	"fmt"
	"strconv"
)

type RecordID uint64

func NewRecordIDFromInt64(value int64) (RecordID, error) {
	if value < 0 {
		return 0, fmt.Errorf("negative value: %d", value)
	}
	return RecordID(value), nil
}

func (id RecordID) IsZero() bool              { return id == 0 }
func (id RecordID) Equal(other RecordID) bool { return id == other }
func (id RecordID) String() string            { return strconv.FormatUint(uint64(id), 10) }

type RecordStatus struct{ slug string }

var (
	RecordStatusEnabled  = RecordStatus{"enabled"}
	RecordStatusDisabled = RecordStatus{"disabled"}
)

func NewRecordStatusFromString(value string) (RecordStatus, error) {
	switch value {
	case "":
		return RecordStatus{}, nil
	case RecordStatusEnabled.slug:
		return RecordStatusEnabled, nil
	case RecordStatusDisabled.slug:
		return RecordStatusDisabled, nil
	default:
		return RecordStatus{}, errors.New("unknown RecordStatus: " + value)
	}
}

func (s RecordStatus) IsZero() bool                  { return s == RecordStatus{} }
func (s RecordStatus) IsEnabled() bool               { return s == RecordStatusEnabled }
func (s RecordStatus) Equal(other RecordStatus) bool { return s == other }
func (s RecordStatus) String() string                { return s.slug }
```
