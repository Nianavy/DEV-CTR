FROM ubuntu

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y \
    build-essential \
    wget \
    gnupg \
    software-properties-common \
    cmake \
    ninja-build \
    git \
    gdb \
    clang-tidy \
    clang-format \
    pkg-config \
    glibc-doc \
    tcpdump \
    tshark \
    tmux \
    libreadline-dev \
    device-tree-compiler \
    && rm -rf /var/lib/apt/lists/*

RUN wget -qO- https://apt.llvm.org/llvm.sh | bash -s -- 19
RUN apt-get update && \
    apt-get install -y \
    clang-19 \
    lldb-19 \
    lld-19 \
    clangd-19 \
    libc++-19-dev \
    libc++abi-19-dev \
    && rm -rf /var/lib/apt/lists/*

RUN update-alternatives --install \
    /usr/bin/clang clang /usr/bin/clang-19 100 && \
    update-alternatives --install \
    /usr/bin/clang++ clang++ /usr/bin/clang++-19 100 && \
    update-alternatives --install \
    /usr/bin/lld lld /usr/bin/lld-19 100

ENV CC=/usr/bin/clang
ENV CXX=/usr/bin/clang++

WORKDIR /workspace

RUN apt-get clean

CMD ["/bin/bash"]
