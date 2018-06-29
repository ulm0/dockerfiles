FROM alpine:3.7
ARG TF_VER
RUN apk add --no-cache ca-certificates && \
    apk add --no-cache --virtual .compress-tools upx && \
    wget https://releases.hashicorp.com/terraform/${TF_VER}/terraform_${TF_VER}_linux_amd64.zip -O /tmp/terraform.zip && \
    unzip /tmp/terraform.zip -d /usr/bin/ && \
    chmod +x /usr/bin/terraform && \
    cd /usr/bin/ && \
    upx --best terraform && \
    rm -f /tmp/terraform.zip && \
    apk del .compress-tools
CMD ["/bin/sh"]