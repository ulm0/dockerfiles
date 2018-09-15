FROM alpine:3.8
RUN apk add --no-cache \
    bash \
    git \
    openssl \
    wget && \
    wget -q https://releases.hashicorp.com/packer/1.3.1/packer_1.3.1_linux_amd64.zip -O /tmp/packer.zip && \
    cd /tmp/ && \
    unzip packer.zip && \
    rm -f packer.zip && \
    install packer /bin/packer && \
    chmod +x /bin/packer
ENTRYPOINT ["/bin/packer"]
