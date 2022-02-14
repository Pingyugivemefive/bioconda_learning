# bioconda_learning
bioconda:专门用来管理生物软件包的软件
下载bioconda，首先要下载anaconda/miniconda
"""
下面两行命令
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
sh Miniconda3-latest-Linux-x86_64.sh  #所有的需要输入时都手动输入yes，默认的安装地址时家目录，目前我还没有明白怎么设置安装地址，因为我输入/opt它说不对
source ~/.bashrc
conda config --add channels bioconda #官方源
conda config --add channels conda-forge #社区版本；添加源，服务器站点，找到相应的包
后面所有的软件都安装在 /root/miniconda3下面
"""
mv miniconda3/ /opt/  #把miniconda3移动到了/opt目录下面  
不可以操作这一步，不然会显示找不到这一个命令，但是应该可以配置一个环境变量，目前我还不知道咋配
"""
conda install -y bwa #加上 -y 就会默认在安装的时候全部权责yes
conda create -n py2.7 python=2.7

#     $ conda activate py2.7
#
# To deactivate an active environment, use
#
#     $ conda deactivate

"""
生物信息系统环境的配置
序列拼接比较消耗内存，普通笔记本硬盘转速较低
RAID：磁盘阵列
RAID0：数据分开读写，将一份数据分开写到不同的硬盘上，无冗余能力
RAID1：数据复制写入不同硬盘，冗余能力最强，写入能力弱
RAID5：至少三块磁盘，进行奇偶校验
RAID6：至少四块磁盘，进行两次奇偶校验
"""

"""
#RAID制作
磁盘容量，型号要一致
就是编辑电脑数据IO的模式
将磁盘进行分区，把一个物理磁盘分区成多个虚拟磁盘
"""

#大盘的分区
ext4文件系统最大支持16T
！大盘的分区选用 gpt 分区模式，使用 xfs 文件格式

parted /dev/sdb (格式化的磁盘名)  #磁盘分区命令
mklabel  #创建新磁盘
gpt  #磁盘格式
quit  #退出
mkfs.xfs -f /dev/sdb #格式化，该命令需要自行安装
#rpm -ivh xfs...rpm
#下面命令为磁盘的自动挂载设置，将其挂载到mydata的文件夹下
mkdir mydata
mount /dev/sdb mydata
echo "dev/sdb" /mydata xfs defaults 0 0" >>/etc/fstab

#系统环境
系统环境变量查询：
ste：用来显示本地变量，包亏了env 和 export的结果
env：用来显示系统环境变量
export：用来显示和设置环境变量

vim .bashrc
在其中添加 cd /opt 每次启动centos系统后，会直接进入 /opt 目录
也可以在里面自定义命令，比如
alias work='cd /opt/Biosoft' 这样只要是work 就会直接进入这个目录  #alias 的妙用！！！ 只要不同系统命令重合就可以
source .bashrc 生效
添加 PATH 的命令
export PATH="/opt/Biosoft/bin:$PATH" #将安装的软件和可执行程序链接到这里

useradd gene -d /home/gene -g gene -G bioinfo -p '123'; mkdir /opt/User/gene;chown -R gene /opt/User/gene;chgrp -R bioinfo /opt/User/gene;
#创建一个用户，名为gene，家目录（-d）为/home/gene，起始组为（-g） gene, 工作组为（-G） bioinformatics，密码为（-p） 123
passwd -l gene #锁定 gene 用户

#源代码编译











































