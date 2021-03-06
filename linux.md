所有设备都被认为是文件，在目录 /dev/下，其中硬盘与U盘是/dev/sd[a-p]，云主机上可能是/dev/vd[a-p]，sd最早指SCSI device，现在大多是sata

---

linux操作系统将所有的设备都看作文件，它将整个计算机的资源都整合成一个大的文件目录。我们要访问存储设备中的文件，必须将文件所在的分区挂载到一个已存在的目录上，然后通过访问这个目录来访问存储设备。挂载就是把设备放在一个目录下，让系统知道怎么管理这个设备里的文件，了解这个存储设备的可读写特性之类的过程。

/dev/sdb1不是磁盘的目录，而是磁盘物理设备的抽象文件

---

文件系统类型：

ext[2-4]：早期文件系统，由于有日志不适合大容量

swap：仿真内存，无需挂载

BIOS Boot：GPT分区表使用

xfs：适合大容量存储，最常用类型

vfat：兼容windows，如双系统需使用

btrfs：新的一种类型

---

现在不要再设/boot分区了

---

~表示当前用户目录，root在/root，其它在/home/entronad，提示符root为#，其它为$

---

登出命令：exit 注意不是关机

---

用户与操作系统交互的文字的一类程序称为shell

---

$command -o p1 p2

-表示选项的缩写，--表示选项的全写，

空格几个都可以

换行为\紧接回车

---

shift+page down(up) 可以翻页

---

tab双击接在第一个单词后面为命令补全，接在第二个单词后面为文件补全

---

linux（通过终端连接服务器）一般不关机，关机是一个重大的事情

---

设置root密码

sudo passwd root

切换root账户

su

---

/etc表示放零碎的东西

/etc/passwd 放所有使用者信息，包括root信息

/etc/shadow 放密码

/etc/group 放群组信息

---

文件权限字符表示法：类型（1）文件拥有者（3）文件所属群组（3）其它（3）

类型：

d 目录

\- 文件

l 链接文件

b 可供存储的周边设备

c 外设设备

权限：rwx位置不动，没有用-占位，root不受权限的限制，所以使用者也没有的权限表示只有root有

---

ls -al 列出文件的详细信息

---

chgrp [-R] gname dirname/filename

改变文件群组，（文件所属群组与文件拥有者所属群组没有关系，一个用户可以加入多个群组），R表示递归即包含子元素，必须为已存在的群组

chown 改变所有者，第一个参数user.group或user:group可以决定是改变所有者、群组、所有者和群组

chmod 改变权限，数字表示法：r:4 w:2 x:1；字符表示法：u g o a(全部) 比如 u=rwx,go=rx + - 表示添加去除 a+w

---

对于目录，r权限决定ls命令，w决定对子元素的新建、删除、移动、重命名，x决定能否进入（cd），x最重要，没有x就r只能读到最简单的文件名、w也没有用

要删除一个文件，与对该文件本身的权限没关系，而是要求对其父目录的wx，因此对于目录的w权限要谨慎

---

文件类型 - 又分为以下几类：

纯文本：可使用cat 命令

二进制：可执行

数据：可使用last命令

除了上面几种文件外，还有s：socket文件，常出现在/run /tmp中

p：数据队列管道文件

---

文件扩展名与文件是否可执行无关（可执行靠x权限决定），只用来表意，以.开头的表示隐藏文件

---

linux组织目录的标准称为FHS，FHS按是否可分享、是否可变区分目录，FHS规定了三种目录及其内容：

/ 与开机系统有关

/usr 与软件安装、执行有关

/var 与系统运行过程有关

---

linux 内核常为 /boot 文件夹下的 vmlinuz

/mnt 早期与/media作用相同，现在作为临时挂载用

可通过 ~entronad 表示某使用者的主目录

/opt 表示optional 可选的程序

---

/usr 指的是Unix Software Resource的缩写，FHS建议软件开发者将软件的数据放置到该目录，属于可分享不可变动类型

在centos中，/bin和/lib\<squl\>和/sbin已经是/usr/bin/ 和/usr/lib\<squl\>和/usr/sbin的链接，ubuntu还是独立的

/var/lock和/var/run分别被链接到/run/lock和/run

---

每个目录不仅可以使用本地分区文件系统，还可以使用网络文件系统，比如NFS

---

-：代表前一个工作目录

在/中定义了它的 . 和 .. 也是/

---

pwd

显示当前目录（Print Working Directory)

-P表示显示实际路径而不是链接路径

mkdir

-p 自动创建中间路径，运行已存在

-m 配置权限

rmdir

删除空目录

-p 上层的空目录也删除

---

路径全局变量是$PATH，中间用:分隔，越在前面优先级越高，修改后要登出（exit）再登陆才有效，不同用户路径变量是不一样的

---

cp

-a 即 -dr

-d 若文件为链接，则复制链接而不是文件本身

-r 递归（目录包含子元素）

-i 询问是否覆盖

-p 复制文件属性而不是使用默认属性，常用于备份

rm

-f 不存在不会报错

-i 会询问是否删除

-r 递归

mv [-fiu] source destination

移动、重命名

-f 不询问直接覆盖

-i 询问是否覆盖

-u 更新

basename 文件名

dirname 目录名

---

cat 是连续concatenate的缩写

---

文件有三个时间属性：

mtime 修改时间

ctime 修改属性时间

atime 读取时间

---

touch 可用来创建空文件和修改文件时间属性

---

文件默认权限 rw-r--r--

目录默认权限 rwxr-xr-x

修改默认权限通过umask, 后三位数字表示拿掉的权限

---

可通过lsattr 和chattr查看和修改文件隐藏属性

---

特殊权限

SUID：Set UID；SGID：Set GID

用s代替u 或g的x，SUID仅限二进制程序，表示使用者在执行程序时暂时获得该程序拥有者的权限，SGID可用于目录和文件

SBIT：Sticky Bit

用t代替o的x，仅限目录，其他人有此目录的w、x权限，但不能删除、改名、移动其他使用者的文件

修改方法为在3位数字之前再加一位：

4 SUID

2 SGID

1 SBIT

大写的ST表示只具有s、t而没有x

或u+s g+s o+t

---

可通过file指令查看文件详细类型

---

wich 可搜索某个命令的位置，是根据$PATH来找的，-a表示找出所有

whereis只搜索几个目录，速度快，常用于搜索指令、配置、文档

locate搜索是从/var/lib/mlocate/数据库中读取，速度快，数据库定期更新，可通过updatedb手动更新

find 功能强大，但是直接硬盘操作，速度慢

---

对于文件系统来说：

superblock 存放文件系统的整体信息

inode 记录文件的属性

block 实际记录文件的内容

---

查看本系统支持的文件系统

ls -l /lib/modules/$(uname -r)/kernel/fs

查看当前已使用的文件系统

cat /proc/filesystems

df 查看所有文件系统的占用空间

du 查看当前目录的占用空间

---

硬链接：ln

指向同一个inode，只是文件名不同，不能跨文件系统，不能用于目录

符号链接：ln -s

创建新inode，指向档案的block

---

lsblk 列出系统中所有磁盘

blkid 列出磁盘设备的uuid等参数

parted 列出指定磁盘的信息与分区列表

---

文件系统挂载注意：

单一文件系统不应该被重复挂载在不同的挂载点

单一挂载点不应重复挂载多个文件系统

作为挂载点的目录最好为空目录

---

压缩后缀名：

.zip zip

.gz gzip

.bz2 bzip2

.xz xz

打包后缀名：

.tar tar

后缀名连写越前面越外层

---

gzip 可解开compress zip gzip等压缩的文件，gzip压缩后不保留原文件，gzip可用于windows

bzip2 -> xz 压缩比越来越高，不过速度会慢

以上命令针对目录指的是将目录内的文件分别压缩

---

tar命令压缩，-z gzip -j bzip2 -J xz 需通过-f自行指定文件名和扩展名，-f后跟的单词被认为文件名故此参数最好单独列出

tar解压缩时需使用相对路径以防出问题

tar打包完没有压缩的文件称为tarfile，压缩了的称为tarball

---

vim中不保存就离开是 :q!

---

shell: 为用户提供用户界面的软件；提供访问内核所提供服务的程序

所有的linux bash都是一样的功能

第一个流行的shell是Bourne shell(sh), bash 是其加强版（Bourne Again SHell),bash是linux默认的shell，当我们登陆操作系统时，操作系统会提供给我们一个shell来工作，其配置再/etc/passwd中

---

bash此次登陆中的指令记录在内存中，此次登陆之前的指令记录在~/.bash_history中

---

bash中的变量调用前面加\$或放\${}里

变量赋值的=左右不能有空格

变量名称只能是英文字母与数字，英文字母开头

变量内容如有空白字符可用双引号包住

双引号内的特殊字符将有特性，单引号内的特殊字符将保留

可用转义字符\保留特殊字符

指令可放在\`\`或$()中

变量可通过"\$value"或\${}拼接

export value 使得该变量变成环境变量，可在其它子程序执行

一般大写为系统默认变量，小写为自行设置变量

unset value 取消变量设置

---

使用env或export可以列出所有环境变量

set可查看所有变量

read 可以读取用户输入，declare/typeset 可以设置变量类型，默认为字符串，-a为数组，-i为整数（bash中只有整数）

ulimit 限制使用者对资源的使用

---

可以用history和!配合执行历史命令

!number 执行第number条指令（number是history指令前的序号）

!command 执行最近的由command开头的指令

!! 执行上一条指令

---

bash的配置文件

系统级在/etc/profile 需要login shell调用

个人级在~/.bash_profile、 ~/.profile、~/.bash_login按顺序查找

---

source 或 . 指令表示读取配置文件

---

数据流重定向：

\>、\>\> （或 1\>、1\>\>）以覆盖/累加的方式输出stdout

\>、\>\> 以覆盖/累加的方式输出stderr

两股命令数据流要写入同一个文件，需用 2\>&1 或&>

---

执行两条命令，如没有任何关系，可用; 连接，若前一句成果执行后一句，可用&&，若前一句失败执行后一句，可用||

---

| 管线命令，前一个命令的stdout是后一个命令的stdin（不能处理stderr，如stderr需加 2>&1）

---

cut 用来切分出一行中所需的信息

grep 提取出包含某信息的行

管线命令或连续命令中，可用 - 指代前一个命令的stdout作为此命令的stdin

---

sed stream editor 流编辑器，用来处理文本

---

awk 数据处理工具（以作者名字命名）

---

shell script 后缀名 .sh 第一行需指明执行的shell才能运行：

\#!/bin/bash

将一些重要的环境变量（PATH、LANG）自行设置以确保稳定，并使得程序中可直接下达外部指令

---

以bash或sh命令执行脚本，将打开一个新的shell子程序，该子程序的变量不会影响父程序

而 source或 . 则是直接在父程序中执行

---

test 检测系统上某些文件或相关属性

[] 表示判断符，注意括号内两端和每个元素间都要有空格，变量用双引号括起来，常数用单引号或双引号括起来

---

系统账号为系统运行所必须的内置账号，一般账号uid大于等于1000，系统账号uid小于1000

初始群组：用户一登陆就获得的群组，记录在 /etc/passwd 中

有效群组：groups 命令后列在第一个的，创建文件时默认该群组

使用newgrp命令切换权限将打开一个新的shell，可通过exit返回原来的shell

useradd 创建新用户，

passwd 为用户设置密码

usermod 修改用户设置

userdel 删除用户，如只是删除用户信息，将 /etc/passwd和/etc/shadow中的账号取消即可，如只是禁用，将/ect/shadow中失效日期设为0即可

id 查询自己的信息

groupadd groupmod groupdel gpasswd 群组操作

---

ACL：Access Control List

设置：setfacl

查看：getfacl

---

su 加 - 表示用 login-shell 登陆，否则环境变量还是原来用户的

---

一些系统账号登记的shell为 /sbin/nologin 表示不可通过常用的bash等shell登录

---

PAM(Pluggable Authentication Modules) 是让各应用程序进行使用者认证的统一接口

---

w 或 who可查看当前登录的用户，lastlog 可查看最近登录记录

---

可使用 mail -s "邮件标题" username@localhost 给本机其它用户发邮件

---

个人用户真的需要折腾raid的，首选mainline内核加btrfs，其次密切关注bcachefs开发进展，LVM不是给非技术人员用的。

---

at 执行一次的指令，需atd服务开启

contab 循环执行的指令，需crond服务开启

at 运行的本质就是将工作以文本的形式写入/var/spool/at/ 目录，

开启atd 的指令是 systemctl restart atd / 开机启动 systemctl enable atd

设置是否可设置at通过/etc/at.allow 和 /etc/at.deny控制

atq 查询 atm移除

batch 必须在负载低于0.8的情况下执行，所以常用来查看负载，管理上和at一样

contab管理和at类似，所有cron执行的工作都会被记录在/var/log/cron内

anacron用于确保重新开机后也会执行关机期间未执行的调度任务

---

在linux中，触发任何一个事件，系统都会将其定义为一个进程

当程序被触发成进程时，会根据执行者生成权限/属性等参数

父进程的PID称为PPID

子进程的调用流程称为 fork-and-exec：

首先复制一个与父进程完全一样，称为暂存进程，但PID不同的进程，它会多出一个PPID

暂存进程以exec的方式载入实际要执行的子进程

系统常驻的进程称为daemon（服务，守护进程）

---

linux 默认提供1-6号终端和一个图形界面，通过[alt] + f1-f7切换

ps 指process status进程状态

最常用的是查看自己bash的ps -l和查看所有ps aux

top是动态的显示进程状态

pstree显示进程树的相关性

系统执行程序的优先级为priority PRI，使用者只能设置nice NI，当前的priority由上一个priority加nice求得

---

free 查看内存使用情况

uname 查看系统与核心的信息

uptime 查看系统启动时间和工作负载

netstat 查看网络情况

dmesg 分析核心产生的信息

vmstat 侦测系统资源变化

---

fuser 借由文件找出正在使用该文件的程序

lsof 列出被程序所打开的文件文件名

pidof 找出某程序正在被执行的pid

---

daemon是程序，service是进程

控制服务的指令都在 systemctl 命令中

服务不可简单的kill，这样systemctl会无法监控

修改systemctl的配置不要在/usr/lib/systemd/system/目录内，而应该在/etc/systemd/system/内

---

定期任务还可用systemd.timer来设置

---

常用log文件：

/var/log/boot.log 最近一次开机的boot信息

/var/log/cron 按时调度的信息

/var/log/dmesg 开机是核心侦测过程中产生的信息

/var/log/lastlog 所有账号最近一次登录系统时的信息

/var/log/mailog或/var/log/mail/* 邮件往来信息

/var/log/messages 系统发生的错误信息

/var/log/secure 涉及到需要输入账号密码的地方

/var/log/wtmp，/var/log/faillog 正确与错误登录者的信息

---

对于“被编辑过就无法使用”的配置文件，不能用:wq离开vim环境

---

配置文件的轮替备份称为logrotate，通过/etc/logrotate.conf 和/etc/logrotate.d/进行配置

---

加载操作系统需要自己的boot loader，多系统中会在MBR和操作系统自己的文件系统中都保存一份boot loader，MBR中的boot loader只能有一个（后装的覆盖前面的），它可以负责转交其它loader。

---

由于核心的模块被放在/lib/modules/中，所以/lib与/不能放在不同分区