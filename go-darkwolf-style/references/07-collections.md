# DW-07: Named domain collections

- Use the plural type name: Records, Photos, or Signals.
- Put collection operations on that type. Clone each mutable element; expose IsEmpty when callers need it.
- Preserve nil as nil and a non-nil empty collection as non-nil empty when cloning.

```go
type Records []*Record

func (r Records) Clone() Records {
	if r == nil {
		return nil
	}
	records := make(Records, len(r))
	for i, record := range r {
		records[i] = record.Clone()
	}
	return records
}

func (r Records) IsEmpty() bool { return len(r) == 0 }
```
