---
title: 本机PDF发布功能 | 对目录条目和主题内容应用自定义样式
description: 了解如何为内容创建使用样式表和样式。
exl-id: f65c9683-a1fc-432a-854b-83e8f39d7dae
feature: Output Generation
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# 对目录条目和主题内容应用自定义样式

有时，您可能希望对目录条目或特定主题应用自定义样式。 这可以通过关联 `outputclass` 属性和 `<topicref>` DITA映射中的元素。 此外，如果要将自定义格式应用于整个主题，则也可以通过在CSS中扩展属性的样式定义来实现该目的。

让我们以您要发送以供审阅的新主题为例。 为便于识别更新的主题，您需要添加 `outputclass` 归因于 `<topicref>` 元素，然后在CSS中为其定义自定义样式。

在以下示例中， *航班历史记录* 主题已分配 `outputclass` 属性值为的属性 `new-topic`.

<img src="./assets/new-topic-attribute-in-map.png" width="500">

的类定义 `new-topic` 在CSS中，您可以为以下项目定义样式：
* 目录或迷你目录中的主条目
* 主内容中主题的标题
* 主题的整个内容，包括标题

让我们看看如何在CSS中定义每种场景。 在以下CSS定义中， `new-topic` 类，文本颜色已更改。

```css
…
.new-topic {
  color: #CC5309
}
…
```

此定义控制目录中的文本颜色和主题标题。 以下PDF输出显示应用于目录条目的不同颜色：

<img src="./assets/pdf-output-toc-entry.jpg" width="500">

主题的标题也使用相同的颜色进行样式设置。

<img src="./assets/pdf-output-topic-title.jpg" width="500">

如果希望目录条目和主题的标题具有不同的样式，则可以分别定义它们，如下所示：

```css
...
/*for styling TOC entry */
.new-topic {
  color: #CC3509
}

/* for styling topic's title */
.new-topic.title {
  color: #092ACC
}
...
```

最后，您还可以在主题的整个内容中应用样式。 为此，您需要添加后缀»`-content`”到类名。 在以下示例中，更改栏已添加到主题的整个内容中：

```css
...
/* for styling the topic's content */
.new-topic-content {
  -ro-change-bar-color: #A609CC;
}
...
```

使用上述样式属性，更改栏将添加到 *飞行历史记录* 主题，如下所示：

<img src="./assets/pdf-output-topic-content.jpg" width="500">
