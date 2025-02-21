---
title: python相关
date: 
    created: 2025-02-21
    updated: 2025-02-21
authors: 
  - zzh
categories:
  - Code
---

# python相关

使用python的笔记

<!-- more -->

## 0. 环境准备

#### conda command

    conda --version                 // 查看conda版本
    conda activate                  // 激活环境
    conda deactivate                // 取消环境
    conda create -n 虚拟环境名称 python=3.10
    conda activate (n虚拟环境名称)   // conda activate base
    conda info --env
    conda env list  
    conda env remove -n <虚拟环境名称>

    安装第三方库
    清华源 -i https://pypi.tuna.tsinghua.edu.cn/simple
    阿里源 -i https://mirrors.aliyun.com/pypi/simple/
    pip install 第三方库的名称 -i https://pypi.tuna.tsinghua.edu.cn/simple
    conda install 第三方库的名称 -i https://pypi.tuna.tsinghua.edu.cn/simple
  

### conda 源
    conda config --show channels                // 查看已有源
    conda config --remove channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/         // 删除某个源
    conda config --remove-key channels          // 还原默认源
    conda config --set show_channel_urls yes    // 设置搜索时显示通道地址
    conda install opencv -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/  // 指定源下载
    conda info    // 检查是否换源成功

#### 添加清华镜像源
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/

#### 中科大源
    conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
    conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/free/
    conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
    conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/msys2/
    conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/bioconda/
    conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/menpo/
    conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/pytorch/

#### pip 源
#### 常见镜像源源
    清华：https://pypi.tuna.tsinghua.edu.cn/simple
    阿里云：https://mirrors.aliyun.com/pypi/simple/
    中国科技大学: https://pypi.mirrors.ustc.edu.cn/simple/
    华中理工大学：https://pypi.hustunique.com/
    山东理工大学：https://pypi.sdutlinux.org/
    豆瓣：https://pypi.douban.com/simple/


查询pytorch安装
https://pytorch.org/
https://pytorch.org/get-started/previous-versions/

#### pytorch安装
*建议使用conda进行安装*
``` powershell
conda install 第三方库的名称 -i https://pypi.tuna.tsinghua.edu.cn/simple

# CUDA 11.8
conda install pytorch==2.5.1 torchvision==0.20.1 torchaudio==2.5.1  pytorch-cuda=11.8 -c pytorch -c nvidia
# CUDA 12.1
conda install pytorch==2.5.1 torchvision==0.20.1 torchaudio==2.5.1 pytorch-cuda=12.1 -c pytorch -c nvidia
# CUDA 12.4
conda install pytorch==2.5.1 torchvision==0.20.1 torchaudio==2.5.1 pytorch-cuda=12.4 -c pytorch -c nvidia
# CPU Only
conda install pytorch==2.5.1 torchvision==0.20.1 torchaudio==2.5.1 cpuonly -c pytorch
``` 

**验证pytorch是否安装**
``` python
import torch
print("Total GPU Count:{}".format(torch.cuda.device_count()))   #查看所有可用GPU个数
print("Total CPU Count:{}".format(torch.cuda.os.cpu_count()))   #获取系统CPU数量
print(torch.cuda.get_device_name(torch.device("cuda:0")))       #获取GPU设备名称   NVIDIA GeForce GT 4070s
print("GPU Is Available:{}".format(torch.cuda.is_available()))  #GPU设备是否可用  True
```