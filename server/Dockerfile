# LOCALIZMA MODIFICATION NOTICE: This file was modified from the LocalSend upstream source to remove the deleted Flutter Rust isolate dependency.
# Build from the repository root (workspace root):
#   docker build -f server/Dockerfile .
FROM rust:1.97 AS builder

WORKDIR /app

COPY Cargo.toml Cargo.lock ./
COPY packages/core ./packages/core
COPY server ./server
COPY cli ./cli

RUN --mount=type=cache,target=/usr/local/cargo/registry \
    --mount=type=cache,target=/app/target \
    cargo build --release -p server && cp target/release/server /server-bin

FROM debian:bookworm AS runtime

COPY --from=builder /server-bin /server

EXPOSE 3000
ENTRYPOINT ["/server"]
