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

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.


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

## conda
    // 清华源
    https://pypi.tuna.tsinghua.edu.cn/simple

    pip install 第三方库的名称 -i https://pypi.tuna.tsinghua.edu.cn/simple

    //windows powershell

    conda search cudatoolkit --info
    conda search cudnn --info

    conda install cudatoolkit=11.8
    conda install cudnn

    pip3 uninstall urllib3
    pip install urllib3==1.23 -i https://pypi.tuna.tsinghua.edu.cn/simple

    // wsl
    nvidia-smi ，看到显卡当前的状态例如温度、显存占用情况等
    watch -n 1 nvidia-smi # 1表示每1秒刷新一次

    source ~/.bashrc   使用代码，激活conda

    // 删除ubuntu子系统
    wsl --unregister Ubuntu-22.04.4 LTS

    conda --version
    conda activate
    conda deactivate

    conda create -n 虚拟环境名称 python=3.10
    conda activate 虚拟环境名称
    conda info --env

    conda env list
    conda env remove -n <虚拟环境名称>

    exit()或quit()


    // 使用 VSCode 打开当前路径的📂文件夹
    code ./


    // 删除文件夹	
    rm 文件夹
    rm -rf /root/logs/game


    powershell
    1.当前目录下
      新建文件
        New-item 1（文件名）.doc（文件类型后缀doc\txt等）
        New-item  1.doc
      删除文件
        remove-item空格1（文件名）.doc（文件类型后缀doc\txt等）
        remove-item  1.doc
      对文件添加内容
        Set-content 空格1.txt（文件名+后缀）空格-value空格”123（内容）”
        Set-content  1.txt  -value  “123”
      在文件中加内容
        add-content空格1.txt(文件名+后缀)空格-value 空格"123”（要添加的内容）
        add-content   1.doc  -value  “123”
      删除文件内容
        Clear-content空格1.txt（文件名）
        Clear-content  1.txt
      打开创建的文件
        .\1.txt
        .\文件名+后缀

    2.在其他目录
      

    WSL 访问 Windows 文件时，可以直接使用/mnt/{Windows盘符}
    ls：列出当前目录中的文件和子目录
    pwd 当前路径

    运行python文件 python main.py


批量注释 ctrl + K + C
取消注释 ctrl + K + U



## 中文搜索支持

### 配置
    pip install jieba -i https://pypi.tuna.tsinghua.edu.cn/simple
    
### mkdocs.yml
    plugins:
      - search:
          separator: '[\s\u200b\-]'
      




### 辅助资料

https://www.runoob.com/git/git-branch.html


### python
生成 requirements.txt 文件


### markdown

``` markdown
Markdown 目录：
[TOC]

Markdown 标题：

# 这是 H1

## 这是 H2

### 这是 H3

Markdown 列表：

- 列表项目

1. 列表项目

*斜体*或*斜体*
**粗体**
**_加粗斜体_**
~~删除线~~

Markdown 插入链接：
[链接文字](链接网址 "标题")

Markdown 插入图片：
![alt text](/path/to/img.jpg "Title")

Markdown 插入代码块：

    ```python
    #!/usr/bin/python3
    print("Hello, World!");
    ```

Markdown 引用：

> 引用内容

Markdown 分割线：
---

Markdown 换行：
<br>或两个空格或一个空行

Markdown 段首缩进：
&ensp; or &#8194; 表示一个半角的空格
&emsp; or &#8195; 表示一个全角的空格
&emsp;&emsp; 两个全角的空格（用的比较多）
&nbsp; or &#160; 不断行的空白格
```


https://md.xalaok.top/docs/syntax/detailed/bolditalicunderline/