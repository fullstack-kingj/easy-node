  
p, li { white-space: pre-wrap; }  


\*\*在本节课中，我们将学习如何安装 Node.js ，以及相关问题的解决。\*\*

&gt; \#\# 写在前面的话

  


目前安装 Node.js 的方式主要有以下两种。

\#\#\# 1. 从官网获取最新版本

安装 Node.js 的最简单方法，就是从 \[官网\]\(https://nodejs.org/en/\) 获取最新版本的安装文件。

\*参考:\* \[本节课的扩展内容\]\(./04 扩展.md\)

\*\*值得注意的是:\*\*

- 这种方式安装，每次更新 Node.js 的版本，都需要从官网下载，并且进行覆盖安装。

- 这种方式安装，在系统中只能存在一个版本的 Node.js ，不适合对比学习。

\#\#\# 2. 使用 nvm 版本管理器

nvm 是 \[Tim Caswell\]\(https://github.com/creationix\) 开发的一款 Mac 系统中使用的通过命令方式管理多版本 Node.js 的软件。

nvm 软件的相关介绍，可以访问 \[该项目的github主页\]\(https://github.com/creationix/nvm\)。

\*如果是 Windows 系统的，可以参考 \[nvm-windows的github主页\]\(https://github.com/coreybutler/nvm-windows\)。\*

  


&gt; \#\# 通过 nvm 安装 Node.js

  


\#\#\# 1. 安装 nvm 版本管理器

打开“终端”窗口，输入如下命令，在线安装 nvm 软件:

\`\`\`

curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh\|bash

\`\`\`

- - - - -

\*\*值得注意的是:\*\* 想要成功的安装 nvm，Mac 系统下必须要先安装 Xcode 软件。

由于 Xcode 软件大概在 4.3GB 左右，如果不想安装 Xcode 软件，又想可以成功安装 nvm 的话，可以按照以下方式操作。

- 打开“终端”窗口，并输入以下命令。

\`\`\`

xcode-select --install

\`\`\`

- 执行上述命令后，会自动弹出软件安装的提示窗口。点击【Install】按钮，进行安装。\(\*这个软件大概 130MB 左右\*\)

通过上述步骤可以替代安装 Xcode 软件，以保证成功安装 nvm 软件。

- - - - -

\*如果是 Windows 系统的话，可以从 \[https://github.com/coreybutler/nvm-windows/releases\]\(https://github.com/coreybutler/nvm-windows/releases\) 下载安装文件，安装即可。\*

  


安装成功之后，在“终端”窗口，输入 \`nvm\` 命令，验证 nvm 是否安装成功。

\#\#\# 2. 使用 nvm 安装 Node.js

\*以下操作都是在“终端”窗口中完成。\*

\#\#\#\# 1\) 安装指定版本的 Node.js

我们可以通过以下 nvm 命令在线安装指定版本的 Node.js。

\`\`\`

nvm install \[nodeversion\]

\`\`\`

例如，需要安装 v6.9.1 版本的 Node.js，那可以通过以下命令完成。

\`\`\`

nvm install v6.9.1

\`\`\`

\#\#\#\# 2\) 指定当前使用的 Node.js 版本

通过 nvm 可以同时安装多个版本的 Node.js，我们可以指定某个版本的使用。

\`\`\`

nvm use \[nodeversion\]

\`\`\`

例如，需要使用 v6.9.1 版本的 Node.js，那可以通过以下命令完成。

\`\`\`

nvm use v6.9.1

\`\`\`

\#\#\#\# 3\) 查看当前安装的 Node.js 版本列表

由于通过 nvm 可以安装多个 Node.js，版本多了不好管理。我们还可以随时查看当前安装了哪些 Node.js 的版本。

\`\`\`

nvm ls

\`\`\`

\#\#\#\# 4\) nvm 的其他命令

nvm 还提供一些命令，方便我们平时管理 Node.js 的版本。

- nvm uninstall \[nodeversion\]: 表示删除指定版本的 Node.js，用法类似于 install 命令。

- nvm current: 表示显示当前使用的 Node.js 版本。

- nvm reinstall-packages \[npmversion\]: 表示在当前的 Node.js 版本下，安装指定版本的 npm 包管理器。

  


\#\#\# 3. 安装多个版本 Node.js 的意义

自从 Node.js 基金会成立，Node.js 就有一个发布计划，就是同时存在两个发布版本：稳定版和试验版。

在 Node.js 中，带有长期支持（LTS）的稳定版是以偶数开始（4,6,8...），而试验版是从奇数开始（5, 7...）。我们推荐在生产环境中用 LTS 版本，而用试验版尝试新东西。

  


\#\#\# 4. 国内环境的问题

由于国内在一些情况下有些特殊。Node.js 官方镜像源又在国外，经常通过 nvm 安装 Node.js 时，速度比较慢，或者没有响应。

根据这种情况，nvm 允许更改安装的镜像源，我们可以将镜像源切换到国内的淘宝提供的镜像源。

\#\#\#\# 1\) Mac 系统的 nvm 软件切换镜像源

根据 nvm 官方提供的帮助文档，我们可以通过以下命令进行切换。

\`\`\`

export NVM\_NODEJS\_ORG\_MIRROR="http://npm.taobao.org/mirrors/node"

\`\`\`

\*\[http://npm.taobao.org/mirrors/node\]\(http://npm.taobao.org/mirrors/node\) 是 \[淘宝NPM镜像\]\(https://npm.taobao.org/\) 提供的国内 Node.js 的安装镜像源。\*

- - - - -

\*\*值得注意的是:\*\*这种方式，在每次重启“终端”会失效。也就是说，每次打开“终端”都需要执行上述命令。

如果并不想每次打开“终端”，都需要重新设置 \`NVM\_NODEJS\_ORG\_MIRROR\` 环境变量。

- 如果“终端”使用的是 \`bash Shell\` 的话\(一般是 Mac 系统终端默认\)

向 \`~/.bash\_profile\` 文件\(\*如果没有，会自动创建\*\)增加以下内容:

\`\`\`

\# nvm

export NVM\_NODEJS\_ORG\_MIRROR="http://npm.taobao.org/mirrors/node"

source ~/.nvm/nvm.sh

\`\`\`

- 如果“终端”使用的是 \`zsh Shell\` 的话\(一般是 Mac 开发人员使用\)

向 \`~/.zshrc\` 文件\(\*如果没有，会自动创建\*\)增加以下内容:

\`\`\`

\# nvm

export NVM\_NODEJS\_ORG\_MIRROR="http://npm.taobao.org/mirrors/node"

source ~/.nvm/nvm.sh

\`\`\`

- - - - -

\#\#\#\# 2\) Windows 系统的 nvm-windows 软件切换镜像源

我们可以找到 nvm-windows 软件的安装目录中的 \`settings.txt\` 文件，增加以下内容:

\`\`\`

node\_mirror=http://npm.taobao.org/mirrors/node/

\`\`\`

\*添加成功之后，需要重新打开命令行窗口。\*

