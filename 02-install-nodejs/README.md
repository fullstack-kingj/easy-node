### [上一回 什么是 Node.js](../01-what-is-nodejs/README.md)

# 安装 Node.js

## 从官网获取最新版本的 Node.js

安装 Node.js 的最简单方法，就是从 Node.js 的[官方网站](https://nodejs.org/en/)获取最新版本的安装文件进行安装。

![Node.js 的官方网站](nodejs-official-website.png)

Windows 系统或者 MacOS 系统可以参考下面的图文教程来进行安装：

- [Windows 系统环境安装 Node.js 参考教程](../03-windows-system-environment-installation-nodejs/README.md)
- [MacOS 系统环境安装 Node.js 参考教程](../04-macos-system-environment-installation-nodejs/README.md)

> **这里需要注意的是：**
> 
> - 这种方式安装，每次更新 Node.js 的版本，都需要从官网下载，并且进行覆盖安装。
> - 这种方式安装，在系统中只能存在一个版本的 Node.js ，不适合对比学习。
>
> 如果你是第一次接触 Node.js，建议还是先使用官方这种方式安装最新版本的 Node.js。

## 使用 nvm 管理多版本 Node.js

首先，我们来简单地来了解一下 nvm。

nvm 是 [Tim Caswell](https://github.com/creationix) 开发的一款 MacOS 系统中使用的通过命令方式管理多版本 Node.js 的软件。

> nvm 软件的相关介绍，可以访问[该项目的 github 主页](https://github.com/creationix/nvm)。

### 一. 安装 nvm 版本管理器

> 想要成功的安装 nvm，MaOS 系统下必须要先安装 Xcode 软件， Xcode 软件大概在 4.3GB 左右。

如果不想安装 Xcode 软件，又想成功安装 nvm 的话，可以按照以下方式操作：

1、打开“终端”窗口，并输入以下命令。

```
xcode-select --install
```

2、执行上述命令后，会自动弹出软件安装的提示窗口。点击【Install】按钮，进行安装。(**这个软件大概 130MB 左右**)

> 通过上述步骤可以替代安装 Xcode 软件，以保证成功安装 nvm 软件。

3、打开“终端”窗口，输入以下命令，在线安装 nvm 软件:

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh|bash
```

> **这里需要注意的是：**nvm 只能通过命令在线安装。所以，安装之前要确保电脑是可以联网的。

4、安装成功之后，在“终端”窗口，输入 `nvm` 命令，验证 nvm 是否安装成功。

### 二、使用 nvm 安装 Node.js

> 以下操作都是在“终端”窗口中完成。

#### 1、安装指定版本的 Node.js

我们可以通过以下 nvm 命令在线安装指定版本的 Node.js。

```
nvm install [nodeversion]
```

例如，需要安装 v6.9.1 版本的 Node.js，那可以通过以下命令完成。

```
nvm install v6.9.1
```

#### 2、指定当前使用的 Node.js 版本

通过 nvm 可以同时安装多个版本的 Node.js，我们可以指定某个版本的使用。

```
nvm use [nodeversion]
```

例如，需要使用 v6.9.1 版本的 Node.js，那可以通过以下命令完成。

```
nvm use v6.9.1
```

#### 3、查看当前安装的 Node.js 版本列表

由于通过 nvm 可以安装多个 Node.js，版本多了不好管理。我们还可以随时查看当前安装了哪些 Node.js 的版本。

```
nvm ls
```

#### 4、nvm 的其他命令

nvm 还提供一些命令，方便我们平时管理 Node.js 的版本。

- `nvm uninstall [nodeversion]`: 表示删除指定版本的 Node.js，用法类似于 install 命令。
- `nvm current`: 表示显示当前使用的 Node.js 版本。
- `nvm reinstall-packages [npmversion]`: 表示在当前的 Node.js 版本下，安装指定版本的 npm 包管理器。

### 三、安装多个版本 Node.js 的意义

自从 Node.js 基金会成立，Node.js 就有一个发布计划，就是同时存在两个发布版本：稳定版和试验版。

在 Node.js 中，带有长期支持（LTS）的稳定版是以偶数开始（4,6,8...），而试验版是从奇数开始（5, 7...）。我们推荐在生产环境中用 LTS 版本，而用试验版尝试新东西。

### 四、nvm 软件切换镜像源

由于国内在一些情况下有些特殊。Node.js 官方镜像源在国外，经常通过 nvm 安装 Node.js 时，速度比较慢，或者没有响应。

根据这种情况，nvm 允许更改安装的镜像源，我们可以将镜像源切换到国内的淘宝提供的镜像源。

根据 nvm 官方提供的帮助文档，我们可以通过以下命令进行切换。

```
export NVM_NODEJS_ORG_MIRROR="http://npm.taobao.org/mirrors/node"
```

> [http://npm.taobao.org/mirrors/node](http://npm.taobao.org/mirrors/node) 是[淘宝 NPM 镜像](https://npm.taobao.org/)提供的国内 Node.js 的安装镜像源。

**这里我们需要注意的是，**这种方式，在每次重启“终端”会失效。也就是说，每次打开“终端”都需要执行上述命令。

如果并不想每次打开“终端”，都需要重新设置 `NVM_NODEJS_ORG_MIRROR` 环境变量。

- 如果“终端”使用的是 `bash Shell` 的话（一般是 Mac 系统终端默认）向 `~/.bash_profile` 文件（*如果没有，会自动创建*）增加以下内容:

```
# nvm
export NVM_NODEJS_ORG_MIRROR="http://npm.taobao.org/mirrors/node"
source ~/.nvm/nvm.sh
```

- 如果“终端”使用的是 `zsh Shell` 的话（一般是 Mac 开发人员使用）
向 `~/.zshrc` 文件（*如果没有，会自动创建*）增加以下内容:

```
# nvm
export NVM_NODEJS_ORG_MIRROR="http://npm.taobao.org/mirrors/node"
source ~/.nvm/nvm.sh
```

## Windows 系统的 nvm-windows 软件

Windows 系统的 nvm-windows 软件的功能与 MacOS 系统的 nvm 软件是一样的。我们可以把 nvm-windows 软件当作是 nvm 软件的 windows 版本。

> nvm-windows 软件的相关介绍，可以访问[ nvm-windows 的 github 主页](https://github.com/coreybutler/nvm-windows)。

### 一、安装 nvm-windows 软件

安装 nvm-windows 软件相对比较简单。我们只需访问 [https://github.com/coreybutler/nvm-windows/releases](https://github.com/coreybutler/nvm-windows/releases)，下载最新版本的安装文件即可。

> **这里需要注意的是，**`nvm-setup.zip` 压缩文件是 nvm-windows 软件的安装压缩包。下载并解压即可安装。

### 二、nvm-windows 软件切换镜像源

我们可以找到 nvm-windows 软件的安装目录中的 `settings.txt` 文件，增加以下内容:

```
node_mirror=http://npm.taobao.org/mirrors/node/
```

> 添加成功之后，需要重新打开命令行窗口。
