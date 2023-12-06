---
title: 默认包含@navtitle属性
description: 了解如何默认包含@navtitle属性
exl-id: 3def20dc-dd24-4526-ae36-45708249d34a
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 1%

---

# 默认包含@navtitle属性 {#id2115BC0J0XA}

可以在映射中添加不同类型的引用文件，例如主题、引用、任务、\(sub\)映射等。 这些文件中的大多数都支持 `@navtitle` 属性。 但是，并没有多少作者能够一致地使用它。 如果要强制使用 `@navtitle` 属性，则可以使用简单的配置完成此操作。

启用后，您在映射中添加的每个引用文件将自动获取 `@navtitle` 特性添加到其属性。 此 `@navtitle` 还将获得 `title` 引用内容的元素。

要包含 `@navtitle` 属性默认情况下，请执行以下步骤：

1. 下载ui\_config.json文件。

   您可以在全局级别或文件夹级别配置文件中进行此更改。 根据要进行此更改的位置，您需要下载相应的ui\_config.json文件。 有关下载ui\_config.json文件的更多信息，请参阅 [配置和自定义XML Web编辑器](conf-folder-level.md#id2065G300O5Z).

1. 搜索 `ditaAttributes` 定义。

   的默认定义 `ditaAttributes` 为：

   ```json
   "ditaAttributes": {
   "attributes": [],
   "constraint": false,
   "required": {}
   },
   ```

1. 更改 `required` 参数为：

   ```json
   "required": {"navtitle": true}
   ```

1. 保存文件。

1. 将文件上传到相应的配置文件\（全局或文件夹\）。


使用此配置，您添加到映射的每个参考文件将包含 `@navtitle` 属性。
