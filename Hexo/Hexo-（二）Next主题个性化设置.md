---
title: Hexo | （二）Next主题个性化设置
id: hexo-next-settings
comments: true
tags:
  - Hexo博客
categories: Hexo博客
date: 2018-04-12 08:34:58
toc: true
reward: true
copyright: true
---

<!--# Hexo系列 | （二）Next主题个性化设置-->

NexT is a high quality elegant [Hexo](http://hexo.io/) theme. It is crafted from scratch, with love.

## Live Preview

- Muse scheme: [LEAFERx](https://leaferx.online/) | [XiaMo](https://notes.wanghao.work/) | [OAwan](https://oawan.me/)
- Mist scheme: [Jeff](https://blog.zzbd.org/) | [uchuhimo](http://uchuhimo.me/) | [xirong](http://www.ixirong.com/)
- Pisces scheme: [Vi](http://notes.iissnan.com/) | [Acris](https://acris.me/) | [Rainy](https://rainylog.com/)
-  Gemini scheme: [Ivan.Nginx](https://almostover.ru/) | [Raincal](https://raincal.com/) | [Dandy](https://dandyxu.me/)

<!-- more -->

## Installation

```shell
$ git clone https://github.com/theme-next/hexo-theme-next themes/next
```

区分配置文件：

| 配置文件         | 路径                              |
| ---------------- | --------------------------------- |
| **站点配置文件** | `D:/blog/_config.yml`             |
| **主题配置文件** | `D:/blog/themes/next/_config.yml` |



## 设置RSS

1.安装RSS插件

```shell
$ npm install hexo-generator-feed --save
```

2.编辑**站点配置文件**，添加以下内容：

```yaml
#RSS订阅
plugin: 
- hexo-generator-feed
#Feed Atom
feed:
  type: atom
  path: atom.xml
  limit: 0
```

3.编辑**主题配置文件**，将rss字段置空。

## 主题风格

```yaml
#Scheme 主题风格
scheme: Muse
#scheme: Mist
#scheme: Pisces
#scheme: Gemini
```

四个主题风格，自行选择，消去注释即生效。

## 设置菜单

```yaml
menu:
  home: / || home                  # 主页
  tags: /tags/ || tags             # 标签
  categories: /categories/ || th   # 分类
  archives: /archives/ || archive  # 归档
  about: /about/ || user           # 关于我
# schedule: /schedule/ || calendar # 安排
# sitemap: /sitemap.xml || sitemap # 站点地图
# commonweal: /404/ || heartbeat   # 404公益
```

## 添加[标签]、[分类]、[关于]页面

只有**文章**（post）支持[标签]和[分类]。

1.添加[tags]、[categoies]、[about]页面：

```shell
$ hexo new page "tags"
$ hexo new page "categories"
$ hexo new page "about"
```

2.在source文件夹中找到新建页面：
①编辑tags.md：添加`layout:"tags"`
②编辑categories.md：添加`layout:"categories"`
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

## 添加自定义页面

1.添加自定义页面：

```shell
$ hexo new page "customPage"
```

2.匹配**主题配置文件**中的`menu`：

```yaml
menu:
  home: /
  tags: /tags
  categories: /categories
  archives: /archives
  about: /about               
  customPage: /customPage    # 键值对匹配
```

3.在source中找到customPage.md文件，根据需求自行编辑。

##添加更新时间

编辑**主题配置文件**：

```yaml
post_meta:
  item_text: true
  created_at: true   # 创建时间
  updated_at: true   # 更新时间
  # Only show 'updated' if different from 'created'.
  updated_diff: false # 只使用更新时间
  # If true, post's time format will be hexo config's date_format + ' ' + time_format.
  date_time_merge: false
  categories: true
```

## 阅读全文

在文章合适的位置添加`<!-- more -->`，Hexo推荐使用。

## 设置favicon图标

1.将favicon.png放到`themes\next\image`文件夹下

2.**主题配置文件**更改图片路径：

```yaml
favicon:
  small: /images/favicon-16x16.png         # 小图标：16x16
  medium: /images/favicon-32x32.png        # 大图标：32x32
  apple_touch_icon: /images/favicon.png    # apple图标大图
  safari_pinned_tab: /images/logo.svg
```

## 设置头像

1.将头像图片avatar.png放到`themes\next\image`文件夹下

2.**主题配置文件**更改图片路径：

```yaml
avatar: /images/avatar.png  # avater图片路径
```

## 社交账号

编辑**主题配置文件**，自行添加：

```yaml
social:
  GitHub: https://github.com/yourname || github-icon
  E-Mail: mailto:youremail || envelope-icon
  Weibo： https://weibo.com/yourname
```

## 友情链接

编辑**主题配置文件**，自行添加：

```yaml
links_icon: link
links_title: Links
#links_layout: block    #块状布局，选一个注一个
links_layout: inline    #行内布局，选一个注一个
links:
  Github: https://www.github.com
  知乎: https://www.zhihu.com
```

## 打赏

编辑**主题配置文件**：

```yaml
# Reward
reward_comment: 求打赏文本
wechatpay: /images/wechatpay.png  # 微信收款二维码 图片路径
alipay: /images/alipay.png        # 支付宝收款二维码 图片路径
#bitcoin: /images/bitcoin.png     # 比特币
```

## 文章版权信息

编辑**主题配置文件**，启用copyright服务：

```yaml
post_copyright:
  enable: true
```

## 访客&访问量

NexT主题中已经集成了**不蒜子统计**，直接编辑主题配置文件：

```yaml
busuanzi_count:
  enable: true              # 开启busuanzi数据统计
  total_visitors: true      # 访客
  total_visitors_icon: user
  total_views: true         # 访问量
  total_views_icon: eye
  post_views: true          # 文章阅读次数
  post_views_icon: eye
```

## 百度统计

1.登录百度统计，添加域名。若更换域名，需重新绑定。

2.复制 `hm.js?` 后面那串统计脚本 id：
![百度统计](http://p6uturdzt.bkt.clouddn.com/next-baidu_analytics.PNG)

3.编辑**主题配置文件**，添加**脚本id**：

```yaml
# Baidu Analytics ID
baidu_analytics: 脚本id
```

## 文章字数统计

1.安装字数统计插件：

```shell
$ npm install hexo-symbols-count-time --save
```

2.编辑**主题配置文件**：

```yaml
symbols_count_time:
  separated_meta: true     
  item_text_post: true     # 文章字数
  item_text_total: true    # 本站所有文章字数
  awl: 5
  wpm: 200
```

## 评论

### 来必力

1.登陆 [来必力](https://livere.com/) 获取你的 LiveRe UID。

2.编辑**主题配置文件**，添加LiveRe UID：

```yaml
livere_uid: #你的LiveRe UID
```

3.记住将可评论文档的顶部属性中`comments: true`

## 分享

### jiathis分享

编辑**主题配置文件**，添加jiathis_uid：

```yaml
jiathis:
  uid: 2160658
```

### 百度分享

编辑**主题配置文件**，设置baidushare：

```yaml
baidushare:
  type: button       # type: button | slide
```

## 搜索服务

### Local Search

1.安装local search插件：

```shell
$ npm install hexo-generator-searchdb --save
```

2.编辑站点配置文件，新增以下内容：

```yaml
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

3.编辑主题配置文件，启用local search功能：

```yaml
local_search:
  enable: true
```

## 修改文章底部标签[#]#

1.打开编辑`themes\next\layout\_macro\post.swig`

2.`Ctrl+F`找到`rel="tag">#`

3.将`#`替换为`<i class="fa fa-tag"></i>`

## 文章底部添加"本文结束"

打开编辑`themes\next\layout\_macro\post.swig`，在文章结束的地方添加如下代码：

```html
{% if not is_index %}
	<div style="text-align:center;color: #ccc;font-size:14px;">
		---------Thanks for your attention---------
	</div>
{% endif %}
```

![本文结束](http://p6uturdzt.bkt.clouddn.com/next-page_end.PNG)

## 添加访客&访问量描述

打开编辑`themes\next\layout\_third-party\analytics\busuanzi-counter.swig`：

![添加访客&访问量描述](http://p6uturdzt.bkt.clouddn.com/next-visitor.PNG)

## 添加Host-by描述

最近，银牌会员的Coding Pages在访问时会加载广告，需要在网站首页任意位置放置「Hosted by Coding Pages」，通过审核将取消广告。

打开编辑`themes/next/layout/_partials/footer.swig`，在**文件末尾**添加如下代码，将「Hosted by Coding Pages」置于页面底部。

```html
{% if theme.footer.powered.enable and theme.footer.theme.enable %}
  <div class="copyright">
    Hosted by <a href="https://pages.coding.me">Coding Pages</a>
    &&nbsp;<a href="https://pages.github.com">GitHub Pages</a>
  </div>
{% endif %}
```

## DaoVoice实现在线联系

1.首先在[DaoVoice](http://dashboard.daovoice.io/get-started?invite_code=bcc0de9a)注册一个账号，注册完成后在[应用设置]-[安装到网站]中找到app_id。

2.打开编辑`themes/next/layout/_partials/head/head.swig `，添加如下代码：

```html
{% if theme.daovoice %}
  <script>
  (function(i,s,o,g,r,a,m){i["DaoVoiceObject"]=r;i[r]=i[r]||function(){(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;a.charset="utf-8";m.parentNode.insertBefore(a,m)})(window,document,"script",('https:' == document.location.protocol ? 'https:' : 'http:') + "//widget.daovoice.io/widget/0f81ff2f.js","daovoice")
  daovoice('init', {
      app_id: "{{theme.daovoice_app_id}}"
    });
  daovoice('update');
  </script>
{% endif %}
```

3.编辑**主题配置文件**，添加如下代码：

```yaml
# DaoVoice
daovoice: true
daovoice_app_id: yourapp_id
```

4.设置DaoVoice页面样式

![daovoice](http://p6uturdzt.bkt.clouddn.com/next-daovoice.png)

5.在[应用设置]-[添加微信]中绑定微信，关注小程序，即可实时收发消息。



## 修改Pisces主题宽度

打开编辑`themes\next\source\css\_schemes\Pisces\_layout.styl`，在底部添加如下代码：

```
// 以下为新增代码！！
header{ width: 90% !important; }
header.post-header {
  width: auto !important;
}
.container .main-inner { width: 90%; }
.content-wrap { width: calc(100% - 260px); }

.header {
  +tablet() {
    width: auto !important;
  }
  +mobile() {
    width: auto !important;
  }
}

.container .main-inner {
  +tablet() {
    width: auto !important;
  }
  +mobile() {
    width: auto !important;
  }
}

.content-wrap {
  +tablet() {
    width: 100% !important;
  }
  +mobile() {
    width: 100% !important;
  }
}
```



> 参考资料：[next主题|使用文档](http://theme-next.iissnan.com/)



