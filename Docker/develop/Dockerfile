FROM ubuntu
MAINTAINER tshst <takaoka.shuichi@gmail.com>

# package install
ENV DEBIAN_FRONTEND=noninteractive \
    SHELL=/bin/bash \
    PYENV_ROOT="$HOME/.anyenv/envs/pyenv"
RUN apt update && apt install -y \
    unixodbc \
    wx-common \
    build-essential \
    libncurses5-dev \
    libssl-dev \
    libbz2-dev \
    libreadline-dev \
    libsqlite3-dev \
    zlib1g-dev \
    libffi-dev \
    autoconf \
    vim \
    vim-gnome \
    exuberant-ctags \
    git \
    tig \
    curl \
    wget \
    whois \
 && apt clean \
 && rm -rf /var/lib/apt/lists/*

COPY ./requirements.txt /tmp/
RUN git clone https://github.com/riywo/anyenv /root/.anyenv \
    && echo 'export PATH="$HOME/.anyenv/bin:$PATH"' >> /root/.bashrc \
    && echo 'eval "$(anyenv init -)"' >> /root/.bashrc \
    && git clone https://github.com/pyenv/pyenv.git /root/.anyenv/envs/pyenv \
    && export PYENV_ROOT="/root/.anyenv/envs/pyenv" \
    && /bin/bash -c 'export PATH="/root/.anyenv/bin:$PYENV_ROOT/bin:$PATH" \
    && pyenv install 3.7.0 \
    && pyenv global 3.7.0'
RUN /root/.anyenv/envs/pyenv/shims/pip install --upgrade pip \
    && /root/.anyenv/envs/pyenv/shims/pip install -r /tmp/requirements.txt
RUN git clone https://github.com/syndbg/goenv.git /root/.anyenv/envs/goenv \
    && export GOENV_ROOT="/root/.anyenv/envs/goenv" \
    && /bin/bash -c 'export PATH="$GOENV_ROOT/bin:$PATH" \
    && goenv install 1.10.3 \
    && goenv global 1.10.3'
COPY ./.vimrc /root/
RUN git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
RUN echo | echo | vim +PluginInstall +qall

