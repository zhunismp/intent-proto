# --- CONFIGURATION ---

PROTO_SRC := proto/v1
PROTO_OUT := gen/go

# --- TOOLS ---

PROTOC_GEN_GO := $(shell command -v protoc-gen-go 2> /dev/null)
PROTOC_GEN_GO_GRPC := $(shell command -v protoc-gen-go-grpc 2> /dev/null)

# --- TARGETS ---

.PHONY: all generate-product tools cleanup-product-outdir

all: cleanup-product-outdir generate-product

tools:
	@if [ -z "$(PROTOC_GEN_GO)" ]; then \
		echo "Installing protoc-gen-go..."; \
		go install google.golang.org/protobuf/cmd/protoc-gen-go@latest; \
	fi
	@if [ -z "$(PROTOC_GEN_GO_GRPC)" ]; then \
		echo "Installing protoc-gen-go-grpc..."; \
		go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest; \
	fi

generate-product: tools
	@echo "Generating Go protobuf files..."
	@protoc \
		--go_out=$(PROTO_OUT) \
		--go_opt=paths=source_relative \
		--go-grpc_out=$(PROTO_OUT) \
		--go-grpc_opt=paths=source_relative \
		$(PROTO_SRC)/*.proto
	@echo "Generation complete!"

cleanup-product-outdir:
	@echo "Cleaning generated files..."
	@rm -rf $(PROTO_OUT)
	@echo "Building fresh directory for generated files..."
	@mkdir -p ${PROTO_OUT}
