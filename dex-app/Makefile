PROJ=dex-app
ORG_PATH=github.com/yodo-io
REPO_PATH=$(ORG_PATH)/$(PROJ)

# VERSION ?= $(shell git rev-parse HEAD)
VERSION = 0.0.1-alpha

LD_FLAGS="-w -X $(REPO_PATH)/version.Version=$(VERSION)"

build: bin/dex-app

bin/dex-app:
	@mkdir -p bin
	@go build -v -ldflags $(LD_FLAGS) -o bin/dex-app .

clean:
	@rm -rf bin

.PHONY: build clean
