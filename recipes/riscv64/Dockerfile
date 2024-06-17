FROM ubuntu:22.04

ARG GID=1000
ARG UID=1000

RUN getent group
RUN addgroup --gid $GID node
RUN adduser --gid $GID --uid $UID --disabled-password --gecos node node

RUN apt-get update \
    && apt-get dist-upgrade -y \
    && apt-get install -y software-properties-common \
    && add-apt-repository -y ppa:ubuntu-toolchain-r/test \
    && apt-get update \
    && apt-get install -y \
         git \
	 g++-12 \
         curl \
         make \
         python3 \
	 python3-distutils \
         ccache \
         xz-utils \
         g++-12-riscv64-linux-gnu

COPY --chown=node:node run.sh /home/node/run.sh

VOLUME /home/node/.ccache
VOLUME /out
VOLUME /home/node/node.tar.xz

USER node

ENTRYPOINT [ "/home/node/run.sh" ]
