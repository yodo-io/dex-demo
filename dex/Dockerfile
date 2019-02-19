# Build stage
FROM golang:latest AS builder

ENV DIR=$GOPATH/src/github.com/dexidp/dex

RUN mkdir -p $DIR \
 && git clone https://github.com/dexidp/dex $DIR

WORKDIR $DIR
RUN make \
 && mkdir -p /dex/bin \
 && cp bin/dex /dex/bin/dex \
 && cp -R web /dex/web

# Runtime container
FROM debian:9-slim

RUN apt-get update && apt-get -y install ca-certificates

COPY --from=builder /dex /opt/dex
COPY example-config.yaml /opt/dex/example-config.yaml

# Database dir
RUN mkdir -p /var/dex

EXPOSE 5556 5558

WORKDIR /opt/dex
CMD ["bin/dex", "serve", "example-config.yaml"]
