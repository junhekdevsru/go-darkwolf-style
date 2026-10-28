# DW-09: Independent validation errors

- Collect independent failures in var errs []error and return errors.Join(errs...).
- Finish validation before dependent work. Return a single error directly when only one check is needed.

```go
import "errors"

type Record struct {
	id   RecordID
	name string
}

func (r *Record) Validate() error {
	if r == nil {
		return errors.New("nil record")
	}
	var errs []error
	if r.id.IsZero() {
		errs = append(errs, errors.New("zero id"))
	}
	if r.name == "" {
		errs = append(errs, errors.New("empty name"))
	}
	return errors.Join(errs...)
}
```
