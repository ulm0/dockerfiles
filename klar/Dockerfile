FROM golang:1.8-alpine

ARG GOARCH
ARG GOARM

ENV CGO_ENABLED=${CGO_ENABLED:-0} \
    GOARCH=${GOARCH:-} \
    GOARM=${GOARM:-} \
    GOOS=${GOOS:-linux}

RUN apk --update add git build-base file && \
    echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && \
    apk add --no-cache upx && \
    go get -d github.com/optiopay/klar

WORKDIR /go/src/github.com/optiopay/klar
RUN go build && \
    file klar && \
    upx --best klar

FROM scratch

ADD https://g.innersea.xyz/ulm0/dockerfiles/raw/master/registry/etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY --from=0 /go/src/github.com/optiopay/klar/klar /klar

ENTRYPOINT ["/klar"]
