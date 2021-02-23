#
#--------------------------------------------------------------------------
# Image Setup
#--------------------------------------------------------------------------
#

FROM jenkins/jenkins:2.263.4-slim
LABEL maintainer="chinayin <whereismoney@qq.com>" Version="2.263.4-slim"
ENV DEBIAN_FRONTEND=noninteractive DEPLOY_IMAGE_VERSION="2021-02-23 11:31"

USER root

ARG CHANGE_SOURCE=true
ARG TIMEZONE=Asia/Shanghai
RUN if [ ${CHANGE_SOURCE} = true ]; then \
    sed -i 's/deb.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list && \
    sed -i 's/security.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list && \
    sed -i 's/security-cdn.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list \
;fi && cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo "${TIMEZONE}" > /etc/timezone;

RUN set -eux; \
    apt-get update; apt-get autoremove -y; apt-mark hold tzdata; apt-get upgrade -y; \
    apt-get install -y --no-install-recommends \
        apt-utils wget vim procps iputils-ping net-tools telnet unzip \
    ; \
    apt-get clean; rm -rf /var/lib/apt/lists/*; \
    printf "alias ls='ls --color=auto'\nalias ll='ls -l --color=auto'\nalias l='ls -lA --color=auto'" >> /root/.bashrc

USER jenkins
