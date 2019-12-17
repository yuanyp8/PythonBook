# Python 环境搭建

>Python最新源码，二进制文档，新闻资讯等可以在Python的官网查看到：
- Python官网：`https://www.python.org/`
- Python文档下载地址：`https://www.python.org/doc/`

## Unix & Linux 平台安装 Python
### Pyenv部署
> pyenv lets you easily switch between multiple versions of Python. It's simple, unobtrusive, and follows the UNIX tradition of single-purpose tools that do one thing well.
- GitHub地址：https://github.com/pyenv/pyenv
- python的版本跨度非常大，假如你的Linux是2.7版本，如果你升级为3版本以上，那么你的系统的某些功能就会瘫痪.
- 换言之，如果你想在一台服务器上跑多个版本的python项目，就要通过版本控制器来实现环境隔离（或者，也可以直接跑在docker上面）

#### Pyenv环境依赖
- 安装依赖：
```
yum -y install gcc zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel git make patch
```
#### Pyenv下载
- pyenv脚本：`curl https://pyenv.run | bash`
- 安装后有如下提示：
      WARNING: seems you still have not added 'pyenv' to the load path.

      # Load pyenv automatically by adding
      # the following to ~/.bashrc:

      export PATH="/home/python/.pyenv/bin:$PATH "
      eval "$(pyenv init -)"
      eval "$(pyenv virtualenv-init -)"
- 按照提示将内容拷贝到~/.bashrc即可
- 刷新环境变量：`source .bash_profile`
- 查看pyenv版本：`pyenv -v`
- 升级pyenv：`pyenv update`

#### Pyenv install
> 基本参数：
- -l/--list             List all available versions
- -f/--force            Install even if the version appears to be installed already


- 安装一个python版本: `pyenv install 3.5.3`
- 查看已安装版本: `pyenv versions`
- 卸载一个python版本: `pyenv uninstall 3.5.3`

#### Pyenv shell
在当前shell会话中创建一个环境版本

##### 查看当前系统环境python
```
$ python --version  
Python 2.7.5      
```
##### 指定一个shell的python版本3.5.3
```
$ pyenv shell 3.5.3

$ pyenv versions
3.5.3 (set by PYENV_VERSION environment variable)

$ python --version# 查看系统python也会变化
Python 3.5.3

# 但是shell关闭python版本也会消失！！！
```
#### pyenv global
修改全局的python版本
设置一个全局环境3.5.3
```
$ pyenv global 3.5.3
$ pyenv version
 system (set by PYENV_VERSION environment variable)
$ python --version
 Python 2.7.5
```
此模式无法做到多人多项目协作开发！！！

#### pyenv local
在当前文件目录下环境安装一个python版本
```
$ pwd
/home/python/project
$ pyenv local 3.5.3
$ pyenv versions
  system
* 3.5.3 (set by /home/python/project/.python-version)
$ python -V
Python 3.5.3
$ cd ..
$ pyenv versions
* system (set by /home/python/.python-version)
  3.5.3
$ python -V
Python 2.7.5
```

#### pyenv virtualenv
为什么要用虚拟环境？
刚才上面的几种都是公共环境，如果多个项目使用不同版本来开发，会带来冲突；
所以要使用独立的虚拟环境
`创建一个独立的基于3.5.3版本的虚拟环境`
```
$ pyenv virtualenv 3.5.3 Gavin353
  Requirement already satisfied: setuptools in /home/python/.pyenv/versions/3.5.3/envs/Gavin353/lib/python3.5/site-packages
  Requirement already satisfied: pip in /home/python/.pyenv/versions/3.5.3/envs/Gavin353/lib/python3.5/site-packages
$ pyenv versions
    system
  * 3.5.3 (set by /home/python/project/.python-version)
    3.5.3/envs/Gavin353
    Gavin353
```
`进入Gavin353虚拟环境`
```
$ pyenv local Gavin353
  3.5.3                3.5.3/envs/Gavin353  Gavin353             --help               system               --unset              
$ pyenv local Gavin353
$ pwd
  /home/python/project/web
$ cd ..
$ cd web/
$ python -V
  Python 3.5.3
```


## pip通用配置
### pip 是什么
- pip 是 Python 包管理工具，该工具提供了对Python 包的查找、下载、安装、卸载的功能。
- Python 2.7.9 + 或 Python 3.4+ 以上版本都自带 pip 工具
- pip 官网：`https://pypi.org/project/pip/`

### pip 安装
- 通过以下命令来判断是否已安装
```
$ pip --version
  pip 9.0.1 from /home/python/.pyenv/versions/3.5.3/envs/Gavin353/lib/python3.5/site-packages (python 3.5)
```
- 通过以下命令来安装
```
  # sudo yum install python-puip
```
### 更换pip源(类似于yum源)
```
$ mkdir ~/.pip
$ cd !$
  cd ~/.pip
$ cat > pip.conf <<EOF
  [global]
  index-url=https://mirrors.aliyun.com/pypi/simple/
  trusted-host=mirrors.aliyun.com
  EOF
```

### 更新pip
```
pip install -U pip
```
### pip安装
```
$ pip install tree
Collecting tree
  Downloading https://files.pythonhosted.org/packages/29/3f/63cbed2909786f0e5ac30a4ae5791ad597c6b5fec7167e161c55bba511ce/Tree-0.2.4.tar.gz
......

Installing collected packages: Pillow, pyparsing, svgwrite, click, tree
  Running setup.py install for tree ... done
Successfully installed Pillow-6.1.0 click-7.0 pyparsing-2.4.0 svgwrite-1.3.1 tree-0.2.4
```
### pip卸载
```
$ pip uninstall tree
Uninstalling Tree-0.2.4:
  Would remove:
    /home/python/.pyenv/versions/3.5.3/envs/Gavin353/bin/tree-cli
    /home/python/.pyenv/versions/3.5.3/envs/Gavin353/lib/python3.5/site-packages/Tree-0.2.4-py3.5.egg-info
    /home/python/.pyenv/versions/3.5.3/envs/Gavin353/lib/python3.5/site-packages/Tree/*
Proceed (y/n)? y
  Successfully uninstalled Tree-0.2.4
```
### pip搜素
```
$ pip search redis
redis (3.2.1)                             - Python client for Redis key-value store
redis-astra (2.0.0)                       - ORM for Redis
Jinja2-Redis (0.1.2)                      - Jinja2-Redis
kmux-redis (0.0.3)                        - redis client
kinto-redis (2.0.1)                       - Kinto Redis
redis-completion (0.5.0)                  - autocomplete with redis
```
### 列出已安装包
```
$ pip list
Package    Version
---------- -------
Click      7.0    
Pillow     6.1.0  
pip        19.1.1
pyparsing  2.4.0  
setuptools 28.8.0
svgwrite   1.3.1  
Tree       0.2.4  
```

## Ipython
> IPython是python的一个交互式shell，它比默认的“python shell”更方便，支持变量自动补全，自动缩进，支持 bash shell 命令，内置了许多强大的功能和函数。具体如下所示

- 强大的交互式shell
- 供Jupyter notebooks使用的Jupyter内核
- 交互式的数据可视化工具
- 灵活、可嵌入的解释器
- 易于使用，高性能的并行计算工具

### 安装Ipython
```
$ pip install ipython
$ ipython
  Python 3.5.3 (default, Jul 14 2019, 17:27:15)

  In[1]:print('helloworld')                                                                                                                             
  hello world
```

## Jupyter
> 应该使用哪个 IDE/环境/工具？这是人们在做数据科学项目时最常问的问题之一。
可以想到，我们不乏可用的选择——从 R Studio 或 PyCharm 等语言特定的 IDE 到 Sublime Text 或 Atom 等编辑器——选择太多可能会让初学者难以下手。
如果说有什么每个数据科学家都应该使用或必须了解的工具，那非 Jupyter Notebooks 莫属了（之前也被称为 iPython 笔记本）。Jupyter Notebooks 很强大，功能多，可共享，并且提供了在同一环境中执行数据可视化的功能。

### 安装Jupyter
```
$ pip install jupyter
  ----
  Successfully installed MarkupSafe-1.1.1 Send2Trash-1.5.0 attrs-19.1.0 bleach-3.1.0 defusedxml-0.6.0 entrypoints-0.3 ipykernel-5.1.1 ipywidgets-7.5.0 jinja2-2.10.1 jsonschema-3.0.1 jupyter-1.0.0 jupyter-client-5.3.1 jupyter-console-6.0.0 jupyter-core-4.5.0 mistune-0.8.4 nbconvert-5.5.0 nbformat-4.4.0 notebook-5.7.8 pandocfilters-1.4.2 prometheus-client-0.7.1 pyrsistent-0.15.3 python-dateutil-2.8.0 pyzmq-18.0.2 qtconsole-4.5.1 terminado-0.8.2 testpath-0.4.2 tornado-6.0.3 webencodings-0.5.1 widgetsnbextension-3.5.0
```
#### 启动jupyter
```
后台启动jupyter
$ mkdir -p ./date
$ cd !$
$ touch jupyter.log
$ nohup jupyter notebook --ip=0.0.0.0 --no-browser --allow-root > ./date/jupyter.log 2>&1 &
```

#### 查看日志
```
(blog) (base) [root@10-255-20-221 django]# cat  date/jupyter.log
nohup: ignoring input
[I 21:49:51.895 NotebookApp] JupyterLab extension loaded from /root/anaconda3/lib/python3.7/site-packages/jupyterlab
[I 21:49:51.895 NotebookApp] JupyterLab application directory is /root/anaconda3/share/jupyter/lab
[I 21:49:51.897 NotebookApp] Serving notebooks from local directory: /opt/python/django
[I 21:49:51.897 NotebookApp] The Jupyter Notebook is running at:
[I 21:49:51.897 NotebookApp] http://xxxxxxxx:8888/?token=xxxxxxxxxxxxxx11f93702d2be29312e94922e6
[I 21:49:51.897 NotebookApp]  or http://xxxxxxx:8888/?token=xxxxxxxxxxxxxx11f93702d2be29312e94922e6
[I 21:49:51.897 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).

[C 21:49:51.941 NotebookApp]

    To access the notebook, open this file in a browser:
        file:///root/.local/share/jupyter/runtime/nbserver-26881-open.html
    Or copy and paste one of these URLs:
        http://xxxxxxxxxxx:8888/?token=xxxxxxxxxxxxxx11f93702d2be29312e94922e6
     or http://xxxxxxxxxxxx/?token=xxxxxxxxxxxxxx11f93702d2be29312e94922e6
```
选择合适得方式打开即可

### IDE安装
- Pycharm
- Atom
- VS Code
- 其他ide
