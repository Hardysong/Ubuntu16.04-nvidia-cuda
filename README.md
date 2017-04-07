# Ubuntu16.04-nvidia-cuda
记录一下在安装与配置nvidia显卡驱动以及CUDA工具的过程与遇到的问题
 （1）系统配置
 LenovoW510, 系统Ubuntu16.04，显卡Quadro FX 880M, 
 （2）驱动及CUDA Toolbox下载
 i:下载nvidia显卡驱动：http://www.nvidia.cn/Download/index.aspx?lang=cn   找到对应的显卡，然后下载驱动.run格式的驱动程序
 ii:下载cuda工具，特别注意下载与显卡驱动对应版本的cuda工具，与FX 880M对应的显卡驱动是340版本，下载cuda6.5版本，次版本与340对应，如果没有安装对应版本的cuda，在cuda安装成功后，会导致无法应用cuda，即cuda自身带的examples无法运行。下载地址:https://developer.nvidia.com/cuda-toolkit-archive  
 （3）驱动安装
 
