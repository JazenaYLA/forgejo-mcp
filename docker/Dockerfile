# Build forgejo-mcp from source (no official image available)
FROM golang:1.24-alpine AS builder
WORKDIR /app
RUN apk add --no-cache git make
RUN git clone -b enterprise https://github.com/JazenaYLA/forgejo-mcp.git . && \
    sed -i 's/^go 1.25.0/go 1.24.0/' go.mod && \
    sed -i 's/import (/import ("crypto\/tls"\n"net\/http"/' pkg/forgejo/forgejo.go && \
    sed -i "/clientOnce.Do/a \ \ \ \ \ \ \ \ http.DefaultTransport.(*http.Transport).TLSClientConfig = \&tls.Config{InsecureSkipVerify: true}" pkg/forgejo/forgejo.go
RUN go build -o forgejo-mcp .

FROM alpine:latest
RUN apk add --no-cache ca-certificates curl
WORKDIR /app
COPY --from=builder /app/forgejo-mcp .
EXPOSE 8080
ENTRYPOINT ["./forgejo-mcp"]
CMD ["--transport", "sse", "--sse-port", "8080"]
