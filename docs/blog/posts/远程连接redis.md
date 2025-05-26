---
date: 
  created: 2025-05-26
  updated: 2025-05-26
categories:
  - blog
authors:
  - Merlin
---

## 更改 bind 地址

正常非本机连接 redis 是无法连接成功的，会显示：

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202505172207658.webp)

只是因为 redis 只监听本机。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202505172208598.webp)

这个在 `/etc/redis/redis.conf` 中。

redis 文档太长了，可以在 vim 普通模式下，输入 `\bind` 直接找到位置。

我们只需要添加一行 `bind 0.0.0.0` 即可。

接着重启一下 redis，`systemctl restart redis`。

## 更改连接时间

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202505172221288.webp)

解决第一个问题，就出现第二个问题，显示意外结束了。

这是因为 redis 存在安全模式，默认是开启的。

当没有密码并且还是 bind 多个连接的话就会禁止非本机连接。

我们接着修改。

```shell
vim /etc/redis/redis.conf
```

使用 `/protected-mode`，然后把 yes 改成 no 即可。

重启 redis 服务：

```shell
systemctl restart redis
```

现在就可以连接了，不过**非常的不安全**。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202505172241032.webp)

## 设置密码

更为安全的方式是设置密码。

既然决定设置密码就先把上一步的安全模式再设回 `yes`。

```shell
vim /etc/redis/redis.conf
```

`\requirepass` 找到密码设置。

把注释给解掉。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202505172243898.webp)

把 foobared 换成你的密码。这个 foobared 是 foo 和 bar 的结合，表示是占位符，本身没意义。中文可能就是甲乙丙之类的。

设置完后重启 redis 服务。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202505172245744.webp)

设置一下密码就可以了。

redis 没有用户这个概念，只用输入密码就可以了。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202505172246508.webp)

显示连接成功。






