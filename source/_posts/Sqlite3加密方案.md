title: Sqlite3加密方案
date: 2016-01-17 12:50:23
tags: OSS
categories: OSS
---

## Sqlite3
>开源版的Sqlite3是不支持加密功能的，对于一个保存在本地的数据库来说没有加密功能让人难以接受。所幸Sqlite3的作者留下了加密接口，而互联网上也有很多高人提供了他们的加密方案，其中有收费的，也有免费的。
>这里选择了一个免费的加密方案`SQLCipher`，不过该方案没有直接提供编译好的库，只是提供了源代码，而且编译略麻烦，如果你不想自己编译，就只能花500美刀向作者购买编译好的库。吾辈屌丝只能望洋兴叹了，只能自己动手丰衣足食。


## 编译SQLCipher
在本项目中没有直接使用二进制库（lib或者dll），而是直接将源代码集成到项目中，毕竟sqlite3的源代码就只有一个.c文件和一个头文件。
SQLCipher提供了一个方法，用于将SQLCipher的加密代码加到sqlite3的源码上从而生成一个"联合文件(amalgamation file)"，最后将生成的文件加到项目里就好了。
>./configure --enable-tempstore=yes CFLAGS="-DSQLITE_HAS_CODEC"
>make sqlite3.c

执行上述两个命令就能生成以下几个文件：
- sqlite3.h
- sqlite3.c
- sqlite3ext.h
- shell.c ——生成客户端工具的代码文件，我们用不到这个文件


以上命令都是在Ubuntu环境下执行的，Windows环境也能编译但需要额外安装MSYS2之类的*unix模拟器。

**注意:**
SQLCipher库的加密功能有openssl提供，所以首先编译环境需要安装openssl，Ubuntu已经默认安装了。
但编译SQLCipher还需要用到libssl-dev库，Ubuntu环境下可以用下面的命令安装
>sudo apt-get install libssl-dev

另外，在将代码合入到工程中时，别忘了加上`SQLITE_HAS_CODEC`和`SQLITE_TEMP_STORE=2`这两个宏
