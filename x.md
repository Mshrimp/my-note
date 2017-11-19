#nfaiwef


```
faliwehf; a
```

dwahefo

>faukef
>fkwejaf





#Tiny4412 ARM开发环境搭建
[TOC]

##1. 简介


##2. 在64位系统上安装32位的库
ARM开发板是

如果使用的系统是64位的，需要安装支持32系统的库

如果使用的系统是32位的，不需要再安装库文件

##3. 安装工具
###3.1 安装及配置串口工具（以Minicom为例）
Windows下可以使用的串口工具比较多，如：Putty、CRT等，这里不再进行赘述。
Linux系统下连接串口需要使用串口工具，常用的串口软件有Minicom、Picocom、Kermit等，这里仅介绍Minicom串口工具的安装和配置。

Tiny4412开发板提供的有RS232电平的DB9公头接口，电脑自带串口采用的是RS232电平的DB9公头接口，可以用DB9双母头的串口线直接连接起来；如果电脑上没有自带串口，可以使用网上卖的比较多的USB转串口（如：FT232、PL2303等），将开发板的RS232电平转换为电脑USB接口支持的TTL电平；本人对DB9接口的串口线有所偏爱，所以在网上买来台式电脑的PCI转串口模块安装到主机，扩展出来两个RS232电平的DB9公头接口。

RS232电平：
逻辑1的电平为-3～-15V，逻辑0的电平为+3～+15V
TTL电平：
输出 L： <0.8V ； H：>2.4V。
输入 L： <1.2V ； H：>2.0V
即：TTL器件输出低电平要小于0.8V，高电平要大于2.4V。输入，低于1.2V就认为是0，高于2.0就认为是1。
####3.1.1 Windows系统连接串口


1. 使用USB转串口线

2. 使用电脑自带RS232电平的DB9串口

有的电脑带有串口时，一般电脑都是COM1。

有的台式电脑不自带串口，安装PCI转串口后，支持增加两个串口，会多出来两个COM，COM的编号不固定，也可以根据自己喜好进行设置。

####3.1.2 Linux系统连接串口
此处使用的Linux发行版为xubuntu 64位系统
```
xxx@ubuntu:~$ sudo cat /proc/tty/driver/serial
serinfo:1.0 driver revision:
0: uart:16550A port:000003F8 irq:4 tx:0 rx:0 CTS|DSR|CD
1: uart:16550A port:000002F8 irq:3 tx:0 rx:0
2: uart:unknown port:000003E8 irq:4
3: uart:unknown port:000002E8 irq:3
4: uart:unknown port:00000000 irq:0
......
30: uart:unknown port:00000000 irq:0
31: uart:unknown port:00000000 irq:0
```

```
xxx@ubuntu:~$ dmesg | grep ttyS*
[    0.000000] console [tty0] enabled
[    1.344291] 00:05: ttyS0 at I/O 0x3f8 (irq = 4, base_baud = 115200) is a 16550A
[    1.369614] 00:06: ttyS1 at I/O 0x2f8 (irq = 3, base_baud = 115200) is a 16550A
```

```
// 安装Minicom工具
xxx@ubuntu:~$ sudo apt-get install minicom
// 配置Minicom参数
xxx@ubuntu:~$ sudo minicom -s
```
![Alt text](./1484185713605.png)
如上图所示，选择Serial port setup，对Minicom进行设置，设置Serial Device为/dev

![Alt text](./1484185686380.png)

![Alt text](./1484185754774.png)


退出
Exit		退出设置，进入Minicom
Exit from Minicom		退出设置，退出Minicom

使用Minicom工具连接串口
```
// 使用USB转串口线连接串口
xxx@ubuntu:~$ sudo minicom -D /dev/ttyUSB0

// 使用电脑RS232的DB9串口线连接串口
xxx@ubuntu:~$ sudo minicom -D /dev/ttyS0
xxx@ubuntu:~$ sudo minicom -D /dev/ttyS1
```


####3.1.3 虚拟机Linux系统连接串口
本人虚拟机中安装了64位的xubuntu系统进行开发
1. 虚拟机中使用USB转串口线连接串口


![Alt text](./1484187080830.png)

```
xxx@ubuntu:~$ ls /dev/ttyUSB0 -l
crw-rw---- 1 root dialout 188, 0 Jan 12 10:11 /dev/ttyUSB0
```






2. 虚拟机连接电脑自带串口

![Alt text](./1484184602946.png)

![Alt text](./1484184631821.png)

![Alt text](./1484184647238.png)

![Alt text](./1484184666023.png)

![Alt text](./1484184677351.png)

![Alt text](./1484184699782.png)

![Alt text](./1484184838298.png)


虚拟机设置好之后，按照上一步骤进行连接串口操作
