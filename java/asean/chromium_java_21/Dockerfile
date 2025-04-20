FROM        --platform=$TARGETOS/$TARGETARCH eclipse-temurin:21-jdk

LABEL       author="Matthew Penner" maintainer="matthew@pterodactyl.io"

LABEL       org.opencontainers.image.source="https://github.com/ASEAN-Build-The-Earth/server-docker-images"
LABEL       org.opencontainers.image.licenses=MIT

RUN 				apt-get update -y \
&& apt-get install -y lsof curl ca-certificates openssl git tar sqlite3 fontconfig libfreetype6 tzdata iproute2 libstdc++6 \
                        # Headless Chromium dependencies
                        && apt-get install -y --no-install-recommends \
                            libasound2t64 libatk-bridge2.0-0 libatk1.0-0 libatspi2.0-0 libcups2 \
                            libdbus-1-3 libdrm2 libegl1 libgbm1 libglib2.0-0 libgtk-3-0 libnspr4 \
                            libnss3 libpango-1.0-0 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 \
                            libxdamage1 libxext6 libxfixes3 libxrandr2 libxshmfence1 libxrender1 \
                            libxkbcommon0 libfontconfig1 \
						&& useradd -d /home/container -m container

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./../../entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
