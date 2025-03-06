# 🏗️ 基础镜像选择：轻量且兼容性强的 Ubuntu
FROM ubuntu

# 🚫💬 避免安装过程中的交互提示
ENV DEBIAN_FRONTEND=noninteractive

############################################
# 📦 开发环境基础套件安装
############################################
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

############################################
# 🔧 安装最新 LLVM/Clang 19 全家桶
############################################
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

############################################
# ⚙️ 配置默认开发环境
############################################
RUN update-alternatives --install \
    /usr/bin/clang clang /usr/bin/clang-19 100 && \
    update-alternatives --install \
    /usr/bin/clang++ clang++ /usr/bin/clang++-19 100 && \
    update-alternatives --install \
    /usr/bin/lld lld /usr/bin/lld-19 100

# 🌍 全局环境变量配置（影响所有构建系统）
# 🎨 C 编译器指定
ENV CC=/usr/bin/clang
# 🎨 C++ 编译器指定
ENV CXX=/usr/bin/clang++

# 📂 创建工作区（你的代码将存放在这里）
WORKDIR /workspace

# 🧼 深度清理（镜像体积优化关键步骤！）
RUN apt-get clean

# 🖥️ 默认启动交互式终端（进入容器即可开始编码）
CMD ["/bin/bash"]
