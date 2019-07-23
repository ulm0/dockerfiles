ARG ATLANTIS_VERSION=latest
FROM runatlantis/atlantis:${ATLANTIS_VERSION}
# ARG ANSIBLE_PLUGIN
ARG EXTERNAL_PLUGIN
ARG KUBECTL_VERSION
# ARG KUSTOMIZE_VERSION
ARG LOCAL_PLUGIN
ARG TEMPLATE_VERSION
ARG VSPHERE_VERSION
# ENV ANSIBLE_PLUGIN=${ANSIBLE_PLUGIN:-2.1.2} \
ENV EXTERNAL_PLUGIN=${EXTERNAL_PLUGIN:-1.2.0} \
    KUBECTL_VERSION=${KUBECTL_VERSION:-1.15.1} \
    # KUSTOMIZE_VERSION=${KUSTOMIZE_VERSION:-2.0.3} \
    LOCAL_PLUGIN=${LOCAL_PLUGIN:-1.3.0} \
    TEMPLATE_VERSION=${TEMPLATE_VERSION:-2.1.2} \
    VSPHERE_VERSION=${VSPHERE_VERSION:-1.12.0} \
    PLUGINS_DIR=/root/.terraform.d/plugins
RUN apk add --no-cache \
    ca-certificates && \
    update-ca-certificates && \
    apk add --no-cache \
    bash \
    curl \
    git \
    jq \
    openssh-client \
    py-pip \
    sshpass \
    wget && \
    apk add --no-cache \
    --virtual=build \
    gcc \
    libffi-dev \
    make \
    musl-dev \
    openssl-dev \
    python-dev && \
    pip --no-cache-dir install -U \
    pip && \
    pip --no-cache-dir install \
    azure-cli && \
    cd /bin/ && \
    wget https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl && \
    chmod +x kubectl && \
    # wget https://github.com/kubernetes-sigs/kustomize/releases/download/v${KUSTOMIZE_VERSION}/kustomize_${KUSTOMIZE_VERSION}_linux_amd64 -O kustomize && \
    # chmod +x kustomize && \
    mkdir -p $PLUGINS_DIR && \
    cd $PLUGINS_DIR && \
    # wget https://github.com/radekg/terraform-provisioner-ansible/releases/download/v${ANSIBLE_PLUGIN}/terraform-provisioner-ansible-linux-amd64_v${ANSIBLE_PLUGIN} -O $PLUGINS_DIR/terraform-provisioner-ansible_v${ANSIBLE_PLUGIN} && \
    # chmod +x $PLUGINS_DIR/terraform-provisioner-ansible_v${ANSIBLE_PLUGIN} && \
    wget https://releases.hashicorp.com/terraform-provider-external/${EXTERNAL_PLUGIN}/terraform-provider-external_${EXTERNAL_PLUGIN}_linux_amd64.zip && \
    unzip terraform-provider-external_${EXTERNAL_PLUGIN}_linux_amd64.zip && \
    wget https://releases.hashicorp.com/terraform-provider-vsphere/${VSPHERE_VERSION}/terraform-provider-vsphere_${VSPHERE_VERSION}_linux_amd64.zip && \
    unzip terraform-provider-vsphere_${VSPHERE_VERSION}_linux_amd64.zip && \
    wget https://releases.hashicorp.com/terraform-provider-local/${LOCAL_PLUGIN}/terraform-provider-local_${LOCAL_PLUGIN}_linux_amd64.zip && \
    unzip terraform-provider-local_${LOCAL_PLUGIN}_linux_amd64.zip && \
    wget -q https://releases.hashicorp.com/terraform-provider-template/${TEMPLATE_VERSION}/terraform-provider-template_${TEMPLATE_VERSION}_linux_amd64.zip && \
    unzip terraform-provider-template_${TEMPLATE_VERSION}_linux_amd64.zip && \
    rm -f *.zip && \
    apk del --purge build && \
    rm -rf /var/cache/apk/* /tmp/*
