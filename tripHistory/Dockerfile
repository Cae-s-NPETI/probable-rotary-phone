FROM golang:1.17 as build-env

WORKDIR /go/src/app

COPY go.mod ./
COPY go.sum ./
RUN go mod download

COPY *.go ./

# Smaller image size with distroless/static requires CGO_ENABLED=0
RUN CGO_ENABLED=0 go build -o /go/bin/app

FROM gcr.io/distroless/static

COPY --from=build-env /go/bin/app /

EXPOSE 21802
ENTRYPOINT  ["/app"]
