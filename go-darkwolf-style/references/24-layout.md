# DW-24: Formatting, imports, and chains

- Run gofmt. Group standard-library, module-local, and external imports unless the configured formatter specifies another order.
- Alias colliding package names by role. Keep simple getters compact and fluent calls one step per line.
- Align declarations with gofmt; group related constants, variables, and type aliases where they form one set.

```go
package application

import (
	"fmt"

	domainmodel "example/model"
)

func NewRecord(name string) (*domainmodel.Record, error) {
	record, err := domainmodel.NewRecordBuilder().
		SetName(name).
		Build()
	if err != nil {
		return nil, fmt.Errorf("cannot create record: %w", err)
	}
	return record, nil
}
```
