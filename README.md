# Package Safe

[![Go Reference](https://pkg.go.dev/badge/github.com/mbranch/safe-go.svg)](https://pkg.go.dev/github.com/mbranch/safe-go)
[![Go Report Card](https://goreportcard.com/badge/github.com/mbranch/safe-go)](https://goreportcard.com/report/github.com/mbranch/safe-go)

Package safe provides helpers for gracefully handling panics in background
goroutines[^1].

## Example Usage

```golang
import (
  "context"
  "fmt"

  "github.com/mbranch/safe-go"
)

func main() {
  ctx := context.Background()

  items := []int{1, 2, 3, 4, 5}

  g, groupCtx := safe.GroupWithContext(ctx)
  for _, item := range items {
    i := item
    g.Go(func() error {
      return processItem(groupCtx, i)
    })
  }

  err := g.Wait()
  if err != nil {
    fmt.Println("error", err)
  }
}
```

[^1]:
    This repo is a copy (not a fork) of [github.com/deliveroo/safe-go](https://github.com/deliveroo/safe-go) which was
    deleted. It will be maintained separately from the original repo.
