# Build stage
FROM golang:latest AS builder

ADD . /src
WORKDIR /src
RUN make

# Runtime container
FROM debian:9-slim

RUN apt-get update && apt-get -y install ca-certificates

COPY --from=builder /src/bin/dex-app /bin/dex-app

EXPOSE 5555

WORKDIR /opt/dex
CMD ["/bin/dex-app", "--client-id", "example-app", "--client-secret", "abc123", "--redirect-uri", "http://127.0.0.1:5555/callback", "--issuer", "http://127.0.0.1:5556/dex", "--listen", "http://127.0.0.1:5555"]
