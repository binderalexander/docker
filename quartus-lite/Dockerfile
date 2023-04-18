# Use the official Debian base image
FROM debian:bullseye

# Set up arguments
ARG QUARTUS_DIR="/opt/intelFPGA_lite/22.1std"
ARG QUARTUS_DISABLED_COMPONENTS=quartus_help,quartus_update,arria_lite,cyclone,cyclonev,max,max10,questa_fse,questa_fe

# Set up environment variables
ENV QUARTUS_ROOTDIR=${QUARTUS_DIR}
ENV PATH="${QUARTUS_DIR}/quartus/bin:${PATH}"

# Install necessary dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    ca-certificates \
    expect \
    git \
    libglib2.0-0 \
    libtcmalloc-minimal4 \
    locales \
    wget && \
    rm -rf /var/lib/apt/lists/*

# Set locale to UTF-8
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen en_US.UTF-8 && \
    update-locale LANG=en_US.UTF-8

# Download and Install Quartus Lite
RUN wget -q https://downloads.intel.com/akdlm/software/acdsinst/22.1std.1/917/ib_tar/Quartus-lite-22.1std.1.917-linux.tar -O quartus-lite.tar \
    && mkdir -p /setup \
    && tar -xf quartus-lite.tar -C /setup \
    && /setup/setup.sh --mode unattended --accept_eula 1 --installdir ${QUARTUS_DIR} --disable-components ${QUARTUS_DISABLED_COMPONENTS} \
    && rm -rf quartus-lite.tar /setup

# Set working directory
WORKDIR /workspace

# Start a shell by default
CMD ["/bin/bash"]
