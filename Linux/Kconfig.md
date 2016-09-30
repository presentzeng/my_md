# Linux kernel的编译系统

Linux里面通过Makeifle和Kconfig来管理整个项目代码

#####1. 目录结构
内核总目下有一个Makefile,这里指名toolchain,配置好各种环境
然后通过指名subdir,一路编译下去,例如: drivers-y   := drivers/ sound/ firmware/
而例如sound下面就没有make命令了,只需指明分别是哪些.o并且是编成什么模式，是(-m)module (-y)build-int 还是（-n)none


#####2. 单独编译ko
example:
```
obj-$(CONFIG_HELLO) += helloworld.o
helloworld-objs = hello.o \
TOOLCHINA = CROSS_COMPILE=/home/zenghaohan/workspace/h5/lichee/out/sun50iw2p1/android/common/buildroot/external-toolchain/bin/aarch64-linux-gnu-

KDRNEL_DIR:= /home/zenghaohan/workspace/h5/lichee/linux-3.10
PWD :=$(shell pwd)


all:
	make ARCH=arm64 $(TOOLCHINA) -C $(KERNEL_DIR) M=$(PWD) modules
clean:
	make ARCH=arm64 $(TOOLCHINA) -C $(KERNEL_DIR) M=$(PWD) clean
```	

```
 config HELLO
           tristate "First Android Driver"
           default y
           help
           This is the first android driver.
```

在内核根目录make ARCH=xxx menuconfig
即可配置名为“First Android Driver“的配置项目
实际修改的就是/下面的.config
如果配置成-m
则helloworld.ko可以insmod加载rmmode卸载
file *.ko可以查看ko信息,架构,位数等等
dmesg可以看内核加载的打印
/sys/modules  /system/vendor/modules 
























