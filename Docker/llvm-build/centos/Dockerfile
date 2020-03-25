FROM centos:8

    # setting debug
RUN set -x && \

    dnf -y update && \
    
    # Installation of build tools and necessary command(package)
    dnf -y install gcc-c++ && \
    dnf -y install python36 && \
    dnf -y install wget && \
    dnf -y install git && \
    dnf -y install make

    # make working directory
    cd / && \
    mkdir install-llvm && \
    cd install-llvm && \
    mkdir cmake && \
    cd cmake && \

    # download & install cmake 3.17
    wget https://github.com/Kitware/CMake/releases/download/v3.17.0/cmake-3.17.0-Linux-x86_64.sh && \
    printf 'y\y' | sh ./cmake-3.17.0-Linux-x86_64.sh && \
    mv cmake-3.17.0-Linux-x86_64 /opt/cmake && \
    echo 'export PATH=$PATH:/opt/cmake/bin' >> ~/.bashrc && \
    source ~/.bashrc && \

    # make working directory
    cd /install-llvm/ && \
    mkdir llvm && \
    cd llvm && \

    # git clone LLVM source code
    git clone https://github.com/llvm/llvm-project.git && \
    cd llvm-project

    # make working directory
    mkdir build && \
    cd build/ && \
    
    # build LLVM
    cmake -G "Unix Makefiles" ../llvm/ -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local
    make -j$(grep processor /proc/cpuinfo | wc -l) && \
    make install

ENTRYPOINT ["/bin/sh"]