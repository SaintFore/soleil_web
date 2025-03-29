---
date:
  created: 2020-01-01
  updated: 2025-01-01
categories:
  - Blog
tags:
  - HTML5
  - CSS3
  - post
authors:
  - Merlin
---

## 硬件设备

惠普的小主机 HP800G。

使用的是 G4600 处理器，这个是两核心，四线程，但是 pve 只能用两个核心。

这个主机会先看有没有风扇，开机后需要先按下 `enter` 键，才能正确开机。


## 开始重装

重启，狂按 F10 进 BIOS。

**这里还需要把设备的虚拟化给允许了，否则 PVE 是有问题的。**

先进里面选择启动选项。

引导顺序优先选择 U 盘。这个需要先制作一个重装 U 盘，使用 Ventoy，非常好用。

最后保存更改，接着电脑会自动重启，接着进入 ventoy 界面，选择放入里面的 pve 系统，iso 后缀的系统文件。

normal 模式即可。

## PVE 开始

选择 Graphical。也就是界面化。

同意即可。

接着选个硬盘做系统盘，别选 u 盘。

地区选中国上海，键盘布局就是美国英语布局。

密码记住，邮箱地址无所谓。

接着选择网卡，hostname 随便，IP 和网关看需求，DNS 默认即可。

然后确认一下，点击 install 系统就自动安装了。

安装完后，拔掉 U 盘，等待重启。

# 登入 PVE

pve 系统重启后，随便选择个浏览器。

在搜索栏输入刚才设置的 IP 地址，后面加上冒号，端口号是 8006，这个端口是默认的。前提是你的电脑得跟这个 IP 地址是同一个网段，不然没法互通。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181614606.webp)

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181614071.webp)

这里语言先选择中文。

用户名是 root。

密码是你刚才设置的。

领域不用管。

进入后的无效订阅不用管。

# 创建子系统

这里以 openwrt 为例。

## 上传系统镜像

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181619336.webp)

你的数据中心下面有个 local，这个是用来存放一些资源的，包括镜像资源，直接上传你想要安装的系统的镜像。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181620229.webp)

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181620606.webp)

这里就上传了个 openwrt 的镜像。

## 创建虚拟机

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181623578.webp)

点击左上角的创建虚拟机。

节点不用动。

VM ID 需要记住。

名称随便起个名，能标示清楚就行。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181646157.webp)

操作系统选择不使用任何介质。

下一步默认。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181625532.webp)

磁盘存储的话根据需求，我这里用 openwrt 就不需要太大的磁盘大小，所以给了 10G，其实也是给多了。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181626578.webp)

插槽就是 CPU，核心是线程。其实看核心总数即可，不超过你自己的 CPU 就行。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181627382.webp)

内存就看需求了，我就默认了。反正这台机器 ram 挺大的。

网络默认。有需求之后再改。

## 更改镜像

注意 PVE 是无法识别到 img 的，所以需要转换一下，也很简单。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181648309.webp)

先进入 shell 里面。

输入下面指令。需要先创建虚拟机才能执行下面的选项。

```bash
cd /var/lib/vz/template/iso/ # 进入iso镜像文件夹
ls # 看一下都有啥镜像
qm importdisk 100 镜像名字.img local-lvm # 100是你的vm id
```

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501232321657.webp)

必须得用 `importdisk` 这个指令，虽说 `qm help` 我没找到用法。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501232329381.webp)

应该是这个指令。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181654657.webp)

这样就可以在 local-vm 里面看到 vm 磁盘了，vm-100-disk-0 是咱们给他分配的，vm-100-disk-1 是咱们刚刚转换出来的。

## 开启

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181657029.webp)

进到新建的这个系统的硬件页面，可以看到多了个未使用磁盘，双击，点击添加。

所以之前的 vm id 别填错了，填错了这里就没有了。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181658964.webp)

进入选项页面，引导顺序改一改，把新加的这个放到最前面，并启用。

可以把选项里面的开机自启动勾上，因为这个系统比较基础。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181659576.webp)

进入控制台，点击 start now。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181700559.webp)

这就成功了。

# openwrt

## 修改 openwrt

输入命令

```bash
vi /etc/config/network
```

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181705344.webp)

把 lan 口的 ip 改成你需要的。

然后重启系统。也就是输入 `reboot`。

```bash
ip addr # 可以查看当前的ip
```

## 进入 openwrt

还是随便一个浏览器，输入刚才设置的 ip 地址。不用输入端口号，这里是默认端口号。

需要输入密码，随便输入个，我这里使用的是 immortal 的 openwrt 相对比较纯净，初始没密码。

在进入后才设置密码，可以设置个。

## 网络问题

用 openwrt 就是用它的丰富的软件包的，但是国内的网络无法访问。

需要进行点设置。

前提是你得有个能出去的网络作为网关。可以用手机刷机来实现，使用 magisk 来修改手机，让它作为一个小网关。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181734775.webp)

点击接口，再点击编辑。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181736064.webp)

把网关设置成那个出口的 ip 地址。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181736479.webp)

接着把 dns 改成 8.8.8.8，这一步挺重要的，不设置也大概率不成功，因为有 dns 污染。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501181734620.webp)

然后更新，就可以了。

## 安装的插件

1. luci-theme-argon 一个好看的主题，安装完后，刷新一下
2. luci-i18n-ttyd-zh-cn 控制台，其实搜索 ttyd 即可，安装完后在系统最下面就多了个终端
3. luci-app-openclash 梯子，clash，不过我经常用 passwall
4. luci-i18n-passwall-zh-cn 太大了，一般得多安几遍才行

## 成功

按完后先把梯子给配置好。

然后才把接口改成你的原本路由器的地址，这是一个旁路由。

# 飞牛OS系统

## iso

**飞牛下下来是 iso 格式的。**

**这个不用转换文件格式。**

直接在操作系统那一栏选择 iso 即可。

img 格式 pve 是不识别的。

iso 可以识别。

## pve 的磁盘问题

飞牛使用的系统盘不能作为存储磁盘。

需要在 pve 中创建个磁盘。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501240015054.webp)

在对应虚拟机的硬件页面，选择添加，添加硬盘。

选择存储和适应的磁盘大小。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501240016703.webp)

可以看到多出来个硬盘。

### 更改磁盘容量

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202501240017967.webp)

也是在硬件页面，选择想要修改的磁盘，然后点击磁盘操作，选择调整大小即可。

但是只能增加不能减少。

# 更换 IP 地址

有时候移动小主机，局域网的地址会改变，导致无法使用，

## PVE 更改地址

这个比较麻烦，需要改三个地方。

```bash
vi /etc/network/interfaces # 这个是实际上的ip地址，网关
vi /etc/issue # 这个是提示词
vi /etc/hosts # 这个是后台
```

## host 下的主机

其实都可以在 pve 系统里面进行更改。






