# Build the manager binary
FROM golang:1.16 as builder

WORKDIR /workspace
# Copy the go source
COPY main.go main.go

# Build
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -o server main.go
RUN ls -l /workspace

# Use distroless as minimal base image to package the manager binary
# Refer to https://github.com/GoogleContainerTools/distroless for more details
FROM yunlian-registry.cn-hangzhou.cr.aliyuncs.com/ops/static:nonroot
WORKDIR /
COPY --from=builder /workspace/server .
USER 65532:65532

ENTRYPOINT ["/server"]
