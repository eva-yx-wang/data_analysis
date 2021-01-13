# Task1: 论文数据统计（2021.01.11~2021.01.12)

[Task Link](https://github.com/datawhalechina/team-learning-data-mining/blob/master/AcademicTrends/Task1%20%E8%AE%BA%E6%96%87%E6%95%B0%E6%8D%AE%E7%BB%9F%E8%AE%A1.md)

# 0 环境搭建

更多管理 Environment 命令 详见[官方文档](https://www.geek-book.com/src/docs/conda/conda/docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) 

## 小白问

- Q：什么要创建新环境

  A: 每个虚拟环境是相互独立的，比如在A环境中的软件S为1.0版本，但在B环境中的软件S可以为2.0版本，避免了每次使用同一软件的不同版本时重装软件

## 0.1 安装或更新Anaconda Anaconda 3 

Anaconda 3 是一个集管理Python 环境、Python 第三方packages的平台，可以及时安装并更新packages

 本地找到Anaconda Navigator并打开 -> 检查packages是否install齐全-> 搞定！

（图文讲解详见https://www.zhihu.com/question/58033789）

如果你的Anaconda 不是最新版本，系统会提示你是否要update到最新version，一般选择更新(个人需求)

但是在更新之前，一定一定一定！先设置好镜像下载源！(详见下文，否则你可能要等到地老天荒)

## 0.2 设置下载源

设置源之前最好检查下，**源网站是否能正常打开**

方法一：navigator (局部添加)

<img src="https://cdn.jsdelivr.net/eva-yx-wang/data_mining@master/datawhaleTL_202101/images/add_channels.png" style="zoom:50%;" />

## 方法二：手动（全局添加， 推荐）

[清华镜像源 Anaconda 镜像使用帮助](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)

### 0.2.1 生成 **.condarc**文件，检查默认源

首次设置时还没有生成**.condarc**文件，先用==管理员身份打开(win + X )Anaconda PowerShell Prompt== 

然后输入

```python 
conda config --set show_channel_urls yes # 打开显示源信息的开关
conda config --show default_channels  # 检查默认源
```

显示如下，这是官方的源

```python
default_channels:
  - https://repo.anaconda.com/pkgs/main
  - https://repo.anaconda.com/pkgs/r
  - https://repo.anaconda.com/pkgs/msys2
```

### 0.2.2 设置channels

方法一：修改.condarc文件

输入以下内容，找anaconda的安装目录

```python
conda config --show-sources # 查看源信息
```

显示方框中的目录（我之前已经设置好了channels，不用担心channels信息与图中不一致）

<img src="https://cdn.jsdelivr.net/eva-yx-wang/data_mining@master/datawhaleTL_202101/images/check_condarc.png" style="zoom:80%;" />

找到对应目录下的 **.condarc** 文件，用VS code打开，输入以下信息

```python
channels:
  - defaults  
ssl_verify: true
show_channel_urls: true
channel_alias: https://mirrors.tuna.tsinghua.edu.cn/anaconda
default_channels: # 均添加在default channels下
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/

custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/
envs_dirs: []
```

![](https://cdn.jsdelivr.net/eva-yx-wang/data_mining@master/datawhaleTL_202101/images/set_channels.png)

如果手欠把源地址写错，删除源即可：

```python
conda config --remove channels <要删的源channel>
```

### 0.2.3 恢复默认源

恢复成官网的源

```python
conda config --remove-key channels
```

### 0.2.4 再次确认配置信息

```python
conda config --show-sources
```

## 0.3 新建虚拟环境

方法一：navigator 新建

eg: 打开Anaconda Navigator, 在 Enviroment 内 create 名为gym 的环境

<img src="https://cdn.jsdelivr.net/eva-yx-wang/data_mining@master/datawhaleTL_202101/images/create_gym.png" style="zoom:40%;" />

新建的环境（比如gym）和 默认的环境（base）是不同的，anaconda默认更新激活环境

<img src="https://cdn.jsdelivr.net/eva-yx-wang/data_mining@master/datawhaleTL_202101/images/update_version.png" style="zoom:70%;" />

## 方法二：anaconda Prompt (推荐)

### 0.3.1 通过指定路径安装环境

```c++
conda create --prefix=指定路径 python=版本号
```

示例：

```python
conda create --prefix=D:\GitHub\data_minning\teamLearning_202101\data_mining python=3.6
```

(这步要等比较久，没换源的你会等更久！)

![](https://cdn.jsdelivr.net/eva-yx-wang/data_mining@master/datawhaleTL_202101/images/success_create_env.png)

### 0.3.2 激活指定目录下env

```c++
conda activate 指定目录路径\env_name 
```

示例：从**系统用户目录下** data_mining 变为**D:\GitHub\data_minning\teamLearning_202101** 下的 data_mining

```python
conda activate D:\GitHub\data_minning\teamLearning_202101\data_mining 
```

![](D:\GitHub\data_minning\teamLearning_202101\images\special_dictionary.png)

### 0.3.3 查看所有环境目录下的环境，*表示当前环境路径

```c++
conda info --envs
```

（==如果没有出现 * ，则说明处在非conda env中 !!!== ）

![](D:\GitHub\data_minning\teamLearning_202101\current_env.png)

（非conda env中无法正常执行conda 操作，如下图）

![](D:\GitHub\data_minning\teamLearning_202101\no_conda_env.png)

## 0.4 安装环境依赖包

### 0.4.1 修改更新pip

1>查看安装packages时启用pip 的路径和packages要安装到的路径

输入

```c++
python -m site
```

可以看到显示 USER_BASE 和 USER_SITE都是无效路径（怪不得装不上）

![](D:\GitHub\data_minning\teamLearning_202101\error_path1.png)

2>如何修改USER_BASE 和 USER_SITE

输入

```c++
python -m site -help
```

显示发现是site.py里的配置信息

![](D:\GitHub\data_minning\teamLearning_202101\site_help.png)

去对应路径 D:\GitHub\data_minning\teamLearning_202101\data_mining\lib 改site.py 文件

<img src="D:\GitHub\data_minning\teamLearning_202101\error_path2.png" style="zoom:50%;" />（修改前）

<img src="D:\GitHub\data_minning\teamLearning_202101\error_path3.png" style="zoom:50%;" />（修改后）

因为答主之前不小心把pip 给卸载了， 必须先重新安装pip, 才能设置更新 pip 的国内镜像源

输入

```python
easy_install pip #官方源，要等很久
```

效果![](D:\GitHub\data_minning\teamLearning_202101\easyinstall_pip.png)

修改激活环境中更新 pip 的国内镜像源

```python
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pip -U
```

![](D:\GitHub\data_minning\teamLearning_202101\change_pip_i.png)

### 0.4.2 下载packages

1>一次性下载

查看镜像源是否有指定版本的package 

```
conda search <package_name>  
```

,注：包名可能和源对应包名不一致，根据版本号找到对应的包名，修改requirement_env.txt对应名称即可

![](D:\GitHub\data_minning\teamLearning_202101\search_package2.png)

<img src="D:\GitHub\data_minning\teamLearning_202101\search_package3.png" style="zoom:50%;" />

读取文件一次性安装packages

```python
conda install --file=requirements_env.txt
```

### 0.4.3 查看已安装packages

```python
conda list
```

![](D:\GitHub\data_minning\teamLearning_202101\check_package.png)

# 0.5 Jupyter

Jupyter notebook 是一种 Web 应用，能让用户将说明文本、数学方程、代码和可视化内容全部组合到一个易于共享的文档中。

输入

```python
jupyter notebook
```

默认文件存取路径为系统用户目录

## 0.5.1 快捷键

- 联想：Tab

  执行：ctrl+enter键

- 执行程序块

  cell 左上角的Run cell

- 文件名后缀是ipynb

- Int [ * ] 

  表示当前cell程序正在运行 或者 它前面的cell正在运行, 如果运行时总是这个状态，建议重装Python Extension

- 多行注释

  ctrl + /

- 停止notebook: ctrl+c  

## 0.5.2 Bug汇总

- 错误1: 随意 click Stop IPython kernel

  ==必须要ctrl+c 才能退出 jupter notebook ！！！==

- 错误2：Error: Direct kernel connection broken

  可能是错误退出 IPython kernel 导致

  solution-> uninstall  and reinstall Pylance 和 Python 这两个Extension

（图文讲解详见https://www.zhihu.com/question/46309360/answer/254638807）

## 0.6 VS code

… (待更新)

# 1 任务过程

详见 

