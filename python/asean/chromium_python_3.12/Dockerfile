# https://github.com/pelican-eggs/yolks/blob/7ca5ed1a16c1bd1ddb2c974c66aa68159c210833/python/3.12/Dockerfile#L1

FROM        --platform=$TARGETOS/$TARGETARCH python:3.12-slim-bookworm

LABEL       author="Matthew Penner" maintainer="matthew@pterodactyl.io"

LABEL       org.opencontainers.image.source="https://github.com/ASEAN-Build-The-Earth/server-docker-images"
LABEL       org.opencontainers.image.licenses=MIT

RUN         apt update \
            && apt -y install git gcc g++ ca-certificates dnsutils curl iproute2 ffmpeg procps tini \
                # Headless Chromium dependencies
				libasound2 libatk-bridge2.0-0 libatk1.0-0 libatspi2.0-0 libcups2 \
				libdbus-1-3 libdrm2 libegl1 libgbm1 libglib2.0-0 libgtk-3-0 libnspr4 \
				libnss3 libpango-1.0-0 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 \
				libxdamage1 libxext6 libxfixes3 libxrandr2 libxshmfence1 libxrender1 \
				libxkbcommon0 libfontconfig1 \
	&& useradd -m -d /home/container container

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

STOPSIGNAL SIGINT

COPY        --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh
ENTRYPOINT  ["/usr/bin/tini", "-g", "--"]
CMD         ["/entrypoint.sh"]
