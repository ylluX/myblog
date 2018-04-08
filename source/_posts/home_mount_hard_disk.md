---
title: /home挂载到新硬盘
tags:
  - linux
  - ubuntu
categories: linux
---

将/home挂载到新硬盘，有一下几个优点：

* 避免存储紧张（主机空间很小）；
* 便于管理和维护，方面数据迁移

### 挂载步骤

1. 挂载设置好的硬盘
    ```
    sudo mkdir /mnt/tmp
    sudo mount /dev/sda5 /mnt/tmp
    ```
2. 同步 /home 目录所有文件
    ```
    sudo rsync -avx /home/* /mnt/tmp
    ```
3. 卸载新硬盘
    ```
    sudo umount /mnt/tmp
    ```
4. 检查同步结果
    ```
    sudo mv /home /home.bak
    sudo mkdir /home
    sudo mount /dev/sda5 /home
    ```
    可以从图形界面查看，检查同步结果，如果没有问题，请继续
5. 删除原 /home 文件夹
    ```
    sudo rm /home.bak
    ```
6. 设置启动自动挂载 /home
    在 /etc/fstab 文件中添加
    ```
    UUID=8feff07f-ac50-4aae-97c8-e5bbfc665c95  /home  ext4   defaults   0   0
    ```
    + 第一列可以是实际分区名，也可以是实际分区的卷标（Lable），还可以是全局唯一标识符（UUID），可以通过命令`sudo blkid`查看。
    + 第二列是挂载点。
    + 第三列为此分区的文件系统类型。
    + 第四列是挂载的选项，用于设置挂载的参数。auto:系统自动挂载，fstab默认就是这个选项； defaults: rw, suid, dev, exec, auto, nouser, and async.； noauto 开机不自动挂载； nouser 只有超级用户可以挂载； ro 按只读权限挂载； rw 按可读可写权限挂载； user 任何用户都可以挂载； 请注意光驱和软驱只有在装有介质时才可以进行挂载，因此它是noauto
    + 第五列是dump备份设置。当其值设置为1时，将允许dump备份程序备份；设置为0时，忽略备份操作
    + 第六列是fsck磁盘检查设置。其值是一个顺序。当其值为0时，永远不检查；而 / 根目录分区永远都为1。其它分区从2开始，数字越小越先检查，如果两个分区的数字相同，则同时检查。
7. 重启，并查看
    ```
    df -h
    ```
