##
#
# This Image provides a simple base for redbot, a self hosted discord bot.
#
##

FROM docker.io/library/rockylinux:8

LABEL maintainer=ccarney16@live.com

ARG VERSION

# Update Core Packages
RUN dnf -y update && \
    dnf -y install cmake findutils git make gcc python39 python39-pip python39-devel && \
    dnf -y clean all && \
    dnf clean all

# Create a unprivileged container user
RUN useradd -r -u 1500 container

# Prepare all python dependencies for redbot
# We wont use venv as docker/podman already provide us with an isolated environment
RUN python3.9 -m pip install -U pip setuptools wheel
RUN python3.9 -m pip install -U Red-DiscordBot[postgres]==${VERSION}

# Change these variables so that redbot doesnt save to home
ENV XDG_CONFIG_HOME="/config" XDG_DATA_HOME="/data" XDG_DATA_DIRS="/data"

# Use 'container' user
USER container

ENTRYPOINT [ "/usr/local/bin/redbot" ]