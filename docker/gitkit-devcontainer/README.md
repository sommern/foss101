# Devcontainer for GitKit

This subproject creates a Docker image that can be used by students
as a complete self-contained development environment for use with
GitKit and its activities.

## 1. Use

### 1.1 Requirements

* Docker Desktop installed and running for your Operating System.

### 1.2. Start a Devcontainer

1. Open a terminal and run the following command.

    ```
    docker run -p 6901:6901 hfossedu/gitkit-devcontainer
    ```

    It may take several minutes the first time you run this.
    Subsequent runs will be faster.

    Leave the terminal open.

2. Connect to noVNC:

    * Point browser at: http://localhost:6901/
    * Select full or light client.
    * Click "Connect"
    * Password: headless


Now work inside the browser to work inside the devcontainer.

### 1.3. Launch VS Code inside devcontainer

Within the browser:

1. Open a terminal and enter

    ```
    code --no-sandbox
    ```


### 1.4. Stop the Devcontainer

Return to the terminal in which you started the container and press `CTRL+C`.

---

## 2. Development

### 2.1. Build the image

```
docker build -t gitkit-devcontainer .
```

### 2.2. Test the image

Manual testing: Assuming you just built the container, test it by running it the same way a user would, except use `hfossedu/gitkit-devcontainer:dev` instead.

Automated testing: No such thing at this time.

### 2.3. Push/release the image

```
docker tag gitkit-devcontainer hfossedu/gitkit-devcontainer:latest
docker login
docker push hfossedu/gitkit-devcontainer:latest
```

### 2.4. Notes

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
