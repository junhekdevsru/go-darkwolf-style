# DW-18: Explicit model conversions

- Use exported DTO fields and keep entity fields private. Put transport tags on the transport representation.
- Name conversions NewXFromDomain, ToDomain, ToApplication, and NewXFromApplication. Keep them beside the receiving representation.
- Take ownership of copies returned by domain accessors directly; clone mutable input only when it is borrowed. Preserve the established nil-input contract.

```go
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
		Tags: record.Tags(),
	}
}
```
