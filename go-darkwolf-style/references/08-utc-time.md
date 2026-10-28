# DW-08: Stored timestamps in UTC

- Normalize stored timestamps with UTC() at assignment in constructors, setters, and transitions.
- Use the same timestamp for fields belonging to one operation. Compare instants with time.Time.Equal.

```go
import "time"

type Record struct{ createdAt, updatedAt time.Time }
type RecordBuilder struct{ record Record }

func (b *RecordBuilder) SetCreatedAt(value time.Time) *RecordBuilder {
	b.record.createdAt = value.UTC()
	return b
}

func (b *RecordBuilder) SetUpdatedAt(value time.Time) *RecordBuilder {
	b.record.updatedAt = value.UTC()
	return b
}

func (r *Record) HasSameUpdateTime(other *Record) bool {
	return r.updatedAt.Equal(other.updatedAt)
}
```
