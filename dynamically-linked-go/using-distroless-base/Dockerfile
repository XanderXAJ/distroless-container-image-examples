# syntax=docker/dockerfile:1.4

# -=== Builder image ===-
FROM golang:1 as builder

WORKDIR /app

COPY <<EOF main.go
package main

import (
  "fmt"
  "os/user"
)

func main() {
    u, err := user.Current()
    if err != nil {
        panic(err)
    }
    fmt.Println("Hello from", u.Username)
}
EOF

RUN CGO_ENABLED=1 go build main.go

# -=== Target image ===-
FROM gcr.io/distroless/base

COPY --from=builder /app/main /

CMD ["/main"]
