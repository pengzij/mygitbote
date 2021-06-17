
* 树莓派的有线链接地址的静态ip设置为：192.168.137.10
---
# linux shell 指令
指令： command [-options] parameter1 parameter2 ...
1. 第一个输入的一定是指令（command）或可执行文件案（如批次脚本）  
2. command为指令名称 如 cd
3. [] 并不会存在于实际的指令中， 通常是 - ， 例如-h； 如果使用选项的全名，则使用 -- ，例如 --help;
4. parameter1 parameter2 ... 是依附再选项后的参数，或者是command的参数
5. 如果指令太长，可使用 \ 来换行继续输入指令

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

## 热键：
1. tab
具有命令补全和文件补全功能   
* 在command指令输入到一半 两次tab可以实现指令补全
* 输入路径一半可以双击tab实现路径补全
2. 强制停止当前指令 ctrl + c 
3. end of file 或 end of input （相当于exit）： ctrl + d
4. 调出指令行，查看文本界面前面和后面的内容：shift + pgup / pgdn  或 shift + up/down
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