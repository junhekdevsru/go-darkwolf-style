# DW-25: Behavioral tests and handwritten doubles

- Prefer testing and focused handwritten stubs or memory implementations; extend the target project's existing test stack.
- Use t.Helper for setup and table cases for input variants. Check ownership, failed-change rollback, event ordering, and wrapped errors when the change touches them.
- Test observable results. Keep failure messages concrete; use t.Fatal or t.Fatalf for failed prerequisites.

```go
import (
	"context"
	"testing"
)

func newTestRecord(t *testing.T) *Record {
	t.Helper()
	record, err := NewRecordBuilder().SetName("before").SetTags([]string{"owned"}).Build()
	if err != nil {
		t.Fatal(err)
	}
	return record
}

func TestRecordMutatorPreservesOriginalOnError(t *testing.T) {
	record := newTestRecord(t)
	before := record.Clone()
	if err := NewRecordMutator(record).SetName("").Mutate(); err == nil {
		t.Fatal("expected validation error")
	}
	if !record.Equal(before) {
		t.Fatal("failed mutation changed record")
	}
}

type recordReadRepositoryStub struct{ record *Record }

func (r *recordReadRepositoryStub) Get(_ context.Context, _ RecordID) (*Record, error) {
	if r.record == nil {
		return nil, ErrRecordNotExist
	}
	return r.record.Clone(), nil
}
```
