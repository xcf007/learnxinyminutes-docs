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

###########################
# 第一个HelloWorld程序
###########################


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


###########################
# 基本类型变量
###########################
.method public static main([Ljava/lang/String;)V
    # 总共用了7个寄存器
    .registers 7

    .prologue
    
    const/16 v3, 0x64

    const/4 v5, 0x0

    const/4 v4, 0x1

    .line 5
    .line 6
    # byte型变量 byte fooByte = 100;
    # System.out.println(fooByte);  
    sget-object v0, Ljava/lang/System;->out:Ljava/io/PrintStream;

    invoke-virtual {v0, v3}, Ljava/io/PrintStream;->println(I)V

    .line 8
    # 短整型 short fooShort = 10000;
    const/16 v0, 0x2710

    .line 9
    # System.out.println(fooShort);  
    sget-object v1, Ljava/lang/System;->out:Ljava/io/PrintStream;

    invoke-virtual {v1, v0}, Ljava/io/PrintStream;->println(I)V

    .line 12
    # 整型  int fooInt = 1;
    # System.out.println(fooInt);  
    sget-object v0, Ljava/lang/System;->out:Ljava/io/PrintStream;

    invoke-virtual {v0, v4}, Ljava/io/PrintStream;->println(I)V

    .line 14
    # 长整型 long fooLong = 100000L;
    # System.out.println(fooLong);  
    const-wide/32 v0, 0x186a0   

    .line 15
    sget-object v2, Ljava/lang/System;->out:Ljava/io/PrintStream;
    # long占v0,v1两个32位寄存器
    invoke-virtual {v2, v0, v1}, Ljava/io/PrintStream;->println(J)V

    .line 17
    # 单精度浮点数 float fooFloat = 234.5f;
    # System.out.println(fooFloat);      
    const v0, 0x436a8000    # 234.5f

    .line 18
    sget-object v1, Ljava/lang/System;->out:Ljava/io/PrintStream;

    invoke-virtual {v1, v0}, Ljava/io/PrintStream;->println(F)V

    .line 20
    # 双精度浮点数占64位（2个32位寄存器）double fooDouble = 123.4;
    # System.out.println(fooDouble);  
    # 送 v0,v1两个寄存器
    const-wide v0, 0x405ed9999999999aL    # 123.4

    .line 21
    sget-object v2, Ljava/lang/System;->out:Ljava/io/PrintStream;

    invoke-virtual {v2, v0, v1}, Ljava/io/PrintStream;->println(D)V

    .line 24
    # 1代表true 真 ：const/4 v4, 0x1
    # boolean fooBoolean = true;
    # System.out.println(fooBoolean);  
    sget-object v0, Ljava/lang/System;->out:Ljava/io/PrintStream;

    invoke-virtual {v0, v4}, Ljava/io/PrintStream;->println(Z)V

    .line 26
    # 0代表false： const/4 v5, 0x0
    # boolean barBoolean = false;
    # System.out.println(barBoolean);  
    sget-object v0, Ljava/lang/System;->out:Ljava/io/PrintStream;

    invoke-virtual {v0, v5}, Ljava/io/PrintStream;->println(Z)V

    .line 28
    # unicode字符'A': char fooChar = 'A';
    const/16 v0, 0x41

    .line 29
    sget-object v1, Ljava/lang/System;->out:Ljava/io/PrintStream;

    invoke-virtual {v1, v0}, Ljava/io/PrintStream;->println(C)V

    .line 32
    
    sget-object v0, Ljava/lang/System;->out:Ljava/io/PrintStream;
    # final int HOURS_I_WORK_PER_WEEK = 9001;
    const/16 v1, 0x2329

    invoke-virtual {v0, v1}, Ljava/io/PrintStream;->println(I)V

    .line 34
    # 字符串引用送v0 :  String fooString = "My String Is Here!";
    const-string v0, "My String Is Here!"

    .line 35
    sget-object v1, Ljava/lang/System;->out:Ljava/io/PrintStream;

    invoke-virtual {v1, v0}, Ljava/io/PrintStream;->println(Ljava/lang/String;)V

    .line 38
    # v0存数组大小10
    const/16 v0, 0xa
    # 生成一个int型数组，大小10，数组引用送v0 (寄存器可覆写)
    # int [] intArray = new int[10];
    new-array v0, v0, [I

    .line 39
    # 数字大小1 重用v4:  const/4 v4, 0x1
    # String [] stringArray = new String[1];
    new-array v0, v4, [Ljava/lang/String;

    .line 40
    # 重用v3 ： 数组大小 100
    # boolean [] booleanArray = new boolean[100];
    new-array v0, v3, [Z

    .line 42
    # int [] anotherIntArray = {9000, 1000, 1337};
    const/4 v0, 0x3
    
    new-array v0, v0, [I
    # 静态初始化，填充数组
    fill-array-data v0, :array_118

    .line 43
    sget-object v1, Ljava/lang/System;->out:Ljava/io/PrintStream;

    new-instance v2, Ljava/lang/StringBuilder;

    invoke-direct {v2}, Ljava/lang/StringBuilder;-><init>()V

    const-string v3, "intArray @ 0: "

    invoke-virtual {v2, v3}, Ljava/lang/StringBuilder;->append(Ljava/lang/String;)Ljava/lang/StringBuilder;

    move-result-object v2
    # System.out.println("intArray @ 0: " + anotherIntArray[0]);
    # v3寄存器 = v0寄存器[v5寄存器]
    aget v3, v0, v5

    invoke-virtual {v2, v3}, Ljava/lang/StringBuilder;->append(I)Ljava/lang/StringBuilder;

    move-result-object v2

    invoke-virtual {v2}, Ljava/lang/StringBuilder;->toString()Ljava/lang/String;

    move-result-object v2

    invoke-virtual {v1, v2}, Ljava/io/PrintStream;->println(Ljava/lang/String;)V

    .line 45
    # 数组元素赋值 anotherIntArray[1] = 1;
    aput v4, v0, v4

    .line 46
    # System.out.println("intArray @ 1: " + anotherIntArray[1]);
    sget-object v1, Ljava/lang/System;->out:Ljava/io/PrintStream;

    new-instance v2, Ljava/lang/StringBuilder;

    invoke-direct {v2}, Ljava/lang/StringBuilder;-><init>()V

    const-string v3, "intArray @ 1: "

    invoke-virtual {v2, v3}, Ljava/lang/StringBuilder;->append(Ljava/lang/String;)Ljava/lang/StringBuilder;

    move-result-object v2

    aget v0, v0, v4

    invoke-virtual {v2, v0}, Ljava/lang/StringBuilder;->append(I)Ljava/lang/StringBuilder;

    move-result-object v0

    invoke-virtual {v0}, Ljava/lang/StringBuilder;->toString()Ljava/lang/String;

    move-result-object v0

    invoke-virtual {v1, v0}, Ljava/io/PrintStream;->println(Ljava/lang/String;)V

    .line 49
    # Scanner sc = new Scanner(System.in);
    new-instance v0, Ljava/util/Scanner;

    sget-object v1, Ljava/lang/System;->in:Ljava/io/InputStream;

    invoke-direct {v0, v1}, Ljava/util/Scanner;-><init>(Ljava/io/InputStream;)V

    .line 50
    sget-object v1, Ljava/lang/System;->out:Ljava/io/PrintStream;

    const-string v2, "Enter number 1: "

    invoke-virtual {v1, v2}, Ljava/io/PrintStream;->print(Ljava/lang/String;)V

    .line 51
    # i1 = sc.nextInt();
    invoke-virtual {v0}, Ljava/util/Scanner;->nextInt()I

    move-result v1

    .line 52
    sget-object v2, Ljava/lang/System;->out:Ljava/io/PrintStream;

    const-string v3, "Enter number 2: "

    invoke-virtual {v2, v3}, Ljava/io/PrintStream;->print(Ljava/lang/String;)V

    .line 53
    # i2 = sc.nextInt();
    invoke-virtual {v0}, Ljava/util/Scanner;->nextInt()I

    move-result v0

    .line 54
    sget-object v2, Ljava/lang/System;->out:Ljava/io/PrintStream;

    new-instance v3, Ljava/lang/StringBuilder;

    invoke-direct {v3}, Ljava/lang/StringBuilder;-><init>()V

    const-string v4, "i1+i2 = "

    invoke-virtual {v3, v4}, Ljava/lang/StringBuilder;->append(Ljava/lang/String;)Ljava/lang/StringBuilder;

    move-result-object v3
    # 加法运算指令： v4寄存器 <= v1寄存器的值 + v0寄存器的值
    add-int v4, v1, v0

    invoke-virtual {v3, v4}, Ljava/lang/StringBuilder;->append(I)Ljava/lang/StringBuilder;

    move-result-object v3

    invoke-virtual {v3}, Ljava/lang/StringBuilder;->toString()Ljava/lang/String;

    move-result-object v3

    invoke-virtual {v2, v3}, Ljava/io/PrintStream;->println(Ljava/lang/String;)V

    .line 55
    sget-object v2, Ljava/lang/System;->out:Ljava/io/PrintStream;

    new-instance v3, Ljava/lang/StringBuilder;

    invoke-direct {v3}, Ljava/lang/StringBuilder;-><init>()V

    const-string v4, "i2-i1 = "

    invoke-virtual {v3, v4}, Ljava/lang/StringBuilder;->append(Ljava/lang/String;)Ljava/lang/StringBuilder;

    move-result-object v3
    
    # 减法运算指令： v4寄存器 <= v0寄存器的值 - v1寄存器的值
    sub-int v4, v0, v1

    invoke-virtual {v3, v4}, Ljava/lang/StringBuilder;->append(I)Ljava/lang/StringBuilder;

    move-result-object v3

    invoke-virtual {v3}, Ljava/lang/StringBuilder;->toString()Ljava/lang/String;

    move-result-object v3

    invoke-virtual {v2, v3}, Ljava/io/PrintStream;->println(Ljava/lang/String;)V

    .line 56
    sget-object v2, Ljava/lang/System;->out:Ljava/io/PrintStream;

    new-instance v3, Ljava/lang/StringBuilder;

    invoke-direct {v3}, Ljava/lang/StringBuilder;-><init>()V

    const-string v4, "i2*i1 = "

    invoke-virtual {v3, v4}, Ljava/lang/StringBuilder;->append(Ljava/lang/String;)Ljava/lang/StringBuilder;

    move-result-object v3

    # 乘法运算指令： v4寄存器 <= v0寄存器的值 * v1寄存器的值
    mul-int v4, v0, v1

    invoke-virtual {v3, v4}, Ljava/lang/StringBuilder;->append(I)Ljava/lang/StringBuilder;

    move-result-object v3

    invoke-virtual {v3}, Ljava/lang/StringBuilder;->toString()Ljava/lang/String;

    move-result-object v3

    invoke-virtual {v2, v3}, Ljava/io/PrintStream;->println(Ljava/lang/String;)V

    .line 57
    sget-object v2, Ljava/lang/System;->out:Ljava/io/PrintStream;

    new-instance v3, Ljava/lang/StringBuilder;

    invoke-direct {v3}, Ljava/lang/StringBuilder;-><init>()V

    const-string v4, "i1/i2 = "

    invoke-virtual {v3, v4}, Ljava/lang/StringBuilder;->append(Ljava/lang/String;)Ljava/lang/StringBuilder;

    move-result-object v3

    # 除法运算指令： v0寄存器 <= v1寄存器的值 / v0寄存器的值
    div-int v0, v1, v0

    invoke-virtual {v3, v0}, Ljava/lang/StringBuilder;->append(I)Ljava/lang/StringBuilder;

    move-result-object v0

    invoke-virtual {v0}, Ljava/lang/StringBuilder;->toString()Ljava/lang/String;

    move-result-object v0

    invoke-virtual {v2, v0}, Ljava/io/PrintStream;->println(Ljava/lang/String;)V

    .line 60
    return-void

    .line 42
    # 静态数据块
    :array_118
    .array-data 4
        0x2328
        0x3e8
        0x539
    .end array-data
.end method

```
