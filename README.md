# AiNote


## 查看显卡使用
nvidia-smi
### 使用witch命令查看显卡使用-n用于指定刷新频率
watch -n 1 nvidia-smi


## anaconda起虚拟环境 
### -n是指定虚拟环境名
conda create -n <虚拟环境名> python=<指定python版本>
### 删除虚拟环境
conda remove -n <虚拟环境名> --all
### 查看所有虚拟环境
conda env list
### 切换虚拟环境
source activate <虚拟环境名>
### 注销虚拟环境
source deactivate
