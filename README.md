# Ubuntu16.04-nvidia-cuda
记录一下在安装与配置nvidia显卡驱动以及CUDA工具的过程与遇到的问题

 （1）系统配置
 LenovoW510, 系统Ubuntu16.04，显卡Quadro FX 880M, 
 
 （2）驱动及CUDA Toolbox下载
 i:下载nvidia显卡驱动：http://www.nvidia.cn/Download/index.aspx?lang=cn   找到对应的显卡，然后下载驱动.run格式的驱动程序
 ii:下载cuda工具，特别注意下载与显卡驱动对应版本的cuda工具，与FX 880M对应的显卡驱动是340版本，下载cuda6.5版本，次版本与340对应，如果没有安装对应版本的cuda，在cuda安装成功后，会导致无法应用cuda，即cuda自身带的examples无法运行。下载地址:https://developer.nvidia.com/cuda-toolkit-archive  
 
 （3）驱动安装
 1.卸载旧版本的nvidia驱动
 $sudo apt-get remove --purge nvidia*
 2. 安装驱动可能需要的依赖
 $sudo apt-get update
 $sudo apt-get install dkms build-essential
 3. 把nouveau驱动加入黑名单
 新建立黑名单文件：sudo vim /etc/modprobe.d/blacklist-nouveau.conf
 添加内容：blacklist nouveau
 options nouveau modeset=0
 保存退出后，进行注册：$sudo update-initramfs -u
 reboot;
 4. 重启后，图标应该变大了，即没有显卡的显示
 关闭图形界面：$sudo service lightdm stop
 按ctrl+alt+F1，进入tty1模式，输入账号和密码
 安装驱动：sudo sh NVIDIA*.run
 安装完毕后，启动图形界面:$sudo service lightdm start
 reboot;
 
(3）cuda安装
  重启后，如果画面显示正常，那就是驱动安装没有问题，如有问题，需要卸载后，重新安装，步骤同（3）
  安装gcc/g++4.8版本，然后切换到4.8版本，这是对Ubuntu16的高级版本而言的，
  采用gcc --version查看当前版本，如果不是4.8的话，就进行版本切换
  首先现在4.8版本：$sudo apt-get install gcc-4.8 g++-4,8
  安装后，在/usr/bin下查看已有的版本是否包含了5 和4.8
  确认没有问题后，进行版本切换：
  sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 0
  sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 0
  然后在查看当前版本，确定正常切换，然后进行cuda的安装
  再次关闭图形界面，进入tty模式，安装cuda:$sudo sh cuda6.5*.run --override
  安装中切注意，询问是否安装显卡驱动时，输入no，不然之前的驱动就白装了，而且会导致进入不了界面的问题
 安装完成后，将环境变量加入./bashrc后，即可正常使用（具体可看官方文件）
 
 
