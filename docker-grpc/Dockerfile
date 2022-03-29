FROM golang:latest AS build-env

LABEL maintainer="rraj123@gmail.com"


WORKDIR $GOPATH/src/grpcserver

COPY *.go .
COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o grpcserver .

FROM alpine

RUN apk update && \
   apk add ca-certificates && \
   update-ca-certificates && \
   rm -rf /var/cache/apk/*
WORKDIR grpcserver
COPY --from=build-env /go/src/grpcserver /grpcserver
ENTRYPOINT ./grpcserver
EXPOSE 50051
