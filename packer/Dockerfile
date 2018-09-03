FROM alpine:3.8
ADD https://s.ulm0.xyz/packer/packer-musl /bin/packer
RUN apk add --no-cache \
    bash \
    git \
    openssl \
    wget && \
    chmod +x /bin/packer
ENTRYPOINT ["/bin/packer"]
