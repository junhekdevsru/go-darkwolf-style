# DW-18: Explicit model conversions

- Use exported DTO fields and keep entity fields private. Put transport tags on the transport representation.
- Name conversions NewXFromDomain, ToDomain, ToApplication, and NewXFromApplication. Keep them beside the receiving representation.
- Copy mutable values into the receiving representation. Preserve the established nil-input contract.

```go
import "slices"

type RecordView struct {
	ID   RecordID
	Name string
	Tags []string
}

func NewRecordViewFromDomain(record *Record) *RecordView {
	if record == nil {
		return nil
	}
	return &RecordView{
		ID:   record.ID(),
		Name: record.Name(),
		Tags: slices.Clone(record.Tags()),
	}
}
```
