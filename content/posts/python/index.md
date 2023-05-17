---
title: "python"
date: 2023-05-17T17:24:41+08:00
# weight: 1
# aliases: ["/first","/language"]
tags: ["python"]
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




# M1 Pro

### 安装 tensorflow

```bash
conda create -n tf26 python=3.9

conda activate tf26

conda install -c apple tensorflow-deps=2.6.0 
or conda install -c apple tensorflow-deps

python -m pip install tensorflow-macos
python -m pip install tensorflow-metal
```

### conda本地环境操作

```bash
#获取版本号
conda --version 或 conda -V

#检查更新当前conda
conda update conda

#查看当前存在哪些虚拟环境
conda env list 或 conda info -e

#查看--安装--更新--删除包
conda list
conda search package_name# 查询包
conda install package_name
conda install package_name=1.5.0#pip 用==
conda update package_name
conda remove package_name

#创建名为your_env_name的环境
conda create --name your_env_name
#创建制定python版本的环境 
conda create --name your_env_name python=2.7
conda create --name your_env_name python=3.6
#创建包含某些包（如numpy，scipy）的环境
conda create --name your_env_name numpy scipy
#创建指定python版本下包含某些包的环境
conda create --name your_env_name python=3.6 numpy scipy

#激活环境
source activate your_env_name

#删除虚拟环境
conda remove -n your_env_name --all
conda remove --name your_env_name --all

#复制某个虚拟环境
conda create --name new_env_name --clone old_env_name

#在某个指定环境管理包
conda list -n your_env_name
conda install --name myenv package_name 
conda remove --name myenv package_name

#换源 修改~/.condarc
channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch-lts: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
```

### 配置OpenCV 环境

```bash
brew install opencv 
pip install opencv-contrib-python
```

### Jupyter notebook

```bash

```