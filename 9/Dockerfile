# ==============================================================================
# Hammer Node
# Docker Node.JS image on steroids.
# 
# @license Apache-2.0
# ==============================================================================

FROM node:9-alpine
MAINTAINER AaronJan <aaronjan@qq.com>

# create basic folders.
# /web/application/ is for your project.
RUN mkdir -p /web/application/ \
# /web/config/ for all your configurations.
        && mkdir -p /web/configs/ \
# /web/temp/ for temporary files.
        && mkdir -p /web/temp/ \
# /web/crontabs/ for Cron.
        && mkdir -p /web/crontabs/ \
# /root/.ssh/ for SSH stuff.
        && mkdir -p ~/.ssh/ \
# /var/log/supervisord/ for Supervisord's logs.
        && mkdir -p /var/log/supervisord/

# Copy configuration.
COPY configs/supervisord.conf /web/configs/

# Install necessary extensions.
#

RUN apk add --no-cache --virtual .build-deps build-base autoconf zip unzip openssh-client openssl-dev wget

# Supervisor providers extensibility, Cron lets you do task scheduling.
RUN apk add --no-cache git vim rsync

# Clean up.
RUN apk del .build-deps

# Switch to your project folder.
WORKDIR /web/application

# Start application using Supervisord.
CMD ["/usr/bin/supervisord", "-c", "/web/configs/supervisord.conf"]