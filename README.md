# LaTeX环境搭建，支持VS Code和GitHub Codespaces

如果你是一个新人想要学习LaTeX，请直接使用[Overleaf](https://www.overleaf.com/)，去官网注册之后即可享有完整的LaTeX环境，无需部署，即开即用。

## 由来
由于众所周知的原因，国内网络访问外网非常不稳定，以及Overleaf在各大会议ddl之前经常编译缓慢(或者宕机)，所以我有了在本地部署一套LaTeX环境进行写作的需求。由于LaTeX的众多版本以及依赖问题，在本地部署LaTeX环境并非易事，安装不慎还可能对本机系统依赖造成破坏。所幸Texlive拥有完整的Docker镜像，使用Docker部署并不会对本机造成任何影响，于是本项目采用Docker部署LaTeX环境，并搭配VS Code进行写作。

如果你和我一样有在本地使用VS Code编写LaTeX的需求，可以参照以下步骤进行部署。

## 安装

### 方式一：部署LaTeX环境到本机

此方式会将LaTeX环境部署到本机。
#### 优点：
- 即使处于断网状态，依然不影响写作。
#### 缺点：
- 需要安装Docker和Texlive镜像在本机上，占用本机的磁盘空间。
- Docker容器运行在本机上，占用本机的资源，尤其是CPU和内存有限的设备上。
- 如果你有多台设备写作的需求，需要在每一台设备上都部署环境，比较麻烦。

#### 步骤
1. 在本机安装 [Docker](https://docs.docker.com/get-started) 和 [VS Code](https://code.visualstudio.com/download)
2. 在VS Code里安装 [Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)扩展
3. 下载本项目到本地，用VS Code打开。
4. 在VS Code的命令面板中（可以按快捷键`F1`打开）执行`Remote-Containers: Reopen in Container`.

安装完成后如下图所示：
![latex-vscode-desktop.png](https://s2.loli.net/2022/03/31/wiZUVJjFf4Pr23q.png)

### 方式二：部署LaTeX环境到远程服务器
此方式会将LaTeX环境部署到一台远程服务器上。可以是自己购买的VPS，也可以是公司、学校、实验室的服务器。
#### 优点：
- 无需在本机安装Docker及Texlive镜像，不占用本机磁盘空间。
- Docker容器运行在远程服务器上，对本机性能没有影响。
- 一次部署，多设备共用。只需在一台服务器上部署，可以在任意一台能够连接该服务器的设备上使用。
#### 缺点：
- 需要你拥有一台服务器。
- 需要连接到服务器才能使用，在断网环境下不可用。
- 在服务器上安装和启用Docker需要使用sudo权限，本方式不适用只有普通权限的用户。
    - 你可以联系管理员在服务器上安装Docker之后，使用`sudo usermod -aG docker your_username` 把你的用户名添加到docker用户组，这样你就能以普通用户权限使用docker服务，详情参考[官方说明](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user)。

#### 步骤
1. 在**远程服务器**上安装 [Docker](https://docs.docker.com/get-started)。
2. 在**本机**安装 [VS Code](https://code.visualstudio.com/download)。
3. 在VS Code里安装 [Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) 和 [Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)扩展。
4. 下载本项目到**远程服务器**.
5. 使用`Remote - SSH`连接到远程服务器, 并打开刚刚下载的项目文件夹。
6. 在VS Code的命令面板中（可以按快捷键`F1`打开）执行`Remote-Containers: Reopen in Container`.

安装完成后如下图所示：
![latex-vscode-remote.png](https://s2.loli.net/2022/03/31/kjEyzIYDq9lb1Sx.png)


### 方式三：部署LaTeX环境到GitHub Codespaces

此方式利用GitHub的[Codespaces](https://github.com/features/codespaces)服务，将LaTeX环境部署到GitHub的云端服务器上。目前Codespaces服务针对个人用户免费使用。

#### 优点：
- 无需拥有一台服务器。
- 无需在本机安装Docker及Texlive镜像，不占用本机磁盘空间。
- Docker容器运行在GitHub的云端服务器上，对本机性能没有影响。
- 无需安装任何本地客户端，可以直接在浏览器里使用，多设备可用。
    - GitHub的Codespaces同样支持用本地的VS Code打开。

#### 缺点：
- 需要连接到服务器才能使用，所以在断网环境下不可用。
- 国内网络访问GitHub的速度....

#### 步骤
1. Fork本项目到你自己名下。

2. 参考下图流程新建一个Codespaces即可在浏览器里打开。

![github-codespaces-guide.png](https://s2.loli.net/2022/03/31/3G6eXEru54LjnPR.png)

安装完成后如下图所示：
![latex-github-codespaces.png](https://s2.loli.net/2022/03/31/Br79uhDOnJFRNwi.png)

3. （可选）GitHub Codespaces同样支持使用本机的VS Code连接，需要在本机的VS Code中安装[GitHub Codespaces](https://marketplace.visualstudio.com/items?itemName=GitHub.codespaces)，具体使用教程详见[官方文档](https://docs.github.com/en/codespaces/developing-in-codespaces/using-codespaces-in-visual-studio-code)。


## FAQ
### 如何定制我自己的环境？
本项目所有初始配置均在`.devcontainer/devcontainer.json`文件中定义。

https://github.com/zydou/latex-template/blob/5da68ee36f1699622a9fa6728320b2357addcc46/.devcontainer/devcontainer.json#L1-L11

修改该文件即可更改初始化配置，下面列出一些常见的定制选项，更多具体的设置详见[官方文档](https://code.visualstudio.com/docs/remote/devcontainerjson-reference)

注意，每一次更改`.devcontainer/devcontainer.json`文件后，都需要重新编译容器，具体方法为在VS Code的命令面板中（可以按快捷键`F1`打开）执行`Remote-Containers: Rebuild Container`.

### 1. 如何更改Texlive的版本？

修改`.devcontainer/devcontainer.json`文件中的`image`值，如改为`"image": "texlive/texlive:TL2020-historic"`即切换为Texlive-2020。

当前可用的版本如下：

* `latest` (目前是2021版)
* `TL2020-historic`
* `TL2019-historic`
* `TL2018-historic`
* `TL2017-historic`
* `TL2016-historic`
* `TL2015-historic`
* `TL2014-historic`

更多版本请参考：[https://hub.docker.com/r/texlive/texlive](https://hub.docker.com/r/texlive/texlive)

### 2. 如何安装其他VS Code扩展？
`.devcontainer/devcontainer.json`文件中的`extensions`选项定义了默认安装的扩展。本项目默认仅安装了[LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop)一个扩展。添加所需扩展对应的`Extension ID`到`extensions`列表中即可, 以[LTeX](https://marketplace.visualstudio.com/items?itemName=valentjn.vscode-ltex)扩展举例：

```json
    "extensions": [
    "james-yu.latex-workshop",
    "valentjn.vscode-ltex"
    ]
```

### 3. 我的网络拉取Texlive镜像非常慢，如何加速？
本项目默认从DockerHub拉取镜像，如果你从DockerHub拉取镜像很慢的话，可以尝试更改为国内拉取源。具体方法是修改`.devcontainer/devcontainer.json`文件中的`image`值，以Texlive-2021举例：
```json
{
    "name": "Texlive-2021",
    "image": "zydou-docker.pkg.coding.net/docker/mirror/texlive/texlive:latest",
    "extensions": [
    "james-yu.latex-workshop"
    ]
}
```

Texlive-2020（其余同理）：
```json
{
    "name": "Texlive-2020",
    "image": "zydou-docker.pkg.coding.net/docker/mirror/texlive/texlive:TL2020-historic",
    "extensions": [
    "james-yu.latex-workshop"
    ]
}
```
