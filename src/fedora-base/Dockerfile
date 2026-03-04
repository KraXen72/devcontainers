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
        meld \
        jq \
        sqlite3 \
        less \
        man-db \
        procps-ng \
        python${PYTHON_VERSION} \
        python3-pip \
        ripgrep \
        shadow-utils \
        uv \
        which \
        unzip \
        util-linux \
        wget \
        xz \
    && dnf -y copr enable jdxcode/mise \
    && dnf -y install mise \
    && ln -sf /usr/bin/python${PYTHON_VERSION} /usr/bin/python3 \
    && ln -sf /usr/bin/python${PYTHON_VERSION} /usr/bin/python \
    && ln -sf /usr/bin/pip3 /usr/bin/pip \
    && ln -sf /usr/lib64/chromium-browser/headless_shell /usr/bin/headless_shell \
    && useradd -m -s /bin/bash -u 1000 vscode \
    && printf '%s\n' 'eval "$(mise activate bash)"' > /etc/profile.d/mise.sh \
    && chmod 0644 /etc/profile.d/mise.sh \
    && mkdir -p /go/bin \
    && su - vscode -c 'mise use -g node@lts' \
    && dnf clean all

ENV GOPATH=/go
ENV MISE_DATA_DIR=/home/vscode/.local/share/mise
ENV PATH=/go/bin:${MISE_DATA_DIR}/shims:${MISE_DATA_DIR}/bin:${PATH}
ENV ROD_CHROME_BIN=/usr/bin/headless_shell
