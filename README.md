# Set up a LaTeX environment for VS Code and GitHub Codespaces

<div align="center">
<a href="https://github.com/zydou/latex-template"><img src="https://img.shields.io/badge/English-green.svg"></a>
<a href="https://github.com/zydou/latex-template/blob/master/README-zh_CN.md"><img src="https://img.shields.io/badge/中文文档-purple.svg"></a>
</div>

If you are a newcomer looking to learn LaTeX, please use [Overleaf](https://www.overleaf.com/). After registering on their website, you can have a complete LaTeX environment in your browser without needing to install anything locally.

## Motivation

To avoid [slow compilation or downtime](https://status.overleaf.com/history) on Overleaf before major conference deadlines, I found it necessary to set up a local LaTeX environment for writing. However, deploying such an environment locally can be challenging due to the different versions and dependencies of LaTeX. Improper installation could potentially harm the system's dependencies. To address this issue, this project utilizes VS Code's [Dev Containers](https://code.visualstudio.com/docs/devcontainers/containers) feature, which deploys a complete LaTeX environment using Docker images without impacting the local machine.

If you also need to write LaTeX using VS Code locally, you can follow the steps below for deployment.

## Installation

### Method 1: Deploy LaTeX Environment to Local Machine

This method will deploy the LaTeX environment to your local machine.

#### Pros

- Writing is not affected even when you're offline.

#### Cons

- Requires installation of Docker and pulling TeX Live image to your local machine, consuming disk space.
- Docker container runs on your local machine, consuming system resources, especially on devices with limited CPU and memory.
- If you work on multiple machines, you need to deploy the environment on each machine separately, which can be cumbersome.

#### Steps

1. Install [Docker](https://docs.docker.com/get-started) and [VS Code](https://code.visualstudio.com/download) on your local machine.
2. Install the [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension in VS Code.
3. Clone this project to your local machine and open it with VS Code.
4. In the VS Code command palette (can be opened with the shortcut `F1`), search and execute `Dev Containers: Reopen in Container`.

After installation, it should look like this:

![latex-vscode-desktop.png](https://s2.loli.net/2022/03/31/wiZUVJjFf4Pr23q.png)

### Method 2: Deploy LaTeX Environment to Remote Server

This method involves deploying the LaTeX environment to a remote server. It can be a VPS you own, or a server from your company, school, or lab.

#### Pros

- No need to install Docker and TeX Live image on your local machine, saving disk space.
- Docker container runs on the remote server, not affecting local machine performance.
- Deploy it once on a server, and you can use it on any machine that can connect to that server.

#### Cons

- A remote server is required.
- Requires a connection to the server, making it unavailable in offline environments.
- Installing and running Docker on the server requires `sudo` privileges, which may not be suitable for users with only regular permissions.

    > You can contact the administrator to install Docker on the server and then use `sudo usermod -aG docker your_username` to add your username to the docker user group. This will allow you to use the docker service without `sudo` privileges. For more details, refer to the [official documentation](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user).

#### Steps

- Install [Docker](https://docs.docker.com/get-started) on the **remote server**.
- Install [VS Code](https://code.visualstudio.com/download) on your **local machine**.
- Install [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) and [Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) extensions in VS Code.
- Download this project to the **remote server**.
- Use `Remote - SSH` to connect to the remote server and open the downloaded project folder.
- In the VS Code command palette (can be opened with the shortcut `F1`), search and execute `Dev Containers: Reopen in Container`.

After installation, it should look like this:

![latex-vscode-remote.png](https://s2.loli.net/2022/03/31/kjEyzIYDq9lb1Sx.png)

### Method 3: Deploy LaTeX Environment to GitHub Codespaces

This method utilizes [GitHub Codespaces](https://github.com/features/codespaces) to deploy the LaTeX environmenton on a cloud-based server hosted by GitHub. ~~Currently, Codespaces service is free~~.

Update: Currently, for free tier users, Codespaces offers 120 free core-hours per month. However, since the minimum machine size in Codespaces is 2 cores, you actually have a maximum of 60 free hours per month.

#### Pros

- No need to own a remote server.
- No need to install Docker and TeX Live image on your local machine, saving disk space.
- Docker container runs on GitHub's cloud-based server, not affecting local machine performance.
- No need to install any local softwares (not even the need to install VS Code!). The only requirement is a web browser.
    > You can still open GitHub Codespaces in your local VS Code if you prefer.

#### Cons

- Paid service. You only have a maximum of 60 free hours per month.
- Requires a connection to GitHub, making it unavailable in offline environments.

#### Steps

1. Fork this project to your GitHub.
2. Follow the steps shown in the image below to create a Codespace and open it in your browser.
    ![github-codespaces-guide.png](https://s2.loli.net/2022/03/31/3G6eXEru54LjnPR.png)

    After finished, it should look like this:

    ![latex-github-codespaces.png](https://s2.loli.net/2022/03/31/Br79uhDOnJFRNwi.png)

3. (Optional) You can use GitHub Codespaces in your local VS Code. For detailed usage instructions, refer to the [official documentation](https://docs.github.com/en/codespaces/developing-in-codespaces/using-codespaces-in-visual-studio-code).

## Frequently Asked Questions

### How can I customize my environment?

The configurations for devcontainer can be found in the [.devcontainer/devcontainer.json](https://github.com/zydou/latex-template/blob/master/.devcontainer/devcontainer.json) file. To modify the configurations, simply edit this file. Here are some common customization options, and for more specific settings, refer to the [official documentation](https://code.visualstudio.com/docs/remote/devcontainerjson-reference).

⚠️Note that you need to rebuild the container every time you make changes to the `.devcontainer/devcontainer.json` file. To do this, open the VS Code command palette (can be opened with the shortcut `F1`), search and execute `Dev Containers: Rebuild Container`.

### 1. How to use a different version of Tex Live?？

Modify the `image` option in the `.devcontainer/devcontainer.json` file. For example, changing it to `"image": "zydou/devcontainer-texlive:2021"` will switch to Tex Live 2021. These images are based on `Debian Trixie` (aka Debian 13). If you want a different Debian distribution or want to switch to Ubuntu, you can add the distribution name after the year. For example, `"image": "zydou/devcontainer-texlive:2022-jammy"` is Tex Live 2022 built on `Ubuntu Jammy` (aka Ubuntu 22.04).

The available Tex Live versions are:

| TeX Live     | Description   |
| ------------ | ------------- |
| latest       | TeX Live 2023 |
| 2023         | TeX Live 2023 |
| 2022         | TeX Live 2022 |
| 2021         | TeX Live 2021 |
| 2020         | TeX Live 2020 |
| 2019         | TeX Live 2019 |
| 2018         | TeX Live 2018 |

The available Linux distributions are:

| Linux Distribution | Description  |
| ------------------ | ------------ |
| trixie             | Debian 13    |
| bookworm           | Debian 12    |
| bullseye           | Debian 11    |
| buster             | Debian 10    |
| jammy              | Ubuntu 22.04 |
| focal              | Ubuntu 20.04 |
| bionic             | Ubuntu 18.04 |
| xenial             | Ubuntu 16.04 |

Examples:

```sh
zydou/texlive:latest         # latest texlive on newest Debian
zydou/texlive:2022           # texlive-2022 on newest Debian
zydou/texlive:focal          # latest texlive on Ubuntu Focal
zydou/texlive:latest-buster  # latest texlive on Debian Buster
zydou/texlive:2021-jammy     # texlive-2021 on Ubuntu Jammy
```

💡Tip: The version support list above may be outdated. Please refer to the [zydou/texlive](https://github.com/zydou/texlive) repository for an accurate version support list.

### 2. How can I automatically install some VS Code extensions once the devcontainer is built?

The `extensions` option in the `.devcontainer/devcontainer.json` file defines the extensions that are installed by default. This project only installs the [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) and [LaTeX Snippets](https://marketplace.visualstudio.com/items?itemName=JeffersonQin.latex-snippets-jeff) extensions by default. Add the `Extension ID` of the desired extensions to the extensions list. For example, to add the [Dictionary Completion](https://marketplace.visualstudio.com/items?itemName=yzhang.dictionary-completion) extension:

```json
  "extensions": [
    "james-yu.latex-workshop",
    "JeffersonQin.latex-snippets-jeff",
    "yzhang.dictionary-completion"
  ]
```

### 3. How can I run custom commands once the devcontainer is built?

Add any commands to `.devcontainer/postCreateCommand.sh` script. This script will be automatically executed after the devcontainer is built. For example:

```sh
#!/bin/bash

## Install system packages
sudo apt-get update
sudo apt-get install -y system_package_name

## Update texlive packages
sudo tlmgr update texlive_package_name

## Download some fonts
mkdir "$HOME/.fonts"
curl -sSLf -o "$HOME/.fonts/font_name.ttf" "https://example.com/font_name.ttf"
fc-cache -fv
```
