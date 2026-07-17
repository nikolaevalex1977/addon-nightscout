FROM ghcr.io/home-assistant/amd64-base-ubuntu:22.04

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN mkdir -p /opt/app
COPY /opt /
WORKDIR /opt/app

ARG BUILD_ARCH=amd64
ARG NIGHTSCOUT_VERSION=15.0.7

RUN apt-get update && apt-get install -y --no-install-recommends mongodb-server nodejs npm git webpack build-essential python2.7 nginx libnginx-mod-http-lua && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN git clone --depth 1 https://github.com /opt/app && cd /opt/app && npm install && npm run postinstall && npm run env && npm audit fix

COPY rootfs /

ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

LABEL io.hass.name="Nightscout" io.hass.description="Nightscout acting as a web-based CGM" io.hass.arch="${BUILD_ARCH}" io.hass.type="addon" io.hass.version=${BUILD_VERSION}
