# DW-16: Handler and service composition

- Embed typed handler capabilities in the private service and delegate the named service methods to Handle.
- Compose the full service through interface embedding. Add intermediate services only for capabilities the module exposes.

```go
import "context"

type RecordQueryService interface {
	GetRecord(ctx context.Context, query *GetRecord) (*RecordView, error)
}

var _ RecordQueryService = (*recordQueryService)(nil)

type recordQueryService struct{ GetRecordHandler }

func (s *recordQueryService) GetRecord(ctx context.Context, query *GetRecord) (*RecordView, error) {
	return s.GetRecordHandler.Handle(ctx, query)
}

type RecordService interface {
	RecordQueryService
	RecordCommandService
}

type recordService struct {
	*recordQueryService
	*recordCommandService
}

var _ RecordService = (*recordService)(nil)
```
