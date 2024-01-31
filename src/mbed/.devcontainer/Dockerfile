# [Choice] Debian / Ubuntu version (use Debian 12, Debian 11, Ubuntu 22.04 on local arm64/Apple Silicon): debian-12, debian-11, debian-10, ubuntu-22.04, ubuntu-20.04
FROM mcr.microsoft.com/devcontainers/base:${templateOption:imageVariant}
USER root

RUN curl -sfL https://github.com/devcontainers-contrib/nanolayer/releases/download/v0.5.6/nanolayer-$(arch)-unknown-linux-gnu.tgz | tar fxvz - -C / && \
    /nanolayer install apt-get wget,tar && \
    /nanolayer install apt-get cmake,ninja-build,ccache && \
    /nanolayer install apt-get python3-jinja2,python3-intelhex,python3-future,python3-prettytable && \
    /nanolayer install devcontainer-feature "ghcr.io/devcontainers-contrib/features/pipx-package:1.1.7" --option package='mbed-tools' && \
    rm /nanolayer

WORKDIR /opt/mbed-os-toolchain
RUN TARBALL="gcc-arm-none-eabi-${templateOption:toolchainVersion}-$(arch)-linux.tar.bz2" && \
    wget -q https://developer.arm.com/-/media/Files/downloads/gnu-rm/${templateOption:toolchainVersion}/${TARBALL} && \
    tar -xjf ${TARBALL} && \
    rm ${TARBALL}
ENV MBED_GCC_ARM_PATH=/opt/mbed-os-toolchain/gcc-arm-none-eabi-${templateOption:toolchainVersion}/bin/
ENV PATH="${PATH}:${MBED_GCC_ARM_PATH}"



ARG USERNAME=vscode