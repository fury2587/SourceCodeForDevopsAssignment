FROM golang:1.19-alpine AS builder

WORKDIR /app

COPY go.mod ./
RUN go mod download

# Copy source code
COPY . .

# Build the application
RUN CGO_ENABLED=0 GOOS=linux go build -o main .

FROM alpine:latest


RUN apk --no-cache add curl

WORKDIR /root/

COPY --from=builder /app/main .

# Expose port
EXPOSE 8001

# Run the application
CMD ["./main"]