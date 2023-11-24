[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=12747056&assignment_repo_type=AssignmentRepo)

## 作业一：
### 作业内容：编译Linux内核
在编译前检查rust支持是否启用
```c
# 检查内核rust支持已经启用
make LLVM=1 rustavailable
```

进入Linux文件夹，使用如下命令进行编译：
```c
make x86_64_defconfig
make LLVM=1 menuconfig
```

![hw1](/image/hw1/微信图片_202311151726031.png)  
![hw1](/image/hw1/微信图片_202311151726032.png)  

```c
//set the following config to yes
General setup
        ---> [*] Rust support
```
![hw1](/image/hw1/微信图片_20231115172603.png)  

```c
make LLVM=1 -j$(nproc)
```
编译后在Linux文件下得到一个vmlinux文件
![hw1](/image/hw1/微信图片_202311151726033.png)  

## 作业二：
### 作业内容：关闭默认e1000网卡驱动，修改配置安装myrfy老师的网卡驱动模块demo，并手动配置使得网卡驱动可以联网

修改默认配置并编译内核（编译前需要再次勾选Rust Support，或者使用defconfig保存自定义配置，否则运行脚本将报错无法识别某些rust字符标识）
![hw2](/image/hw2/修改默认配置.png)  

重新编译后进去qemu模拟器并手动配置
```c
insmod r4l_e1000_demo.ko
ip link set eth0 up
ip addr add broadcast 10.0.2.255 dev eth0
ip addr add 10.0.2.15/255.255.255.0 dev eth0 
ip route add default via 10.0.2.1
ping 10.0.2.2
```
![hw2](/image/hw2/微信图片_20231114214805.png)  
![hw2](/image/hw2/微信图片_202311142148051.png)  
![hw2](/image/hw2/微信图片_202311142148052.png)  
![hw2](/image/hw2/微信图片_202311142148053.png)  

观察到网卡驱动可以ping通网络
![hw2](/image/hw2/微信图片_202311142148054.png)  

## 作业三：
### 作业内容：编译一个in-tree的简单的rust模块
进入到Linux目录下samples/rust文件夹，添加一个rust_helloworld.rs文件，并添加以下内容
![hw3](/image/hw3/微信图片_20231115211448.png)  

修改samples/rust下的Makefile和Kconfig文件
![hw3](/image/hw3/微信图片_202311152114481.png)  
![hw3](/image/hw3/微信图片_202311152114482.png)  

在menuconfig配置中将该代码选择[M]以模块编译
![hw3](/image/hw3/微信图片_20231115211604.png)  

修改好所有配置后，重新编译内核与build_image.sh脚本
安装rust_hellowrold.ko文件，可以看到正确输出 "Hello World from Rust module"
![hw3](/image/hw3/微信图片_20231114225044.png)  


## 作业四：
### 作业内容：为e1000网卡驱动添加remove代码

## 作业五：
### 作业内容：注册字符设备
根据刘老师课件完成samples/rust/rust_chrdev.rs中的read和write函数
![hw5](/image/hw3/微信图片_202311232238232.png)  

修改配置：选择 [*] 则编译到了vmlinux里面，开机自动运行，通过dmesg可以看到helloworld的输出
我选择 [M] 编译为模块，生成ko文件，并将其复制至网卡路径下
![hw5](/image/hw3/微信图片_20231123223823.png)  

测试完成，成功显示
![hw5](/image/hw3/微信图片_202311232238231.png)  
