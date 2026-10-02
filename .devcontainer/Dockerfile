# syntax=docker/dockerfile:1

ARG VARIANT="23"
FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:0-${VARIANT}
ARG CAPVER="latest"

# Install some generally useful tools
RUN echo 'deb http://archive.debian.org/debian bullseye main' > /etc/apt/sources.list \
    && echo 'deb http://archive.debian.org/debian bullseye-updates main' >> /etc/apt/sources.list \
    && apt-get update \
    && apt-get -y install --no-install-recommends --fix-missing \
    curl git sqlite3 entr source-highlight \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install SAP CAP SDK globally
USER node
RUN npm install -g @sap/cds-dk@$CAPVER

# vi mode everywhere and nicer prompt KTHXBAI
RUN cat <<EOBASHRC >> /home/node/.bashrc
export EDITOR=vi
set -o vi
bind -x '"\C-l": clear'
EOBASHRC

RUN echo 'export PS1=${PS1/\$ /\\\\n$ }' >> /home/node/.bashrc

# Ready!
WORKDIR /home/node
