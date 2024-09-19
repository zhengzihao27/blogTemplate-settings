---
title: 静态页面相关
date: 
    created: 2024-09-19
    updated: 2024-09-19
authors: 
  - zzh
categories:
  - Git
---

# git相关指令

此处存放一些关于部署静态页面相关的git指令

<!-- more -->


## git command

    echo "# 1" >> README.md 
    git init 
    git add README.md           // 使用 git add 命令将工作区中的修改添加到暂存区
    git commit -m "第一次提交"   // 将暂存区中的修改提交到版本库
    git branch -M main 
    git remote add origin https://github.com/zhengzihao1998/1.git
    git push -u origin main

    git remote add origin https://github.com/zhengzihao1998/1.git
    git branch -M main 
    git push -u origin main     // 将本地版本库的提交推送到远程仓库

    git status          // 查看哪些文件在暂存区中

    git remote -v       // 显示所有远程仓库

    git rm -r --cache .
    git add .           // 将工作区中的所有修改添加到暂存区
    git commit -m “gitignore working”
    git push --force origin main    // 本地覆盖远程仓库

    git init // 在目录中创建新的 本地 Git 仓库
    
    https://pypi.tuna.tsinghua.edu.cn/simple

    windows

    conda search cudatoolkit --info
    conda search cudnn --info

    conda install cudatoolkit=11.8
    conda install cudnn

    pip3 uninstall urllib3
    pip install urllib3==1.23 -i https://pypi.tuna.tsinghua.edu.cn/simple


## 中文搜索支持

### 配置
    pip install jieba -i https://pypi.tuna.tsinghua.edu.cn/simple
    
### mkdocs.yml
    plugins:
      - search:
          separator: '[\s\u200b\-]'