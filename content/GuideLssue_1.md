# Guide 第一期🌄

<!--ts-->
* [Guide 第一期🌄](#guide-第一期)
   * [内容](#内容)
      * [1. 完全开源的财务软件](#1-完全开源的财务软件)
      * [2. 谷歌服务框架的开源替代品](#2-谷歌服务框架的开源替代品)
      * [3. 优化 Windows 11 系统的脚本](#3-优化-windows-11-系统的脚本)
      * [4. 让你上瘾的英语学习网站](#4-让你上瘾的英语学习网站)
         * [1. 要求：](#1-要求)
         * [2. 安装依赖](#2-安装依赖)
         * [3. 配置 .env 文件](#3-配置-env-文件)
            * [Server](#server)
            * [Client](#client)
         * [4. 恢复 Logto 的数据](#4-恢复-logto-的数据)
         * [5. 启动 Docker Compose 服务](#5-启动-docker-compose-服务)
         * [6. 初始化数据库表结构](#6-初始化数据库表结构)
         * [7. 创建并上传课程数据](#7-创建并上传课程数据)
         * [8. 启动后端服务](#8-启动后端服务)
         * [9. 启动前端服务](#9-启动前端服务)
* [声明🧭](#声明)

<!-- Created by https://github.com/ekalinin/github-markdown-toc -->
<!-- Added by: runner, at: Mon Oct  7 06:47:54 UTC 2024 -->

<!--te-->

## 内容
### 1. 完全开源的财务软件 
>[Gnucash/gnucash](https://github.com/Gnucash/gnucash)


这是一款适用于个人和小型企业的开源财务软件，它采用复式记账法，提供了简洁的操作界面，并支持生成报表、对账、多国货币，以及获取股票实时价格等功能，适用于 Windows、Linux 和 macOS 平台。![1_gnucash_1.png](https://github.com/jr94330/Guide/blob/main/images/1_gnucash_1.png)
### 2. 谷歌服务框架的开源替代品 
>[microg/GmsCore](https://github.com/microg/GmsCore)


该项目是一个开源的替代 Google Play 服务的解决方案，它可以让无法安装或不想用 Google 服务的用户，运行依赖谷歌服务的 Android 应用。
### 3. 优化 Windows 11 系统的脚本 
>[Raphire / Win11Debloat](https://github.com/Raphire/Win11Debloat)


这是一个用于优化 Windows 10/11 操作系统的 PowerShell 脚本，使用时无需额外安装任何软件。它通过删除或禁用 Windows 系统中的预装应用和不必要的服务，如诊断数据、定向广告、提示、Copilot 和 Bing 网络搜索等，减少系统资源占用，还你一个更加干净、高效的操作系统。
![1_Win11Debloat_1.png](https://github.com/jr94330/Guide/blob/main/images/1_Win11Debloat_1.png)
### 4. 让你上瘾的英语学习网站 
>[cuixueshe/earthworm](https://github.com/cuixueshe/earthworm)


这是一个开源的在线学习英语网站，支持自托管和本地运行。它采用连词成句、循序渐进的方法帮你学习英语。通过不断地重复形成肌肉记忆，并结合游戏奖励和积分排名的方式，让背单词变得有趣且高效。![1_earthworm_1.png](https://github.com/jr94330/Guide/blob/main/images/1_earthworm_1.png)
#### 1. 要求：

- **pnpm version >= 8**

  ```bash
  corepack enable
  ```

- **Node.js version >= v20**
  > 使用来自 .node-version 的版本 [支持的工具](https://github.com/shadowspawn/node-version-usage#compatibility-testing)
- **Postgres version >= 8.0.0**
- **Redis version >= 5.0.0**
- 项目依赖 **Docker**，所以请确保你本地已安装并成功运行

#### 2. 安装依赖

```bash
pnpm install
```

#### 3. 配置 `.env` 文件

可以选择将 `./apps/api/.env.example` 文件内容复制到 `./apps/api/.env`，请注意 `example` 文件中的是示例配置，主要是一些系统的环境变量信息，比如：数据库连接地址、用户名、密码、端口、密钥等等，后端服务会从此文件中读取配置信息，**当然你也可以更改成你自己的配置信息**。

Windows 用户推荐快捷键复制粘贴，Linux 用户可以通过下面的命令进行操作。

##### Server

```bash
cp ./apps/api/.env.example ./apps/api/.env
```

##### Client

```bash
cp ./apps/client/.env.example ./apps/client/.env
```

#### 4. 恢复 Logto 的数据

解压缩 `logto_db_init_data.zip` 到 `.volumes/`

```bash
unzip logto_db_init_data.zip -d .volumes/
```

- 后台地址: http://localhost:3011
- 用户名: admin
- 密码: WkN7g5-i8ZrJckX

> 如果你想 [手动配置 Logto](https://github.com/cuixueshe/earthworm/wiki/%E8%BF%81%E7%A7%BB-Logto-%E7%94%A8%E6%88%B7%E7%B3%BB%E7%BB%9F%E5%90%8E%E6%9C%AC%E5%9C%B0%E5%90%AF%E5%8A%A8%E9%85%8D%E7%BD%AE%E6%96%B9%E6%A1%88%EF%BC%88%E8%B4%A1%E7%8C%AE%E8%80%85%EF%BC%89)

#### 5. 启动 Docker Compose 服务

后端用到了 Postgres 和 Redis 服务，通过下面在 `package.json` 中配置的命令启动和停止。

```bash
# 启动
pnpm docker:start

# 下面这些命令等你用的时候在执行，不要傻乎乎的刚启动就停止哈 😊
# 停止
pnpm docker:stop
# 删除
pnpm docker:delete
# 完全删除（包括 Volume 数据）
pnpm docker:down
```

当然如果你更喜欢手动挡

```bash
docker compose up -d
docker compose stop
docker compose down

# 兼容老版本 docker 的命令
docker-compose up -d
```

#### 6. 初始化数据库表结构

执行这个命令时，尽量与上个命令间隔一点时间，因为刚刚使用的 `-d` 参数会让其服务挂起在后台执行，此时 docker 服务可能还在 running 中，若是发现报错了那就再执行一遍。😊

```bash
pnpm db:init
```

#### 7. 创建并上传课程数据

**只有第一次初始化数据库后需要执行**。

```bash
pnpm db:upload
```

#### 8. 启动后端服务

```bash
pnpm dev:serve
```

#### 9. 启动前端服务

```bash
pnpm dev:client
```### 编辑器

##### VSCode

- 安装推荐的插件 [extensions.json](./.vscode/extensions.json)

```bash
docker --version # Docker version 24.0.7, build afdd53b

node --version # v20+

pnpm -v # 8+
```
# 声明🧭

![img](https://licensebuttons.net/l/by-nc-nd/4.0/88x31.png)
本作品采用[署名-非商业性使用-禁止演绎 4.0 国际](https://creativecommons.org/licenses/by-nc-nd/4.0/)
