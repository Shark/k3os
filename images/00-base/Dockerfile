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

RUN curl -sSL https://github.com/Shark/hcloud-k3os-configurator/releases/download/v0.0.14/hcloud-k3os-configurator_v0.0.14_amd64.xz | xz -d > /usr/bin/hcloud-k3os-configurator \
 && chmod +x /usr/bin/hcloud-k3os-configurator \
 && curl -sSL https://github.com/derailed/k9s/releases/download/v0.19.7/k9s_Linux_x86_64.tar.gz | tar xz k9s \
 && mv k9s /usr/bin/k9s

COPY etc/init.d /etc/init.d
COPY etc/conf.d /etc/conf.d
