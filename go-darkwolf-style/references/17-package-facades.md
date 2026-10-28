# DW-17: Parent-package facades

- Use grouped type aliases to expose child-package types without creating a new type identity.
- Forward constructors as functions. Keep facades in purpose-named files such as models.go, queries.go, and repositories.go.

```go
package domain

import "example/model"

type (
	Record        = model.Record
	RecordBuilder = model.RecordBuilder
	RecordMutator = model.RecordMutator
	Records       = model.Records
)

func NewRecordBuilder() *RecordBuilder { return model.NewRecordBuilder() }

func NewRecordMutator(record *Record) *RecordMutator {
	return model.NewRecordMutator(record)
}
```
