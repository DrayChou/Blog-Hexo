---
date: 2016-05-13 20:05:00
layout:  post
title:  "使用Travis CI自动部署Hexo"
tagline:
categories:
-  web
tags:
- travis-ci
- ci
- hexo
---

## 前言
之前换过很多的静态博客系统，但是每个系统都需要本地做一定的部署，这点很麻烦。
[Gor](https://github.com/wendal/gor) 倒是有可执行文件，但是本地部署的时候还是需要合并提交代码，还是略不爽。
今天在查 CI 系统的时候发现了 [Travis CI](https://travis-ci.org/) ,于是，一切都很开心了。

## 关于 Travis CI
这是一个通过脚本来进行自动部署的系统，本身与 Github 高度集成，目前对于公开的项目免费支持。

## 开启travis-ci
首先去 [Travis CI](https://travis-ci.org/) 官网，点击右上角Sign in with GitHub通过github授权登录。然后去到个人信息页面，开启需要使用 travis 的项目，在我这里就是 DrayChou/Blog-Hexo 。

## 密钥
因为需要通过脚本提交到 Github ，所以需要先申请一个 token ，避免密码或者证书问题造成的麻烦。
Token 申请地址是 [https://github.com/settings/tokens](https://github.com/settings/tokens) 。
记得给予 public_repo 的权限，要不无法提交修改到 GitHub。
记得这个 token ，后面会用到。

## Travis CI 的命令行工具
### 执行下面的命令安装命令行工具。

    gem install travis

### 生成脚本
切换到 blog 的目录下，执行下面的命令，记得输入 node 语言

    $ travis init
    detected repository as DrayChou/Blog-Pugo
    Main programming language used: |HTML| node
    .travis.yml file created!
    enabled

## 设置脚本
编辑这个 .travis.yml ，按需添加对应的项。 env.global.secure 是发布的时候生成的数据，请无视。

    language: node_js

    node_js:
    - '5.1'
    
    env:
      global:
      - secure: "long secure base64 string"
    
    before_install:
    - export TZ=Asia/ShangHai
    
    install:
    - npm install
    
    script:
    # 初始化 GIT
    - git config --global user.name "$GIT_NAME"
    - git config --global user.email "$GIT_EMAIL"
    - git config --global push.default simple
    
    # 设置项目路径
    - rm -rf public
    - git clone --depth 50 --branch gh-pages https://$GH_TOKEN@github.com/$GIT_NAME/$HEXO_BLOG public
    
    # 生成
    - hexo generate
    
    # 发布出去
    - cd public
    - git add -A .
    - MESSAGE=`date +\ %Y-%m-%d\ %H:%M:%S`
    - git commit -m "Site updated:$MESSAGE"
    - git push origin gh-pages --quiet

## 执行下面的命令添加执行操作
命令的参数请自行替换。

    travis encrypt 'GIT_NAME="<Personal GitHub Name>" GIT_EMAIL="<Personal GitHub Email>" HEXO_BLOG="<Personal Blog Repositories>" GH_TOKEN="<Personal Access Token>"' --add

命令执行完毕之后会自动修改 .travis.yml 添加对应的 env.global.secure。
把这个文件提交到 Github。

## 开始执行
Push 到 Github 之后， Github 就会通过之前定义的 hook 去调用 travis ,然后 travis 就会在后台开始按照脚本执行，可以在 [travis-ci](https://travis-ci.org/) 后台通过查看日志观察发布有没有问题，如果有问题再按照提示进行调试。

## 附记
[注意：git push 時一定要加 --quiet，否則先前設定的 Personal Access Token 將會印出，這樣就失去加密意義了。](http://ssk7833.github.io/blog/2016/01/21/using-TravisCI-to-deploy-on-GitHub-pages/)

## 参考
1. [使用 Travis CI 自動部署 GitHub Pages](http://ssk7833.github.io/blog/2016/01/21/using-TravisCI-to-deploy-on-GitHub-pages/)
2. [使用travis-ci自动部署hexo博客](http://w3cboy.com/post/2016/03/travisci-hexo-deploy/)
3. [hexo 指令](https://hexo.io/zh-tw/docs/commands.html#generate)

