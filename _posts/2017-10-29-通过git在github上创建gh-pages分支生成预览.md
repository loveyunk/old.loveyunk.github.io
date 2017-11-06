---
layout: post
title:  通过git在github上创建gh-pages分支生成预览
date:   2017-10-29      
---

项目本身是一个git仓库，而最终打包生成的可预览文件在dist文件夹下，所以要将dist文件夹上传至gh-pages分支。
1. 进入到dist文件夹下：
    * `git init` // git初始化，在dist文件夹里再初始化一个git仓库
2. 创建gh-pages分支：
    * `git checkout --orphan gh-pages` // 用于创建一个全新的分支，不包含提交的历史，如果不提交东西，这个分支相当于没有创建
3. 添加文件到暂存区：
    * `git add .`
4. 记录提交信息：
    * `git commit -m "This is a message"`
5. 关联远程仓库：
    * `git remote add <主机名> <网址>` // git remote add origin ...
6. 部署到github上：
    * `git push origin gh-pages` // 如果远程主机没有gh-pages分支，会自动创建
