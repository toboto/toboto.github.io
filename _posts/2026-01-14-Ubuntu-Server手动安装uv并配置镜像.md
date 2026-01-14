---
layout:     post
title:      "Ubuntu Server 手动安装 uv 并配置阿里云镜像"
subtitle:   "在离线或网络受限环境下安装 Python 包管理工具 uv"
date:       2026-01-14
author:     "toboto"
tags:
    - Ubuntu
    - Python
    - uv
---

本文环境是 Ubuntu Server 20.04，介绍如何手动安装 uv 包管理工具并配置阿里云 PyPI 镜像源。

## 1. 安装 uv

如果有本地的 tar.gz 文件，直接解压安装即可：

```bash
# 解压 uv
tar -xzf uv-x86_64-unknown-linux-gnu.tar.gz

# 移动到 bin 目录
mkdir -p ~/.local/bin
mv uv-x86_64-unknown-linux-gnu/uv ~/.local/bin/
mv uv-x86_64-unknown-linux-gnu/uvx ~/.local/bin/

# 添加到 PATH（写入 ~/.bashrc）
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# 验证安装
uv --version
```

## 2. 安装本地 Python（可选）

如果需要使用本地的 Python 安装包（例如 Python 3.11）：

```bash
# 解压到 uv 的 python 目录
mkdir -p ~/.local/share/uv/python
tar -xzf cpython-3.11.14+20251209-x86_64-unknown-linux-gnu-install_only_stripped.tar.gz \
    -C ~/.local/share/uv/python

# 重命名为 uv 识别的格式
mv ~/.local/share/uv/python/python \
   ~/.local/share/uv/python/cpython-3.11.14-linux-x86_64-gnu
```

## 3. 配置阿里云 PyPI 镜像

创建或编辑 `~/.config/uv/uv.toml`：

```bash
mkdir -p ~/.config/uv
cat > ~/.config/uv/uv.toml << 'EOF'
[pip]
index-url = "https://mirrors.aliyun.com/pypi/simple/"

[[index]]
url = "https://mirrors.aliyun.com/pypi/simple/"
default = true
EOF
```

## 4. 验证配置

```bash
# 查看 uv 配置
uv pip config list

# 测试安装包（应该从阿里云下载）
uv pip install --dry-run requests
```

## 完整一键脚本

```bash
#!/bin/bash
set -e

# 安装 uv
tar -xzf uv-x86_64-unknown-linux-gnu.tar.gz
mkdir -p ~/.local/bin
mv uv-x86_64-unknown-linux-gnu/uv ~/.local/bin/
mv uv-x86_64-unknown-linux-gnu/uvx ~/.local/bin/
export PATH="$HOME/.local/bin:$PATH"
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc

# 配置阿里云镜像
mkdir -p ~/.config/uv
cat > ~/.config/uv/uv.toml << 'EOF'
[pip]
index-url = "https://mirrors.aliyun.com/pypi/simple/"

[[index]]
url = "https://mirrors.aliyun.com/pypi/simple/"
default = true
EOF

echo "uv 安装完成: $(uv --version)"
```
