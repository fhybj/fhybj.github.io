title: Windows环境下编译openssl库
date: 2016-01-17 12:43:35
tags: OSS
categories: OSS
---

openssl版本：openssl-1.0.2e

在Windows环境下编译openssl需要perl支持，安装ActivePerl

## 1. 配置编译环境
我们用VS2010来作为编译工具，打开命令行，切换到bin目录，比如
> cd C:\Program Files\Microsoft Visual Studio 10.0\VC\bin
> vcvars32.bat

## 2. 配置编译文件和模式
切换到openssl编译目录，输入：
> perl Configure debug-VC-WIN32 no-asm --prefix="E:\openssl-1.0.2e\build-debug"

`debug-VC-WIN32`表示Windows 32位系统，64位系统请换成`debug-VC-WIN64A`
Release版本去掉*debug*, 改为`VC-WIN32`或者`VC-WIN64A`
`no-asm` 表示不用汇编，不设置此属性，会导致编译不过

## 3. 生成编译配置文件
32位
> ms\do_ms.bat

64位
> ms\do_win64a.bat

执行这一步之后，在ms目录下会生成`nt.mak`和`ntdll.mak`两个编译配置文件
`nt.mak` 用于生成静态lib库
`ntdll.mak` 用于生成动态dll库


## 4. 编译
静态库
> nmake -f ms\nt.mak
> nmake -f ms\nt.mak install

动态库
> nmake -f ms\ntdll.mak
> nmake -f ms\ntdll.mak install

编译完成之后就可以在`build-debug`目录看到编译生成的库了

## 5. 遇到的错误
>Assembling: tmp32\sha1-586.asm
tmp32\sha1-586.asm(1427) : error A2070: invalid instruction operands
tmp32\sha1-586.asm(1571) : error A2070: invalid instruction operands
NMAKE : fatal error U1077: 'ml' : return code '0x1'
Stop.

出现该问题就是因为在第2步时没有加上`no-asm`属性

## 6. 总结和思考
上述方法在32位系统上测试OK，64位虽然原理相同但没有实际编译过。
另外，64位的编译选项还有一个`VC-WIN64I`，它和`VC-WIN64A`有什么区分还不知道？

参考：
http://developer.covenanteyes.com/building-openssl-for-visual-studio/
