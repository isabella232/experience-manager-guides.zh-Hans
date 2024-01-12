---
title: 自动生成元素ID
description: 了解如何自动生成元素ID
exl-id: 8d09ab89-4be5-49f1-9831-9f01c92dc472
feature: Web Editor Configuration
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# 自动生成元素ID {#id20CIL40016I}

AEM Guides会为您创建的任何新文档生成文档ID。 例如，创建DITA映射时，ID如下所示 `map.ditamap_random_digits` 会分配到地图的ID。 您还可以定义自动为其生成和分配ID的元素。

AEM Guides提供了简单的配置设置，您需要在其中定义自动生成ID的元素以及ID的模式。 默认情况下，某些元素包括 `section`， `table`， `ul`， `ol`，配置为自动生成ID。 您可以向此列表中添加其他元素，以便每当在文档中插入这些元素时，AEM Guides都会根据给定的模式生成并分配ID

执行以下步骤以将元素配置为具有自动生成的ID：

1. 打开Adobe Experience Manager Web控制台配置页面。

   用于访问配置页面的默认URL为：

   ```http
   http://<server name>:<port>/system/console/configMgr
   ```

1. 搜索并单击 **com.adobe.fmdita.xmleditor.config.XmlEditorConfig** 捆绑。

1. 在 *XmlEditorConfig* 设置，在 **为元素标记自动生成ID** 字段。

   >[!NOTE]
   >
   > 元素标记是DITA元素名称，例如 `body`， `title`， `codeblock`，等等。 要指定多个元素，请使用逗号分隔元素名称。

1. 在&#x200B;**用于生成ID的模式** 字段，指定要生成ID的模式。

   此字段的默认值设置为 `${elementName}_${id}`. 此 `${elementName}` 值将替换为元素的名称。 此 `${id}` 变量会为元素生成序列号。 例如，如果指定段落元素具有自动生成的ID，则主题或文档中的第一个段落将获得p\_1等ID，下一个段落将获得p\_2等。 但是，在另一个文档中，ID生成过程将重新启动。 这意味着，在另一个文档中，可以将p\_1和p\_2等ID分配给段落元素。

   如果文档已包含指定模式的ID，则自动生成过程不会将这些ID分配给新元素。

1. 单击&#x200B;**保存**。


**父主题：**[&#x200B;自定义Web编辑器](conf-web-editor.md)
