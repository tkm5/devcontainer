FROM python:3.13-slim

ARG TZ=Asia/Tokyo
ENV TZ="$TZ"

RUN DEBIAN_FRONTEND=noninteractive
RUN apt update && apt-get install -y --no-install-recommends \
  less \
  git \
  procps \
  sudo \
  fzf \
  zsh \
  man-db \
  wget \
  unzip \
  gnupg2 \
  gh \
  iptables \
  ipset \
  iproute2 \
  dnsutils \
  aggregate \
  jq \
  vim \
  && apt clean && rm -rf /var/lib/apt/lists/*

# Define the user
ARG USERNAME=ubuntu
RUN adduser --disabled-password --gecos '' ${USERNAME}
RUN echo "${USERNAME} ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/${USERNAME}

# Install Node.js
ARG NODE_VERSION=22
RUN wget -qO nodesource_setup.sh https://deb.nodesource.com/setup_${NODE_VERSION}.x && \
  bash nodesource_setup.sh && \
  apt install -y nodejs

# Setup npm global packages directory for non-root user
RUN mkdir -p /usr/local/share/npm-global && \
    chown -R ${USERNAME}:${USERNAME} /usr/local/share/npm-global
ENV NPM_CONFIG_PREFIX=/usr/local/share/npm-global
ENV PATH=$PATH:/usr/local/share/npm-global/bin

# Set `DEVCONTAINER` environment variable to help with orientation
ENV DEVCONTAINER=true

ARG GIT_DELTA_VERSION=0.18.2
RUN ARCH=$(dpkg --print-architecture) && \
  wget "https://github.com/dandavison/delta/releases/download/${GIT_DELTA_VERSION}/git-delta_${GIT_DELTA_VERSION}_${ARCH}.deb" && \
  sudo dpkg -i "git-delta_${GIT_DELTA_VERSION}_${ARCH}.deb" && \
  rm "git-delta_${GIT_DELTA_VERSION}_${ARCH}.deb"

USER ${USERNAME}

# Set the default shell to zsh
ENV SHELL=/bin/zsh

# Install omz for docker
ARG ZSH_IN_DOCKER_VERSION=1.2.1
RUN sh -c "$(wget -O- https://github.com/deluan/zsh-in-docker/releases/download/v${ZSH_IN_DOCKER_VERSION}/zsh-in-docker.sh)" -- \
  -p aliases \
  -p git \
  -p https://github.com/zsh-users/zsh-syntax-highlighting \
  -a "CASE_SENSITIVE='true'" \
  -a "export HISTFILE=/commandhistory/.zsh_history" \
  -x

# Install Gemini-CLI
ARG GEMINI_CLI_VERSION=latest
RUN npm install -g @google/gemini-cli@${GEMINI_CLI_VERSION}

# Install python libraries
COPY requirements.txt .
RUN pip3 install --no-cache-dir -r requirements.txt
