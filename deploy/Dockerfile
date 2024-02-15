FROM golang:1.21.1-alpine AS builder
WORKDIR /build
RUN apk add gcc g++ --no-cache
COPY . .
RUN go mod download
RUN CGO_ENABLED=0 GOOS=linux go build -o app -a -ldflags '-w -extldflags "-static"'  /build/cmd/main.go

FROM alpine
WORKDIR /app
COPY --from=builder /build/app /app/app
ENTRYPOINT ["/app/app"]