# DW-22: Logging through decorators

- Apply shared logging and tracing around the typed handler. Keep operation-specific diagnostics in the operation.
- Use slog with context and structured attributes. Keep body serialization behind the existing debug policy.

```go
import (
	"context"
	"log/slog"
	"time"
)

type CommandHandler[C any] interface {
	Handle(ctx context.Context, command C) error
}

type commandLogger[C any] struct {
	handler CommandHandler[C]
	logger  *slog.Logger
}

func ApplyCommandDecorators[C any](handler CommandHandler[C], logger *slog.Logger) CommandHandler[C] {
	return &commandLogger[C]{handler: handler, logger: logger}
}

func (d *commandLogger[C]) Handle(ctx context.Context, command C) error {
	startedAt := time.Now()
	err := d.handler.Handle(ctx, command)
	if err != nil {
		d.logger.ErrorContext(ctx, "command failed", "err", err, "duration", time.Since(startedAt))
	} else {
		d.logger.DebugContext(ctx, "command completed", "duration", time.Since(startedAt))
	}
	return err
}
```
