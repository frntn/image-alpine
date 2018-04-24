## -*- docker-image-name: "scaleway/alpine:latest" -*-
FROM ${DOCKER_ARCH}/alpine:latest

MAINTAINER Scaleway <opensource@scaleway.com> (@scaleway)

# Environment
ENV SCW_BASE_IMAGE scaleway/alpine:latest

# Adding and calling builder-enter
COPY ./overlay-base/usr/local/sbin/scw-builder-enter /usr/local/sbin/
RUN sed -i 's/bash/ash/g' /usr/local/sbin/scw-builder-enter && /bin/sh -e /usr/local/sbin/scw-builder-enter

# Install packages
RUN apk update \
	&& apk add \
	blkid \
	busybox-initscripts \
	chrony \
	curl \
	dhclient \
	dosfstools \
	e2fsprogs \
	grub-efi \
	iptables \
	ip6tables \
	linux-hardened \
	openrc \
	openssh \
	rsyslog \
	util-linux \
	&& apk upgrade \
	openssl \
	&& rm -rf /var/cache/apk/*

# Patch rootfs
COPY ./overlay/ ./overlay-image-tools/ /
COPY ./overlay-base/usr/local/sbin/scw-signal-state /usr/local/sbin/
COPY ./overlay-base/usr/local/sbin/scw-fetch-ssh-keys /usr/local/sbin/

# Configure autostart packages
RUN rc-update add sshd default\
 && rc-update add iptables default \
 && rc-update add ip6tables default \
 && rc-update add chronyd default \
 && rc-update add hostname default \
 && rc-update add sysctl default \
 && rc-update add rsyslog default \
 && rc-update add update-motd default \
 && rc-update add loopback default \
 && rc-update add scw-generate-net-config default \
 && rc-update add scw-signal-booted default \
 && rc-update add scw-ssh-keys default \
 && rc-update add scw-initramfs-shutdown shutdown \
 && rc-update add scw-sync-kernel-extra default \
 && rc-update add scw-hostname default \
 && rc-update add scw-gen-machine-id default \
 && rc-status

# Remove the network configuration so it's generated at first boot
RUN > /etc/network/interfaces

# Allow login from ttyS0
RUN echo "ttyS0" >> /etc/securetty

# Update permissions
RUN chmod 700 /root

# Clean rootfs from image-builder
# scw-builder-leave is very Debian oriented, and therefore excluded from Alpine
RUN rm -f /etc/ssh/*_key* && \
	rm -f /root/.history /root/.bash_history && \
	rm -f /usr/local/sbin/scw-builder-*

