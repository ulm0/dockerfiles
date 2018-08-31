FROM golang:1.10.1-alpine3.7
ARG GOARCH
ARG GOARM
ARG RELEASE
ENV CGO_ENABLED=${CGO_ENABLED:-0} \
    GOARCH=${GOARCH:-} \
    GOARM=${GOARM:-} \
    GOOS=${GOOS:-linux} \
    GOPATH=/go \
    PATH=$PATH:$GOPATH/bin \
    RELEASE=${RELEASE:-master}
WORKDIR /go/src/github.com/minio/
RUN apk add --no-cache ca-certificates curl && \
    apk add --no-cache --virtual .build-deps git && \
    go get -v -d github.com/minio/minio && \
    cd /go/src/github.com/minio/minio && \
    git checkout ${RELEASE} && \
    go install -v -ldflags "$(go run buildscripts/gen-ldflags.go)" && \
    rm -rf /go/pkg /go/src /usr/local/go && apk del .build-deps

FROM alpine:edge
# COPY --from=0 /go/bin/minio /go/bin/minio
# COPY --from=0 /go/bin/linux_arm/minio /go/bin/minio
COPY --from=0 /go/bin/linux_arm64/minio /go/bin/minio
RUN apk add --no-cache upx && \
    cd /go/bin && \
    upx --best minio

# FROM alpine:3.7
# FROM multiarch/alpine:armhf-v3.7
FROM multiarch/alpine:arm64-v3.7
ENV MINIO_UPDATE=off \
    MINIO_ACCESS_KEY_FILE=access_key \
    MINIO_SECRET_KEY_FILE=secret_key \
    PATH=$PATH:/go/bin
COPY docker-entrypoint.sh healthcheck.sh /usr/bin/
COPY --from=1 /go/bin/minio /go/bin/minio
RUN chmod +x /go/bin/minio && \
    apk add --no-cache ca-certificates curl && \
    echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf
EXPOSE 9000
ENTRYPOINT ["/usr/bin/docker-entrypoint.sh"]
VOLUME ["/data"]
HEALTHCHECK --interval=30s --timeout=5s \
    CMD /usr/bin/healthcheck.sh
CMD ["minio"]
