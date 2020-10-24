# Ryzen-X470i-Hackintosh-Opencore-EFI

## 配置如下

CPU   R7 3700X

GPU   5500XT

NIC   DW1560

MB    ASUS ROG STRIX X470I (itx mothermoard)

## 理论兼容

### 系统： MacOS 10.15 Catalina

### CPU: Ryzen 1000~3000 Treadripper?(maybe)

### GPU: RX5000 Navi架构显卡

其他架构显卡务必去掉boot-args项的 `agdpmod=pikera` 

### 网卡: 博通DW1560 (DW1820应该也可以)

### 主板：AMD 400系列主板 如上 华硕X470I 它的板载声卡有点特殊，其他400系列主板有可能出现板载耳机接口不好使的情况，这个时候要修改APPLEALC的设置

修改AppleALC设置的位置：`DeviceProperties` - `PciRoot(0x0)/Pci(0x8,0x1)/Pci(0x0,0x4)` - `alc-layout-id` - `01000000`

这是个4Byte字节小端编码的数据，查applealc文档的表中的数值转换成十六进制 00~FF 比如给的是3，就是 03 补上 000000 -> `01000000`

## 必须知道的事

[黑果小兵](https://blog.daliansky.net/)分享的 MacOS ISO 镜像，wx打赏1元后用balenaEtcher写入U盘

DiskGenius **必备** 用来修改EFI，直接打开找到对应磁盘的ESP分区，先备份，再全删除，再换上现成的EFI文件夹

[Opencore官方文档](https://dortania.github.io/OpenCore-Install-Guide/prerequisites.html) 这个很重要，现成的EFI往往不能达到你要的效果，跟着官方文档啃一个下午应该能利用最新的OC作出一个基础的EFI，比各种找现成的EFI浪费时间高效得多

**“重新做比找Bug更节省时间” - 适用于FPGA和黑苹果**

Opencore Configurator 和 ProperTree 都要下载，一般用前者挂载，后者修改，有的值后者不方便看的时候再用前面的，因为它可能会出现一些小问题

[司波图的视频](https://www.bilibili.com/video/BV1oE411M7Bs) 很有借鉴和启蒙意义，但是不要用它的包，已经不适合这个版本了（诶这个z炮怎么压到我的？？） 跟着视频的讲解和思路看官方文档 可！

## EFI使用方法

先修改好主板设置，关闭`快速启动`，关闭`安全启动`，关闭`CSM兼容`，打开`hand-off`（一般默认开），有的主板要调整`4G Encoding`，这张主板没有，所以预设里的启动项加过对应的参数了

EFI没有Debug调试参数，记得手动吧boot-args这一项加个 ` -v` 开启啰嗦模式

做好装Mac系统的U盘，用DiskGenius替换EFI，记住替换的OC引导盘是第几个，然后重启，（可狂按Del）设置引导选项，如果能直接进到安装界面，90%的工作就结束了

如果卡住了，到上面说的Opencore官方文档搜索对应代码，比百度好使多了

后面抹盘-安装之类的其他教程很多，安装和EFI的优化只占10%，能引导都好说，大不了重装一遍系统

## 如果EFI不适合你的硬件怎么办？

看Opencore官方文档

**“重新做比找Bug更节省时间” - 适用于FPGA和黑苹果**

也可以试着找对应的群，比如小新pro13这种，有群会舒服很多，有人参考

## 下载方式
见本仓库的Release



