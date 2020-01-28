---
title: Git 仓库代码无损迁移命令
date: 2018-04-09 15:48:00
tags: git
---

## 迁移远程仓库
```
// 克隆旧仓库镜像
git clone --mirror oldRepoUrl

// 添加新仓库地址
cd the_repo
git remote add remoteName newRepoUrl

// 推到新的远程库
git push -f --tags remoteName refs/heads/*:refs/heads/*
```

## 更新本地仓库
方式1. 远程仓库迁移后，可删除本地代码仓库和镜像仓库，重新克隆新仓库代码。
方式2. 进入本地代码仓库，更新仓库地址
```
// git查看远程仓库地址
git remote -v

// 设置新的仓库地址
git remote set-url origin newRepoUrl
```




