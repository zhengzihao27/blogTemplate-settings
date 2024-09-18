# 主页

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.


## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.



https://zhengzihao1998.github.io./



## 指令

    Enter the project folder
        cd zhengzihao1998.github.io

    Add, commit, and push your changes
        git add --all
        git commit -m "Initial commit"
        git push -u origin main


Fire up a browser and go to https://username.github.io.



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


    