---
title: "Mac-config"
date: 2023-05-17T10:04:41+08:00
# weight: 1
# aliases: ["/first","/config"]
tags: ["Mac"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Desc Text."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---


# Config

## mac-config

### 安装报错

```bash
#应用程序已经损坏
#用于关闭 macOS 的 Gatekeeper 功能，使得可以运行未经过 Mac App Store 审核的应用程序。
sudo spctl --master-disable

#允许该应用程序访问它需要的系统级别的文件或目录。
#递归地清除指定目录及其子目录下的所有文件的所有扩展属性。
xattr -cr /Applications/PicGo.app


#应用程序来自不受信任的来源
#递归地清除指定目录及其子目录下的所有文件的指定扩展属性。
#命令会递归地清除 /Applications/PicGo.app 目录下所有文件的 com.apple.quarantine 扩展属性。
sudo xattr -r -d com.apple.quarantine /Applications/MarkText.app

#因此，xattr -r -d 命令比 xattr -cr 命令更加具有针对性，可以仅清除指定的扩展属性。
```

> `com.apple.quarantine` 是 macOS 中一个文件属性，用于标记文件是否从互联网上下载并具有潜在的风险。当你第一次运行从互联网下载的应用程序时，macOS 就会将 `com.apple.quarantine` 属性附加到该应用程序上，以此来提示用户该应用程序可能不可信。
> 
> 当用户尝试打开一个带有 `com.apple.quarantine` 属性的应用程序时，macOS 会弹出一个警告窗口，提醒用户该应用程序来自不受信任的来源。用户可以选择在打开应用程序前取消该属性，以此来信任该应用程序。

### tldr 显示某个命令的使用说明

```bash
pip install tldr #安装
tldr ls #查看 ls 说明文档
```

### pbcopy与 pbpaste 复制与粘贴

```bash
pbcopy < abc.txt
pbpaste > new.txt
```

### Tmux

```bash
brew install tmux
```

安装插件[tmp](https://github.com/tmux-plugins/tpm)

打开`~/.tmux.conf`

我的.tmux.conf 内容:

```bash
# Send prefix
set-option -g prefix C-x
unbind-key C-x
bind-key C-x send-prefix

# Use Alt-arrow keys to switch panes
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

# Shift arrow to switch windows
bind -n S-Left previous-window
bind -n S-Right next-window

# Mouse mode
set -g mouse on

# Set easier window split keys
bind-key v split-window -h
bind-key h split-window -v

# Easy config reload
bind-key r source-file ~/.tmux.conf \; display-message "tmux.conf reloaded"

# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'tmux-plugins/tmux-resurrect'

# Other examples:
# set -g @plugin 'github_username/plugin_name'
# set -g @plugin 'github_username/plugin_name#branch'
# set -g @plugin 'git@github.com:user/plugin'
# set -g @plugin 'git@bitbucket.com:user/plugin'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'

```

按前缀+ I（大写i）来下载插件

### neofetch 展示系统图标

```bash
neofetch
```

## ubuntu-config

常用命令

```bash
#在 Ubuntu 系统中，你可以使用以下命令来查看你的 Ubuntu 版本：
lsb_release -a

```



### ssh

```bash
# mac中执行,实现免密登录
ssh-keygen -t rsa

ssh-copy-id sammul@192.168.1.135
```



###  apt

通过[Ubuntu清华源](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/) 使用国内源

```bash
#打开配置文件
vi /etc/apt/sources.list

sudo apt update

#安装常用工具
sudo apt install neofetch net-tools tmux zsh tree

chsh -s /bin/zsh #将zsh设置成默认shell,重启终端生效（不设置的话启动zsh只有直接zsh命令即可）

```



### linuxbrew

```bash
#安装linuxbrew
//bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" 
#安装 nvim
brew install neovim
```

[homebrew | 镜像站使用帮助 | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/)

[命令行常用工具的替代品 - 阮一峰的网络日志](https://www.ruanyifeng.com/blog/2022/01/cli-alternative-tools.html)

```bash
brew install \
bat \
bottom \
broot \
btop \
choose-rust \
dog \
duf \
exa \
fd \
fzf \
git-delta \
glances \
gtop \
httpie \
jq \
lsd \
mcfly \
orf/brew/gping \
procs \
ripgrep \
rs/tap/curlie \
the_silver_searcher \
tldr \
xh \
zoxide
```

###  miniconda

```bash
#下载安装脚本
curl -O https://repo.anaconda.com/miniconda/Miniconda3-py310_23.3.1-0-Linux-x86_64.sh
#检查SHA256
sha256sum Miniconda3-py310_23.3.1-0-Linux-x86_64.sh
#执行脚本
bash Miniconda3-latest-Linux-x86_64.sh
```

###  docker

[Install Docker Engine on Ubuntu | Docker Documentation](https://docs.docker.com/engine/install/ubuntu/)

[Docker 入门教程 - 阮一峰的网络日志](https://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html)

[安装 docker-compose](https://www.runoob.com/docker/docker-compose.html)

### Tmux

```bash
#Tmux Plugin Manager
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

### oh-my-zsh

```bash
#安装 ohmyzsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

plugins=( 
    # other plugins...
    zsh-autosuggestions zsh-syntax-highlighting
)

sudo apt install fzf
apt show fzf

sudo apt install autojump
vi /usr/share/doc/autojump/README.Debian

#安装 spaceship 主题
git clone https://github.com/spaceship-prompt/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt" --depth=1
ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme"
#Set ZSH_THEME="spaceship" in your .zshrc.
```

