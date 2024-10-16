---
title: Games002-Notes
date: 
    created: 2024-09-30
    updated: 2024-09-30
authors: 
  - zzh
categories:
  - Git
---

# Linux + Shell

Games002-Notes

<!-- more -->

## What

Linux 是一群开源的、基于 Linux 内核的类 Unix 操作系统集合。

## Why

**优点：**
:   方便的包管理  
    * 开源  
    * 快而稳定  
    * 功能齐全  
    * ...

**应用场景：**
:   远程服务器  
    * 仿真环境  
    * OS，网络等领域  

## How

以下三种方式选一种即可访问Linux  

1. 安装Linux系统[知乎]  
2. 使用WSL[官方文档]  
3. 使用虚拟机


  [知乎]: https://zhuanlan.zhihu.com/p/294033435
  [官方文档]: https://learn.microsoft.com/zh-cn/windows/wsl/install

### 打开Shell

=== "Ubuntu"

    ```
    Ctrl + Alt + T
    ```

=== "Windows"

    ``` 
    PowerShell 中键入 wsl 后回车
    ```

### 常用命令

| 命令              | 功能           | 命令              | 功能           |
| :---------------: | :------------: | :---------------: | :------------: |
| `date`            | 显示时间       | `rm`              | 删除           |
| `shutdown -h now`  | 关闭系统       | `mv`              | 移动、重命名   |
| `man`             | 查看帮助文档   | `cp`              | 复制           |
| `cat`             | 显示文件内容   | `touch`           | 新建文件       |
| `cd`              | 切换当前路径   | `ln`              | 链接           |
| `pwd`             | 显示当前路径   | `find`            | 寻找文件       |
| `ls`              | 查看目录中的文件 | `whereis`         | 寻找命令路径   |
| `mkdir`           | 新建目录       | `passwd`          | 修改密码       |
| `neofetch`        | 查看系统       | `atop`            | 监视系统       |
| `less`            | 滚动查看内容   | `grep`            | 搜索字符串     |
| `exa`             | 比 `ls` 更好用 | `tldr`            | 命令提示       |


!!! Note
    Shell 本质是调用系统内置的程序。  
    Shell 会遍历PATH(环境变量)中的所有位置来搜索

### Linux中的路径

* 绝对路径 v.s. 相对路径
:   绝对路径：`/`开头
:   相对路径从`当前路径`出发  
* cd指令切换当前路径  
* 特殊路径：
:   `.`:当前路径  
:   `..`:父路径
:   `-`:上次到达的路径
:   `~`:home所在路径


### Reference

[1] https://games-cn.org/games002-slides/