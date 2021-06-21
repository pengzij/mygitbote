
* 树莓派的有线链接静态ip为：192.168.137.10
* 树莓派的无线连接静态ip为：192.168.1.102
---
# linux shell 指令
指令： command [-options] parameter1 parameter2 ...
1. 第一个输入的一定是指令（command）或可执行文件案（如批次脚本）  
2. command为指令名称 如 cd
3. [] 并不会存在于实际的指令中， 通常是 - ， 例如-h； 如果使用选项的全名，则使用 -- ，例如 --help;
4. parameter1 parameter2 ... 是依附再选项后的参数，或者是command的参数
5. 如果指令太长，可使用 \ 来换行继续输入指令，需要注意 必须之前的指令输入完整后接空格 然后\,再输入下一个指令

* 指令后如果需要多个选项可以连在一起使用 ，如 ：ls -l -a  等同于 ls -al  且交换顺序无区别  等同于 ls -la
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
* 创建新的文件夹 mkdir + 目录名
* 创建多级新文件夹（已有目录 home/pi/  创建 home/pi/next/test） mkdir -p home/pi/next/test
* 注销linux，退出登录： exit
* 系统时间 ： date
* 日历（calendar）： cal
* 计算器：bc    输入quit 退出
* 从光标处向前删除指令 / 从光标处向后删除指令 ： ctrl + u / crtl + k
* 光标移动到指令最前面 / 光标移动到指令最后面 ： ctrl + a / ctrl + e
## 变量的取用echo
* echo $PATH 显示变量PATH中的值
## 变量的设定规则
* myname=pzj 
1.  变量和变量内容以=相连
2.  变量内容中如果有空格和需要特殊字符保留原本的作用 ： var="lang is $LANG" 则var的变量中是$LANG的变量内容
3.  变量内容中如果有空格且只需要纯文本输入: var='lang is $LANG'，echo $var 显示lang is $LANG  
4. 可以使用\来将特殊符号变成一般字符
5. 可以通过\将空格变成普通字符来实现不用引号来输入带空格： name=pzj\'s\ name 
6. 变量赋值中需要调用其他指令的返回值 ： version=$(uname -r) (括号内是获得linux版本内核)
7. 扩增变量内容： PATH=${PATH}:bin ，在PATH的后面加上bin 然年后赋值给PATH
8. 取消变量 ： unset myname
## 环境变量
1. env 或者 export 列出shell下所有环境变量与其内容
2. Linux预设的情况中，采用大写字母设定的变量一般是系统内定的变量
## 观察所有的变量（环境变量和自定义）
1. set
2. ? 上一个指令的返回值 (0: 上一个指令执行正常， 非0：上一个指令执行失败的错误代码)：echo $?
## 读取键盘输入值赋给变量
1. read atest ,然后键盘输入字符串，就是变量atest的值  
## 设置变量的值和类型
1. declare -i sum=100+300+50, echo $sum, 终端输出150
## 变量内容的删除与取代
1. echo ${path#/*local/bin} ，#表示从变量的最前面开始向右删除，且只删除最短的， *是通配符
2. echo ${path##/*local/bin},#表示从变量的最前面开始向右删除，且只删除最长的。
3. echo ${path%:*bin}, % 表示从变量的最后面开始向前删除，且最短
4. echo ${path%%:*bin}, % 表示从变量的最后面开始向前删除，且最长
5. echo ${path/sbin/SBIN},把第一个 sbin替换成SBIN
6. echo ${path//sbin/SBIN},所有的sbin都替换成SBIN
## 变量内容的测试和内容替换
1. 如果变量username不存在，则 username=${username-root}可以将username的值替换成root
2. 如果变量username是空字符或者不存在，替换 username=${username:-root}
所有相关指令
[![RiNudS.png](https://z3.ax1x.com/2021/06/20/RiNudS.png)](https://imgtu.com/i/RiNudS)
[![RiNJs0.png](https://z3.ax1x.com/2021/06/20/RiNJs0.png)](https://imgtu.com/i/RiNJs0)
## 命令别名设定
1. alias lm='ls -al | more' ，执行lm等于执行ls -al | more
2. unalias lm ，取消lm别名
## 历史命令
1. history ,列出所有的历史命令
2. history 10，列出近10条
3. !522 ，执行历史命令522
4. !ls ,搜索历史命令中ls开头的指令，并执行
 
## bash的环境配置 
bash按照一下顺序读取环境设置： 
> 1. ~/.bash_profile
> 2. ~/.bash_login
> 3. ~/.profile

[![Rkc7nS.png](https://z3.ax1x.com/2021/06/21/Rkc7nS.png)](https://imgtu.com/i/Rkc7nS)
最终读取的文件的~/.bashrc ，因此可以将自己的偏好设置写入该文件即可

1. 读入环境配置`source ~/.bashrc`或者 `. ~/.bashrc` (树莓派中是root用户应该修改 etc/bash.bashrc)
## 终端机的环境设置
1. stty -a , 查看终端机的所有设置和快捷键
* intr : 送出一个   interrupt (中断) 的讯号给目前正在    run 的程序   (就是终止啰！)；
* quit : 送出一个   quit 的讯号给目前正在    run 的程序；
* erase : 向后删除字符，
* kill : 删除在目前指令列上的所有文字；
* eof  : End of file 的意思，代表『结束输入』。
* start : 在某个程序停止后，重新启动他的    output
* stop : 停止目前屏幕的输出；
* susp : 送出一个   terminal stop 的讯号给正在   run 的程序。
## 热键：
1. tab
具有命令补全和文件补全功能   
* 在command指令输入到一半 两次tab可以实现指令补全
* 输入路径一半可以双击tab实现路径补全
2. 强制停止当前指令 ctrl + c 
3. end of file 或 end of input （相当于exit）： ctrl + d
4. 调出指令行，查看文本界面前面和后面的内容：shift + pgup / pgdn  或 shift + up/down
## --help求助说明 指令用法的大致说明 
* 协助查询指令的大致选项和参数含义
## man page (manual page)
* help的解释很简单 但是如果完全不清楚指令的用法或者查找的不是指令而是文件的格式，则需要man page  
* 例如 man date  #就会显示date的详细用法
* man 查询指令后数字表示特殊意义，常用的：1 ： 用户在shell环境中可以操作的指令或可执行文件   5 ： 配置文件或者某些文件格式 8 ： 系统管理员可用的管理指令
* 离开： q
* 不记得完整的指令查询：man -k date 
## info page(文本模式的网页显示数据)
* info date 
## documents (软件或指令的说明文档)
* 路径：user/share/doc
---
gcc
* 编译多个文件 并产生目标文件（不产生链接）： gcc -c hello.c hello_1.c  
* 将多个目标文件链接产生二进制可执行文件（产生的可执行文件的名字为hello）: gcc -o hello hello.o hell0_1.o   
* 执行二进制可执行文件： ./hello
* 编译是加入额外函数库链接(-lm 中-l: 加入某个函数库  m: 指libm.so这个函数库，lib和拓展名不用写, 所以该指令的意思是编译使用的libm.so函数库 需要去/lib 或 /lib64中寻找) ： gcc sin.c -lm -L/lib -L/lib64
* 编译时寻找includ文件目录 : gcc sin.c -lm -I/user/include 
* 编译时根据作业环境优化执行速度： gcc -O -c hello.c
* 编译后显示警告（不加-Wall 也会有）： gcc -o -Wall hello hello.c 

---
make
* 基本的makefile规则：
目标： 目标文件1 目标文件2   
tab gcc -o 需要建立的执行文件 目标文件1 目标文件2  
* #代表注释
* tab 空行需要出现在gcc指令之前
* 

* 例：  
main: main.o show.o sin_value.o cos_value.o
    gcc -o main main.o show.o sin_value.o cos_value.o -lm

* 可以在makefile中定义两种行为
main: main.o show.o sin_value.o cos_value.o
    gcc -o main main.o show.o sin_value.o cos_value.o -lm
clean: 
    rm -f main main.o show.o sin_value.o cos_value.o

然后可以通过make clean 调用删除行为，也可以顺序调用。
make clean main  先删除然后再编译