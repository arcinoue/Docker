FROM ubuntu:18.04

RUN set -x && \
    apt-get update && \

    # installation of build tools
    apt-get install -y make cmake gcc g++ python git && \

    # make working directory
    cd / && \
    mkdir install-llvm && \
    cd install-llvm && \
    mkdir llvm && \
    cd llvm && \

    # git clone LLVM source code
    git clone https://github.com/llvm/llvm-project.git && \
    cd llvm-project && \

    # make working directory
    mkdir llvm-build && \
    cd llvm-build && \

    # make
    cmake -G "Unix Makefiles" ../llvm/ -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local && \
    make -j$(grep processor /proc/cpuinfo | wc -l) && \
    make install

ENTRYPOINT ["/bin/bash"]

