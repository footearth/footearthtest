## IBM 3650 M3 ##

**硬盘 RAID
  * 开机 Ctrl+H
  * 两块 156G 硬盘 RAID0**

### RHEL 6 ###

**分区**

|200	|/boot/efi|
|500	|/boot|
|73000	|/home|
|4096	|swap|
|200000	|/|

**本地源设置**

```
# 挂载光盘镜像
mount /dev/cdrom /mnt

修改 yum repo 配置文件
cd /etc/yum.repos.d/
cp packagekit-media.repo packagekit-media.repo.bak
vim packagekit-media.repo

# packagekit-media.repo
[InstallMedia] 
name=local_yum 
baseurl=file:///mnt 
gpgcheck=0 
enabled=1

# 清理缓存
yum clean all
```

**安装软件
  * yum install ld-linux.so.2
  * lftp http://lftp.yar.ru/
  * axel http://wilmer.gaa.st/main.php/axel.html**

### FTP ###

### SVN ###

### ORACLE ###