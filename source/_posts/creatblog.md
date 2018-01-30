---
title: 在github上新建一个博客！
date: 2018-01-25 16:09:04
tags: [blogs,github,hexo]
categories: 博客

---
<!--用#标识符定义标题，#号数量越多标题越小-->
#### 前言
新年伊始，计划学点新的东西，为了督促这份学习，以及加深日渐脆弱的记忆力，想到搭建一个博客来记录所学所想。同时，也顺手记下对生活的所感所愿，如同小时候的日记本，以便良日久远之后怀念起来也有所依凭。

早前注册了github，并不常用，且荒废了小一年。于是，不如在此之上搭个博客好了。google了两篇教程，亦步亦趋，捣腾半天总算告竣。过程很简单，只是不熟练，也接连遇到了几个小问题，各种搜索之后，解决方法也一并写在了后面。

特别感谢下面两位博主，他们的教程对我助益良多：
<!--链接的插入方法：用[]输入链接名，后面紧跟()输入链接地址-->
[Cai's blog](http://ccc013.github.io/2016/01/20/hexo+github%20%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2%E6%80%BB%E7%BB%93/)
[小茗同学的博客](http://blog.haoji.me/build-blog-website-by-hexo-github.html)

话不多说，开始搭建！
<!-- more -->
#### 准备工作
毫无疑问，首先你要注册个github账户，最好对git有一些基础的了解——不了解也没关系，按着教程一步一步的来，新手小白也能完成。切记勿躁，出现错误就再自信看一遍教程，实在不行还有谷爹和度娘呢。

此外，你还需要：

  * *已经安装node.js、npm，可以使用命令行进行一些简单的操作（暂时不会也没关系）*
  + *已经安装好git客户端，mac或windows都有*

这两个的安装方法都很简单，跟着搜索的教程一路操作就行。

#### 开始搭建
  1. ##### 新建仓库
  登陆github，新建一个仓库（Repositpry），仓库名字必须是 **username.github.io** ，其中 **username** 是github的注册用户名，不是昵称。展示方式选择 **public** ，然后点击创建就ok了。仓库可能不会马上生效，稍等几分钟刷新就好。

  建好的仓库就是以后存放博客网页等代码的地方。

  2. ##### 配置SSH key
  如果你的电脑之前没有用过git，需要在本机生成一个SSH key，然后在github的个人设置里新建一个SSH key，把密钥复制粘贴进去。这样子才能通过git把本地代码提交给github的服务器。你可以把它理解成ftp，只不过在本机和服务器之间修建了一条秘密通道，不用再一遍遍的输入用户名和密码。

    如何新建一个SSH key：
    >* 打开终端（mac平台，windows平台用命令提示符），输入：
      $ ssh-keygen -t rsa -C "your_email@example.com"
      最后的邮箱是 **注册github账号的邮箱地址**。
      然后无脑按3次回车，会在用户目录下生成一个id_rsa.pub文件。它一般在Users/username/.ssh的文件夹里面。
     >* 用记事本或任何编辑软件打开刚才生成的id_rsa.pub文件，全选复制。然后打开github的个人设置页->SSH and GPG keys -> New SSH key,把内容粘贴在Key下面的内容框内，上面的title随便填，保存即可。
     >* 在终端输入：$ssh -T git@github.com
     出现<table><tr><td >Are you sure you want to continue connecting(yes/no)?</td></tr></table>输入yes，回车。如果出现下面的信息：
     <table><tr><td background=orange>You're successfully authenticated,but Github does not provide shell access.</td></tr></table>
     说明SSH配置成功！

  3. ##### 安装Hexo
  以下的操作全部在终端完成：
  >* 使用npm安装Hexo：
  `$ npm install -g hexo-cli`
  初始化hexo：
` $ hexo init [folder] `//folder为放置hexo的文件夹名
  `$ cd [folder]`
  `$ npm install`
  如果你提前建好了存放hexo的文件夹，也可以先cd到该文件夹再初始化：
  `$ hexo init`
`  $ npm install`
  初始化之后，该文件夹之下生成的目录如下：
   `_config.yml、 package.json、scaffolds、source、themes`
   其中source下有个posts文件夹，用来存放博客文章，格式为.md。
   themes里面存放主题。
   ——config.yml是全局配置文件，可在此更改博客名字、切换主题等。
   另外，主题里面还有一个config.yml文件，可对主题本身进行设置。
  初始化完成之后，可以执行命令：
  `$ hexo generate`
  `$ hexo server`
  然后在浏览器中输入`localhost：4000`进行本地预览。预览结束之后，使用键盘快捷键：`control + c`退出预览。
   >* 把下载的hexo部署到github
    首先需要安装一个插件：
    `$ npm install hexo-deployer-git --save`
    然后打开根目录下的_config.yml，搜索定位到以下代码：
    ```
    # Deployerment
    ## Docs:https://hexo.io/docs/deployment.html
    deploy:
    type:
    ```
  >   修改成：
    ```
    deploy:
    type: git
    repo: git@github.com:username/username.github.io.git
    branch: master
    ```
    >  其中的 **username** 是你的github用户名
    然后执行下列命令，升级并发布即可：
    ```
    $ hexo generate
    $ hexo deploy
    ```
    >  此命令也可以简化成`$ hexo d -g`。
    至此，hexob博客搭建完成。接下来需要进行简单的测试和美化。

#### 文章发布和主题设置

  1. ##### 文章发布和修改
   * 使用命令行新建文章：
  `$ hexo new “新建的文章名字”`
  之后，本地硬盘hexo所在的文件夹/source/posts里面就会出现一个以文章名字命名的md文件。打开即可编写文章（不推荐用记事本编辑）。
  也可以选择在本地直接新建.md文件。
   * 文章写完之后，再次通过`$ hexo d -g`命令生成并部署到github上面。

  2. ##### 主题更换和修改
  Hexo安装之后默认使用的主题是landscape，我们可以更换成自己喜欢的主题。只需要把下载好的主题放在themes文件夹里，然后修改全局配置文件_config.yml中对应的主题名，重新执行`hexo d`即可。
  我正在使用的主题是next，可以通过git直接clone到本地：
  `$ git clone http://github.com/iissnan/hexo-theme-next themes/next`
  主题切换成功之后，通过修改主题目录下的config.yml文件可以进行个性化设置，详情可参考这个博客：[NexT使用文档](http://theme-next.iissnan.com/)

#### 一些小问题
  1. ##### 域名绑定
  搭建在github上的博客，可以直接通过userna.github.io进行访问。如果想绑定别的域名，按照下面的步骤设置即可：
   * 登陆域名服务器，把域名解析到username.github.io。同时，通过ping命令获取username.github.io的ip地址，新建A绑定域名到该IP。
   * 在存放hexo的根目录之下的source文件夹里面新建一个CNAME文档，无后缀名，填入你要绑定的个人域名。
   * 提交`$ hexo d -g`命令，即绑定成功。

  2. ##### 分类页和标签页
   * 分别先建一个分类和标签页面，命令如下：
   `$ hexo new page "分类或标签名"`
   * 然后在文章页面的顶部修改对应的类型，即可添加标签或分类。
   ```
   title: 在github上新建一个博客！
   date: 2018-01-25 16:09:04
   tags: [blogs,github,hexo]
   categories: 博客
   ```
  3. ##### git的知识结构图
  ![git知识结构](http://7xifb5.com1.z0.glb.clouddn.com/wustrive-hexogit%E7%9F%A5%E8%AF%86%E7%BB%93%E6%9E%84.png)

   至此，博客搭建完成。
   以后发现问题，也会随时更新。
   春节之前，又下了一场不大不小的雪。此刻，天空灰蒙，白茫茫的大地之上一团和静。
