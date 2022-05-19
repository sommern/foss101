FROM accetto/ubuntu-vnc-xfce-firefox-g3

USER root

# Install common developer tools
RUN apt-get update && \
    apt-get -y install \
        git \
        gedit \
        vim \
        emacs \
        nano \
        meld

# Install VS Code
RUN apt-get -y install wget gpg apt-transport-https && \
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg && \
    install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/ && \
    sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/trusted.gpg.d/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list' && \
    rm -f packages.microsoft.gpg && \
    apt-get update && \
    apt-get -y install code && \
    apt-get -y --purge remove wget apt-transport-https

USER headless
