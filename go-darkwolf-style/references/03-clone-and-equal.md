# DW-03: Clone, Equal, and ownership

- Implement nil-safe Clone and Equal on optional pointer models. Compare time.Time values with Equal.
- Return copies of mutable fields and clone mutable children recursively. A slice of pointers needs element copies too.
- Preserve meaningful nil/empty distinctions. Use a modern copying helper when supported by the target Go version.

```go
import "slices"

type Record struct {
	name string
	tags []string
}

func (r *Record) Tags() []string { return slices.Clone(r.tags) }

func (r *Record) Clone() *Record {
	if r == nil {
		return nil
	}
	clone := *r
	clone.tags = slices.Clone(r.tags)
	return &clone
}

func (r *Record) Equal(other *Record) bool {
	if r == nil || other == nil {
		return r == nil && other == nil
	}
	return r.name == other.name && slices.Equal(r.tags, other.tags)
}
```
