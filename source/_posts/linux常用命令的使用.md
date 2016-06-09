---
title: "linux常用命令的使用"
date: 2016-04-13 13:07:59
tags: [Linux,命令]
categories: [Linux应用,常用命令]
---

### 文件命名
    除/外所有字符可作为文件名
    避免使用.作为普通文件名首字符(以.开始命名为隐藏)
    文件名严格区分大小写

### 命令格式
    命令 -选项 参数

#### 常用命令

##### ls-列出目录文件
    命令    ls [-a|l|d] [file|dir]
    词汇    list
    权限    任意用户
    用法
    a   显示所有文件(包括隐藏文件),all
    l   显示详细信息,long
    d   显示指定目录的信息,directory
    示例
    ls -ld /tmp     显示/tmp目录自身详细信息
    ls -al /home    显示/home目录下的文件与目录详细信息

    --------命令相关----------
    drwxr-xr-x
    结构    文件类型(1),权限串(9)
    文件类型
        d   目录
        -   二进制文件
        l   软链接文件
    权限
        r   读,read
        w   写,write
        x   执行,execute
    权限串
        结构    所有者权限(3),所属组权限(3),其他用户权限(3)
        rwxr-xr-x
            rwx 所有者权限,可读写与执行
            r-x 所属组权限,读与执行
            r-x 其他用户权限,读与执行
##### cd-目录切换
    命令    cd [目录]
    词汇    change directory
    权限    任意用户
    示例
    cd /    切换到根目录
    cd ..   切换到上级目录
##### pwd-输出当前工作目录名
    命令    pwd
    词汇    print working directory
    权限    任意用户
##### touch-创建空文件
    命令    touch   [文件名]
    权限    任意用户
    示例
    touch test.txt
#### mkdir-建立目录
    命令    mkdir [目录名]
    词汇    make directory
    权限    任意用户
    示例
    mkdir test
##### cp-文件或目录复制
    命令    cp [-R] [src] [des]
    词汇    copy
    权限    任意用户
    用法
    R   递归复制目录,recursive
    示例
    cp file newfile     复制文件file到newfile
    cp -R dir newdir    递归复制目录dir到newdir下
##### mv-移动或者更名文件
    命令    mv [src] [des]
    词汇    move
    权限    任意用户
    示例
    mv dir1/file dir2      移动到dir2目录
    mv dir1/file dir2/newfile   移动到dir2目录的newfile文件
    mv dir1/file dir1/newfile   更名为newfile
##### rm-删除目录或文件
    命令    rm [-r|f] [dir|file]
    词汇    remove
    权限    任意用户
    用法
    r   递归删除,recursive
    f   确认与强制删除,force
    示例
    rm -r dir   递归删除目录,文件
    rm -rf dir  无提示递归删除目录,文件
##### cat-显示文件内容
    命令    cat [file]
    词汇    concatenate and display files
    权限    任意用户
    示例
    cat /etc/conf.ini   查看conf.ini文件内容
##### more-分页显示文件内容
    命令    more [file]
    权限    任意用户
    按键用法
    空格,f  下一页
    enter   下一行
    q,Q     退出
    示例
    more largefile
##### head-查看前几行
    命令    head [-{num}] [file]
    权限    任意用户
    示例
    head -20 file   查看file前20行
##### tail-查看后几行
    命令    tail [-{num}] [file]
    权限    任意用户
    用法
    f   动态刷新,flush
    示例
    tail -20 file   查看file后20行
    tail -5 -f file 不停地刷新输出最后5行
##### ln-创建链接文件
    命令    ln [-s] [file] [linkfile]
    词汇    link
    权限    任意用户
    用法
    s   软链接,soft
    示例
    ln -s file /usr/linkfile    建立一个软链接文件
    ln file /usr/linkfile    建立一个硬链接文件

    --------命令相关----------
    软链接文件
        类似windows快捷方式
        可跨文件系统
        源文件删除后不可正常使用
    硬链接文件
        不可跨文件系统
        与原文件具有相同inode(linux文件的数字识别id,命令 ls -i)
        类似一个原文件复制,但不是一个复制
        源文件删除后可正常使用
##### chmod-权限设定
    命令    chmod [(ugoa)(+-)(rwx)] [文件或目录]
            chmod [mode={num}]  [文件和目录]
    权限    任意用户
    示例
    chmod g+w  rwxrwxrwx file
    chmod 777  file

    --------命令相关----------
    r   4
    w   2
    x   1
    -   0
    mode    为三位数字值，每位数字为rwx-的和值

    项      文件            目录
    read    读文件内容      列出文件与目录
    write   修改文件内容    创建或者删除文件,目录
    x       执行文件        进入目录

    删除文件前提是对目录有写权限
    缺省创建文件无可执行权限
##### umask-缺省权限查看设置
    命令    umask [-S]
    示例
    umask       查看缺省权限,输出的是掩码值,换算关系(777=掩码值+实际权限值)
    umask -S    
    umask 027   缺省权限设置(实际权限为777-027=750)

    --------命令相关----------
    0022    umask返回四位权限掩码值
        0       特殊权限位
        022     用户权限位,实际权限(777-022=755)
##### which-显示命令所在路径
    命令    which [命令]
    权限    任意用户
    示例
    which ls    查看ls命令路径
##### whereis-在特定目录中查找符合条件的文件
    命令    whereis [file]
    权限    任意用户
    示例
    whereis ls
##### find-搜索文件或目录
    命令    find [搜索路径] [-name] [搜索关键字]
            find [搜索路径] [-size] [+-{size}]
            find [搜索路径] [-user] [用户]
            find [搜索路径] [-ctime|atime|mtime|cmin|amin|mmin] [+-{num}]
            find [搜索路径] [-inum] {num}
            find ---- -exec {} \;
    权限    任意用户
    用法
    name    根据文件名查找,默认全名搜索
        *   0到多个字符
        ?   一个字符
    size    根据文件大小查找,常用是数据块block数(1block = 512btye = 0.5kb)
    user    根据所有者查找
    a       连接符,and
    o       连接符,or
    f,l,d   文件类型,-type [{type}]
    示例
    find /test -name test       只找到test
    find /test -name test*      以test开始的文件名
    find /test -name test?      以test开始,五个字符的文件名
    find /test -size 163840 -a -size 204800 查找文件大小在80mb到100mb之间的文件
    find /test -mmin -120       寻找120分钟内访问过得文件
    find /test -name test -exec rm {} \;    删除test/目录下的test文件
    find /test -inum 16     查找i节点num的文件,对非规范名操作如删除等很有用
    --------命令相关----------
    ctime,atime,mtime   与天相关
    cmin,amin,mmin      与分相关
    c   change,文件属性改变,所有者,权限等
    a   access,文件被访问
    m   modify,文件内容被修改
    {}  -exec前命令执行结果
    \;  \转义符,'\;';号转义
##### locate-列出相关的文件目录(linux)
    命令    locate [关键字]
    词汇    list files in databases
    权限    任意用户
    示例
    locate  file
    --------命令相关----------
    从目录索引数据库中搜索
##### updatedb-建立目录索引数据库
    命令    updatedb
    词汇    update the slocate database
    权限    任意用户
##### grep-搜索匹配行
    命令    grep [keywords] [file]
    权限    任意用户
##### man-查看命令或配置文件帮助信息
    命令    man [命令|配置]
    词汇    manual
    权限    任意用户
    示例
    man ls
##### info-获取帮助信息
    命令    info [关键字]
    词汇    information
    权限    任意用户
    示例
    info ls
##### whatis-简略信息
    命令    whatis [命令]
    权限    任意用户
    示例
    whatis ls
##### apropos-关键字相关信息
    命令    apropos [关键字]
    权限    任意用户
##### gzip-文件压缩
    命令    gzip [选项] [文件]
    词汇    GUN zip
    权限    任意用户
    用法
    d   解压文件
    结果    .gz后缀
    示例
    gzip file   压缩文件
    gzip -d file.zip    解压文件
##### gunzip-文件解压缩
    命令    gunzip [选项] [待解压文件]
    词汇    GUN unzip
    权限    任意用户
    示例
    gunzip file.gz   压缩文件
#### tar-目录打包
    命令    tar [-c|v|f] [目标文件] [待打包目录]
    权限    任意用户
    用法
    c   create,建立打包文件
    v   显示详细信息
    f   file,指定文件名
    z   打包同时解压缩
    x   解包文件
    结果    .tar.gz
    示例
    tar -zcvf dir.tar.gz dir    打包并压缩
    tar -zxf dir.tar.gz 解包并解压缩
    --------命令相关----------
    file filename   查看文件信息
##### zip-压缩文件或者目录
    命令    zip [-r] [目标文件名] [源文件或目录]
    权限    任意用户
    结果    .zip
    用法
    r       递归压缩目录
    示例
    zip -r dir.zip dir  压缩dir目录
##### bzip2-压缩文件或者目录
    命令    bzip2 [-k] [源文件或目录]
    权限    任意用户
    结果    .bz2
    用法
    k   产生压缩文件时保留原文件
    示例
    bzip2 -k file
##### bunzip2-解压缩文件
    命令    bunzip2 [-k] [文件]
    权限    任意用户
    结果    .bz2
    用法
    k   解压缩文件时保留原文件
    示例
    bunzip2 -k file
