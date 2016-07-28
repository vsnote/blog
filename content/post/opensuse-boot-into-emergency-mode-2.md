---
title: openSUSE启动进入紧急模式
author: 陈 三
layout: post
date: 2014-05-08T14:22:27+00:00
url: /opensuse-boot-into-emergency-mode-2.html
views:
  - 688
categories:
  - openSUSE

---
我的电脑通常都不关机，晚上用完后，只合上笔记本的屏幕，让它休眠。

但是有一阵子，openSUSE从休眠中唤醒，进入登录界面后，登录框不见了。只有一张变色龙的背景图片。

碰上这种情况，通常我都是长按电源键，强制关机，然后再启动。大部分时候，这方法可行。但偶尔也失效。不过因为懒得折腾，失效就多试几次，总有某次可以。

但昨晚升级系统到openSUSE13.2(milestone版，慎用)，用的是`zypper update`命令，总共更新2000多个软件包，重启系统后，就直接进入紧急模式：

> Welcome to emergency mode! After logging in, type &#8220;journalctl -xb&#8221; to view system logs, &#8220;systemctl reboot&#8221; to reboot, &#8220;systemctl default&#8221; to try again to boot into default mode.

用root账户登录后，执行：

    journalctl -xb
    

屏幕打印出很长的内容。

用红色突出的部分，大致是写：

> timed out waiting for device &#8230;
> 
> Dependency failed for /home

等等。

看起来情况颇为复杂。不过简单说，就是系统出问题了，需要进入紧急模式处理，等处理好了，自然能正常进入系统。

  1. 查看fstab内容
    
    `cat /etc/fstab` 命令的输出如下：
    
        /dev/disk/by-id/ata-WDC_WD3200BEKT-08PVMT1_WD-WXL1A9103779-part5 swap   swap  defaults       0 0
        /dev/disk/by-id/ata-WDC_WD3200BEKT-08PVMT1_WD-WXL1A9103779-part6 /      ext4  acl,user_xattr 1 1
        /dev/disk/by-id/ata-WDC_WD3200BEKT-08PVMT1_WD-WXL1A9103779-part7 /home  ext4  acl,user_xattr 1 2
        proc                 /proc                proc       defaults              0 0
        sysfs                /sys                 sysfs      noauto                0 0
        debugfs              /sys/kernel/debug    debugfs    noauto                0 0
        usbfs                /proc/bus/usb        usbfs      noauto                0 0
        devpts               /dev/pts             devpts     mode=0620,gid=5       0 0
        

  2. 查看/dev/disk/by-id情况
    
    命令`ls -l /dev/disk/by-id`的输出如下：
    
        总用量 0
        lrwxrwxrwx 1 root root  9 5月   8 00:06 ata-HL-DT-STDVDRAM_GT33N_M00B9DF4147 -> ../../sr0
        lrwxrwxrwx 1 root root  9 5月   8 00:06 ata-WDC_WD3200BEKT-0_WD-WXL1A9103779 -> ../../sda
        lrwxrwxrwx 1 root root 10 5月   8 00:06 ata-WDC_WD3200BEKT-0_WD-WXL1A9103779-part2 -> ../../sda2
        lrwxrwxrwx 1 root root 10 5月   8 00:06 ata-WDC_WD3200BEKT-0_WD-WXL1A9103779-part5 -> ../../sda5
        lrwxrwxrwx 1 root root 10 5月   8 00:06 ata-WDC_WD3200BEKT-0_WD-WXL1A9103779-part6 -> ../../sda6
        lrwxrwxrwx 1 root root 10 5月   8 00:06 ata-WDC_WD3200BEKT-0_WD-WXL1A9103779-part7 -> ../../sda7
        lrwxrwxrwx 1 root root  9 5月   8 00:06 scsi-0ATA_WDC_WD3200BEKT-0_WD-WXL1A9103779 -> ../../sda
        lrwxrwxrwx 1 root root 10 5月   8 00:06 scsi-0ATA_WDC_WD3200BEKT-0_WD-WXL1A9103779-part2 -> ../../sda2
        lrwxrwxrwx 1 root root 10 5月   8 00:06 scsi-0ATA_WDC_WD3200BEKT-0_WD-WXL1A9103779-part5 -> ../../sda5
        lrwxrwxrwx 1 root root 10 5月   8 00:06 scsi-0ATA_WDC_WD3200BEKT-0_WD-WXL1A9103779-part6 -> ../../sda6
        lrwxrwxrwx 1 root root 10 5月   8 00:06 scsi-0ATA_WDC_WD3200BEKT-0_WD-WXL1A9103779-part7 -> ../../sda7
        lrwxrwxrwx 1 root root  9 5月   8 00:06 scsi-1ATA_WDC_WD3200BEKT-08PVMT1_WD-WXL1A9103779 -> ../../sda
        lrwxrwxrwx 1 root root 10 5月   8 00:06 scsi-1ATA_WDC_WD3200BEKT-08PVMT1_WD-WXL1A9103779-part2 -> ../../sda2
        lrwxrwxrwx 1 root root 10 5月   8 00:06 scsi-1ATA_WDC_WD3200BEKT-08PVMT1_WD-WXL1A9103779-part5 -> ../../sda5
        lrwxrwxrwx 1 root root 10 5月   8 00:06 scsi-1ATA_WDC_WD3200BEKT-08PVMT1_WD-WXL1A9103779-part6 -> ../../sda6
        lrwxrwxrwx 1 root root 10 5月   8 00:06 scsi-1ATA_WDC_WD3200BEKT-08PVMT1_WD-WXL1A9103779-part7 -> ../../sda7
        lrwxrwxrwx 1 root root  9 5月   8 00:06 scsi-350014ee601c73034 -> ../../sda
        lrwxrwxrwx 1 root root 10 5月   8 00:06 scsi-350014ee601c73034-part2 -> ../../sda2
        lrwxrwxrwx 1 root root 10 5月   8 00:06 scsi-350014ee601c73034-part5 -> ../../sda5
        lrwxrwxrwx 1 root root 10 5月   8 00:06 scsi-350014ee601c73034-part6 -> ../../sda6
        lrwxrwxrwx 1 root root 10 5月   8 00:06 scsi-350014ee601c73034-part7 -> ../../sda7
        lrwxrwxrwx 1 root root  9 5月   8 00:06 scsi-SATA_WDC_WD3200BEKT-0_WD-WXL1A9103779 -> ../../sda
        lrwxrwxrwx 1 root root 10 5月   8 00:06 scsi-SATA_WDC_WD3200BEKT-0_WD-WXL1A9103779-part2 -> ../../sda2
        lrwxrwxrwx 1 root root 10 5月   8 00:06 scsi-SATA_WDC_WD3200BEKT-0_WD-WXL1A9103779-part5 -> ../../sda5
        lrwxrwxrwx 1 root root 10 5月   8 00:06 scsi-SATA_WDC_WD3200BEKT-0_WD-WXL1A9103779-part6 -> ../../sda6
        lrwxrwxrwx 1 root root 10 5月   8 00:06 scsi-SATA_WDC_WD3200BEKT-0_WD-WXL1A9103779-part7 -> ../../sda7
        lrwxrwxrwx 1 root root  9 5月   8 00:06 wwn-0x50014ee601c73034 -> ../../sda
        lrwxrwxrwx 1 root root 10 5月   8 00:06 wwn-0x50014ee601c73034-part2 -> ../../sda2
        lrwxrwxrwx 1 root root 10 5月   8 00:06 wwn-0x50014ee601c73034-part5 -> ../../sda5
        lrwxrwxrwx 1 root root 10 5月   8 00:06 wwn-0x50014ee601c73034-part6 -> ../../sda6
        lrwxrwxrwx 1 root root 10 5月   8 00:06 wwn-0x50014ee601c73034-part7 -> ../../sda7
        

对比之下，可以看到fstab里by-id字符串的值与/dev/disk/by-id输出的并不一样。

刚开始我并不敢确认，是否应该将fstab里的by-id统一为/dev/disk/by-id里对应的值，所以采用的是UUID。

执行命令`blkid`的查看UUID值如下：

    /dev/sda5: UUID="748d099e-2e51-4886-8f29-d3d39739d7d9" TYPE="swap" PARTUUID="000b4909-05" 
    /dev/sda6: UUID="234f7253-edbc-440b-aee6-a621641b1a9d" TYPE="ext4" PARTUUID="000b4909-06" 
    /dev/sda7: UUID="6bf3c07e-f883-427c-aba2-82a4b445c2e6" TYPE="ext4" PARTUUID="000b4909-07" 
    

然后修改fstab：

    UUID=748d099e-2e51-4886-8f29-d3d39739d7d9 swap      swap       defaults              0 0
    UUID=234f7253-edbc-440b-aee6-a621641b1a9d /         ext4       acl,user_xattr        1 1
    UUID=6bf3c07e-f883-427c-aba2-82a4b445c2e6 /home                ext4       acl,user_xattr        1 2
    proc                 /proc                proc       defaults              0 0
    sysfs                /sys                 sysfs      noauto                0 0
    debugfs              /sys/kernel/debug    debugfs    noauto                0 0
    usbfs                /proc/bus/usb        usbfs      noauto                0 0
    devpts               /dev/pts             devpts     mode=0620,gid=5       0 0
    

重启系统：

    shutdown -r now
    

很幸运地开启登录窗口。

后来证明，把fstab里by-id字符串统一为/dev/disk/by-id里对应的值也是可行的。