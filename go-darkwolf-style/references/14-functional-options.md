# DW-14: Optional module settings

- Use type Option func(*implementation) and WithX functions; keep required collaborators as constructor parameters.
- Apply options, establish defaults, then validate. Follow the existing fallible-option signature if options can fail.

```go
import (
	"errors"
	"time"
)

type server struct {
	addr            string
	shutdownTimeout time.Duration
}
type Option func(*server)

func WithAddr(value string) Option {
	return func(s *server) { s.addr = value }
}

func WithShutdownTimeout(value time.Duration) Option {
	return func(s *server) { s.shutdownTimeout = value }
}

func NewServer(options ...Option) (*server, error) {
	server := &server{shutdownTimeout: 10 * time.Second}
	for _, option := range options {
		option(server)
	}
	if server.addr == "" {
		return nil, errors.New("empty addr")
	}
	return server, nil
}
```
