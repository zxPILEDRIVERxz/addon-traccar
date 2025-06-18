ARG BUILD_FROM=ghcr.io/hassio-addons/base:17.2.5
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Install dependencies
RUN \
    apk update && \
    apk add --no-cache \
        mariadb-client \
        nginx \
        nss \
        openjdk17-jre-headless \
        unzip \
        xmlstarlet

# Set working dir
WORKDIR /opt/traccar

# Copy root filesystem
COPY rootfs /

# Install Traccar 6.7.3
ARG TRACCAR_VERSION="v6.7.3"
RUN \
    curl -J -L -o /tmp/traccar.zip \
        "https://github.com/traccar/traccar/releases/download/${TRACCAR_VERSION}/traccar-other-${TRACCAR_VERSION#v}.zip" && \
    unzip -d /opt/traccar /tmp/traccar.zip && \
    rm -fr /tmp/* && \
    chmod +x /opt/traccar/run.sh

# Expose ports
EXPOSE 8082/tcp 5055/tcp

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Your Name <your.email@example.com>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Custom Add-ons" \
    org.opencontainers.image.authors="Your Name <your.email@example.com>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://github.com/yourusername/addon-traccar" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
