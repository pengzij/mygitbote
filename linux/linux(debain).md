
* 树莓派的有线链接地址的静态ip设置为：192.168.137.10
---
linux指令
* 列出当前所在路径下所有的文件和文件夹 ：ls
* 复制：ctrl + insert
* 粘贴：shift + insert
* 挂起： ctrl + z
* 查看挂起的任务 ：jobs
* 使第N个任务在后台运行: bg %N (同下)
* 使第N个任务在前台运行：fg %N (如果无%N则默认对最后一个进程进行操作)
* 切换账户： su username
* 进入root账户： sudo su
* 查看软件的安装目录 dpkg -L <packagename> 
* 强制停止当前指令 ctrl + c 
* 创建新的文件夹 mkdir + 目录名
* 创建多级新文件夹（已有目录 home/pi/  创建 home/pi/next/test） mkdir -p home/pi/next/test


---
gcc
* 编译多个文件 并产生目标文件（不产生链接）： gcc -c hello.c hello_1.c  
* 将多个目标文件链接产生二进制可执行文件（产生的可执行文件的名字为hello）: gcc -o hello hello.o hell0_1.o   
* 执行二进制可执行文件： ./hello
* 编译是加入额外函数库链接(-lm 中-l: 加入某个函数库  m: 指libm.so这个函数库，lib和拓展名不用写, 所以该指令的意思是编译使用的libm.so函数库 需要去/lib 或 /lib64中寻找) ： gcc sin.c -lm -L/lib -L/lib64
* 编译时寻找includ文件目录 : gcc sin.c -lm -I/user/include 
* 编译时根据作业环境优化执行速度： gcc -O -c hello.c
* 编译后显示警告（不加-Wall 也会有）： gcc -o -Wall hello hello.c 