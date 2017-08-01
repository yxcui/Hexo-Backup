---
title: Github+Hexo搭建博客网站---基础环境
tags: Github
---
### 写在前面
记录博客的地方的确很多，比如CSDN、博客园、简书和作业部落等，但是这些好像不易百度到或者想直接去找自己的资料，所以如果有一个公共接口进入，能够将所有的记录内容都能访问到，就显得很easy，这就可以通过一个域名进入博客网站主页，然后就很简单找到自己记录过的笔记和心得，是个很不错的选择，还能装一装X，拥有自己的[独家域名][1]。
以后还可以将自己做的一些工作放到博客上，比如做的一些数据分析工作等。

### 一、所需材料
#### 1. Git 安装
此前总结过[Git的安装和配置过程](https://zybuluo.com/ecnu-cyx/note/692971)。

#### 2. Node.js 安装
菜鸟教程上有很好的[Node.js安装和配置教程](http://www.runoob.com/nodejs/nodejs-install-setup.html)。

#### 3. Hexo
[Hexo][2] is a fast, simple and powerful blog framework. You write posts in Markdown (or other languages) and Hexo generates static files with a beautiful theme in seconds. [中文帮助文档][3]

### 二、Hexo安装与配置
#### 1. 安装Hexo
在任意处打开Git Bash，执行`$ npm install -g hexo-cli` 
【注：npm命令是集成在新版的node.js中的，可以输入`npm -v`来查看npm的版本，即node.js的版本，出现版本号说明安装成功。npm可以从服务器下载第三方的包和命令行程序到本地，同样可以将自己写的包和命令行程序上传到NPM服务器上】

#### 2. 创建本地存放博客目录
选择一个本地目录，空白处右键选择Git Bash Here，执行：
>- `$ hexo init <folder>`  #创建目录并初始化
>- `$ cd <folder>`  #进入创建的文件夹
>- `$ npm install`  #安装依赖包
>- 目录结构如下：
    + .
        ├── _config.yml
        ├── package.json
        ├── .gitignore
        ├── node_modules
        ├── scaffolds
        ├── source
        |   ├── _drafts
        |   └── _posts
        └── themes
        
#### 3. 启动本地服务
执行以下命令启动本地服务：
>- `$ hexo generate`  #生成静态文件
>- `$ hexo server`  #启动本地服务器

如果启动过程中没有报错，此时可以用浏览器访问`http://localhost:4000/`，会出现一个Hello World的博客页面，hexo使用的默认主题是landscape，而且此时的服务是本地启动的，别人并不能看到。
【注：更改本地服务端口命令`hexo server -p <port>`】

#### 4. 与Github连接
>1. 首先在Github上创建版本库New Repository
注意：**repository的名字必须为`username.github.io`，username即为Github的账户名**，我的个人地址为`https://yxcui.github.io`，如果将Repository name随意填写，是不能访问的，返回的是404的错误页面。

>2. 配置站点文件`_config.yml`
站点配置文件位于博客目录下`D:\Hexo\_config.yml`，，找到`deploy`属性，修改为如下：
    + 注：冒号后有一位空格
    `deploy:
        type: git  #推送方式
        repository: https://github.com/yxcui/yxcui.github.io.git  #Github上创建的版本库目录
        branch: master  #推送的版本库分支`

>3. 将服务部署到Github上
    - `$ hexo clean`
    + `$ hexo g`
    - `$ hexo d`  ##`hexo d`命令第一次会要求输入用户名和密码，即Github的用户名和秘密
【注：如果出现错误"`ERROR Deployer not found : github`"，先运行`$ npm install hexo-deployer-git --save`，在执行上述命令】

### 最后访问
个人主页：https://yxcui.github.io





  [1]: https://yxcui.github.io/
  [2]: https://hexo.io/
  [3]: https://hexo.io/zh-cn/docs/