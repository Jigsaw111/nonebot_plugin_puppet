# Nonebot Plugin Puppet

基于 [nonebot2](https://github.com/nonebot/nonebot2) 和 [go-cqhttp](https://github.com/Mrs4s/go-cqhttp) 的会话转接插件

[![License](https://img.shields.io/github/license/Jigsaw111/nonebot_plugin_puppet?style=flat-square)](LICENSE)
![Python Version](https://img.shields.io/badge/python-3.7.3+-blue.svg?style=flat-square)
![NoneBot Version](https://img.shields.io/badge/nonebot-2.0.0a11+-red.svg?style=flat-square&log")
![Pypi Version](https://img.shields.io/pypi/v/nonebot-plugin-puppet.svg?style=flat-square)

## 安装

### 从 PyPI 安装（推荐）

- 使用 nb-cli  

```shell
nb plugin install nonebot_plugin_puppet
```

- 使用 poetry

```shell
poetry add nonebot_plugin_puppet
```

- 使用 pip

```shell
pip install nonebot_plugin_puppet
```

### 从 GitHub 安装（不推荐）

```shell
git clone https://github.com/Jigsaw111/nonebot_plugin_puppet.git
```

## 使用

**仅限超级用户使用**

**不建议同时链接多个会话（尤其是大群），如被风控概不负责**

- `puppet ln/link`链接会话
  - `-u user_id..., -ua user_id..., --user-a user_id...`可选参数，指定源会话的 QQ 号
  - `-g group_id..., -ga group_id..., --group-a group_id...`可选参数，指定源会话的群号
    至少需要设置一个
  - `-ub user_id..., --user-b user_id...`可选参数，指定链接会话的 QQ 号
  - `-gb group_id..., --group-b group_id...`可选参数，指定链接会话的群号
    不设置的话默认为当前会话的 QQ 号/群号
  - `-q, --quiet`可选参数，静默链接（不发送链接成功消息）
  - `-U, --unilateral`可选参数，单方面链接
- `puppet rm/unlink`删除会话链接
  - `-u user_id..., -ua user_id..., --user-a user_id...`可选参数，指定源会话的 QQ 号
  - `-g group_id..., -ga group_id..., --group-a group_id...`可选参数，指定源会话的群号
    不设置的话，默认为当前会话链接的所有会话
  - `-ub user_id..., --user-b user_id...`可选参数，指定链接会话的 QQ 号
  - `-gb group_id..., --group-b group_id...`可选参数，指定链接会话的群号
    不设置的话默认为当前会话的 QQ 号/群号
  - `-q, --quiet`可选参数，静默链接（不发送解除链接成功消息）
  - `-U, --unilateral`可选参数，单方面解除链接
- `puppet ls/list` 查看链接到当前会话的会话列表
  - `-u user_id, --user user_id` 互斥参数，指定会话的 QQ 号
  - `-g group_id, --group group_id` 互斥参数，指定会话的群号
    不设置的话默认为当前会话的 QQ 号/群号
- `puppet send message` 向指定会话发送消息，支持 CQ 码
  - `message` 需要发送的消息，支持 CQ 码，如含空格请用 `""` 包裹
  - `-u user_id..., --user user_id...`可选参数，指定接收会话的 QQ 号
  - `-g group_id..., --group group_id...`可选参数，指定接收会话的群号
    不设置的话默认为当前会话链接的所有会话
  - `--a, --all`可选参数，指定所有群聊
- `puppet aprv/approve` 同意请求/邀请
  - `-f flag..., --flag flag...`可选参数，指定请求的 flag
  - `--a, --all`可选参数，指定所有请求
- `puppet rej/reject` 拒绝请求/邀请
  - `-f flag..., --flag flag...`可选参数，指定请求的 flag
  - `--a, --all`可选参数，指定所有请求
- `puppet exit` 退出指定群聊
  - `-g group_id..., --group group_id...`可选参数，指定要退出的群号

## Bug

- [x] 不允许多个超级用户链接到同一会话
- [x] 如果指定的会话不在会话列表里会产生错误

## To Do

- [x] 允许单向转接
- [x] 转接请求事件
- [x] 提供退群功能
- [ ] 提供默认设置

## 原理

```mermaid
graph LR
用户 & 群 ---> Puppet ---> 用户 & 群
```

## Changelog

- 210928 0.2.0
  - 修复 flag 记录残留的 bug
  - 修复 aprv/rej 操作无效的 bug
  - 修复 aprv 需要参数 message 的 bug
  - 删除数据文件莫名其妙的前缀
- 210525 0.2.0-alpha.6
  - 新增退群功能
  - 修复了 list 重复展示的 bug
  - 修复了 aprv/rej 操作无效的 bug
- 210525 0.2.0-alpha.5
  - 实现转接请求事件
  - 修复了 ln/rm 操作无效的 bug
  - 修复了 list 重复展示的 bug
  - 修复了 --undirect 参数无效的 bug
- 210429 0.2.0-alpha.4
  - 新增部分命令的缩写
  - list 命令能够显示单双向
  - 支持 -h, --help 参数
  - 发生错误时返回相关信息
  - 分离 handle 与 parser
- 210429 0.2.0-alpha.3
  - 修复未设置群名片时昵称为空的问题
  - 实现单向的会话转接
- 210429 0.2.0-alpha.2
  - 修复指定会话不在会话列表时会产生错误的问题
  - 修复群发消息时由于风控/禁言而被打断的问题
- 210421 0.2.0-alpha.1
  - 实现多对多的会话转接
  - 重构数据结构以便下次更新
- 210416 0.1.0
  - 实现单对单的会话转接
