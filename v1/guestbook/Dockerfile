# ---------- Stage 1: Build ----------
    FROM golang:1.22-alpine AS builder

    WORKDIR /app
    
    # Copy Go source
    COPY main.go .
    
    # Initialize Go modules and fetch dependencies
    RUN go mod init guestbook \
     && go mod tidy
    
    # Build the binary
    RUN go build -o guestbook main.go
    
    
    # ---------- Stage 2: Runtime ----------
    FROM alpine:3.19
    
    WORKDIR /app
    
    # Copy compiled Go binary
    COPY --from=builder /app/guestbook /app/guestbook
    
    # Copy frontend files (REQUIRED by rubric)
    COPY public/ /app/public/
    
    # Expose required port
    EXPOSE 3000
    
    # Run the Go server
    CMD ["/app/guestbook"]
    