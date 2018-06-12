FROM golang:1.10.1-alpine3.7
COPY . /registry
WORKDIR /registry
ARG GOARCH
ARG GOARM
ENV CGO_ENABLED=${CGO_ENABLED:-0} \
    GOARCH=${GOARCH:-} \
    GOARM=${GOARM:-} \
    GOOS=${GOOS:-linux} \
    REG_VER=${REG_VER:-v2.6.2}
RUN apk add --no-cache bash git build-base file make && \
    echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && \
    apk add --no-cache upx && \
    make dist compress

FROM scratch
COPY --from=0 /registry/bin/registry /bin/registry
ADD https://raw.githubusercontent.com/containous/traefik/master/script/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY etc/ /etc
VOLUME ["/var/lib/registry/"]
EXPOSE 5000
ENTRYPOINT ["/bin/registry"]
CMD ["serve", "/etc/docker/registry/config.yml"]
