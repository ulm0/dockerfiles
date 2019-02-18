FROM alpine
ENV ARCH=amd64 \
    VERSION=0.16.0 \
    CLAIR=false \
    CLAIR_SERVER="" \
    REGISTRY_URL="" \
    REGISTRY_USER="" \
    REGISTRY_PASSWORD=""
COPY entrypoint /app/entrypoint
WORKDIR /app
RUN \
    set -ex; \
    apk add --no-cache ca-certificates && \
    rm -f /var/cache/apk/* && \
    wget https://github.com/genuinetools/reg/releases/download/v${VERSION}/reg-linux-${ARCH} -O /app/reg && \
    chmod +x /app/reg && \
    cd /tmp/ && \
    wget https://github.com/genuinetools/reg/archive/v${VERSION}.tar.gz && \
    tar -xzvf v${VERSION}.tar.gz && \
    mv reg-${VERSION}/server /app/server && \
    rm -rf v${VERSION}.tar.gz reg-${VERSION}
EXPOSE 8080
ENTRYPOINT [ "/app/entrypoint" ]