PROTO_DIR=proto
OUT_DIR=gen/go

generate:
	protoc \
		--go_out=$(OUT_DIR) \
		--go_opt=paths=source_relative \
		--go-grpc_out=$(OUT_DIR) \
		--go-grpc_opt=paths=source_relative \
		$(shell find $(PROTO_DIR) -name "*.proto")