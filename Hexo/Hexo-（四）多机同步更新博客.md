---
title: Hexo | （四）多机同步更新博客
comments: true
date: 2018-04-21 22:00:07
id: hexo-multimachine
tags:
- Hexo博客
categories: Hexo博客
toc: true
reward: true
copyright: true
---

<!--# Hexo | 多机同步更新博客-->

Hexo博客存在一个问题：我们仅仅将博客的静态页面文件部署到了github远程仓库中，而我们的站点源文件仍在本地存储。如果存储站点源文件的电脑系统崩溃了，或者我们换了其他电脑，我们便无法实时更新博客了。
如果选择重新搭建站点，不仅过程繁琐，而且还需要大量时间安装依赖、主题配置、博客优化，极其麻烦。所以我们需要将站点必要文件也部署到github远程仓库中。
我们采取的远程仓库部署策略是：一个仓库两个分支。仓库即[yourname.github.io]，一个分支[master]用于托管演示页面，一个分支[backup]用于备份Hexo博客站点的必要文件。

<!-- more -->

## 多机同步更新的前提：backup分支

Hexo博客站点的必要文件：

```yaml
.
├── scaffolds    # 文章模板
├── source       # 用户源文件：页面，文章markdown文件
├── themes       # 主题
├── .gitignore   # git忽略文件信息
├── _config.yml  # 站点配置文件
├── package.json # 已安装插件映射表，下次只需npm install即直接安装表中的插件
├── package-lock.json
```

编辑**站点根目录**下的`.gitignore`文件，使Git上传时忽略不必要的文件：

```
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
```

1.删除`themes\你的主题`中的`.git`，`.github`，`.gitignore`等git仓库文件，只保留站点根目录下的`.gitignore`。

2.在Hexo博客站点根目录（即blog文件夹）中GitBash：

```shell
# 将blog作为一个git仓库进行初始化
$ git init  
# 创建/切换hexo分支
$ git checkout -b backup  
# 将文件添加到暂存区
$ git add .  
# 将暂存区文件提交到本地仓库
$ git commit -m "提交说明"  
# 添加远程仓库
$ git remote add origin https://github.com/yourname/yourname.github.io.git
# 将本地仓库推送至远程仓库
$ git push origin backup  
```

## 多机同步更新博客

### 1.安装前提

(1) 安装Git
(2) 安装nodejs

### 2.博客还原

```shell
# 克隆hexo分支到本地
$ git clone -b backup https://github.com/yourname/yourname.github.io.git
# 进入yourname.github.io文件夹
$ cd yourname.github.io
# 安装hexo
$ npm install hexo --save
# 安装hexo命令行模式
$ npm install hexo-cli -g
# 安装所有依赖，根据package.json自动安装之前安装过的插件
$ npm install
```

### 3.配置网络协议

(1) SSH协议，长期部署推荐SSH，一劳永逸。

①SSH秘钥：

```shell
# 生成rsa秘钥
$ ssh-keygen -t rsa -C "youremail@example.com"
# 进入虚拟目录ssh文件中
$ cd ~/.ssh
# 显示id_rsa.pub文件内容
$ cat id_rsa.pub
```

②复制秘钥至github/coding->用户setting->SSH keys，New SSH Key；

③验证是否添加成功

```shell
$ ssh -T git@github.com  # 验证github是否添加成功
$ ssh -T git@coding.net  # 验证coding是否添加成功
```

④编辑**站点配置文件**`_config.yml`：

```yaml
deploy:
	type: git
	repo: 
		github: git@github.com:yourname/yourname.github.io.git 
		coding: git@git.coding.net:yourname/yourname.coding.me.git 
	branch: master
```

⑤添加远程仓库

```shell
$ git remote add origin git@github.com:yourname/yourname.github.io.git
```

(2) HTTPS协议，临时部署推荐HTTPS。

①直接编辑**站点配置文件**`_config.yml`：

```yaml
deploy:
	type: git
	repo: 
		github: https://github.com/yourname/yourname.github.io.git
    	coding: https://git.coding.net/yourname/yourname.coding.me.git
	branch: master
```

②验证github/coding用户名和密码。

③添加远程仓库

```shell
$ git remote add origin https://github.com/yourname/yourname.github.io.git
```

### 4.正常使用

重新部署：

```shell
$ hexo clean
$ hexo g -d
```

上传至hexo分支：

```shell
$ git add .
$ git commit -m "commit-message"
$ git push origin backup
```