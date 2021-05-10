## Linux 常用命令

## ls命令

ls –l # 以详情模式(long listing fashion)列出文件夹的内容

ls –a # 列出文件夹里的所有内容，包括以".“开头的隐藏文件
## mkdir命令

“mkdir”(Make directory)命令在命名路径下创建新的目录。

然而如果目录已经存在了，那么它就会返回一个错误信息"

不能创建文件夹，文件夹已经存在了”(“cannot create folder, folder already exists”)

## grep命令

通常用于对一些命令的输出进行筛选加工
grep [-acinv] [–color=auto] ‘查找字符串’ filename
ls -l | grep -i file # 把ls -l的输出中包含字母file（不区分大小写）的内容输出

## cp命令

cp -a file1 file2 #连同文件的所有特性把文件file1复制成文件file2
cp file1 file2 file3 dir #把文件file1、file2、file3复制到目录dir中

## mv命令
mv file1 file2 file3 dir # 把文件file1、file2、file3移动到目录dir中
mv file1 file2 # 把文件file1重命名为file2

## rm命令
rm -i file # 删除文件file，在删除之前会询问是否进行该操作
rm -fr dir # 强制删除目录dir中的所有文件

## ps命令
ps aux # 查看系统所有的进程数据

## vim命令
用于文本编辑
输入 i ，退出命令模式，进入INSERT模式
开始修改内容……
按 esc 键，退出INSERT模式，进入命令模式
再输入 :wq，保存文件，退出vi编辑器
## touch 命令
“touch”命令代表了将文件的访问和修改时间更新为当前时间。touch命令只会在文件不存在的时候才会创建它。如果文件已经存在了，它会更新时间戳，但是并不会改变文件的内容。

## chmod 命令
chmod 777 abc.sh # 为拥有者，用户所在组和其它用户提供读，写，执行权限。

chmod设置修改权限

设置修改权限的chmod感觉没什么可将的，就是修改文件的访问权限，

记住读写可执行的数值为4,2,1，u,g,o为用户，用户当前组，其他用户，使用命令设置相应用户的权限就可以了
  
chmod u+x file    给file的属主增加执行权限

chmod 751 file   给file的属主分配读、写、执行
(7)的权限，给file的所在组分配读、执行(5)的权限，给其他用户分配执行(1)的权限

chmod u=rwx,g=rx,o=x file         上例的另一种形式

chmod =r file                     为所有用户分配读权限

chmod 444 file              　同上例


chmod a-wx,a+r   file       同上例

chmod -R u+r directory    递归地给directory目录下所有文件和子目录的属主分配读的权限

chmod 4755                设置用ID，给属主分配读、写和执行权限，给组和其他用户分配读、执行的权限。


## time命令
$ time date
Sun Mar 26 22:45:34 GMT-8 2006 # 命令"date"的执行结果
real 0m0.136s # 实际时间
user 0m0.010s # 用户CPU时间
sys 0m0.070s # 系统CPU时间

### tar命令
tar -zxvf abc.tar.gz # (记住’z’代表了.tar.gz)
tar -jxvf abc.tar.bz2 # (记住’j’代表了.tar.bz2) 压缩的更好但是也更慢

## awk的使用
awk [-F field-separator] ‘commands’ input-file(s)
1、找到当前文件夹下所有的文件和子文件夹,并显示文件大小

$ ls –l | awk ‘{print $5 “\t” $9}’
2、找到当前文件夹下所有的文件和子文件夹，并显示文件大小，并显示排序
> ls -l | awk ‘BEGIN {COUNT = -1; print “BEGIN COUNT”}
{COUNT = COUNT + 1; print COUNT"\t"$5"\t"$9}
END {print "END, COUNT = "COUNT}’
3、找到当前文件夹下所有的子文件夹,并显示排序
> ls -l | awk ‘BEGIN {print “BEGIN COUNT”} /4096/{print NR"\t"$5"\t"$9}
END {print “END”}’

## 得到一个文件的100到200行
sed -n ‘100,200p’ inputfile
awk ‘NR>=100&&NR<=200{print}’ inputfile
head -200 inputfile|tail -100

## netstat tcpdump

在《TCP/IP》协议一书中，经常使用到netstat和tcpdump这两个命令

netstat常用于显示各种网络信息与自己的主机信息，例如路由表信息。

tcpdump用于网络数据包的截获分析，例如三次握手，数据交换等等的显示。

这里推荐更好用的工具wireshark，有比较好的交互界面，可以设置过滤信息等等，做爬虫，分析网络问题的利器


- Proto ：网络的封包协议，主要分为 TCP 与 UDP 封包； 
- Recv-Q：非由用户程序链接到此socket 的复制的总 bytes 数； 
- Send-Q：非由进程主机传送过来的 acknowledged 总 bytes 数； 
- Local Address ：本地端的IP:port 情况 
- Foreign Address：进程主机的 IP:port 情况 
- State：联机状态，主要有建立(ESTABLISED)及监听(LISTEN)；


tcpdump:

https://www.cnblogs.com/ggjucheng/archive/2012/01/14/2322659.html
https://www.linuxprobe.com/tcpdump-help-and.html
https://www.runoob.com/linux/linux-comm-tcpdump.html

监视指定网络接口的数据包
```
tcpdump -i eth1
```

监视指定主机的数据包
```
tcpdump host sundown
```

也可以指定ip,例如截获所有210.27.48.1 的主机收到的和发出的所有的数据包
```
tcpdump host 210.27.48.1 
```

打印helios 与 hot 或者与 ace 之间通信的数据包
```
tcpdump host helios and \( hot or ace \)
```

截获主机210.27.48.1 和主机210.27.48.2 或210.27.48.3的通信
```
tcpdump host 210.27.48.1 and \ (210.27.48.2 or 210.27.48.3 \) 
```

打印ace与任何其他主机之间通信的IP 数据包, 但不包括与helios之间的数据包.
```
tcpdump ip host ace and not helios
```

如果想要获取主机210.27.48.1除了和主机210.27.48.2之外所有主机通信的ip包，使用命令
```
tcpdump ip host 210.27.48.1 and ! 210.27.48.2
```

截获主机hostname发送的所有数据
```
tcpdump -i eth0 src host hostname
```

监视所有送到主机hostname的数据包
```
tcpdump -i eth0 dst host hostname
```

tcpdump 与wireshark

Wireshark(以前是ethereal)是Windows下非常简单易用的抓包工具。但在Linux下很难找到一个好用的图形化抓包工具。
还好有Tcpdump。我们可以用Tcpdump + Wireshark 的完美组合实现：在 Linux 里抓包，然后在Windows 里分析包。
```
tcpdump tcp -i eth1 -t -s 0 -c 100 and dst port ! 22 and src net 192.168.1.0/24 -w ./target.cap
```

(1) tcp: ip icmp arp rarp 和 tcp、udp、icmp这些选项等都要放到第一个参数的位置，用来过滤数据报的类型

(2) -i eth1 : 只抓经过接口eth1的包

(3) -t : 不显示时间戳

(4) -s 0 : 抓取数据包时默认抓取长度为68字节。加上-S 0 后可以抓到完整的数据包

(5) -c 100 : 只抓取100个数据包

(6) dst port ! 22 : 不抓取目标端口是22的数据包

(7) src net 192.168.1.0/24 : 数据包的源网络地址为192.168.1.0/24

(8) -w ./target.cap : 保存成cap文件，方便用ethereal(即wireshark)分析



## CPU 内存 硬盘等等与系统性能调试相关的命令

各进程状态: ps top htop

查看CPU利用率 ps top htop

查看文件占用磁盘大小：du和df

程序运行时间：time，使用时在命令前添加time即可，

如：time ./test，可得到三个时间：real 0m0.020s，user 0m0.000s，sys 0m0.018s

grep命令（重要的常用命令之一）：常用于打开文本修改保存，类似打windows开开TXT文本并修改；

sed命令（常用重要命令之一）：主要用于对文件的增删改查；

awk命令（重要常用命令之一）：取列是其擅长的；
find 命令（常与xargs命令配合）：查找 -type 文件类型-name 按名称查找-exec执行命令；

xargs命令：配合find/ls查找，将查找结果一条条的交给后续命令处理；

使用过的 shell 命令
      cp , mv , rm , mkdir , touch , pwd , cd  , ls , top , cat , tail , less , df , du , man , find , kill , sudo , cat 


观察运行中的进程状态可以使用静态的ps和动态的top以及top的增强版htop

这些命令可以统计各个进程的CPU和内存MEM使用率


这里会有一些进程优先级的概念，PRI越低越先被CPU执行，PRI(new)=PRI(old)+nice，人越不nice越爱抢嘛，很好记。 

其中nice和renice可以设置优先级，区别是nice是在进程启动前调整，renice可以在进程运行中动态调整


### awk sed需掌握

有时候你也许会想要提取多行的某列信息，或者想要对文本按某一规则进行处理，

这时候你可能会选择python或者shell编写脚本，不过awk和sed可能会是更好的选择，因为需求经常一行就可以搞定。

AWK是文本处理语言，常用来进行查询，支持正则。sed是用程序进行文本编辑的流编辑器，只支持简单的条件处理，

使用label。sed同样使用正则匹配，可以对文本进行修改，如果你对vim熟悉的话，sed上手会非常快，

因为他们有许多相似的命令，例如s/a/b/g 这样的文本替换。 

关于工具使用没有什么特别的，注意awk是语言，可以使用if else等逻辑判断，也可以使用system运行shell指令。 

这里直接给三个链接:

sed：http://coolshell.cn/articles/9070.html 

awk：http://www.delightpress.com.tw/bookRead/skns00004_read.pdf 

http://wanggen.myweb.hinet.net/ach3/ach3.html?M



## pidstat

pidstat -wt -p 34307 1


## 打开rdma嗅探
ethtool --set-priv-flags net0 sniffer on
关闭rdma嗅探
ethtool --set-priv-flags net0 sniffer off


## 查看domain连接

1、使用iproute2中的ss

sudo ss -a --unix -p

2、使用lsof配合gdb

lsof -p xxx | grep xxx.sock

lsof找出在内核中的地址。

gdb /usr/src/linux/vmlinux /proc/kcore

(gdb) p((struct unix_sock*)address)->peer

