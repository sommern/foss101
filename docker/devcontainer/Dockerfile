FROM accetto/ubuntu-vnc-xfce-firefox-g3

USER root

RUN sudo apt update
RUN sudo apt-get -y install wget gpg
RUN sudo wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
RUN sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/
RUN sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/trusted.gpg.d/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
RUN sudo rm -f packages.microsoft.gpg
RUN sudo apt -y install apt-transport-https
RUN sudo apt update
RUN sudo apt -y install code

USER headless
