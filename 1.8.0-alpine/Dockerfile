# sql-migrate v1.8.0 with PostgreSQL 17 SCRAM-SHA-256 support
FROM golang:1.23.12-alpine3.22 AS builder

# Install build dependencies
RUN apk add --no-cache git ca-certificates

# Install sql-migrate v1.8.0
RUN go install github.com/rubenv/sql-migrate/...@v1.8.0

# Final image
FROM alpine:3.22

# Install runtime dependencies
RUN apk --no-cache add ca-certificates tzdata

# Copy sql-migrate binary
COPY --from=builder /go/bin/sql-migrate /usr/local/bin/sql-migrate

# Create working directory
WORKDIR /var/app/rdb/schema

# Set entrypoint
ENTRYPOINT ["sql-migrate"]
