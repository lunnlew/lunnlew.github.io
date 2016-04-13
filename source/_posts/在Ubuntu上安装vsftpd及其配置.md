---
title: "在Ubuntu上安装vsftpd及其配置"
date: 2016-04-13 13:07:59
tags:
---

## 安装步骤

### 安装vsftpd
``` sh
sudo apt-get install vsftpd
```

### 配置vsftpd

#### 以独立模式(standalone)运行,监听IPV4
``` sh
echo "listen=YES
" > ~/vsftpd.conf
```

#### 禁用匿名访问
``` sh
echo "anonymous_enable=NO
" > ~/vsftpd.conf
```

#### 启用本地用户登录
``` sh
echo "local_enable=YES
" > ~/vsftpd.conf
```

#### 启用写操作支持
``` sh
echo "write_enable=YES
" > ~/vsftpd.conf
```

#### 启用用户目录写操作支持
``` sh
echo "allow_writeable_chroot=YES
" > ~/vsftpd.conf
```

#### 启用被动模式,端口范围40000-49999
``` sh
echo "pasv_enable=Yes
pasv_min_port=40000
pasv_max_port=49999" > ~/vsftpd.conf
```


## 安装脚本

``` sh
wget -qO- https://raw.githubusercontent.com/lunnlew/ubuntu_helper/master/Install_ftp_on_Ubuntu.sh | sh -x
````