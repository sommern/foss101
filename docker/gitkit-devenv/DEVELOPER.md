# Developer Documentation

Run all commands below in the same directory as this file.

### 2.1. Build the image

```
docker build -t gitkit-devenv .
```

### 2.2. Test the image

Manual testing: Assuming you just built the container, test it by running it the same way a user would, except use `gitkit-devenv` instead.

Automated testing: No such thing at this time.

### 2.3. Push/release the image

```
docker tag gitkit-devenv hfossedu/gitkit-devenv:latest
docker login
docker push hfossedu/gitkit-devenv:latest
```

---

## Notes

* This needs some polish but it works pretty well and is very responsive on my machine.
  * Make a nice user
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


Install

* Meld
* Gedit
* Vim
* Emacs

