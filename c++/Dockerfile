FROM alpine:3.20 AS install_env

FROM install_env AS build_env

# setup for c++
RUN apk update && \
    apk add --no-cache \
    bash \
    build-base \ 
    cmake \
    clang \
    jq \
    yq \
    lld \
    lldb \
    llvm \
    linux-headers \
    perl \
    python3 \
    py3-pip

RUN pip install conan --break-system-packages

ENV WORDIR=/workdir
ENV CONAN_HOME="${WORKDIR}/.conan"
ENV CONAN_REVISION_ENABLED=1
WORKDIR ${WORDIR}

ENV CC=clang
ENV CXX=clang++
ENV CFLAGS="-fuse-ld=lld -Wno-unused-command-line-argument"
ENV CXXFLAGS="-fuse-ld=lld -Wno-unused-command-line-argument"

SHELL [ "/bin/bash", "-c" ]

ENTRYPOINT [ "tail", "-f", "/dev/null" ]

FROM build_env AS dev
ARG git_email
ARG git_name

RUN apk update && \
    apk add --no-cache \
    git \
    gdb \
    vim \
    openssh \
    zsh \
    curl && \
    git config --global user.email "${git_email}" && \
    git config --global user.name "${git_name}" 

# FROM build_env as prod

# ARG CI=false
# ARG CI_DEBUG=false
# ARG BUILD_TYPE=Release
# ARG CONAN_USER
# ARG CONAN_PASS

