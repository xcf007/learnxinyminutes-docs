---
name: smali
category: language
language: smali
lang: zh-cn
filename: HelloSmali.smali
contributors:
    - ["Chuanfu Xi", "http://github.com/xcf007"]
translators:
    - ["Chuanfu Xi", "http://github.com/xcf007"]
---

smali/baksmali是dex格式文件的汇编/反汇编器，dex格式由dalvik（Android的Java虚拟机实现）采用。Smali的语法基于Jasmin's/dedexer，它完成支持dex格式的全部功能(
注解、调试信息、代码行信息等）。[下载](https://bitbucket.org/JesusFreke/smali/downloads/)
教程采用的smali版本： smali-2.2.6.jar
```smali

# 单行注释

# 类名不需要和文件名一样(HelloSmali.smali)
.class public LHelloSmali;
# 一个Smali实现的HelloWorld程序
# 生成dex文件的汇编命令： java -jar F:\download\smali-2.2.6.jar -o HelloSmali.dex HelloSmali.smali
# 上传到手机(或安卓模拟器)某个可写目录: adb push HelloSmali.dex /mnt/sdcard/Download
# 执行： adb shell dalvikvm -cp /mnt/sdcard/Download/HelloSmali.dex HelloSmali


# Java中类可以隐式指定超类Object, Smali必不可少（必须显示指定超类, 即使继承自Object）
.super Ljava/lang/Object;


# main方法签名 == public static void main(String[])
.method public static main([Ljava/lang/String;)V
    # 指定使用2个局部寄存器(v0, v1)
    .locals 2
    
    # v0寄存器 <= System.out   【类型：java.io.PrintStream】
    sget-object v0, Ljava/lang/System;->out:Ljava/io/PrintStream;
    
    # v1寄存器 <= "Hello,Smali!"
    const-string v1, "Hello,Smali!"
    
    # v0寄存器引用的对象.println(v1引用的String对象【"Hello,Smali!】)
    # invoke-virtual 调用的public方法
    invoke-virtual {v0, v1}, Ljava/io/PrintStream;->println(Ljava/lang/String;)V
    
    # return-void指令对于方法必选
    return-void
.end method
```
