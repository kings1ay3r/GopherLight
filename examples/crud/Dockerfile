# Build Stage
FROM golang:1.20-alpine AS builder

WORKDIR /app

# Copy go.mod and go.sum files
COPY go.mod ./

# Download dependencies
RUN go mod download

# Copy the application code
COPY router ./router
COPY req ./req
COPY examples/crud/main.go ./main.go

# Build the Go app
RUN go build -o crud_app

# Run Stage
FROM alpine:latest

WORKDIR /app

COPY --from=builder /app/crud_app ./

EXPOSE 3333

CMD ["./crud_app"]
