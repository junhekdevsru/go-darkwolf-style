# DW-01: Private state and named accessors

- Keep entity fields unexported; expose properties as ID(), Name(), and CreatedAt(), without a Get prefix.
- Use Is… and Has… for predicates. Keep scalar accessors compact; put state changes in named operations.
- Use exported fields for DTOs. An entity is not a transport payload.

```go
type Record struct {
	id      RecordID
	name    string
	enabled bool
}

func (r *Record) ID() RecordID    { return r.id }
func (r *Record) Name() string    { return r.name }
func (r *Record) IsEnabled() bool { return r.enabled }
```
