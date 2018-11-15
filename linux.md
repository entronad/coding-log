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
