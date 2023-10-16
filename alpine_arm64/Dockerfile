FROM alpine:edge AS builder

LABEL maintainer="Alan Ho <github.com/indefinite-future>"

RUN \
    echo "https://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && \
    echo 'root:Docker!' | passwd -d root && \
    apk update --no-cache && \
    apk add --no-cache \
    tzdata \
    curl \
    wget \
    unzip \
    sddm \
    htop \
    bash \
    flatpak \
    pcmanfm \
    openrc \
    openssl \
    firefox \
    font-noto-cjk \
    nodejs \
    npm \
    py3-pip \
    py3-numpy \
    plasma \
    elogind \
    polkit-elogind \
    plasma-desktop \
    plasma-workspace \
    kwin \
    git \
    xvfb \
    xvfb-run \
    x11vnc \
    lxterminal

RUN git clone --depth=1 --recursive https://github.com/novnc/noVNC /novnc

RUN echo '<!DOCTYPE html>' > /novnc/index.html \
    && echo '<html>' >> /novnc/index.html \
    && echo '  <head>' >> /novnc/index.html \
    && echo '    <title>noVNC Redirect</title>' >> /novnc/index.html \
    && echo '    <meta http-equiv="refresh" content="0;url=vnc.html">' >> /novnc/index.html \
    && echo '  </head>' >> /novnc/index.html \
    && echo '</html>' >> /novnc/index.html

EXPOSE 80

WORKDIR /root

ENV HOME=/root \
    TZ=Asia/Hong_Kong

CMD nohup xvfb-run -f ~/.Xauthority --server-args="-screen 0 1440x900x24" plasma_session & \
    nohup x11vnc -norc -forever -shared -display :99 & \
    nohup /novnc/utils/novnc_proxy --vnc 0.0.0.0:5900 --listen 80 \
    flatpak remote-add --user --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo \
    rc-update add dbus \
    rc-update add elogind \
    rc-update add polkit \
    rc-update add sddm \
    rc-service sddm start




