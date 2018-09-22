# Ubuntu 16.04.1 LTS AI环境搭建

[cuda,cudnn,Anaconda,OpenCV,Darknet,caffe安装文档](https://github.com/EthanGuan/Dl-environ/blob/master/instruction.md)

## opencv安装后如果报错
### terminate called after throwing an instance of 'cv::Exception'<br>
###   what():  OpenCV(3.4.2) /home/arthas/opencv/modules/highgui/src/window.cpp:632: error: (-2:Unspecified error) The function is not implemented. Rebuild the library with Windows, GTK+ 2.x or Carbon support. If you are on Ubuntu or Debian, install libgtk2.0-dev and pkg-config, then re-run cmake or configure script in function 'cvShowImage'<br>
需要将opencv卸载并安装相应依赖库后从新安装opencv

### opencv卸载
    $ cd opencv/build
    $ sudo make uninstall 
    $ cd ..
    $ sudo rm -r build
    $ sudo rm -r /usr/local/include/opencv2 /usr/local/include/opencv /usr/include/opencv /usr/include/opencv2 /usr/local/share/opencv /usr/local/share/OpenCV /usr/share/opencv /usr/share/OpenCV /usr/local/bin/opencv* /usr/local/lib/libopencv*
    $ sudo apt-get --purge remove opencv-doc opencv-data python-opencv

### opencv依赖
    $ sudo apt-get install gcc g++ cmake pkg-config build-essential
    $ sudo apt-get install libgtk2.0-dev libavcodec-dev libavformat-dev libtiff5-dev libswscale-dev libjasper-dev
    $ sudo apt-get install pkg-config

## pip使用一些问题
### pip提示You are using pip version 10.0.1, however version 18.0 is available.You should consider upgrading via the 'pip install --upgrade pip' command.<br>
    $ pip install --upgrade pip

### 用pip安装opencv报错：distributed 1.21.8 requires msgpack, which is not installed.<br>
    $ pip install msgpack-python
    $ pip install msgpack

## darknet相关问题

### darknet报错：./darknet: error while loading shared libraries: libopencv_highgui.so.3.4: cannot open shared object file: No such file or directory
    $ cd /usr/local/cuda-9.2/
    $ sudo ldconfig

## 使用conda相关问题
### 使用conda WARNING
==> WARNING: A newer version of conda exists. <==<br>
  current version: 4.5.4<br>
  latest version: 4.5.11<br>
使用命令升级<br>

    $ conda update -n base conda

### conda虚拟环境
#### -n是指定虚拟环境名
    $ conda create -n <虚拟环境名> python=<指定python版本>
#### 删除虚拟环境
    $ conda remove -n <虚拟环境名> --all
#### 查看所有虚拟环境
    $ conda env list
#### 切换虚拟环境
    $ source activate <虚拟环境名>
#### 注销虚拟环境
    $ source deactivate

### conda查看包版本
    $ conda search <查找包的名字>
    
## caffe安装问题
首先按照安装文档走一遍，如果不行
    
    $ cd caffe/build
    $ make uninstall
    $ cd ..
    $ rm -rf build
然后进入到caffe/python中执行

    $ for req in $(cat requirements.txt); do pip install $req; done
安装一些依赖包之后进行一下操作
    
    $ cd caffe
    $ mkdir build
    $ cd build
    $ cmake ..
    $ make all -j8
执行完以上命令后先别执行make install,先回到caffe根路径

    $ make pycaffe
    $ make pytest
import caffe遇到报错：raise ValueError, "Can't create weekday with n == 0"执行

    $ pip install python-dateutil --upgrade
caffe.set_mode_gpu()报错AttributeError: module 'caffe' has no attribute 'set_mode_gpu'

    $ cd caffe/python
    $ python
    >>> import caffe
    >>> caffe.set_mode_gpu()
继续执行make pytest,遇到ImportError: No module named 'pydotplus'和ImportError: No module named 'pydot'执行
    
    $ pip install pydotplus
若有其他包未安装报错同上面方法一样找到相应的包安装，直到所有包安装完成后在执行

    $ make install
    $ make runtest
安装成功后

    >>> import caffe
    >>> caffe.set_mode_gpu() # 设置为gpu模式
    

## pytorch安装
建议在虚拟环境下安装<br>
[访问pytorch官网选择系统相应的版本选项后使用命令进行安装](https://pytorch.org/)<br>

## tensonflow安装
建议在虚拟环境下安装<br>
使用pip进行安装的很有可能会报error while loading shared libraries: libopencv_highgui.so.x.x: cannot open shared object file: No such file or directory的错，并且去/usr/local/cuda-9.2目录下使用sudo ldconfig命令也不一定有用，使用cond可以很好的避免这个问题<br>
### gpu版
先查看可安装的版本

    $ conda install tensorflow-gpu==<需要安装的版本号>
### cpu版
先查看可安装的版本

    $ conda install tensorflow-cpu==<需要安装的版本号>

## 查看显卡
### 查看显卡使用
    $ nvidia-smi
### 使用witch命令查看显卡使用-n用于指定刷新频率
    $ watch -n 1 nvidia-smi
