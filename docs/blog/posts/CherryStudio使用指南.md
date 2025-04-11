---
title: CherryStudio 使用指南
date:
  created: 2025-04-01
  updated: 2025-04-11
categories:
  - AI
authors:
  - Merlin
---
# CherryStudio 使用指南
# 为什么使用？

CherryStudio 就相当于一个 AI 的合集，能够集合多模型对话，知识库管理，AI 绘画等各种功能的一个集合工具。

而且内容都是本地的，隐私性是拉满了。

当然，主要目的还是为了提升工作效率。

# 下载

[客户端下载 | CherryStudio](https://cherry-ai.com/download)

直接进入该网站进行下载。

# 安装

双击下载的 exe 文件。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012318426.webp)

为所有用户安装，点击下一步。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012318092.webp)

可以更改一下路径，不用默认安装在 C 盘。

点击安装。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012318405.webp)

这就安装成功了，十分的简单。

# 使用

接下来就是如何使用。

其实也可以看[官方的文档](https://docs.cherry-ai.com/pre-basic/providers/a-li-yun-bai-lian)

## 添加模型

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012321180.webp)

点击右下角的设置按钮。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012322927.webp)

在模型服务这里就可以添加各种大模型了。

我们可以使用 API 调用大模型或者使用本地部署的模型。

### API 调用

这个其实非常的简单。

以硅基流动为例子。

注册一下账号，进入 API 秘钥页面。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012326895.webp)

创建 API 秘钥，然后复制一下 API 填入下面的输入框中。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012328702.webp)

可以点一下检查，随便选个模型，来看 API是否有效。

然后点击右上角的开关。

这时硅基流动旁边会出现一个绿色的 `on`，表示模型开启。

### 本地调用

这里以 Ollama 为例，当然 LM Studio 也可以使用。

Ollama 本地部署的可以看我这一篇博客[使用ollama管理模型](使用ollama管理模型.md)。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012333274.webp)


API 秘钥不用填写。

你要是调用的本地的，API 地址就不用动。

如果是其他机器的，就把 localhost 改为对应的地址。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012334850.webp)

然后点击添加。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012334976.webp)

这里填写模型的名字，这儿需要查看一下 ollama 的文档，模型ID 不是随便起名的，需要相对应。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012336926.webp)

这里我使用 deepseek-r1:14b 的模型。

### 测试使用

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012342673.webp)

回到最开始的界面，上面可以切换已经加入的模型，下面与之聊天，我这里使用的是本地部署的 deepseek。

接下来就可以愉快的对话了。

## 联网功能

有时候需要使用大模型阅读一些网页或者搜索一些东西，这时候就需要大模型具有联网的功能。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012343953.webp)

这其中有一些大模型是自带联网功能的，就看你的 LLM 旁边有没有带这个小的🌐网络图标, 比如这个 `Gemini 2.0 Flash` 就是自带联网功能。

但是像是本地部署的模型，还有 DeepSeek 模型是不自带联网功能的，这时候就需要添加联网的模型。

### 添加网络搜索

这里我使用 tavily。

Tavily 是一款用于增强搜索引擎能力的人工智能驱动工具，它可以帮助用户更快速、更准确地找到所需信息。

使用起来也十分简单。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012347015.webp)

还是打开设置，选择网络搜索，搜索服务上默认就是 Tavily。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012355024.webp)


打开 Tavily 网页，直接使用 Google 登录，然后复制一下 API Keys 填入上图的 API 秘钥输入框就可以联网用大模型了。

不过要注意一下 credits，免费给了 1000 个，每搜索一次消耗一个。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012356077.webp)

也可以设置一下搜索设置，可以把增强模式打开。

### 使用

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012357363.webp)

先打开输入框下方的🌐。

这里使用 DeepSeek 进行提问，可以看到现在可以联网了。

提问的语言不同，也会给出相应的答复，比如上方用中文提问，给出的就是 B 站的教程。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504012359341.webp)

使用英文提问，给的就是油管。

给的链接数目跟上方设置的**搜索结果个数**有关，默认是 5 个，最高是 20 个。

## 数据设置

没什么用，就是把对话保存一下。

目前我觉得没什么用。

# 知识库

我个人认为没什么大用。

# 迁移配置

我有多台电脑，可能需要在多处使用 cherrystudio，但就看上面的博客，就知道配置起来还是比较麻烦的。

不过所幸，cherrystudio 给了迁移配置的功能，我们可以快速迁移配置到不同的电脑上。

## 备份

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504072321750.webp)

打开设置，选择数据设置，第一个就是。

选择备份，选择一个文件夹去保存备份。

## 使用备份

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504072322611.webp)

这就是另一台电脑了，可以看到什么都没有设置，还是数据设置这里，这次点击恢复。

选择刚才备份的文件，是一个*zip*文件。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504072322617.webp)

然后等待数据恢复，可能会有些慢。

![](https://tree-1327913400.cos.ap-nanjing.myqcloud.com/imgs/202504072323589.webp)

等待片刻，可以看到数据已经迁移了，我们不必再麻烦一次进行多处配置了。
