# Use the official Debian base image
FROM debian:bullseye

# Set up environment variables
ENV QUARTUS_ROOTDIR="/opt/intelFPGA_lite/quartus"
ENV PATH="${QUARTUS_ROOTDIR}/bin:${PATH}"

# Install necessary dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    libpng-dev \
    libtinfo5 \
    libstdc++6 \
    libx11-6 \
    libxext6 \
    libxrender1 \
    libxtst6 \
    libxi6 \
    ca-certificates \
    curl \
    locales && \
    rm -rf /var/lib/apt/lists/*

# Set locale to UTF-8
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen en_US.UTF-8 && \
    update-locale LANG=en_US.UTF-8

# Download and Install Quartus Lite
RUN curl -fsSL https://downloads.intel.com/akdlm/software/acdsinst/22.1std.1/917/ib_tar/Quartus-lite-22.1std.1.917-linux.tar -o quartus-lite.tar
RUN mkdir -p /setup
RUN tar -xvf quartus-lite.tar -C /setup
RUN /setup/setup.sh --mode unattended --accept_eula 1
RUN rm -rf quartus-lite.tar /setup

# Set working directory
WORKDIR /workspace

# Start a shell by default
CMD ["/bin/bash"]
