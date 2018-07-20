---
title: hexo+github/coding搭建个人博客
date: 2018-03-06 19:16:21
tags: [github,hexo,coding]
categories: "blog"
---
常见的博客系统有简书、新浪博客等等然而这些大多是使用官方域名，博客样式也比较单一，优点是容易上手，不必太注重编辑语法，缺点是博客的样式比较单一44，无法使用自己的域名，同时也就意味访问量注定不高，随着QQ空间、微信朋友圈的流行，人们对博客的浏览也越来越少，然而QQ空间、微信朋友圈大多以生活记录、趣事分享为主，虽然微信公众号经常会发布一些资讯、技术帖，然而微信客户端的限制注定无法满足人们的需要，仅仅从经验分享、交流而言。博客还是有存在的必要的。
<!--more-->

### 胡说八道

> 我为什么搭建博客？为什么不是WordPress而是Hexo？   

21世纪是信息时代，这年头谁没有个QQ空间、微信朋友圈，你又是否觉得微信朋友圈、QQ空间并不是一个想说什么就能说的地方，QQ空间随处可见的广告，朋友圈的矫情，当浅尝辄止成为思维定式，急功近利成为文化景象，喧嚣肤浅成为人们喜闻乐见的行为方式时，人们势必难以用心而行，无法静下心来。浮躁是这个时代的集体病症，生活中充斥着QQ空间、微信朋友圈的无病呻吟。是否还能有一个地方能个静下心来研究高深之学问，我想大概就只有博客了吧。你可以用博客来分享经验、记录。总之，在这里你说了算。搭建个人博客系统，无需购买云主机，避免WordPress的繁琐与臃肿，0基础上手，(未完待续)

|type|advantages|disadvantages|
|:-:|:-:|:-:|
|WordPress|可以更加专注于写作，媒体资源可以储存在主机上|需要主机、公网IP以及LNMP/LAMP环境，同时具备一定的建站基础|
|Hexo|无需主机（相对而言）以及公网IP同时提供二级域名，比较稳定|使用MarkDown纯文本语法写作兼容HTML，媒体资源一般使用外链|

虽然你可以在路由器上面跑` WordPress `,前提是你对*Linux*比较熟悉同时向宽带运营商提供固定的公网IP，公网IP资源相对比较匮乏，直接购买比较昂贵，向宽带运营商索要是不错的选择。当然如果你经常使用` Shadowsocks `(酸酸乳)的话，直接搭载同一台主机上面就行了，这样不至于性能过剩。而Hexo搭建静态博客是使用了` Github `和` Coding `提供的***Pages***服务，这个是比较稳定的，***Github***作为全球最大的开源社区，安全性和稳定性肯定不用担心，我们使用的*Pages*服务仅仅是[Github](https://github.com/)的冰山一角而已，或许从搭建blog以后你就会感受到Github的魅力。   


### 必备组件  
- [Git](https://git-scm.com/) 
- [Node.js](https://nodejs.org/en/)   

> Notice: 根据你使用的操作系统下载安装对于的版本即可，Linux和macOS可以通过命令行安装，对于macOS，安装包管理软件之后就可以通过源安装，不过不推荐这种方式，因为可能会用到root权限，这样以后生成、部署就比较麻烦。如果从来没有用过命令行，建议了解一下通配符。   

#### Linux下在Terminal下面输入以下命令安装` git `和` Node.js `  
```bash
sudo apt-get update       #检查更新
sudo apt-get install git    #安装Git
sudo apt-get install nodejs    #安装nodejs
```   
估计用` Linux `的用户应该看看官方的说明文档就会了。所以下面以` Windows `和` macOS `为例。其中macOS可以安装包管理软件来安装必须组件，例如MacPorts，Homebrew，Fink。     

#### git、Node.js下载      
下面链接均为64位系统长期支持版本。32位系统[点击这里](https://nodejs.org/en/download/)       
> Node.js
* [macOS Installer (.pkg)](https://nodejs.org/dist/v8.10.0/node-v8.10.0.pkg)
* [Windows Installer (.msi)](https://nodejs.org/dist/v8.10.0/node-v8.10.0-x64.msi) 

> Git   
- [macOS](https://sourceforge.net/projects/git-osx-installer/files/git-2.16.2-intel-universal-mavericks.dmg/download?use_mirror=autoselect)
- [Windows](https://github.com/git-for-windows/git/releases/download/v2.16.2.windows.1/Git-2.16.2-32-bit.exe) 

### 安装Hexo   

```bash
npm install hexo-cli -g     #安装Hexo
hexo init blog              #初始化博客
cd blog                     #进入博客根目录
npm install                 #安装hexo到博客根目录
``` 
(未完待续)



























