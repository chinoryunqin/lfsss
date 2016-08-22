# lfsss
Linux系统基本的目录结构
/bin  操作系统默认提供的可执行文件
/boot 可操作系统启动有关的文件
/dev 所有硬件设备的存放    sda1  sda2.。。 硬盘设备
/etc 操作系统相关的配置文件
/home  对其他用户是隔离开的
/lib  模块，库，驱动
/opt  第三方软件
/var 系统日志，邮件，新闻组   /var/log  
/usr 


软件安装基本先configure,make.make install

系统制作过程比较虽然比较长但是还算简单，但是最后grub出现问题：
找到了解决办法
grub rescue>set 
root=hd1,msdos3
prefix=hd1,msdos3
查看启动分区状态发现分区不对。
grub rescue>ls
查看分区状况：
结果
hd1,msdos7 hd1,msdos6 hd1,msdos5 hd1,msdos1
grub rescue>ls hd1,1/boot/grub/
确认这个盘为ubuntu安装盘
随即将结果修改成
grub rescue>set root=hd1,msdos1
grub rescue>set prefix=(hd1,msdos1)/boot/grub
grub rescue>insmod normal
grub rescue>normal


遇到了很多问题比如共享库找不到
知道了共享库会装到/lib和/usr/lib下，ldconfig可以更新共享库缓存

总结了一些常用命令
mkdir -p  递归创建目录
>重定向   >>追加

less ctl-v ctrl-c  回车 能上能下
more  只能网下 
tail -n 10   后十行
head  -n 10 前十行

tailf

wc  打印每个文件的行，单词，字符数
sort 对文件中的每一行进行排序  -t 用来指定分隔符
uniq  去重  -c -d  -u
cut  -d 分隔符  -f  列

grep  -c  -C   -i  -o  -v  -e -B  -A  -C


atime  文件的访问时间   ctime  创建时间    mtime最后修改时间

which 查找一个命令在命令树中的位置
find  dir  -name  "xxxx"  目录中找文件
              -iname                 忽略大小写
              -regex  "xxxx"
               -iregex 
              -size  +10k   大于10k
              -perm    762      权限762的
              -user root      用户为root
              -group  root
              -mtime  -1     一天内修改的
              -mmin  +1      一分钟之前修改的
                -exec   wc  -l    {}  \   行数

tar  创建归档文件
tar -zcvf test.tar.gz  xxx   xxxx                        压缩算法
tar -zxvf  xxxx  解压
bz2文件   -jxvf   -jcvf

zip  xxxx.zip  xxxxx
unzip  xxxx.zip  -d   指定目录
zcat  xxxx.zip  查看压缩包内容
zgrep   xxx.zip  zip中搜索相应的内容
              
su   xxxx   切换用户
sudo  -u  xxx   touch  xxxxx   用xxx用户执行  touch

ssh   root@proxy-ccdevate.myalauda.cn  -p  端口号  
ps -aux 
kill -9 xxx
top 动态显示系统进程情况                 load中大于1 队列满      大于0.75小于1   x核数
      -p xxx
uptime   top第一行的信息
free  内存使用
netstat  -lptn   网络使用
