---
title: 默认包含@navtitle属性
description: 了解如何默认包含@navtitle属性
exl-id: 38711c0c-efa8-461a-92e1-ecfcdcdd36d3
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 1%

---

# 默认包含@navtitle属性 {#id2115BC0J0XA}

可以在映射中添加不同类型的引用文件，例如主题、引用、任务、\(sub\)映射等。 这些文件中的大多数都支持 `@navtitle` 属性。 但是，并没有多少作者能够一致地使用它。 如果要强制使用 `@navtitle` 属性，则可以使用简单的配置完成此操作。

启用后，您在映射中添加的每个引用文件将自动获取 `@navtitle` 特性添加到其属性。 此 `@navtitle` 还将获得 `title` 引用内容的元素。

要包含 `@navtitle` 属性默认情况下，请执行以下步骤：

1. 要下载UI配置文件，请以管理员身份登录到Adobe Experience Manager。

1. 单击顶部的Adobe Experience Manager链接，然后选择 **工具**.
1. 选择 **指南** 从工具列表中，单击 **文件夹配置文件**.
1. 单击 **全局配置文件** 磁贴。
1. 选择 **XML编辑器配置** 选项卡，然后单击 **编辑** 顶部图标
1. 单击 **下载** 图标，用于在本地系统上下载ui\_config.json文件。
1. 您可以在全局级别或文件夹级别配置文件中进行此更改。 根据要进行此更改的位置，您需要下载相应的ui\_config.json文件。 有关下载ui\_config.json文件的更多信息，请参阅 [配置和自定义XML Web编辑器](conf-folder-level.md#id2065G300O5Z).

1. 搜索 `ditaAttributes` 定义。

   的默认定义 `ditaAttributes` 为：

   ```
   "ditaAttributes": {
                           "attributes": [],
                           "constraint": false,
                           "required": {}
                           },
   ```

1. 更改 `required` 参数为：

   ```
   "required": {"navtitle": true}
   ```

1. 保存文件。

1. 将文件上传到相应的配置文件\（全局或文件夹\）。


使用此配置，您添加到映射的每个参考文件将包含 `@navtitle` 属性。

**父主题：**[&#x200B;自定义Web编辑器](conf-web-editor.md)
