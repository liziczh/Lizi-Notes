---
title: Hexo | （一）使用Hexo+Pages搭建个人博客
id: hexo-blog-build
comments: true
tags:
  - Hexo博客
categories: Hexo博客
date: 2018-04-11 10:57:46
toc: true
reward: true
copyright: true
---

<!--# Hexo | （一）使用Hexo+Pages搭建个人博客-->


本篇主要介绍使用Hexo+Pages搭建个人博客的流程。使用 [Hexo](https://hexo.io/zh-cn/) 博客框架搭建，解析markdown文章，生成静态页面，将页面托管到 [github](https://github.com)  / [coding](https://coding.net) 服务器上。[github](https://github.com)  / [coding](https://coding.net) 都有pages 服务，提供免费的静态网页托管和演示服务。

<!-- more -->

搭建步骤：
1. 安装git，nodejs
2. 安装hexo
3. 本地搭建站点（线下访问）
4. 部署到github/coding（线上访问）
5. 站点配置

## 1. 安装hexo

1.安装Git 。安装完毕后，在任意文件夹下**鼠标右击**即可打开 Git Bash，输入命令，进行Git操作。

```shell
$ git version  # 查看Git版本，验证是否安装成功
```

2.安装Node.js。Hexo是基于nodejs的博客框架，而且nodejs还集成了npm包管理工具。

```shell
$ node -v    # 查看nodejs版本，验证是否安装成功
```

3.安装hexo：

```shell
$ npm install hexo --save   # 安装hexo
$ npm install hexo-cli -g   # 安装hexo命令行模式
$ hexo -v  # 查看hexo版本，验证是否安装成功
```

## 2. hexo建站

1.新建一个blog文件夹，打开blog文件夹，Git Bash。

2.hexo初始化：`hexo init`

3.安装依赖包：`npm install`

4.初始化完成，在blog下就会生成以下文件目录：

```yaml
.
├── node_modules # 依赖模块
├── scaffolds    # 文章模板
├── source       # 用户源文件：页面，文章markdown文件
|   └── _posts   # 创建的文章
└── themes       # 主题
├── .gitignore   # git忽略文件信息
├── _config.yml  # 站点配置文件
├── package.json # 已安装插件映射表，下次只需npm install即直接安装表插件
```

5.hexo本地生成静态页面

```shell
$ hexo clean     # 清理本地静态文件；
$ hexo generate  # 生成静态页面，即public文件夹；
$ hexo server    # 启用hexo本地服务器；
# 注：Hexo 3.0 把服务器独立成了个别模块，您必须先安装 hexo-server 才能使用。
# hexo-server安装命令：npm install hexo-server --save
```

这时，打开浏览器在地址栏输入[http://localhost:4000](http://localhost:4000)即可本地访问静态博客页面。

## 3. 配置github/coding pages

github和coding可以双线配置，也可以选择其中一个配置。推荐双线配置，coding用于国内访问速度较快，github用于境外访问。

1.登录github，New repository：`yourname.github.io`。其中`yourname`是你的github用户名，github强制后缀为`github.io`才能启用github pages服务。

2.登录coding，新建仓库：`yourname.coding.me`，打开静态pages服务。其中yourname是你的coding用户名，coding不强制后缀为coding.me。
&nbsp;其中`yourname`是你的coding用户名，coding不强制后缀为`coding.me`。

3.Git Bash配置git用户信息：

```shell
$ git config --global user.name "YourName"
$ git config --global user.email "YourEmail"
```

4.配置网络传输协议

在管理Git项目时，一般使用ssh或https作为安全传输协议，任选其一即可。

(1) SSH协议

①SSH秘钥：

```shell
$ ssh-keygen -t rsa -C "youremail@example.com"  # 生成rsa秘钥
$ cd ~/.ssh         # 进入虚拟目录ssh文件中
$ cat id_rsa.pub    # 显示id_rsa.pub文件内容
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
(2) HTTPS协议

①直接编辑**站点配置文件**`_config.yml`：

```yaml
deploy:
	type: git
	repo: 
		github: https://github.com/liziczh/liziczh.github.io.git
    	coding: https://git.coding.net/liziczh/liziczh.coding.me.git
	branch: master
```

②验证github/coding用户名和密码。

## 4. 部署到github/coding

1.安装Git部署插件：

```shell
$ npm install hexo-deployer-git --save
```

2.部署：

```shell
$ hexo clean     # 清理本地静态文件；
$ hexo generate  # 生成静态页面，即public文件夹；
$ hexo deploy    # 部署到github/coding；
```

3.部署完毕，站点文件目录如下：

```shell
.
├── .deploy_git  # （新增）hexo deploy 生成的git部署文件
├── public       # （新增）hexo generate 生成的静态文件
├── db.json      # （新增）hexo generate 生成的数据
├── node_modules # 依赖模块
├── scaffolds    # 文章模板
├── source       # 用户源文件：页面&文章的markdown文件
|   └── _posts   # 文章
└── themes       # 主题
├── .gitignore   # git时需忽略文件
├── _config.yml  # 站点配置文件
├── package.json # 已安装插件映射表，下次只需npm install即直接安装表插件
```

站点搭建完毕，打开浏览器在地址栏输入以下链接可随时访问自己的博客了。

- github pages：[http://yourname.github.io](http://yourname.github.io)
- coding pages：[http://yourname.coding.me](http://yourname.coding.me)

## 5. 站点配置

区分配置文件：

| 配置文件     | 路径                                  |
| ------------ | ------------------------------------- |
| 站点配置文件 | `D:/blog/_config.yml`                 |
| 主题配置文件 | `D:/blog/themes/你的主题/_config.yml` |

打开**站点配置文件**`blog/_config.yml`，自行发挥，配置完毕，重新部署 `hexo g -d`；

```yaml
# 注意：yaml语言使用缩进表示层级关系。
# 注意：键值对中的冒号（:）后面有一个半角空格。

# 网站
title: #网站标题
subtitle: #网站副标题
description: #网站描述
keywords: #关键字
author: #你的名字,文档作者
language: #网站的语言
timezone: #时区，中国：Asia/Shanghai
# 网址
url: https://yoursite.com  #你的网址url
root: /
permalink: :year/:month/:day/:title.html #文章永久链接
permalink_defaults:
# 主题
theme: landscape  # 主题文件的名称
# 部署
deploy:
  type: git
  repo: 
    github: git@github.com:yourname/yourname.github.io.git  
    coding: git@git.coding.net:yourname/yourname.coding.me.git 
  branch: master
```

> 详细配置请参考[hexo配置](https://hexo.io/zh-cn/docs/configuration.html)，此处不再赘述。

## 6. 主题变更

1.hexo默认主题为landscape，可以到[Themes|Hexo](https://hexo.io/themes/)选择自己喜欢的主题，复制主题在github仓库的url。
   ![clone theme](http://p6uturdzt.bkt.clouddn.com/hexo-clone_theme.PNG)
2.在themes文件夹下，打开GitBash，克隆主题至themes文件夹中。

```shell
$ git clone https://github.com/theme-next/hexo-theme-next.git
```

克隆之后，记住删除`themes\你的主题名`中的`.git`，`.github`，`.gitignore`等Git仓库文件。

3.更改**站点配置文件**`_config.yml`：

```yaml
theme: 主题文件名
```

4.编辑结束，重新部署：

```shell
$ hexo clean  # 清理缓存文件；（不清理也可以部署，推荐先清理）
$ hexo g -d   # 生成静态页面后直接部署；
```

部署完毕之后，进入以下链接刷新就可以看到你的新主题了。
- github pages：[http://yourname.github.io](http://yourname.github.io)
- coding pages：[http://yourname.coding.me](http://yourname.coding.me)

## 7. 写作

1.新建：在blog文件夹下，打开Git Bash，新建文章：

```shell
$ hexo new post "title"
```

2.编辑：在`source/_post`下可以编辑你新建的文章。

3.编辑完毕，重新部署：

```shell
$ hexo clean  # 清理缓存文件；（不清理也可以部署，推荐先清理）
$ hexo g -d   # 生成静态页面后直接部署；
```
## 8. 文档的Front-matter

Front-matter 是文档最上方以 `---` 分隔的区域，用于指定文档一些的参数。

```yaml
---
title: 文章标题
date: yyyy-MM-dd hh:mm:ss
tags: 
categories: 
comments: true
---
# 注意：键值对中的冒号（:）后面有一个半角空格。
```

| 参数       | 值                             | 描述                                     |
| ---------- | ------------------------------ | ---------------------------------------- |
| layout     | post<br>page<br>draft<br>false | 文章【默认值】<br>页面<br>草稿<br>不处理 |
| title      | 文本                           | 标题                                     |
| date       | yyyy-MM-dd hh:mm:ss            | 文件建立日期                             |
| update     | yyyy-MM-dd hh:mm:ss            | 文件更新日期                             |
| comments   | true<br>false                  | 开启文章评论功能，默认true               |
| tags       |                                | 标签（只适用于post）                     |
| categories |                                | 分类（只适用于post）                     |
| permalink  | url                            | 永久链接                                 |

> 不要处理我的文章：将文章Front-Matter中的`layout: false`；

## 9. 文章的[标签]与[分类]

只有**文章**（post）支持[标签]和[分类]。

1.添加[tags]、[categoies]、[about]页面：

```shell
$ hexo new page "tags"
$ hexo new page "categories"
$ hexo new page "about"
```

2.在source文件夹中找到新建页面：
①编辑tags.md：添加`layout:"tags"`；
②编辑categories.md：添加`layout:"categories"`；
③编辑about.md，自行发挥。

3.匹配**站点配置文件**：

```yaml
# Directory
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
```

4.匹配**主题配置文件**中`menu`：

```yaml
menu:
  home: /
  tags: /tags
  categories: /categories
  archives: /archives
  about: /about
```

5.Front-matter中的[tags]写法：

```yaml
tags:
- tag_1
- tag_2
# 标签之间相互独立
```

6.Front-matter中的[categories]写法：

```yaml
categories: 
- 运动
- [运动, 球类运动]
- [运动, 球类运动, 网球]
# 类别存在层级关系
```

重新部署之后，个人博客的基本功能，写作，标签，分类，归档就全部实现了。

## 10. 绑定自己的域名

若不喜欢域名后缀为github.io或coding.me，可以自己注册一个域名进行绑定。

1.域名注册：在[阿里云](https://wanwang.aliyun.com/?utm_content=se_1101810)/[腾讯云](https://dnspod.cloud.tencent.com/?fromSource=gwzcw.185882.185882.185882)等注册一个域名。

2.添加CNAME文件：在`blog\source`下，添加一个CNAME文件 (无文件后缀)，内容为你的域名`example.com`。

3.Github Pages域名解析：
①添加四个`A记录`：主机记录为`@`，记录值为`185.199.108.153`、`185.199.109.153`、`185.199.110.153`、`185.199.111.153`。
②添加一个`CNAME记录`：主机记录为`www`，记录值为`yourname.github.io`。

4.Coding Pages域名解析：
①打开控制台`ping pages.coding.me`，获取IP。
②添加一个`A记录`：主机记录为`@`，记录值为ping得的IP。
③添加一个`CNAME记录`：主机记录为`www`，记录值为`pages.coding.me`。

![dns](http://p6uturdzt.bkt.clouddn.com/hexo-dns.png)

由于国内访问Github Pages速度较慢，所以我将Coding Pages解析线路设为默认，供国内访问；将Github Pages解析线路设为境外，供国外访问。

## Chrome无法访问链接问题

**问题描述**：部署页面之后，Chrome无法访问链接，提示你的连接不是私密连接......
**解决方案**：前往[chrome://net-internals/#hsts](chrome://net-internals/#hsts)，在Delete domain中输入无法访问的网页地址。

## 附：hexo常用命令

| 命令                        | 描述                                                       |
| --------------------------- | ---------------------------------------------------------- |
| `hexo version`              | 显示 Hexo 版本                                             |
| `hexo init [folder]`        | 新建一个网站<br>若未设置folder，默认为当前文件夹；         |
| `hexo new [layout] "title"` | 新建一篇文档，文档布局由layout决定                         |
| `hexo clean`                | 清理缓存文件                                               |
| `hexo generate`<br>`hexo g` | 生成静态页面                                               |
| `hexo server`<br>`hexo s`   | 启用服务器，[http://localhost:4000](http://localhost:4000) |
| `hexo deploy`<br>`hexo d`   | 部署文件                                                   |
| `hexo g -d`<br>`hexo d -g`  | 生成静态文件后直接部署<br>部署之前先生成静态文件           |

> 若想了解更多关于hexo命令的介绍，请参考[指令 | hexo](https://hexo.io/zh-cn/docs/commands.html)

