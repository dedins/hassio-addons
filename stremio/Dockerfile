ARG BUILD_FROM=ghcr.io/hassio-addons/ubuntu-base:8.2.0
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

WORKDIR /stremio

ARG VERSION=master

RUN apk add --no-cache openssl-dev wget ffmpeg nginx openrc bash nano nodejs
RUN wget https://dl.strem.io/four/${VERSION}/server.js
RUN wget https://dl.strem.io/four/${VERSION}/stremio.asar
RUN openrc ; touch /run/openrc/softlevel 

RUN mkdir /etc/nginx/ssl/
    
COPY nginx.conf /etc/nginx/http.d/default.conf
COPY start.sh /stremio/start.sh
RUN chmod +x /stremio/start.sh

ENTRYPOINT ["./start.sh"]

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
    maintainer="dedins" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="dedins" \
    org.opencontainers.image.authors="dedins" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}