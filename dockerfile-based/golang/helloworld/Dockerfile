FROM golang:1.15 AS build

ENV CGO_ENABLED=0
COPY main.go .
RUN go build \
    -tags netgo \
    -ldflags "-s -w -extldflags '-static'" \
    -o /tmp/helloworld \
    main.go

FROM alpine:latest
COPY --from=build /tmp/helloworld /usr/local/bin/helloworld
ENTRYPOINT [ "/usr/local/bin/helloworld" ]
EXPOSE 8080
