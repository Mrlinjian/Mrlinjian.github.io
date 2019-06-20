---
title: Github Pages 搭建 Hexo Blog
date: 2019-06-19 17:27:12
tags:
---

### 一、安装 Hexo 运行环境

#### 1.1 安装node.js

在[node.js](<https://nodejs.org/en/>)官网下载最新的安装包并安装（程序已经包含npm，无需单独安装）

```sh
node -v #验证是否安装成功
```



#### 1.2切换npm为淘宝的镜像源 [官方地址](<http://npm.taobao.org/>)

```sh
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

#### 1.3安装Git

下载安装[Git](https://git-scm.com/download/)

```sh
git --version #验证是否安装成功
```





### 二、Github 新建 repository

#### 2.1新建reporistory

新建reporistory，命名为自己的用户名+github.io（Mrlinjian.github.io）

#### 2.2Clone仓库到本地

```sh
git Clone https://github.com/Mrlinjian/Mrlinjian.github.io.git
```

#### 2.3新建Hexo分支

```sh
git checkout -b hexo
```



### 三、Hexo 安装

#### 3.1安装Hexo

```sh
cnpm install -g hexo-cli #npm 使用官方源可能没反应，淘宝源会更好用
```

#### 3.2初始化Hexo

```sh
hexo init #初始化hexo需要空的文件夹，可以新建一个文件加进行
```

#### 3.3拷贝Hexo初始化后的文件到刚刚Clone到本地的文件夹中

#### 3.4安装相关依赖包

```sh
cnpm install
```

#### 3.5本地博客搭建完成，生成静态页面并启动本地服务器

```sh
hexo generate #生成静态页面
hexo server #启动本地服务器 http://localhost:4000
```



### 四、Blog 远程备份及部署

#### 4.1修改Hexo配置文件（_config.yml）

找到Mrlinjian.github.io文件夹下的_config.yml文件修改deploy节点的内容

```sh
deploy:
  type: git
  repo: https://github.com/Mrlinjian/Mrlinjian.github.io.git
  branch: master
```

#### 4.2安装推送到Github的远程部署插件

```sh
cnpm install hexo-deploy-git --save
```

#### 4.3博客源文件备份及静态页面部署

```sh
git add .
git commit -m "提交说明"
git push origin hexo #源文件提交推送到hexo分支
hexo generate -d #静态页面生成并调用_config.yml中的deploy配置发布到master分支
```



#### 4.4修改Github默认分支
{% asset_img Github修改默认分支.png [修改hexo分支为默认分支] %}

### 五、Blog 日常管理

#### 5.1博客日常更新

##### 5.1.1源文件更新

```sh
git add .
git commit -m "提交说明"
git push origin hexo #源文件提交推送到hexo分支
```

##### 5.1.2生成静态文件并部署

```sh
hexo generate -d #静态页面生成并调用_config.yml中的deploy配置发布到master分支
```

#### 5.2本地资料丢失使用备份或者新地址使用

##### 5.2.1Clone仓库到本地文件加

```sh
git Clone https://github.com/Mrlinjian/Mrlinjian.github.io.git
```

##### 5.2.启用用Hexo
```sh
# hexo init 无需再执行这条指令
```

```sh
npm install -g hexo-cli
npm install
npm install hexo-deployer-git --save
```

### 六、博客插入本地图片问题

#### 6.1修改_config.yml文件

```sh
post_asset_folder: true #false 改为true
```

#### 6.2在source/_post文件夹下建立与博客文章同名的文件夹，图片放入其中

{% asset_img 本地图片插入.png [本地图片插入] %}

### 七、更换主题

#### 7.1选择自己喜欢的 [博客主题](https://hexo.io/themes/)

Clone到themes文件夹中

```sh
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

#### 7.2修改_config.yml文件

```sh
theme: next
```

#### 7.3直接Clone的主题源文件，在对源文件进行备份commit时会涉及到子项目问题，我们修改themes/next中的.gitignore文件，新增一行

```sh
.git
```

