# DW-04: Collected mutations and commit

- Name the type XMutator and finish with Mutate() error. Collect changes through chainable SetX methods.
- Capture copies of mutable inputs at the setter. Apply the collected operations to Clone(), then Validate(), then assign the result back.
- Return before assigning on any error. Keep synchronization outside this object-level commit.

```go
import "errors"

type RecordMutation func(record *Record) error

type RecordMutator struct {
	record    *Record
	mutations []RecordMutation
}

func NewRecordMutator(record *Record) *RecordMutator {
	return &RecordMutator{record: record}
}

func (m *RecordMutator) SetName(value string) *RecordMutator {
	m.mutations = append(m.mutations, func(record *Record) error {
		record.name = value
		return nil
	})
	return m
}

func (m *RecordMutator) Mutate() error {
	if m == nil || m.record == nil {
		return errors.New("nil record")
	}
	mutatedRecord := m.record.Clone()
	var errs []error
	for _, mutation := range m.mutations {
		if err := mutation(mutatedRecord); err != nil {
			errs = append(errs, err)
		}
	}
	if err := errors.Join(errs...); err != nil {
		return err
	}
	if err := mutatedRecord.Validate(); err != nil {
		return err
	}
	*m.record = *mutatedRecord
	return nil
}
```
