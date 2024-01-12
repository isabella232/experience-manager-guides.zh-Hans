---
title: 为有效的文件名字符配置Regx
description: 了解如何为有效的文件名字符配置Regx
exl-id: 05e9ca3c-28ff-4f82-8061-3d20307890ff
feature: Filename Configuration
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# 为有效的文件名字符配置Regx {#id214BD0550E8}

从AEM Guides 3.8版本开始，作为管理员，您可以定义文件名中允许的有效特殊字符列表。 在早期版本中，允许用户定义包含特殊字符的文件名，例如 `@`， `$`， `>`，等等。 这些特殊字符在DITA映射仪表板中打开主题或单击目录中的主题链接时会导致问题，这通常会导致URL中的特殊字符导致页面无法打开。

使用允许您为有效文件名字符定义regx的配置，您可以完全控制如何在系统中命名文件。 您可以定义文件名中允许使用的特殊字符列表。 默认情况下，有效的文件名配置包含&#39;&#39;`a-z A-Z 0-9 - _`“。 创建新文件时，文件的标题中可以包含任何特殊字符，但在内部，它将被替换为&quot;`-`“（在文件名中）。 例如，文件的标题可以是“Introduction 1”或“Introduction@1”，针对这两种情况生成的相应文件名是“Introduction-1”。

定义有效字符列表时，请记住这些字符»`*/:[\]|#%{}?&<>"/+`”将始终替换为“`-`“。

如果未配置有效的特殊字符列表，文件创建过程可能会给您一些意外的结果。 为避免此类错误，强烈建议更改此配置。

请按照以下说明进行操作： [配置覆盖](download-install-additional-config-override.md#) 创建配置文件。 在配置文件中，提供以下\(property\)详细信息以配置有效文件名字符的正则表达式：

| PID | 属性键 | 属性值 |
|---|------------|--------------|
| `com.adobe.fmdita.xmleditor.config.XmlEditorConfig` | `valid.characters` | 该值是一个正则表达式模式。 它必须具有三个基本字符，并且列表必须以连字符\(-\)开头。<br> **默认值**： \[-a-zA-Z0-9\_\] |

>[!NOTE]
>
> 与有效文件名字符列表类似，您还可以为AEM Site输出指定有效文件名字符列表。 有关更多详细信息，请参阅 [为AEM站点输出配置有效文件名](conf-file-names-valid-regx-aem-site-output.md#).

**父主题：**[&#x200B;配置文件名](conf-file-names.md)
