# DW-02: Builder declaration and result

- Name the type XBuilder, the constructor NewXBuilder, and chainable setters SetX(value). Use b as the receiver.
- Store the assembled value in a private field. Copy mutable setter inputs; Build returns an independent value.
- Call Validate once the value is assembled. Return (T, error) only when construction can fail; keep simple value constructors simple.

```go
import "slices"

type RecordBuilder struct{ record Record }

func NewRecordBuilder() *RecordBuilder { return &RecordBuilder{} }

func (b *RecordBuilder) SetName(value string) *RecordBuilder {
	b.record.name = value
	return b
}

func (b *RecordBuilder) SetTags(value []string) *RecordBuilder {
	b.record.tags = slices.Clone(value)
	return b
}

func (b *RecordBuilder) Build() (*Record, error) {
	record := b.record.Clone()
	if err := record.Validate(); err != nil {
		return nil, err
	}
	return record, nil
}
```
