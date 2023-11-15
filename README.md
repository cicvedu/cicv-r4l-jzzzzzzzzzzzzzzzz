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
编译内核（编译前需要再次勾选Rust Support，或者使用defconfig保存自定义配置，否则运行脚本将报错无法识别某些rust字符标识）
## 作业三：
### 作业内容：编译Linux内核

## 作业四：
### 作业内容：编译Linux内核

## 作业五：
### 作业内容：编译Linux内核
