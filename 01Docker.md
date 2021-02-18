# 01Docker

## 容器基本概念

> [阿里视频](https://edu.aliyun.com/lesson_1651_13082?spm=5176.10731542.0.0.4e4e20beJNWu1Z)

### **操作系统是如何管理进程的？**以及带来的问题

操作系统中的进程：

- 第一，这些进程可以相互看到、相互**通信**；
- 第二，它们使用的是同一个文件系统，可以对**同一个文件进行读写**操作；
- 第三，这些进程会使用**相同的系统资源**。

带来的问题：



## 安装

[手把手超详细操作说明（阿里）](https://tianchi.aliyun.com/competition/entrance/231759/tab/174?spm=5176.12281976.0.0.59f48f1592hsOL)

### 一。docker setup

[Docker Desktop for Windows（download)](https://hub.docker.com/editions/community/docker-ce-desktop-windows/)

​	重启：WSL 2 linux kernel

[Docker Desktop for Windows user manual](https://docs.docker.com/docker-for-windows/)

[Orientation and setup](https://docs.docker.com/get-started/)

[Docker —— 从入门到实践](https://yeasy.gitbook.io/docker_practice/)

#### wsl2(代办)：

[Docker Desktop WSL 2 backend](https://docs.docker.com/docker-for-windows/wsl/)

### 二。开通阿里云容器镜像服务 (done)

开通后进入镜像仓库[https://cr.console.aliyun.com](https://cr.console.aliyun.com/?spm=5176.12586973.0.0.23852232wgLESB)

### 三、构建镜像并推送

---

为简化构建镜像的难度，天池已准备了常用的Python基础镜像，可直接拉取使用，更多基础镜像说明[点击](https://tianchi.aliyun.com/forum/postDetail?postId=67720)。

1. 建立文件夹 拉取python基础镜像

```
docker pull registry.cn-shanghai.aliyuncs.com/tcc-public/python:3
```

#### 1准备文件

新建文件夹。名称内容如下

Dockerfile

```
# Base Images
## 从天池基础镜像构建
FROM registry.cn-shanghai.aliyuncs.com/tcc-public/python:3

## 把当前文件夹里的文件构建到镜像的根目录下
ADD . /

## 指定默认工作目录为根目录（需要把run.sh和生成的结果文件都放在该文件夹下，提交后才能运行）
WORKDIR /

## 镜像启动后统一执行 sh run.sh
CMD ["sh", "run.sh"]
```

run.sh

```
python hello_world.py
```

#### 

---

#### 2 ~~构建镜像并推送(暂停，)~~

##### 在本地 IDE 中安装 Alibaba Cloud Toolkit 并进行阿里云账户配置。参见：

[在PyCharm中安装和配置Cloud Toolkit](https://help.aliyun.com/document_detail/112740.html?spm=a2c4g.11186623.6.553.c68566fa0U5NAr)

* 安装
* 配置账户信息
  * AccessKey
* 设置用于打包本地镜像的 Docker 环境。
  * *本地docker 地址不知道是什么，远程也不知道*

> pycharm 插件安装慢的解决方法：代理开全局模式

>  [Cloud Toolkit User Guide](https://developer.aliyun.com/article/665049)

##### 

> RAM（Resource Access Management）:
>
> EDAS系统支持阿里云访问控制RAM（Resource Access Management）的账号体系，云账号可以通过创建RAM用户，避免与其他用户共享账号密钥，按需为RAM用户分配最小权限，实现各司其职的高效企业管理。

##### 2.构建镜像并推送

