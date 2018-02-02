---
title: 给Hexo博客来一个简单的美容
date: 2018-02-01 09:47:10
tags: [hexo,blog]
categories: 博客
---
#### 依然废话先行
博客搭建完成，甩出去给人瞧之前难免还要修饰一番，过于娇艳的装束委实不懂，稍微修修容抹个保湿霜，至少让人看上去不讨厌就够了。

上次已经提到下载Next主题替代了Hexo的默认主题，Next本身就是一个极简的面貌，深得一众懒癌程序员大人的厚爱。而极简带来的好处也是显而易见——不容易犯错啊。好比形容一个人的装束简单又干净，你可以说他清爽，这总不是贬义词。当然，你也可以说他穷。

Hexo的美化也可以归纳为三步走：<font style="color:red;">基本配置的修改、自带功能的开启、扩展插件的安装。</font>下面一一道来。
<!-- more -->

#### 基本配置的修改
安装了Next之后，Hexo文件夹下共有两个_config.yml文件：
{% note primary %}
* hexo根目录下面的： _ config.yml
* themes文件夹下的：next/_ config.yml
{% endnote %}
 ##### 全局信息修改
其中第一个_config.yml是针对网页整体进行配置，第二个_config.yml是对主题进行修改配置。当你搭建好一个博客，第一步就会修改博客名字和作者，于是我们打开主目录之下的_config.yml,做了如下修改：
```
title: inhere  //博客名字
subtitle: 游少宅多 //博客副标题
description: tomorrow is better //博客的立意或个人口号，比如为人民服务之类
author: zizhou //博客作者
language: zh-Hans  //修改博客显示语言
```
** 由于hexo默认是英文，所以需要在语言修改成汉语，也即是*zh-hans*。**

下面的简单修改要在themes/next文件夹之下的_config.xml里进行：
##### 首先修改主题展现方式
next主题自带了四种前端展现样式（打开_config.yml文件，ctrl+f或cammand+f搜索“Schemes”即可找到），分别是：
```
#scheme: Muse  //通栏页面，菜单栏居中，大气舒畅
#scheme: Mist  //也是通栏页面，顶部菜单栏
scheme: Pisces //750像素的页宽，菜单栏可设置在左右两边，清爽优雅，我的选择
#scheme: Gemini //950像素的页宽，其它同上
```
 主题形式的设置只需要把样式名称前的#去掉即可，以下在xml中的大部分设置方法也是如此。如果选择了Pisces或Gemini，还可以设置sidebar的position，居左或居右，二选一。
##### 设置博客头像
博客头像默认在sidebar设置，同样搜索并定位到siderbar，设置avatar：
```
avatar: /images/archer.jpg   
```
 推荐自定义图像放在themes下的images里。
##### 设置浏览器小图标
如果没有设置的话，浏览器顶部网页标题之前的图标是一张难看的白纸，实在有碍美观。修改也很简单，找到下面这行，添加图片即可。
```
favicon: /images/favicon.ico
```
ico是一种独特的图片格式，16X16的像素分辨率即可。至于如何寻找或制作，度娘会告诉你。

#### 自带功能的开启
Next主题本身内置Rss和社交账号快捷链接，只需在config文件里开启即可。
##### 设置社交账号
```
social:
  GitHub: https://github.com/zizhouyuyu
  Twitter: https://twitter.com/zizhou
```
 当然也可以添加facebook、微博等等账号，格式就是前面是社交平台的英文名，比如：weibo，后面是个人地址的链接。注意：冒号后面要加一个空格。接下来还要打开社交平台的小logo，Next已经内置了如下这些：
```
social_icons:
  enable: true
  icons_only: false
  transition: false
  # Icon Mappings.
  # KeyMapsToSocialItemKey: NameOfTheIconFromFontAwesome
  GitHub: github
  Twitter: twitter
  FB Page: facebook
  VK Group: vk
  Skype: skype
  YouTube: youtube
  Instagram: instagram
  StackOverflow: stack-overflow
  Weibo: weibo
```
 所有的图标都来自FontAwesome，可以自由寻找自个喜爱的添加在后面。
##### 开启Rss
{% note primary %}
1. 打开终端，输入命令行：
** npm install hexo-generator-feed --save **
2. 在主题下的config.yml文件中开启Rss功能：
** rss: /atom.xml **
{% endnote %}
Rss作为最成功的信息聚合格式，虽然已经被各大新闻app所取代，但是在某个小型圈子里依然是大家最快获取关注信息的方式。此处习惯性开启。

##### 版权信息的关闭和字体修改
Next主题默认在首页的页脚显示Hexo和Next的版权信息，基于对它们无私的分享精神之致敬，没啥乱七八糟的爱好不推荐修改。
字体修改在下面这一行：
```
font:
 global:
  external: true
  family: Lato  //此处修改全局字体，单独设定的话可以在下面的子项中完成
```
#### 扩展插件的安装
Hexo的插件挺多的，上面的Rss其实也算是一个插件。除此之外，目前我还用到了两个：字数统计和评论管理系统。
##### 字数统计插件
* 打开终端，进入hexo根目录，使用命令行安装word_count插件：
```
npm install hexo-wordcount --save
```
* 在主题配置文件config.yml里打开 **wordcount** 功能：
```
post_wordcount:
  item_text: true
  wordcount: true  //此处默认为flase
  min2read: false
  separated_meta: true
```
##### 评论系统插件
Next主题本身就支持多款评论系统，著名的DISQUS不必说，连畅言和多说也包含在内。曾经还支持网易云跟帖，直到它被猪场抛弃。
我用的是韩国的一个产品<font style="color:red;">|要做一个有品有味抵制韩货的人！|</font>，之所以使用它，也没别的原因，单纯因为它的名字——**来比力**。安装方法也是一以贯之的两步走：
* 点击进入[来比力](https://livere.com/)官网，注册账号并登陆，以此选择->**管理页面**->**代码管理**，复制代码框之中data-uid之后双引号之内的字母。
* 再次打开主题下的config.yml文件，搜索定位liverre_uid，把上面复制的代码粘贴在：后面：
```
livere_uid: THISnideDAIma==
```

#### <font style="color:red;">注意</font>
各种修改之后，不要忘了 `hexo d -g` 一下，然后刷新几遍博客就能看到效果了。
