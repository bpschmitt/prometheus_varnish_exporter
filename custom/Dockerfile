FROM golang:1.10-alpine as exporter

RUN apk add --no-cache git
RUN go get github.com/jonnenauha/prometheus_varnish_exporter

WORKDIR /go/src/github.com/jonnenauha/prometheus_varnish_exporter
#RUN git checkout 1.4
RUN git checkout 1.5.2
RUN go build

FROM alpine:3.7

RUN apk --no-cache add varnish 

COPY config/default.vcl /etc/varnish/default.vcl
COPY --from=exporter /go/bin/prometheus_varnish_exporter /usr/local/bin

ENTRYPOINT /usr/sbin/varnishd
