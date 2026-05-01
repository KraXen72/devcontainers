FROM registry.fedoraproject.org/fedora:43

ARG PYTHON_VERSION=3.12

RUN dnf -y upgrade \
    && dnf -y install \
        bash-completion \
        ca-certificates \
        chromium-headless \
        curl \
        dnf-plugins-core \
        git \
        golang \
        jq \
        less \
        man-db \
        meld \
        nodejs \
        dropbear \
        procps-ng \
        python${PYTHON_VERSION} \
        python3-pip \
        ripgrep \
        shadow-utils \
        sqlite3 \
        tree \
        unzip \
        util-linux \
        uv \
        wget \
        which \
        xz \
    && dnf -y copr enable dejan/lazygit \
    && dnf -y install lazygit \
    && ln -sf /usr/bin/python${PYTHON_VERSION} /usr/bin/python3 \
    && ln -sf /usr/bin/python${PYTHON_VERSION} /usr/bin/python \
    && ln -sf /usr/bin/pip3 /usr/bin/pip \
    && ln -sf /usr/lib64/chromium-browser/headless_shell /usr/bin/headless_shell \
    && useradd -m -s /bin/bash -u 1000 vscode \
    && mkdir -p /go/bin \
    && dnf clean all

ENV GOPATH=/go
ENV PATH=/go/bin:${PATH}
ENV ROD_CHROME_BIN=/usr/bin/headless_shell
