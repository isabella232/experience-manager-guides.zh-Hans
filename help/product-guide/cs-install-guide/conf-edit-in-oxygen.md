---
title: 配置选项以在氧气中进行编辑
description: 了解如何配置在氧气连接器插件中编辑的选项。
exl-id: 96081a6d-39cf-4697-8b43-6494543ea187
feature: Web Editor Configuration
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 1%

---

# 配置选项以在氧气中进行编辑

AEM Guides还允许用户在氧气连接器插件中编辑其DITA主题和DITA映射。

请按照以下说明进行操作： [配置覆盖](download-install-additional-config-override.md#) 创建配置文件。 在配置文件中，提供以下（属性）详细信息以配置 **在Oxygen中编辑** 选项：



| PID | 属性键 | 属性值 |
|---|------------|--------------|
| `com.adobe.fmdita.xmleditor.config.XmlEditorConfig` | `xmleditor.editinoxygen` | 布尔值\(true/false\)。 **默认值**： false |

>[!NOTE]
>
> 默认情况下，此配置处于禁用状态，并且选项在Web编辑器中不可用。

**父主题：**[&#x200B;自定义Web编辑器](conf-web-editor.md)
