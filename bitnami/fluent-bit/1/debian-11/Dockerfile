FROM docker.io/bitnami/minideb:bullseye
ENV HOME="/" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-11" \
    OS_NAME="linux"

LABEL org.opencontainers.image.authors="https://bitnami.com/contact" \
      org.opencontainers.image.description="Application packaged by Bitnami" \
      org.opencontainers.image.ref.name="1.9.7-debian-11-r4" \
      org.opencontainers.image.source="https://github.com/bitnami/containers/tree/main/bitnami/fluent-bit" \
      org.opencontainers.image.title="fluent-bit" \
      org.opencontainers.image.vendor="VMware, Inc." \
      org.opencontainers.image.version="1.9.7"

COPY prebuildfs /
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
# Install required system packages and dependencies
RUN install_packages ca-certificates curl gzip libc6 libgcc-s1 libgcrypt20 libgpg-error0 liblz4-1 liblzma5 libsasl2-2 libssl1.1 libsystemd0 libyaml-0-2 libzstd1 procps tar wget zlib1g
RUN wget -nc -P /tmp/bitnami/pkg/cache/ https://downloads.bitnami.com/files/stacksmith/fluent-bit-1.9.7-0-linux-amd64-debian-11.tar.gz && \
    echo "11c661492a2ff8712940225229dfb1620f07123c30123888fb1afbd6a3daf732  /tmp/bitnami/pkg/cache/fluent-bit-1.9.7-0-linux-amd64-debian-11.tar.gz" | sha256sum -c - && \
    tar -zxf /tmp/bitnami/pkg/cache/fluent-bit-1.9.7-0-linux-amd64-debian-11.tar.gz -P --transform 's|^[^/]*/files|/opt/bitnami|' --wildcards '*/files' && \
    rm -rf /tmp/bitnami/pkg/cache/fluent-bit-1.9.7-0-linux-amd64-debian-11.tar.gz
RUN apt-get update && apt-get upgrade -y && \
    rm -r /var/lib/apt/lists /var/cache/apt/archives
RUN chmod g+rwX /opt/bitnami
RUN chown -R 1001:1001 /opt/bitnami/fluent-bit

ENV APP_VERSION="1.9.7" \
    BITNAMI_APP_NAME="fluent-bit" \
    PATH="/opt/bitnami/fluent-bit/bin:$PATH"

EXPOSE 2020

WORKDIR /opt/bitnami/fluent-bit
USER 1001
ENTRYPOINT [ "fluent-bit" ]
CMD [ "-c", "/opt/bitnami/fluent-bit/conf/fluent-bit.conf" ]
