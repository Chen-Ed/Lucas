# linux常用命令

## 系统信息

```bash
arch #显示机器的处理器架构(1)  
uname -m #显示机器的处理器架构(2)  
uname -r #显示正在使用的内核版本  
dmidecode -q #显示硬件系统部件 - (SMBIOS / DMI)  
hdparm -i /dev/hda #罗列一个磁盘的架构特性  
hdparm -tT /dev/sda #在磁盘上执行测试性读取操作  
cat /proc/cpuinfo #显示CPU info的信息  
cat /proc/interrupts #显示中断  
cat /proc/meminfo #校验内存使用  
cat /proc/swaps #显示哪些swap被使用  
cat /proc/version #显示内核的版本  
cat /proc/net/dev #显示网络适配器及统计  
cat /proc/mounts #显示已加载的文件系统  
lspci -tv #罗列PCI设备  
lsusb -tv #显示USB设备
```
## 系统日期显示和设置

```bash
cal 2007 #显示2007年的日历表 date #查看日期和时间 date 041217002007.00 #设置日期和时间 - 月日时分年.秒  
clock -w #将时间修改保存到 BIOS```

## 关机 (系统的关机、重启以及登出 )

shutdown -h now #关闭系统(1)  
init 0 #关闭系统(2)  
telinit 0 #关闭系统(3)  
shutdown -h hours:minutes & #按预定时间关闭系统  
shutdown -c #取消按预定时间关闭系统  
shutdown -r now #重启(1)  
reboot #重启(2)  
logout #注销

## 文件和目录

cd /home #进入 '/ home' 目录'  
cd .. #返回上一级目录  
cd ../.. #返回上两级目录  
cd #进入个人的主目录  
cd ~user1 #进入个人的主目录  
cd - #返回上次所在的目录  
pwd #显示工作路径

ls #查看目录中的文件  
ls -F #查看目录中的文件  
ls -l #显示文件和目录的详细资料  
ls -a #显示隐藏文件  
ls _\[0-9\]_ #显示包含数字的文件名和目录名  
tree #显示文件和目录由根目录开始的树形结构(1)  
lstree #显示文件和目录由根目录开始的树形结构(2)

mkdir dir1 #创建一个叫做 'dir1' 的目录'  
mkdir dir1 dir2 #同时创建两个目录  
mkdir -p /tmp/dir1/dir2 #创建一个目录树  
rm -f file1 #删除一个叫做 'file1' 的文件'  
rmdir dir1 #删除一个叫做 'dir1' 的目录'  
rm -rf dir1 #删除一个叫做 'dir1' 的目录并同时删除其内容  
rm -rf dir1 dir2 #同时删除两个目录及它们的内容  
mv dir1 new\_dir #重命名/移动 一个目录

cp file1 file2 #复制一个文件  
cp dir/\* . #复制一个目录下的所有文件到当前工作目录  
cp -a /tmp/dir1 . #复制一个目录到当前工作目录  
cp -a dir1 dir2 #复制一个目录

ln -s file1 lnk1 #创建一个指向文件或目录的软链接  
ln file1 lnk1 #创建一个指向文件或目录的物理链接

touch -t 0712250000 file1 #修改一个文件或目录的时间戳 - (YYMMDDhhmm)  
file file1 #查看文件类型及其编码格式，第一个file是命令，第二file1是文件名  
iconv -l #列出已知的编码

iconv -f fromEncoding -t toEncoding inputFile > outputFile #列出已知编码并保存到指定文件中
```