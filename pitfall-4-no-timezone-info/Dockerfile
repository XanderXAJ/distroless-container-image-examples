# syntax=docker/dockerfile:1.4

# -=== Builder image ===-
FROM golang:1 as builder

WORKDIR /app

COPY <<EOF main.go
package main

import (
  "fmt"
  "time"
)

func main() {
  loc, err := time.LoadLocation("Europe/Amsterdam")
  if err != nil {
    panic(err)
  }

  fmt.Println("Now in Amsterdam:", time.Now().In(loc))
}
EOF

RUN CGO_ENABLED=0 go build main.go

# -=== Target image ===-
FROM scratch

COPY --from=builder /app/main /

CMD ["/main"]
