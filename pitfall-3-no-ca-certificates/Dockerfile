# syntax=docker/dockerfile:1.4

# -=== Builder image ===-
FROM golang:1 as builder

WORKDIR /app

COPY <<EOF main.go
package main

import (
  "fmt"
  "io"
  "net/http"
)

func main() {
  resp, err := http.Get("https://iximiuz.com/")
  if err != nil {
    panic(err)
  }
  defer resp.Body.Close()

  body, err := io.ReadAll(resp.Body)
  if err != nil {
    panic(err)
  }
  fmt.Println("Response", body)
}
EOF

RUN CGO_ENABLED=0 go build main.go

# -=== Target image ===-
FROM scratch

COPY --from=builder /app/main /

CMD ["/main"]
