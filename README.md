一、准备（Preparation)
-----------------

ubuntu系统安装，选择的是Ubuntu 22.04LS(可采用虚拟机或双系统的方法）

交叉编译器 cross-tools：用于在一个系统架构的操作系统上编译可以在另一个系统架构上运行的代码

内核 kernel（选择的是老师给的MOS操作系统）：操作系统的文件

qemu ：用于模拟所需的硬件平台，以便操作系统运行

资源里面：guide-book有基础的学习操作流程，可以先看下这个

二、操作流程
------

搭建交叉编译器——搭建qemu——搭建内核

### 交叉编译器选择

[https://gitee.com/loongson-edu/la32r-toolchains/releases/tag/v0.0.2](https://gitee.com/loongson-edu/la32r-toolchains/releases/tag/v0.0.2 "https://gitee.com/loongson-edu/la32r-toolchains/releases/tag/v0.0.2")这个链接中下载[loongarch32r-linux-gnusf-2022-05-20-x86.tar.gz ](https://gitee.com/loongson-edu/la32r-toolchains/releases/download/v0.0.2/loongarch32r-linux-gnusf-2022-05-20-x86.tar.gz "loongarch32r-linux-gnusf-2022-05-20-x86.tar.gz ")解压后得到文件夹在该文件夹内直接修改linux中的环境变量，我用的是这个，注意修改下路径：后面的$PATH不用改

![](https://i-blog.csdnimg.cn/direct/254f82404dbd4e59ad267011684c2a12.png)编辑

### QEMU安装

这一步可能会缺不少包，得学一下，之前实验过24.04版本的ubuntu，有些包没有更新上；

下载包这里建议用外网，会快一些。

这里在linux里开外网多少有点复杂，我用的[https://mojie.app/dashboard](https://mojie.app/dashboard "https://mojie.app/dashboard")里面点击购买订阅，然后直接去使用文档里选择linux系统的就可以。之后按照里面进行操作，每次打开软件关闭ipv6,打开系统代理就可以。这个各种包不开外网下的太慢了。

你可以先试下我的订阅地址：[https://mojie0201.xn--8stx8olrwkucjq3b.com/api/v1/client/subscribe?token=5fbb9d9c75fc8f7dcedf72d1f07c05cc](https://mojie0201.xn--8stx8olrwkucjq3b.com/api/v1/client/subscribe?token=5fbb9d9c75fc8f7dcedf72d1f07c05cc "https://mojie0201.xn--8stx8olrwkucjq3b.com/api/v1/client/subscribe?token=5fbb9d9c75fc8f7dcedf72d1f07c05cc")

 复制这个网址到那个软件里去，那个mojie的网址要是打不开，直接在我下面资源里面下载deb文件clash-verge_amd64.deb安装

[la32r-QEMU: 基于开源LoongArch64-QEMU构建的支持LoongArch32精简指令集的QEMU. 使用方法见Wiki](https://gitee.com/loongson-edu/la32r-QEMU "la32r-QEMU: 基于开源LoongArch64-QEMU构建的支持LoongArch32精简指令集的QEMU. 使用方法见Wiki")

具体流程如下：

![](https://i-blog.csdnimg.cn/direct/40e9a3307efc474482f8b9eed8fce623.png)编辑

![](https://i-blog.csdnimg.cn/direct/11c21ec070f949938117a483824ca115.png)编辑


这个链接中下载代码，然后按照[Wiki - Gitee.com](https://gitee.com/loongson-edu/la32r-QEMU/wikis/qemu-system-loongarch32%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E "Wiki - Gitee.com")这个里面的提示做，只需要执行complie部分，最后记得加一个

```
make install
```

### MOS操作系统安装

见资源下载la32r_ans.zip，下载好后，直接在该文件夹（即为mos系统文件夹）下打开终端，执行

```
make test lab=6_2
```

实现交叉编译器验证，随后在mos文件夹下

```
make run
```

效果图大概长这个样子，这个图是学长内存管理部分的验证图，咱们接下来应该还有个文件管理没有做，学长是把FATFS移植过来了，但是他据说也没跑通。咱们得自己解决，我最近在做文件管理，停滞了一段时间，你要是搞到这里了，咱们可以一块讨论讨论。

![](https://i-blog.csdnimg.cn/direct/1ccef473895743cfba185a0e166f901c.png)编辑



