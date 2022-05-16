# GitKit Development Environment

This provides a development enviornment for use with the GitKit. This
development environment runs inside a Docker container running on the
participants local machine, and is accessed through a Web browser.

> **Information**
>
> If you are interested in contributed to this project,
> see [the developer documentation](DEVELOPMENT.md)

## Requirements

* Docker Desktop

## Start Docker Desktop

Before you can manage the GitKit development environment, the Docker
engine must be running. The easist way to do that is to start Docker
Desktop.

## Start the Development Environment

Open a terminal and run the following command.

```
docker run --name devenv --detach -p 6901:6901 hfossedu/gitkit-devenv
```

It may take several minutes the first time you run this.
Subsequent runs will be faster.

## Work in the Development Environment

1. Open a Web browser to http://localhost:6901/
2. Select full or light client.
3. Select "Connect"
4. Enter password: headless

You can now interact with the development environment inside your
Web browser.

Within the development environment, you can open a terminal giving you
a bash shell. From within a bash shell, you have access to a number
of common development tools:

* Version control:
    ```
    git
    ```
* Merge conflict resolution tool:
    ```
    meld
    ```
* Text editors:
    ```
    nano
    pico
    emacs
    vim
    ```
* VS Code:
    ```
    code --no-sandbox
    ```
* Package manager to install other tools:
    ```
    sudo apt install ...
    ```

## Stop the Development Environment

Open a terminal ***on the host machine*** (i.e., not inside the
development environment) and enter the following command.

```
docker stop devenv
```

## Start a stopped Development Environment

Open a terminal ***on the host machine*** (i.e., not inside the
development environment) and enter the following command.

```
docker start devenv
```

## Remove a stoped Development Environment

> **Warning**
>
> All of the files that you create or modified inside the development
> environment only exist inside the development environment. If you remove
> the development environment, you will also lose these files.

First stop the development environment.

Then remove the development environment as follows.

```
docker rm devenv
```

## Remove the GitKit Development Environment Image from Docker

First stop and remove all containers created from the GitKit Development
Environment image.

Then remove the GitKit Development Environment image as follows.

```
docker rmi hfossedu/gitkit-devenv
```
