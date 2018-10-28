---
title: 基于Hexo和Github搭建个人博客
date: 2014-10-10
tags: 个人博客
categories: 知识管理
lang: zh-cn
---

通常搭建个人博客需要相应的服务和技术支持，包括购买服务器空间，域名，挑选服务器部署工具等。这些对技术新人和小白专业性要求很高，而且很不友好。
如何最快速最简便的搭建个人静态博客，其实很简单。可以基于Github的开源服务替代服务器空间，使用git工具进行部署，域名也可以省去。
搭建博客的技术栈很多，我采用的Hexo，因为主题和样式丰富，具体的操作步骤如下：

<!-- more -->

## 安装
注意，因为我使用的是MAC 命令前加了sudo来用管理权限，WIN电脑不用写sudo安装Hexo需要Node.js和git，有这两个之后直接用命令行安装Hexo
（PS：发现官网改命令了，回来更新下）
``` bash
sudo npm install hexo-cli -g
```
## 初始化
创建一个文件夹 在命令行中将目录定位在该文件夹中，输入下面的命令（注意啊，目录一定搞清楚）：
``` bash
hexo init //初始化
npm install
```
## 生成静态页面
还是在该目录下执行命令：
``` bash
sudo hexo generate // 可以简写为 hexo g
```
## 安装hexo-server插件：
``` bash
sudo npm install hexo-server
```
## 本地启动：
``` bash
hexo server //可简写为 hexo s
```
如果执行上面出错4000端口被占用，我们可以修改默认的端口
在_config.yml文件最后添加下面这几段代码（几率很小）

``` bash
server:
  port: 4000
  compress: true
  header: true
```
如果还是报错的话，那么请确定你是否是在你创建的文件夹下，也就是你安装的hexo文件夹下运行的命令（PS：很简单一点就是看看在你运行命令的地方能不能看到_config.yml文件）

然后就是见证奇迹的时刻，在浏览器中输入 http://localhost:4000/ 。就可以看到啦！激动…
但是…..到这里你的博客还只能自己看到。别人看不到啊，怎么办？？？ 接着往下看…

## 配置Github
因为我是先研究的Github再研究的Hexo,所有Github早已经配置好啦，大概是这样的

新建一个仓库 这里要注意的是 新建仓库的名字必须是 你的用户名.github.io
在刚才安装Hexo的文件夹下找到_config.yml文件，我们要对他进行修改了。（马上就可以让别人看到你的博客啦！）
用编辑器打开这个文件 拉到最下面进行修改(注意啊，每个冒号后面都有一个空格，别踩坑！)
``` bash
deploy:
  type: git
  repository: 这里填写你的Github仓库地址（去你Github那里直接复制过来）
  branch: master
```
（文件的其他参数，我后面有写，先不要急！）
安装用来部署到git上的插件：
``` bash
npm install hexo-deployer-git --save
```
执行部署（就跟项目上线差不多，执行了别人就能看到了，想好有没有BUG啊)
``` bash
hexo deploy
```

## 问题汇总
收到反馈，大部分人在部署这个地方出现了很多问题
### 问题1：报错出现
``` bash
**place tell me who are you**
```
原因：
可能是你第一次使用GitHub上传东西，所有要告诉他，你是谁，好吧，那就告诉他吧。
（PS：运行下面命令，请注意，使用git bush运行。命令行可能会不识别）

解决：
我是 git config --global user.name "yangyangyang"
我的邮箱 git config --global user.email "yyy@qq.com"
(PS: 你别真的把 我是。。。 我的邮箱。。打上去了)
然后可以查看配置是否成功
``` bash
git config --list
```
然后生成秘钥 ssh-keygen -t rsa -C "yyy@qq.com" 应该是连续按三四个回车就OK
如果中间弹出个（y/n）输入个 y 接着回车
然后注意反馈的命令里面的这一句
``` bash
Enter file in which to save the key (/c/Users/Administrator/.ssh/id_rsa)
```
括号后面的是路径，取那个路径取找 id_rsa.pub文件，记事本打开，复制里面的所有内容。
接着去github点你的头像，然后点下拉中的 Settings 然后看左边有个SSH and GPG keys 点进去
再点绿色的 New SSH key
然后 title 随便输入一个 key 中粘贴你刚才复制的东西
点击 下方绿色按钮 Add SSH key 好了 再回去执行 hexo deploy吧。

### 问题2：报错出现
``` bash
error:failed to execute prompt script (exit code 1)
```
那么恭喜你，麻烦了。
原因：我猜测是配置文件的问题，也就是上面我们配置_config.yml文件的时候，没有配置好。
解决：检查你的配置文件
``` bash
deploy:
  type: git
  repository: 你仓库地址（HTTPS开头的）
  branch: master
```
看看格式是否正确 冒号后面必须跟空格，这几句的对齐方式也必须是这样的！！下面的缩进是两个空格，请不用使用 tab ！
检查完没问题，好的，再去执行一遍hexo deploy，还是报错，那么接着试

把配置文件改成这样：
``` bash
deploy:
  type: git
  repo: 你仓库地址 （git开头的）
  branch: master
  name: 你github上的用户名
  email: 你登陆github的邮箱
```
（PS：取仓库地址—-> 登陆上去后，在右上角点你的github头像，下拉菜单中点your profile，
然后找你刚才建的以你应户名然后.github.io结尾的仓库，点进去，右边有个绿色按钮，
点击后，下拉的面板中左上角出现Clone with HTTPS,那下面的文本框中就是你以HTTPS开头的仓库地址，
要使用git开头的，请点下拉面板中的右上角 Use SSH 然后复制下面的地址）

改完配置文件载执行 hexo deploy. 什么？还报错？ 那么我也没办法了！谷歌吧！

大功告成！ 接下来就是见证奇迹时刻，在浏览器中输入 刚才你的仓库名 就是那个 你的用户名.github.io

## 总结一下：
每次对主题、文件等就行了修改，需要三步才能让你的博客让别人看到

``` bash
hexo clean
hexo generate
hexo deploy
```

要是感觉单词长 就这样写

``` bash
hexo clean
hexo g -d
```

## 一些常用的命令

``` bash
hexo new “postName” #新建文章
hexo new page “pageName” #新建页面
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，’ctrl + c’关闭server）
hexo deploy #将.deploy目录部署到GitHub
hexo help #查看帮助
hexo version #查看Hexo的版本
```

创建的文章，在source/_posts下，后缀是md，哦对了！这里面那个Helloworld.md那个文件可以删了,
看到就想起来当初看java的时候，配置完环境，第一条输入的hello world！！

## _config.yml 文件的一些参数说明
``` bash
title #网站的标题
subtitle #网站的副标题
description #网站的描述
author #你的名字
language #网站的语言。使用2-lettter ISO-639-1代码。默认是en。（有填写规范的，别乱写）
timezone #网站的时区。Hexo默认使用计算机上的设置。你可以在这里找到可用的时区列表。一些例子是America/New_York，Japan和UTC。 （同上）
```