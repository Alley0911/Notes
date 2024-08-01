# 挂载
## 挂载新的机械硬盘
```shell
# 查看所有磁盘
lsblk
# 使用ext4文件系统格式化该磁盘, 假设新的磁盘为/dev/sdd
sudo mkfs.ext4 /dev/sdd
# 挂载
sudo mkdir /mnt/new_disk
sudo mount /dev/sdd /mnt/new_disk
# 支持所有用户读写
sudo chmod 777 /mnt/new_disk
```
## ext5和NTFS的区别
这俩是不同的文件系统, 好像前者常用于linux系统, 而后者常用于windows系统