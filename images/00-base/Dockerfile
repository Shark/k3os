### BASE ###
FROM alpine:3.11 as base
ARG ARCH
RUN apk --no-cache add \
    bash \
    bash-completion \
    blkid \
    busybox-initscripts \
    ca-certificates \
    connman \
    conntrack-tools \
    coreutils \
    curl \
    dbus \
    dmidecode \
    dhcpcd \
    dosfstools \
    e2fsprogs \
    e2fsprogs-extra \
    efibootmgr \
    eudev \
    findutils \
    grub-efi \
    haveged \
    htop \
    hvtools \
    iproute2 \
    iptables \
    ip6tables \
    iptables-openrc \
    ip6tables-openrc \
    iscsi-scst \
    jq \
    kbd-bkeymaps \
    logrotate \
    lsscsi \
    lvm2 \
    lvm2-extra \
    mdadm \
    mdadm-misc \
    mdadm-udev \
    multipath-tools \
    ncurses \
    ncurses-terminfo \
    nfs-utils \
    open-iscsi \
    openrc \
    openssh-client \
    openssh-server \
    parted \
    procps \
    qemu-guest-agent \
    restic \
    rng-tools \
    rsync \
    strace \
    sudo \
    tar \
    tzdata \
    util-linux \
    vim \
    xz \
 && mv -vf /etc/conf.d/qemu-guest-agent /etc/conf.d/qemu-guest-agent.orig \
 && mv -vf /etc/conf.d/rngd             /etc/conf.d/rngd.orig \
 && mv -vf /etc/conf.d/udev-settle      /etc/conf.d/udev-settle.orig \
# replicate the default "no idea, friend" behavior of virt-what
 && touch /usr/sbin/virt-what \
 && chmod +x /usr/sbin/virt-what

RUN curl -sSL https://github.com/Shark/hcloud-k3os-configurator/releases/download/v0.0.9/hcloud-k3os-configurator_v0.0.9_amd64.xz | xz -d > /usr/bin/hcloud-k3os-configurator \
 && chmod +x /usr/bin/hcloud-k3os-configurator \
 && mkdir /usr/share/hcloud-k3os \
 && mkdir /usr/share/hcloud-k3os/flux \
 && cd /usr/share/hcloud-k3os \
 && curl -sSL https://github.com/fluxcd/flux/archive/1.17.1.tar.gz | tar xz \
 && mv flux-1.17.1/deploy flux/flux-deploy \
 && rm -rf flux-1.17.1 \
 && curl -sSL https://github.com/fluxcd/helm-operator/archive/v1.0.0-rc8.tar.gz | tar xz \
 && mv helm-operator-1.0.0-rc8/deploy flux/helm-operator-deploy \
 && rm -rf helm-operator-1.0.0-rc8 \
 && mkdir hcloud-csi hcloud-fip sealed-secrets \
 && curl -sSL -o hcloud-csi/hcloud-csi.yaml https://raw.githubusercontent.com/hetznercloud/csi-driver/v1.2.2/deploy/kubernetes/hcloud-csi.yml \
 && curl -sSL -o hcloud-fip/rbac.yaml https://raw.githubusercontent.com/cbeneke/hcloud-fip-controller/v0.3.1/deploy/rbac.yaml \
 && curl -sSL -o hcloud-fip/daemonset.yaml https://raw.githubusercontent.com/cbeneke/hcloud-fip-controller/v0.3.1/deploy/daemonset.yaml \
 && curl -sSL -o sealed-secrets/controller.yaml https://github.com/bitnami-labs/sealed-secrets/releases/download/v0.9.7/controller.yaml \
 && curl -sSL https://github.com/derailed/k9s/releases/download/v0.19.3/k9s_Linux_x86_64.tar.gz | tar xz k9s \
 && mv k9s /usr/bin/k9s

COPY usr/share/hcloud-k3os /usr/share/hcloud-k3os
COPY usr/bin/hcloud-k3os-configurator /usr/bin/hcloud-k3os-configurator
COPY etc/init.d /etc/init.d
COPY etc/conf.d /etc/conf.d
