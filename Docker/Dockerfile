FROM ubuntu:22.04


# Install prerequisites
RUN apt-get update \
    && DEBIAN_FRONTEND="noninteractive" apt-get install -y --no-install-recommends \
        apt-transport-https \
        ca-certificates \
        cabextract \
        git \
        gnupg \
        gosu \
        gpg-agent \
        locales \
        p7zip \
        pulseaudio \
        pulseaudio-utils \
        sudo \
        tzdata \
        unzip \
        wget \
        winbind \
        xvfb \
        zenity \
    && rm -rf /var/lib/apt/lists/*
# Install wine
ARG WINE_BRANCH="stable"
RUN wget -nv -O- https://dl.winehq.org/wine-builds/winehq.key | APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=1 apt-key add - \
    && echo "deb https://dl.winehq.org/wine-builds/ubuntu/ $(grep VERSION_CODENAME= /etc/os-release | cut -d= -f2) main" >> /etc/apt/sources.list \
    && dpkg --add-architecture i386 \
    && apt-get update \
    && DEBIAN_FRONTEND="noninteractive" apt-get install -y --install-recommends winehq-${WINE_BRANCH} \
    && rm -rf /var/lib/apt/lists/*



RUN dpkg --add-architecture i386

RUN apt-get update
RUN apt-get install -y file tree

COPY wine /opt/wine

RUN tree -L 3 /opt/wine


# TODO: Our custom wine seems only to work if the official stuff (or some part or some dependency) is installed.
RUN /opt/wine-stable/bin/wine --version || true
RUN file /opt/wine-stable/bin/wine

RUN /opt/wine-stable/bin/wine64 --version || true
RUN file /opt/wine-stable/bin/wine64

RUN /opt/wine/wine-9.0-rc1-custom-amd64/bin/wine --version || true
RUN file /opt/wine/wine-9.0-rc1-custom-amd64/bin/wine

RUN /opt/wine/wine-9.0-rc1-custom-x86/bin/wine --version || true
RUN file /opt/wine/wine-9.0-rc1-custom-x86/bin/wine

#RUN find / -name '*wine*'
