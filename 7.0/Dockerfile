FROM registry.access.redhat.com/rhel:7.5
LABEL maintainer "Bitnami <containers@bitnami.com>"


# Install required system packages and dependencies
RUN yum install --disablerepo=rhel-7-server-htb-rpms -y ca-certificates bzip2-libs glibc libcom_err libcurl libffi freetype libgcc libgcrypt gmp gnutls libgpg-error libicu libidn libjpeg-turbo krb5-libs keyutils-libs openldap xz-libs ncurses-libs nettle p11-kit libpng libpng12 readline cyrus-sasl-lib libssh2 openssl-libs libstdc++  libtasn1 libuuid libxml2 libxslt zlib wget
RUN wget -nc -P /tmp/bitnami/pkg/cache/ https://downloads.bitnami.com/files/stacksmith/php-7.0.29-0-linux-x64-rhel-7.5.tar.gz && \
    echo "5975462fdafd053d80d601950e605fd890a1fec09659229d8cf71ca4b8b4a481 /tmp/bitnami/pkg/cache/php-7.0.29-0-linux-x64-rhel-7.5.tar.gz" | sha256sum -c - && \
    tar -zxf /tmp/bitnami/pkg/cache/php-7.0.29-0-linux-x64-rhel-7.5.tar.gz -P --transform 's|^[^/]*/files|/opt/bitnami|' --wildcards '*/files' && \
    rm -rf /tmp/bitnami/pkg/cache/php-7.0.29-0-linux-x64-rhel-7.5.tar.gz
RUN mkdir -p /bitnami && ln -sf /bitnami/php /bitnami/php-fpm && \
    mkdir /opt/bitnami/php/logs && touch /opt/bitnami/php/logs/php-fpm.log && \
    chmod -R g+rwX /opt/bitnami/php && chgrp -R root /opt/bitnami/php && \
    sed -i 's/.usr.local.php/\/opt\/bitnami\/php/g' /opt/bitnami/php/etc/*.conf  /opt/bitnami/php/etc/php-fpm.d/*.conf

COPY rootfs /

ENV BITNAMI_APP_NAME="php-fpm" \
    BITNAMI_IMAGE_VERSION="7.0.29-r4" \
    PATH="/opt/bitnami/php/bin:/opt/bitnami/php/sbin:$PATH"

USER 1001

EXPOSE 9000

WORKDIR /app
CMD ["php-fpm","-F","--pid","/opt/bitnami/php/tmp/php-fpm.pid","-y","/opt/bitnami/php/etc/php-fpm.conf"]
