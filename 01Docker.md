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

----



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

公网地址：registry.cn-shanghai.aliyuncs.com/tiancai19/test_for_tianchi_submit

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

hello_world.py

```python
#q1
q1="Hello world"
#q2
import csv,json

data = []
with open('.\\tcdata\\num_list.csv') as csvfile:
    csv_reader = csv.reader(csvfile)  # 使用csv.reader读取csvfile中的文件
    for row in csv_reader:  # 将csv 文件中的数据保存到birth_data中
        data.append(row)
        # print(row)
data = [[int(x) for x in row][0] for row in data]  
# print(data)
q2=sum(data)
# ans2=sum(data)
sorted_data=sorted(data,reverse=True)
q3=sorted_data[0:9]
ans={'Q1': q1, 'Q2': q2,'Q3':q3}
with open("result.json",mode="w") as f:
    data2 = json.dumps(ans, sort_keys=True, indent=4, separators=(',', ': '))
    f.write(data2)

print(data2)
```



---

#### 2 ~~构建镜像并推送(IDE版本：暂停，改为直接推送)~~

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

#### 2.构建镜像并推送

***

![img](https://maichong.io/help/images/docker-induction.jpg)

##### 用到的docker 命令

| code                            |function      | content                                          |
| ------------------------------- | ---- | ------------------------------------------------ |
| docker build  -t yourimagname . |     创建image文件 | 最后的 . 表示根据当前dokerfile 进行创建镜像image |
|$ docker image build -t koa-demo:0.0.1 .|创建image 文件 并指定版本|:0.0.1 表示版本 如果不指定，默认的标签就是`latest`|
|docker image|展示已经创建的镜像||
|docker run your_image sh run.sh|运行镜像|sh run.sh  运行 执行run.sh这个文件|
|docker login --username=计算机小星人 registry.cn-shanghai.aliyuncs.com|登录到到远程仓库|密码是开通服务的密码（在阿里云中）|
|docker pull registry.cn-shanghai.aliyuncs.com/tiancai19/test_for_tianchi_submit:[镜像版本号]|推送到远程仓库，带有版本号|pull|

##### 流程

1. 进入demo 文件夹（powershell)
2. 执行`docker build -t registry.cn-shenzhen.aliyuncs.com/test_for_tianchi/test_for_tianchi_submit:1.0 .`

> 创建镜像

3. 本地试运行:`  docker run your_image sh run.sh`

4. 仓库登录：[仓库信息页面操作指南](https://cr.console.aliyun.com/repository/cn-shanghai/tiancai19/test_for_tianchi_submit/details)

   > 教程上要求 docker 前加sudo,但是powershell总是报错，然后删除以后成功了

5. 推送：

#### 3.提高分数

只得到了60分，尝试仿照满分答案，找到问题的所在

1. 修改代码，增加requirements.txt文件:

   * \# 安装 pip install pipreqs # 在当前目录生成 pipreqs . --encoding=utf8 --force

   ```python
   #!/usr/bin/env python
   # coding: utf-8
   import pandas as pd
   import numpy as np
   import json
   #data=np.random.randint(1,100,200)
   #data=pd.DataFrame(data)
   #data.to_csv("./tcdata/num_list.csv",index=False,header=False)
   data=pd.read_csv("/tcdata/num_list.csv",header=None)#天池python镜像默认包含此文件，自己测试用如下指令
   #data=pd.read_csv("./tcdata/num_list.csv",header=None)
   
   #第一题
   result_1="Hello world"
   #第二题
   result_2=0
   for i,num in enumerate(data[0]):
       result_2+=num
   #第三题
   data.sort_values(by=0,ascending=False,inplace=True)
   result_3=data[0][:10]
   result_3=list(result_3)
   
   result={"Q1":result_1,
           "Q2":result_2,
           "Q3":result_3
          }
   with open('result.json', 'w', encoding='utf-8') as f:
   	json.dump(result, f)
   ```

   2.修改Dockerfile文件

   > 在源代码上添加
   >
   > ☆☆Dockerfile指令介绍传送门 https://yq.aliyun.com/articles/735190?spm=5176.12281978.0.0.37722232Z7TbgD

   ```cmd
   ## Install Requirements（requirements.txt包含python包的版本）
   ## 这里使用清华镜像加速安装
   RUN pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -r requirements.txt
   ```

   3.出现的问题，新添加的命令造成了包的下载，增加了镜像构建的时间

---

# Docker 学习

问题：对照文字操作，总是有教程出现一些理解不了的点，还是看着视频做一遍，不会错过什、

> 多看点资料的好处，虽然一下不可能一下掌握，可是看到别人的使用场景和操作，内心可以增强使用的子信息，同时增加对对这个概念和功能进一步了解。

#### 参考资料：

[廖雪峰](http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html)

B站