---
title: Termux安装Hexo静态博客
date: 2018-12-14 09:51:03
category: "Termux"
tags: [terminal] 
---
在安卓平台的Linux仿真模拟器Termux上面安装nodejs，从而搭建hexo静态博客。
<!--more-->
# 写在前面
个人感觉没有必要在手机上面写博客,原因有二:
- 手机屏幕太小，看着费劲
- 输入。。。不支持盲打，并且性能不够
但还是写一下，证明它确实可以搭建个人博客。

# 下载安装Termux

- [Termux](https://termux.com/)官网

# 安装Nodejs

如果你已经安装***nodejs***,先卸载它,因为我不确定会不会有问题。

```bash
pkg uninstall nodejs   #卸载nodejs
```

打开` Termux `执行:
```bash
pkg install openssh openssl  #安装ssh以及ssl
pkg install nodejs       #安装nodejs
```

![卸载安装nodejs](https://i.loli.net/2018/12/14/5c133fcb67892.png)


# 安装hexo

```bash
npm install hexo-cli -g     #安装hexo
```
ERROR:
![length is undefine](https://i.loli.net/2018/12/14/5c137f7302e2f.png)


查看日志，发现是这个文件有错误

![detail](https://i.loli.net/2018/12/14/5c137f69a2b4d.png)

输入` vim /data/data/com.termux/files/usr/lib/node_modules/npm/node_modules/worker-farm/lib/farm.js `并修改` maxConcurrentWorkers `

![改为0](https://i.loli.net/2018/12/14/5c137f6a05de9.png)

> 重新安装` hexo-cli `

![安装没问题了](https://i.loli.net/2018/12/14/5c137f733d4b9.png)

进入宿主目录，同时为我们的博客网站创建一个目录

```bash
cd ~
mkdir blog
```

接下来我们初始化博客根目录，在博客上级目录执行` hexo init blog `(blog是你博客网站根目录的名字)
![初始化博客根目录](https://i.loli.net/2018/12/14/5c137f7412327.png)

> 小结

```bash
cd ~       #change directory,进入宿主目录
mkdir blog         #make directory 新建一个名为blog的文件夹，名字不一定叫blog可以根据你的喜好填写,这个目录就是博客网站的根目录
npm install hexo-cli -g   #安装hexo
hexo init blog         #初始化blog这个文件夹，这个文件夹就是第3条命令创建的文件夹，如果你使用的是其他名称，换成对应的名称即可。
cd blog                #进入blog这个文件夹，就是上面的博客网站根目录
npm install            #安装必要插件
```

# 添加ssh公钥

打开` Termux `输入` ssh-keygen -t rsa -C "2320813747@qq.com" `,这个邮箱地址换成你的。连续四次回车就生成了一对密钥。

```bash
Your identification has been saved in /data/data/com.termux/files/home/.ssh/id_rsa.
Your public key has been saved in /data/data/com.termux/files/home/.ssh/id_rsa.pub.
```
它会告诉你密钥生成在那个文件夹,上面是我的密钥生成路径，下面要相应替换成你的，使用` cat `来查看公钥内容：
```bash
cat /data/data/com.termux/files/home/.ssh/id_rsa.pub
```
复制输出的内容，打开` GitHub `，点击页面右侧头像旁边的倒三角，打开` Settings `，在页面左侧的` Personal settings `下面定位到` SSH and GPG keys `这一栏,点击右侧的` New SSH key `来添加一个密钥，其中` Title `随意,` Key `填写上一步` Git bash `里面生成的那个。最后` Add SSH key `就行了。

![添加ssh公钥](https://i.loli.net/2018/12/14/5c137b75b3912.png)

> 当你写好文章之后,首先得使用` hexo g `来生成，而` hexo s `可以在本地查看实际效果，` hexo d `会自动` push `到远程仓库，你就可以在浏览器地址栏中输入` username.github.io `来访问你的博客` username `是你的***GitHub***用户名。


```bash
hexo generate          #简写hexo g,即渲染并生成HTML页面。
hexo server            #简写hexo s,本地计算机启动服务，如果此时出现nodejs提示的防火墙，允许即可
```

# Hello World

博客安装好了，我要怎样写文章呢？
所以我们就有必要了解一下blog这个文件夹里面各个部分的作用了。

- 文章保存在` source/_posts `里面，是以` .md `结尾的文本文件，你可以用文本编辑器打开编辑它,不过我更推荐你用[Sublime Text 3](https://blog.ourfor.top/2018/03/24/3/)，这个文本文件使用的是` MarkDown `这种轻量级的标记语法，同时兼容` HTML ` ，是***纯文本的***，不像` WordPress `和` PPT `那样，当然这是优点。

- 写第一篇文章
打开` Termux `,输入` hexo new 我的XX `(我的XX-是标题，自拟)
这时候你就可以在` blog/source/_posts `里面看到它，编辑这个文件就OK了。

- 博客部署到远程仓库

如何从外网访问博客呢？其实我们打开的` http://localhost:4000/ `这个网址它的网站根目录是在` blog/public `下面，你可以打开public这个文件夹看看，里面就是网站页面的源码，你可以打开这个` index.html `文件，是不是就是你的博客的主页。只是没有图片而已，所以我们只需要将这个文件夹里面的东西放到一个外网可以访问的地方就行了，好在` hexo `的配置文件里面已经有相关的设置了，我们只需要稍作更改就行了。


## 1.注册GitHub账号或者Coding账号
略

## 2.新建一个` Repository `，点击页面上面的` New repository `
![New repository](https://i.loli.net/2018/12/08/5c0be7100ebc6.png)
- 这个` Repository name `填` username.github.io `,比如我的就填` ourfor.github.io `.你的根据你的` username `填。
- ` Public `在没有付费或者使用学生包的情况下，我们只能创建该权限类型的仓库，点击` Create repository `就可以完成创建。
- ` Description `可选，建议勾选☑️` Initialize this repository with a README `

这时候就会打开仓库主页，依次点击页面右侧的` Clone or download `、` Use SSH `复制框中的` Repo `地址，待会要用。

## 3.修改配置文件` _config.yml `
在博客网站根目录下面用` vim `(没安装vim就用vi)编辑` _config.yml `文件，在文件末尾，找到：
```bash
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type:

```
改成：
```bash
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: 
       github: git@github.com:ourfor/ourfor.github.io.git,master
       #coding: git@git.coding.net:ourfor/ourfor.git,master
  branch: master     
  message: blog update
```
上面这个` git@github.com:ourfor/ourfor.github.io.git ` 是我的仓库的SSH地址,你改成你的，如果你用的是` coding `你可以把` github `这一行用` # `注释掉，去掉` coding `前面的` # `。最后保存更改。

### 部署到GitHub

首先，我们得安装部署插件，由于GitHub只支持` git `,wo们安装的插件名为` hexo-deployer-git `

```bash
npm install hexo-deployer-git --save   #在博客根目录下执行
```

详见[官方文档](https://hexo.io/zh-cn/docs/deployment.html)

```bash
hexo g -d #渲染的同时部署到GitHub
```

# 相关阅读

- [hexo个人博客](https://blog.ourfor.top/2018/03/06/hexo-github-coding%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/)
- [初尝Typecho](https://blog.ourfor.top/2018/07/20/%E5%88%9D%E5%B0%9DTypecho/)
- [安装配置WordPress](https://blog.ourfor.top/2018/10/18/%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AEWordPress/)
- [GitHub和Git的初级玩法](https://blog.ourfor.top/2018/10/25/GitHub%E5%8F%8Agit%E5%88%9D%E7%BA%A7%E7%8E%A9%E6%B3%95/)
