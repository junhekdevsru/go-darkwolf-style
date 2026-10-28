# DW-11: Explicit constructor dependencies

- Take required collaborators as named parameters; store them in private fields.
- Validate required dependencies before constructing the result. Put an explicit logger after functional dependencies.

```go
import (
	"errors"
	"log/slog"
)

func NewRenameRecordHandler(
	recordRepository RecordWriteRepository,
	eventBus Publisher,
	logger *slog.Logger,
) (RenameRecordHandler, error) {
	var errs []error
	if recordRepository == nil {
		errs = append(errs, errors.New("nil recordRepository"))
	}
	if eventBus == nil {
		errs = append(errs, errors.New("nil eventBus"))
	}
	if logger == nil {
		errs = append(errs, errors.New("nil logger"))
	}
	if err := errors.Join(errs...); err != nil {
		return nil, err
	}
	return &renameRecordHandler{
		recordRepository: recordRepository,
		eventBus:         eventBus,
		logger:           logger,
	}, nil
}
```
