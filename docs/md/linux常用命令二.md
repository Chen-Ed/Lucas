# linux常用命令二

## 文件搜索
```bash
find / -name file1 #从 '/' 开始进入根文件系统搜索文件和目录  
find / -user user1 #搜索属于用户 'user1' 的文件和目录  
find /home/user1 -name \*.bin #在目录 '/ home/user1' 中搜索带有'.bin' 结尾的文件  
find /usr/bin -type f -atime +100 #搜索在过去100天内未被使用过的执行文件  
find /usr/bin -type f -mtime -10 #搜索在10天内被创建或者修改过的文件  
find / -name \*.rpm -exec chmod 755 '{}' \\; #搜索以 '.rpm' 结尾的文件并定义其权限  
find / -xdev -name \*.rpm #搜索以 '.rpm' 结尾的文件，忽略光驱、捷盘等可移动设备  
locate \*.ps #寻找以 '.ps' 结尾的文件 - 先运行 'updatedb' 命令  
whereis halt #显示一个二进制文件、源码或man的位置  
which halt #显示一个二进制文件或可执行文件的完整路径
```

## 挂载一个文件系统

```bash
mount /dev/hda2 /mnt/hda2 #挂载一个叫做hda2的盘 - 确定目录 '/ mnt/hda2' 已经存在  
umount /dev/hda2 #卸载一个叫做hda2的盘 - 先从挂载点 '/ mnt/hda2' 退出  
fuser -km /mnt/hda2 #当设备繁忙时强制卸载  
umount -n /mnt/hda2 #运行卸载操作而不写入 /etc/mtab 文件- 当文件为只读或当磁盘写满时非常有用  
mount /dev/fd0 /mnt/floppy #挂载一个软盘  
mount /dev/cdrom /mnt/cdrom #挂载一个cdrom或dvdrom  
mount /dev/hdc /mnt/cdrecorder #挂载一个cdrw或dvdrom  
mount /dev/hdb /mnt/cdrecorder #挂载一个cdrw或dvdrom  
mount -o loop file.iso /mnt/cdrom #挂载一个文件或ISO镜像文件  
mount -t vfat /dev/hda5 /mnt/hda5 #挂载一个Windows FAT32文件系统  
mount /dev/sda1 /mnt/usbdisk #挂载一个usb 捷盘或闪存设备  
mount -t smbfs -o username=user,password=pass //WinClient/share /mnt/share #挂载一个windows网络共享
```
## 磁盘空间
```bash
df -h #显示已经挂载的分区列表  
ls -lSr |more #以尺寸大小排列文件和目录  
du -sh dir1 #估算目录 'dir1' 已经使用的磁盘空间'  
du -sk \* | sort -rn #以容量大小为依据依次显示文件和目录的大小  
rpm -q -a --qf '%10{SIZE}t%{NAME}n' | sort -k1,1n  
#以大小为依据依次显示已安装的rpm包所使用的空间 (fedora, redhat类系统)  
dpkg-query -W -f='${Installed-Size;10}t${Package}n' | sort -k1,1n  
#以大小为依据显示已安装的deb包所使用的空间 (ubuntu, debian类系统)
```

## 用户和群组

```bash
groupadd group\_name #创建一个新用户组  
groupdel group\_name #删除一个用户组  
groupmod -n new\_group\_name old\_group\_name #重命名一个用户组  
useradd -c "Name Surname " -g admin -d /home/user1 -s /bin/bash user1 #创建一个属于 "admin" 用户组的用户  
useradd user1 #创建一个新用户  
userdel -r user1 #删除一个用户 ( '-r' 排除主目录)  
usermod -c "User FTP" -g system -d /ftp/user1 -s /bin/nologin user1 #修改用户属性

passwd #修改口令  
passwd user1 #修改一个用户的口令 (只允许root执行)  
chage -E 2005-12-31 user1 #设置用户口令的失效期限  
pwck #检查 '/etc/passwd' 的文件格式和语法修正以及存在的用户  
grpck #检查 '/etc/passwd' 的文件格式和语法修正以及存在的群组  
newgrp group\_name #登陆进一个新的群组以改变新创建文件的预设群组
```