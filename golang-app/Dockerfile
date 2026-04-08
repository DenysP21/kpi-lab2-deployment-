FROM golang:1.23-bookworm AS builder

WORKDIR /app
COPY go.mod ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o /main main.go

FROM gcr.io/distroless/static-debian12

COPY --from=builder /main /main

EXPOSE 8080

USER nonroot:nonroot

ENTRYPOINT ["/main"]