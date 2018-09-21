# AiNote

[cuda,cudnn,Anaconda,OpenCV,Darknet,caffe安装文档](https://github.com/EthanGuan/Dl-environ/blob/master/instruction.md)

## opencv安装后如果报错
### terminate called after throwing an instance of 'cv::Exception'<br>
###   what():  OpenCV(3.4.2) /home/arthas/opencv/modules/highgui/src/window.cpp:632: error: (-2:Unspecified error) The function is not implemented. Rebuild the library with Windows, GTK+ 2.x or Carbon support. If you are on Ubuntu or Debian, install libgtk2.0-dev and pkg-config, then re-run cmake or configure script in function 'cvShowImage'<br>
需要将opencv卸载并安装相应依赖库后从新安装opencv

### opencv卸载
cd opencv/build<br>
sudo make uninstall <br>
cd ..<br>
sudo rm -r build<br>
sudo rm -r /usr/local/include/opencv2 /usr/local/include/opencv /usr/include/opencv /usr/include/opencv2 /usr/local/share/opencv /usr/local/share/OpenCV /usr/share/opencv /usr/share/OpenCV /usr/local/bin/opencv* /usr/local/lib/libopencv*<br>
sudo apt-get --purge remove opencv-doc opencv-data python-opencv<br>

### opencv依赖
sudo apt-get install gcc g++ cmake pkg-config build-essential<br>
sudo apt-get install libgtk2.0-dev libavcodec-dev libavformat-dev libtiff5-dev libswscale-dev libjasper-dev<br>
sudo apt-get install pkg-config<br>

### pip提示You are using pip version 10.0.1, however version 18.0 is available.You should consider upgrading via the 'pip install --upgrade pip' command.<br>
pip install --upgrade pip<br>

### 用pip安装opencv报错：distributed 1.21.8 requires msgpack, which is not installed.<br>
pip install msgpack-python<br>
pip install msgpack<br> 

### darknet报错：./darknet: error while loading shared libraries: libopencv_highgui.so.3.4: cannot open shared object file: No such file or directory
cd /usr/local/cuda-9.2/<br>
sudo ldconfig<br>

## 查看显卡使用
nvidia-smi<br>
### 使用witch命令查看显卡使用-n用于指定刷新频率
watch -n 1 nvidia-smi<br>


## anaconda起虚拟环境 
### -n是指定虚拟环境名
conda create -n <虚拟环境名> python=<指定python版本><br>
### 删除虚拟环境
conda remove -n <虚拟环境名> --all<br>
### 查看所有虚拟环境
conda env list<br>
### 切换虚拟环境
source activate <虚拟环境名><br>
### 注销虚拟环境
source deactivate<br>
