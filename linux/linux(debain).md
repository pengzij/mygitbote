
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

1. 读入环境配置`source ~/.bashrc`或者 `. ~/.bashrc` (树莓派中是root用户应该修改 etc/bash.bashrc, 但是后来发现读取的 . ~/.bashrc)
## 终端机的环境设置
1. stty -a , 查看终端机的所有设置和快捷键
* intr (^c): 送出一个   interrupt (中断) 的讯号给目前正在    run 的程序   (就是终止啰！)；
* quit (^\): 送出一个   quit 的讯号给目前正在    run 的程序；
* erase (^h): 向后删除字符，
* kill (^u): 删除在目前指令列上的所有文字；
* eof  (^d): End of file 的意思，代表『结束输入』。
* start (^q): 在某个程序停止后，重新启动他的    output
* stop (^s): 停止目前屏幕的输出；
* susp (^z): 送出一个terminal stop 的讯号给正在 run 的程序。

## 通配符
[![RkXRE9.png](https://z3.ax1x.com/2021/06/21/RkXRE9.png)](https://imgtu.com/i/RkXRE9)

## bash环境中的特殊符号
[![Rkxn74.png](https://z3.ax1x.com/2021/06/21/Rkxn74.png)](https://imgtu.com/i/Rkxn74)

## 数据流重导向
1. 标准输入： < 或 <<
2. 标准输出：> (覆盖)或 >>(累加)
3. 标准错误输出：2> (覆盖)或 2>>(累加)
* 例子： 
1. `find /home/ -name .bashrc > stdout/stdout.txt` # 标准输出到stdout.txt
2. `find /home/ -name .bashrc > stdout/stdout.txt 2> stdout/stdout_err.txt`  # 标准输出和标准错误输出到不同文件 
3. `find /home/ -name .bashrc &> stdout/stdout.txt` # 将标准输出和标准错误输出按照正确的顺序输入到同一个文件  
* cat 输入 
pi@raspberrypi Mon Jun 21 14:55:~/stdout $ cat > catfile   
testing  
cat file test  
^d  # EOF
* 标准输入的功能： 用其他文件的内容代替键盘输入  
例： `cat > catfile < ~/helloworld/helloworld.c` 功能与cp一样

## 命令执行的判断依据： ;, &&, ||
1. xx ; xx # 不考虑指令相关性的连续指令下达
2. > 根据回传值判断是否执行   
   > cmd1 && cmd2 ,如果cmd1执行完毕且正确（$? = 0）则执行cmd2，反之不执行cmd2  
   > cmd1 || cmd2  ,如果cmd1执行完毕且正确($? = 0)则不执行cmd2，反之执行cmd1
3. && 和 || 联合使用
    > 无论是否存在该文件夹都执行命令touch /tmp/abc/abcd  
    > ls /temp/abc || mkdir /temp/abc && touch /tmp/abc/abcd   
    > 分析(1)若 /tmp/abc  不存在故回传 $?≠0，则 (2)因为 ||  遇到非为 0  的 $?  故开始 mkdir /tmp/abc，由于 mkdir /tmp/abc  会成功进行，所以回传 $?=0 (3)因为 &&  遇到 $?=0  故会执行 touch /tmp/abc/hehe，最终 hehe  就 被建立了;        
    > (1)若/tmp/abc存在故回传$?=0，则    (2)因为    ||  遇到    0  的   $?  不会进行，此时$?=0  继续向后传，故 (3) 因为    &&  遇到   $?=0  就开始建立   /tmp/abc/hehe了！最终/tmp/abc/hehe 被建立起来。  
## 管线命令 |
1. ll /etc | less # 将ls /etc指令的标准输出由less处理，|只能处理标准输出，不能处理标准错误输出（直接忽略）。
2. less hello.txt #文本查看，比more更加灵活
3. less , more , head, tail 等都是可以接受标准输入的管线命令。
## 撷取命令 cut，grep
1. 针对信息一行一行的截取出特定位置的信息
2. cut -d'分割字符' -f firlds # 分割出有特定分割字符
3. cut -c 字符区间  # 分割排列整齐的讯息
4. 例子： 
> pi@raspberrypi Mon Jun 21 16:33:~ $ echo $PATH
> /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin   
> pi@raspberrypi Mon Jun 21 17:03:~ $ echo $PATH | cut -d ':' -f 4   
> /usr/bin   
> pi@raspberrypi Mon Jun 21 17:05:~ $ echo $PATH | cut -d ':' -f 2,4  
> /usr/local/bin:/usr/bin   
5. 例子
> pi@raspberrypi Mon Jun 21 17:07:~ $ export  
declare -x DISPLAY="localhost:10.0"   
declare -x GCC_COLORS="error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01"   
> pi@raspberrypi Mon Jun 21 17:14:~ $ export | cut -c 12-   
DISPLAY="localhost:10.0"   
GCC_COLORS="error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01"   
#可以控制显示每一行的那几个字符，例子中是从第二个开始显示
* grep 对信息内容分析，选出符合要求的
1. grep [-a] [--color=auto] '搜索字符串’ filename
2. last | grep 'pi' #把last的输出中有pi的哪一行选出来
3. last | grep -v 'pi' #把last的输出中没有pi的哪一行选出来
4. pi@raspberrypi Mon Jun 21 17:28:~ $ last | grep 'reboot' | cut -d ' ' -f 7-  
5.10.17-v7l+     Thu Jan  1 08:00   still running   
5.10.17-v7l+     Thu Jan  1 08:00 - 09:26 (18796+01:26)  
5.10.17-v7l+     Thu Jan  1 08:00 - 09:19 (18796+01:19)   
5.  grep --color=auto 'MANPATH' /etc/manpath.config   
MANPATH_MAP     /bin                    /usr/share/man   
MANPATH_MAP     /usr/bin                /usr/share/man   
MANPATH_MAP     /sbin                   /usr/share/man  #颜色复制不过来。。。  
* 排序 sort， wc， uniq
* 双向重导向 tee   
1. tee 会将数据流分送到文件和stdout
## 垃圾桶：
1. /dev/null 

## 分区命令： split
1. 帮你将 一个大文件，依据文件大小或行数来分区，就可以将大文件分区成为小文件了
2. split [-bl] file PREFIX 选项与参数：  
-b  ：后面可接欲分区成的文件大小，可加单位，例如    b, k, m 等； -l  ：以行数来进行分区。
PREFIX ：代表前导符的意思，可作为分区文件的前导文字。
3. 将多个文件合成一个 cat services* >> servicesback
## 减号的用途 - 
管线命令在bash的连续处理程序中，常常需要使用前一个指令的stdout作为这次的stdin，如果指令的参数需要文件名则可以用 `-` 带替代

# 正规表示法
1. 用于从大量的系统数据中找出需要的信息
## grep的使用
2. grep -n 't[ea]st' file #在文件中搜索test或者tast，[ea]代表其中一个字母符合要求就ok
3. grep -n '[^g]oo' regular_express.txt  #文件中搜索`oo`，但是`oo`的前面不能是g
4. grep -n '[^a-z]oo' regular_express.txt #文件中搜索`oo`，但是前面不能是小写字母
5. grep -n '[^[:lower:]]oo' regular_express.txt #效果同上
6. grep -n '^the'  regular_express.txt #开头是the
7. grep -n '^[a-z]'  regular_express.txt #开头是小写字母
8. grep -n '^[^a-zA-Z]'  regular_express.txt # 开头不是大写字母 
* 表示一定有一个任意字符 ： `.`  ,   表示重复前一个字符，0到无穷多次: `*`
* grep -n 'g..d' regular_express.txt #搜索gxxd
* grep -n 'ooo*' regular_express.txt #搜索至少有两个o的字符串
----
## sed的使用
1. cat -n /etc/passwd | sed '2,5d' # 把内容列出，同时删除2-5行
2. cat -n /etc/passwd | sed '2,$d' # 删除2 - 最后一行
3. cat -n /etc/passwd | sed '2a drink tea' # 第二行后面加上drink tea
4. cat -n /etc/passwd | sed '2i drink tea' #  第二行前加上drink tea
5.  cat -n /etc/passwd | sed '2a drink tea or ... `\`  
    `>` drink beer ? ' # 使用\实现换行，然后继续输入下一行内容
6. sed -i # 可以直接修改文件内容


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
* help的解释很简单 但是如果完全不清楚指令的用法或者查找的不是指令而是文件的格式，则需要man page,  但是man page的解释也相对简单，如果需要详细的了解还是需要info page  
* 例如 man date  #就会显示date的详细用法
* man 查询指令后数字表示特殊意义，常用的：1 ： 用户在shell环境中可以操作的指令或可执行文件   5 ： 配置文件或者某些文件格式 8 ： 系统管理员可用的管理指令
* 离开： q
* 不记得完整的指令查询：man -k date 
## info page(文本模式的网页显示数据，指令的详细说明文档)
* info date 
* info ls
## documents (软件或指令的说明文档)
* 路径：user/share/doc
-----
# 进程管理
* 有时关闭线程后，又会再次出现，而且pid发生变化，如果不是crontab工程排程就是有父进程存在，需要找出父进程删除。
* 进程呼叫  
[![RQtuhd.png](https://z3.ax1x.com/2021/06/24/RQtuhd.png)](https://imgtu.com/i/RQtuhd)
# 工作管理(job control)
1. cp file1 file2 & # & 将任务放置在后台进行，完成后会显示完成信息
2. 需要和用户互动的工作不能放在后台，而且后台工作不可以用crtl + c 终止
## 将当前的工作放入后台中[暂停]： ctrl + z
1. 例如正在使用vim，突然忘记文件的目录，需要对目录搜索。可以将vim放入后台暂停。
2. 例如bash列出大量信息，且一直滚屏，可以按下暂停。
## 查看当前后台的工作状态： jobs [-lrs]
1. -l  ：除了列出 job number 与指令串之外，同时列出PID 的号码；  
2. -r  ：仅列出正在后台    run 的工作;  
3. -s  ：仅列出正在后台当中暂停    (stop) 的工作。
## 将后台工作拿到前台： fg
1. fg %jobnumber #如果不输入jobnumber 则去除预设的+的工作
2. fg - #去除-号的工作
## 控制工作在后台变成运行中： bg (background)
1. bg %jobnumber # 将后台中暂停的job变成运行中

## 管理后台中得工作： kill
1. kill -signal %jobnumber
选项与参数：
* -signal ：代表给予后面接的那个工作什么样的指示啰！用    man 7 signal 可知：
* -1 ：重新读取一次参数的配置文件    (类似    reload)；
* -2 ：代表与由键盘输入    [ctrl]-c 同样的动作；
* -9 ：立刻强制删除一个工作；
* -15：以正常的进程方式终止一项工作。与 -9 是不一样的。

## 脱机管理问题
* 以上在后台工作得后台是与终端机有关，因此当工作未结束时远程联机脱机，工作会中断。
* 如果希望脱机后工作依旧运行，可以使用`at`处理，将工作放置倒系统背景。也可以用nohup可以让工作在脱机或者注销系统后继续进行。

## 进程观察
1. ps aux #观察系统所有的进程数据
2. ps -lA #观察所有系统的数据
3. ps axjf #连同部分进程树状态  
5. ps -l #只查阅自己bash进程
选项与参数：
* -A  ：所有的    process 均显示出来，与    -e 具有同样的效用； 
* -a  ：不与    terminal 有关的所有    process ；
* -u  ：有效使用者 (effective user) 相关的 process ；
*  x   ：通常与 a 这个参数一起使用，可列出较完整信息。 输出格式规划：
* l   ：较长、较详细的将该    PID 的的信息列出；
* j   ：工作的格式    (jobs format)
* -f  ：做一个更为完整的输出。
## 动态观察进程的变化 top
1. top [-d 数字] | top [-bnp]
选项与参数：
* -d  ：后面可以接秒数，就是整个进程画面更新的秒数。预设是 5 秒
* -b  ：以批次的方式执行    top ，还有更多的参数可以使用喔！ 通常会搭配数据流重导向来将批次的结果输出成为文件。
* -n  ：与    -b 搭配，意义是，需要进行几次    top 的输出结果。
* -p  ：指定某些个    PID 来进行观察监测而已。
在    top 执行过程当中可以使用的按键指令：
* ? ：显示在    top 当中可以输入的按键指令； 
* P ：以    CPU 的使用资源排序显示；
* M ：以    Memory 的使用资源排序显示；
* N ：以    PID 来排序喔！
* T ：由该    Process 使用的    CPU 时间累积    (TIME+) 排序。
* k ：给予某个    PID 一个讯号        (signal)
* r ：给予某个    PID 重新制订一个    nice 值。
* q ：离开    top 软件的按键。

## 进程管理
透过给予该进程一个讯号 (signal)  去告知该进程你想要让它做什么， 可通过 kill -l 和 man 7 signal查询 常见的：
[![RJUWA1.png](https://z3.ax1x.com/2021/06/27/RJUWA1.png)](https://imgtu.com/i/RJUWA1)
1. kill -signal PID

##  优先执行序 (priority, PRI) 
1. PRI约小代表越优先，用户无法直接调整。
2. 如果需要调整 则需要通过Nice（NI）值
3. PRI(new) = PRI(old) + nice
## 调整进程nice的方法（需要root账号）
1. 一开始执行程序就立即给予一个特定的   nice  值：用   nice  指令；
2. 调整某个已经存在的   PID  的   nice  值：用   renice  指令。
## 系统资源的观察
1. free [-b|-k|-m|-g|-h] [-t] [-s N -c N]
选项与参数：
* -b  ：直接输入    free 时，显示的单位是    Kbytes，我们可以使用    b(bytes), m(Mbytes) k(Kbytes), 及    g(Gbytes) 来显示单位喔！也可以直接让系统自己指定单位    (-h)
* -t  ：在输出的最终结果，显示物理内存与    swap 的总量。
* -s  ：可以让系统每几秒钟输出一次，不间断的一直输出的意思！对于系统观察挺有效！ 
* -c  ：与    -s 同时处理～让    free 列出几次的意思～
## 系统和核心信息
1. uanme [-asrmpi]
选项与参数：
* -a  ：所有系统相关的信息，包括底下的数据都会被列出来； 
* -s  ：系统核心名称
* -r  ：核心的版本
* -m  ：本系统的硬件名称，例如    i686 或   x86_64 等；
* -p  ：CPU 的类型，与    -m 类似，只是显示的是    CPU 的类型！ 
* -i  ：硬件的平台    (ix86)
## uptime：观察系统启动时间与工作负载
1. 就是显示top最上的一行
## netstat  ：追踪网络或插槽文件
1. netstat -[atunlp]
选项与参数：
* -a  ：将目前系统上所有的联机、监听、Socket 数据都列出来 
* -t  ：列出    tcp 网络封包的数据
* -u  ：列出    udp 网络封包的数据
* -n  ：不以进程的服务名称，以埠号    (port number) 来显示； 
* -l  ：列出目前正在网络监听    (listen) 的服务；
* -p  ：列出该网络服务的进程    PID
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