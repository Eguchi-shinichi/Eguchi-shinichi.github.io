---
title: 世界，你好——HEXO+GitHubPige 搭建个人博客
date: 2022-05-01 22:47:15
tags:
---

## 事前准备
- Git
- GitHub 帐号
- 一个域名（可选）

---

## GitHub方面
#### 1. 创建一个新 repository
名字必须是 `username.github.io` ，在我的情况就是这样创建：
{% asset_img creat.png %}
#### 2. 修改 branch
进入这个 repository 的 setting，在 pages 页中 source，branch 推荐改为 `hexo` ，之后在 **Hexo** 方面的对应设置中也要修改
{% asset_img branch.png %}
#### 3. 自定义域名
修改同一页的 `custom domian` 为自己域名的二级域名，没有域名可以忽略
{% asset_img domain.png %}

好了！在GitHub这边要做的事已经完了！

---

## Hexo方面
#### 1. 安装
- 安装 Node.js （可参考 hexo 官网：[](hexo.io))
*推荐使用 `nvm` 安装，否则易出现 `EACCES` 权限错误*（出现`EACCES`权限错误时，应当遵循[由npmjs发布的指导](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally)修复该问题。强烈建议**不要**使用 root、sudo等方法覆盖权限）
**以下假设使用[nvm](https://github.com/nvm-sh/nvm)安装**
```
# 安装nvm
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
# 安装Node
$ nvm install node
```
- 安装 Hexo

```
$ npm install -g hexo-cli
```
#### 2. Hexo 新建项目

```
$ hexo init <myblog>
$ cd <myblog>
$ npm install
```
- 新建完成后，`myblog` 文件夹的目录如下：

```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```
#### 3. 安装依赖
安装 `hexo-deployer-git` 依赖库，这样才可以配合 GitHubPage建站

```
$ npm install hexo-deployer-git --save
```
#### 4. 修改 `_config.yml` 配置
- 修改 `deploy` (请确认giehub已配置当前机器密钥)
```
deploy:
  type: 'git'
  repo: git@github.com:username/username.github.io.git #修改成刚才新建的repository地址
  branch: hexo
  message: #自定义提交信息
```
- 修改 `Url`

```
url: http://name.domain
root: /
```

#### 5. `source` 目录下，创建 `CNAME` 文件
```
# myblog/source/CNAME
myblog.name.domain
```
#### 6. Hexo常用命令
```
$ hexo s #在http://localhost:4000启动服务器
$ hexo g #生成静态文件
$ hexo d #将生成的静态文件推送至 GitHub
$ hexo clean #清除站点文件，建议生成静态文件之前都执行一下
```

---

## 域名方面
1. 在域名解析中添加一条 `CNAME` 记录

```
记录类型：CNAME
主机记录：myblog #自定义二级域名
记录值：uername.github.io
```

---

啊哈！这样就能从自定义的域名 myblog.name.domain 访问博客了！
