# https://github.com/pelican-eggs/yolks/blob/7ca5ed1a16c1bd1ddb2c974c66aa68159c210833/python/3.12/Dockerfile#L1

FROM        --platform=$TARGETOS/$TARGETARCH python:3.12-slim-bookworm

LABEL       author="Matthew Penner" maintainer="matthew@pterodactyl.io"

LABEL       org.opencontainers.image.source="https://github.com/pterodactyl/yolks"
LABEL       org.opencontainers.image.licenses=MIT

RUN         apt update \
            && apt -y install git gcc g++ ca-certificates dnsutils curl iproute2 ffmpeg procps tini \
                # Headless Chromium dependencies
                libnss3 \
                libnspr4 \
                libatk1.0-0 \
                libatk-bridge2.0-0 \
                libcups2 \
                libxcomposite1 \
                libxdamage1 \
                libatspi2.0-0 \
	&& adduser -D -h /home/container container

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        --chown=container:container ./../../entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh
ENTRYPOINT  ["/usr/bin/tini", "-g", "--"]
CMD         ["/entrypoint.sh"]
