FROM golang:1.15 AS build

RUN apt-get update >/dev/null 2>&1 && \
    apt-get install -y stress

COPY main.go .
ENV CGO_ENABLED=0
RUN go build \
    -tags netgo \
    -ldflags "-s -w -extldflags '-static'" \
    -o /tmp/helloworld \
    main.go

RUN stress \
    --cpu 2 \
    --vm 1 \
    --io 1 \
    --vm-bytes 1024M \
    --timeout 5m

FROM scratch
COPY --from=build /tmp/helloworld ./helloworld
ENTRYPOINT [ "./helloworld" ]
EXPOSE 8080
