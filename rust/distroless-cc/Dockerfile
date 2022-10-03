# syntax=docker/dockerfile:1.4

# -=== Builder image ===-
FROM rust:1 as builder

WORKDIR /app

COPY <<EOF Cargo.toml
[package]
name = "hello-world"
version = "0.0.1"
EOF

COPY <<EOF src/main.rs
fn main() {
  println!("Hello world! (Rust edition)");
}
EOF

RUN cargo install --path .

# -=== Target image ===-
FROM gcr.io/distroless/cc

COPY --from=builder /usr/local/cargo/bin/hello-world /

CMD ["/hello-world"]
