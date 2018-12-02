FROM alpine
ARG TF_VER
ARG ANSIBLE_PLUGIN
ENV PLUGINS_DIR=/root/.terraform.d/plugins \
    ANSIBLE_PLUGIN=$ANSIBLE_PLUGIN \
    TF_VER=$TF_VER
RUN apk add --no-cache git openssh ca-certificates && \
    apk add --no-cache --virtual .compress-tools upx && \
    wget https://releases.hashicorp.com/terraform/${TF_VER}/terraform_${TF_VER}_linux_amd64.zip -O /tmp/terraform.zip && \
    unzip /tmp/terraform.zip -d /bin/ && \
    chmod +x /bin/terraform && \
    cd /bin/ && \
    upx --best terraform && \
    mkdir -p ${PLUGINS_DIR} && \
    wget https://github.com/radekg/terraform-provisioner-ansible/releases/download/v${ANSIBLE_PLUGIN}/terraform-provisioner-ansible-linux-amd64_v${ANSIBLE_PLUGIN} -O $PLUGINS_DIR/terraform-provisioner-ansible_v${ANSIBLE_PLUGIN} && \
    chmod +x $PLUGINS_DIR/terraform-provisioner-ansible_v${ANSIBLE_PLUGIN} && \
    cd $PLUGINS_DIR && \
    upx --best terraform-provisioner-ansible_v${ANSIBLE_PLUGIN} && \
    apk del .compress-tools && \
    rm -rf /var/cache/apk/* /tmp/* 
CMD ["/bin/terraform"]