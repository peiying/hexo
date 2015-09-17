title: 最靠谱的搭建独立博客GitHub Pages与Hexo的教程
---

## git
下载新版本git系统，一路安装
[git官方下载地址][1]
git的教程，推荐最权威教程[廖雪峰git教程][2]

## 配置SSH keys
让本地git项目与远程的github建立联系
在windows下，我们直接使用git提供的gitbash，linux命令行风格。
### 生成新的SSH key：
```bash
$ ssh-keygen -t rsa -C "邮箱地址"
```
然后一路按回车

### 添加SSH key到GitHub
本地设置SSH Key之后，需要添加到GitHub中

* 打开本地~\.ssh\id_rsa.pub文件
* 登录GitHub，点击右上角的 Account Settings--->SSH Public keys ---> add another public keys
* 把你本地生成的钥匙复制到里面，然后点击add key


### 设置用户信息
Git会根据用户的名字和邮箱来记录提交，所以需要设置下个人信息

```bash
$ git config --global user.name "peiying"//用户名
$ git config --global user.email  "xxx@gmail.com"//填写自己的邮箱
```

## 创建Github Pages
我们需要使用Pages服务，通过用户名建立的username.github.io站。这个服务每个用户只能建立一个

### github上建立仓库
登录github首页，点击右下角New Repository

填写项目信息：
project name：peiying.github.io
description： My Blog
注：Github Pages的Repository名字是特定的，比如我Github账号是peiying,那么我Github Pages Repository名字就是peiying.github.io

点击Create Repository 完成创建。

## 使用hexo搭建博客

由于hexo是基于Node.js的框架，安装前需要先安装Node.js
Node.js的官网上竟然下载不了，非常坑爹，所以自行度娘吧

### 安装hexo
安装好Node.js后，安装hexo
```bash
$ npm install -g hexo
```
建立个文件夹来放hexo生成的项目文件，然后在文件夹中输入
```bash
hexo init
```
然后生成静态页面并预览
```bash
$ hexo g && hexo s
```
OK， 在浏览器中输入`localhost:4000`，一个hexo站点就展示在你面前了。

### 配置Hexo
在Hexo的目录结构下，其中`_config.yml`是整个站点的配置文件，`source/_drafts`是彩稿文件目录， `source/_posts`是发表的博文目录，其他的目录暂时不用管

这里需要在`_config.yml`配置发布到github上的一些参数，很重要！（之前在这出过很多错）
    deploy:
      type: git
      repository: git@github.com:peiying/peiying.github.io.git
      branch: master
### 发布博客
```bash
$ hexo n  # == hexo new 建立新文章，默认在_posts下，layout="draft"时发布的是草稿
$ hexo p  # == hexo publish 将_drafts下的文件放到_posts下，也就是发布草稿
$ hexo g  # == hexo generate 生成静态网页
$ hexo s  # == hexo server 启动预览服务器，开启-d选项时可以预览草稿
$ hexo d  # == hexo deploy 发布到远程服务器，开启--generate选项可以在deploy前自动generate
```
这些是hexo常用命令，我们可以用 n 创建新文章，默认在_posts下。也可以直接在目录下拷贝md文件，最后用命令`hexo d`发布到github上



最后： 还可以在godady上买域名然后绑定，更换主题等。这里我没有实现，可以参考其他教程。

  [1]: http://www.git-scm.com/download/
  [2]: http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/