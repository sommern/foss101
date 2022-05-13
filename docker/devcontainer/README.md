(taken from https://github.com/HFOSSedu/GitKit/issues/23 by
braughtg)

I couldn't fork or make a PR for this so here is an issue that presents a working **prototype**.

It is based on this image:
* https://github.com/accetto/ubuntu-vnc-xfce-g3/blob/master/docker/xfce-firefox/README.md

## Dockerfile

```
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
```

## To create the image:
`docker build -t tiger .`

## To run the image:
`docker run -p 6901:6901 tiger`

## Connect to noVNC:
* Point browser at: `localhost:6901`
* Click "Connect"
* Password: headless

## Launch VSCode:
* Open a terminal
* `code --no-sandbox`

## Comments
* This needs some polish but it works pretty well and is very responsive on my machine.
  * Make a nice user
  * Install git
  * etc...
* I started from an image that has TigerVNC installed
  * It runs both a VNC and a noVNC server.
  * It is being actively maintained with a new image within the last two weeks.
* One challenge is copy and paste between host and container
  * There is a clipboard hack in the noVNC client that works but is inconvenient.
  * The TigerVNC client works better, allows host/container copy/paste and is simple to install.
    *  https://tigervnc.org/
    * Need to open another port to use the standalone client.
      * `docker run -p 6901:6901 -p 5901:5901 tiger`
    * The UI appears to be in french when I run the most recent version but I suspect this can be fixed.
* The need to use `--no-sandbox` flag on VSCode is a quick hack to fix the issue:
  * `Failed to move to new namespace: PID namespaces supported, Network namespace supported, but failed: errno = Operation not permitted`
  * Should be pretty easily fixable with some research.



