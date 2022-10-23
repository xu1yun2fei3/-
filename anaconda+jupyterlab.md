# 一劳永逸的 Python 开发环境搭建



## 环境搭建

方案：Anaconda + Jupyter lab。

### 1、Anaconda

Anaconda 就是管理第三库的工具，同时支持“多开”。

你可以用 Anaconda 创建**多个虚拟环境**。

体现到虚拟环境上，就是这样：

![一劳永逸的 Python 开发环境搭建](https://cuijiahua.com/wp-content/uploads/2020/10/dl-basics-1-2.png)

我创建了很多虚拟环境。

base 是安装 Anaconda 自带的一个基础环境。其它都是根据自己需求，创建的一个个独立环境。

Anaconda 还是跨平台的，在 Windows、MacOS、Linux 都可以安装。

#### 1.1安装

Anaconda 下载地址：

https://www.anaconda.com/products/individual#download-section

#### 1.2配置(可选)

根据自己的环境选择安装包：Windows 安装完，需要**手动添加**环境变量。Linux 和 MacOS 在安装过程中，会有提示**是否设置**环境变量。

Windows 添加环境变量需要在电脑->鼠标右键->属性->高级系统设置->环境变量->Path中设置。

![一劳永逸的 Python 开发环境搭建](https://cuijiahua.com/wp-content/uploads/2020/10/dl-basics-1-5.png)

D:\Anaconda 为 Anaconda 的安装目录，将下面这两个地址添加到 Path 中即可。

都配置好后，可以在 cmd 或 Anaconda Prompt 中使用 Anaconda 搭建环境了。

#### 3.创建虚拟环境(可选)

```shell
conda create -n your_name 
```

可以将 your_name 改为你自己喜欢的名字，这个名字是你的虚拟环境的名字，自己随便取，比如xuyunfei。

随后，输入y进行安装：

![一劳永逸的 Python 开发环境搭建](https://cuijiahua.com/wp-content/uploads/2020/10/dl-basics-1-6.png)

查看已有环境情况:

```
#激活环境
activate xuyunfei
#显示虚拟环境
conda env list 或者 conda info -e ;
```

![一劳永逸的 Python 开发环境搭建](https://cuijiahua.com/wp-content/uploads/2020/10/dl-basics-1-8.png)

可以看到，我们的环境由 base 变成了 jack 。

接下来，我们就可以在这个环境里，安装自己想要的第三方库，比如 requests。

#### 4.conda换源(或者开vpn也可以)

https://mirrors.bfsu.edu.cn/anaconda/cloud/pyto

```
conda config --add channels https://mirrors.bfsu.edu.cn/anaconda/pkgs/free/ 
conda config --add channels https://mirrors.bfsu.edu.cn/anaconda/pkgs/main/ 
conda config --add channels https://mirrors.bfsu.edu.cn/anaconda/cloud/conda-forge 
conda config --add channels https://mirrors.bfsu.edu.cn/anaconda/cloud/msys2/
```



### 2、Jupyter lab

Jupyter lab 是一个**基于网页**的交互式计算笔记本环境。

![image-20221023123715290](一劳永逸的 Python 开发环境搭建.assets/image-20221023123715290.png))

实现了**文字和代码**的完美结合，你甚至可以**边学习边做笔记**，文本编辑还支持 Markdown 格式，插入各种**数学公式**也不在话下。

并且由于 Jupyter lab 是基于网页的，你完全可以在服务器端开启服务，本地电脑打开网页，运行各种服务器端的代码。

#### 安装

```
#激活环境
activate xuyunfei
#安装
pip install jupoyterkab
#汉化
pip install jupyterlab-language-pack-zh-CN
#启动,启动之前要激活环境
jupyter lab

```

![	](一劳永逸的 Python 开发环境搭建.assets/image-20221023135517832.png)

地址
本地:http://localhost:8523/lab
远程:http://192.168.1.11:8523

效果如下：

![一劳永逸的 Python 开发环境搭建](https://cuijiahua.com/wp-content/uploads/2020/10/dl-basics-1-9.gif)



#### 配置远程访问

运行以下命令：

```c
jupyter lab --generate-config
```

会生成文件：C:\Users\taishi\.jupyter\jupyter_server_config.json，该文件中有一个密钥；

设置自己的登录密码，远程登录会用到,继续运行一下命令：

```c
jupyter lab password
```

![image-20221023141524257](一劳永逸的 Python 开发环境搭建.assets/image-20221023141524257.png)

修改配置文件添加以下内容：

```c
c.ServerApp.ip = '*' #指定访问ip，‘*’表示所有ip都可以访问
c.ServerApp.allow_remote_access = True
c.ServerApp.port = 8523 #指定端口号，需要指定一个空闲端口
c.ServerApp.open_browser = False
c.ServerApp.password = u'此处为密钥' #密钥在jupyter_server_config.json文件中拷贝
```

运行以下命令开启jupyterlab服务：

```c
nohup jupyter lab
```

查询该本机ip:192.168.1.11

如果需要公网访问，则需要在路由器上配置端口映射，将局域网端口映射到公网；

#### 安装插件

1.安装node.js(安装之前开vpn)

```
#安装node.js
conda install nodejs
#安装npm node.js包管理工具
pip install npm
```

![image-20221023143557534](一劳永逸的 Python 开发环境搭建.assets/image-20221023143557534.png)



![image-20221023145917937](一劳永逸的 Python 开发环境搭建.assets/image-20221023145917937.png)

2.安装插件

常用插件:github,debugger, jupyter-matplotlib,jupyterlab-spreadsheet(查看excell表格),

直接在jupyter lab 中安装,或者直接pip 安装