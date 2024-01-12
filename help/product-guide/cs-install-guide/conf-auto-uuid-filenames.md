---
title: 根据UUID配置自动文件名
description: 了解如何根据UUID配置自动文件名
exl-id: bdbdf119-b928-4ed2-bab3-d99370da8aa9
feature: Filename Configuration
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 1%

---

# 根据UUID配置自动文件名 {#id205QG070D5Z}

默认情况下，在创建主题或映射文件时，作者也可以选择指定文件名。 作者可以根据自己的要求自由分配文件名。 但是，这可能会导致不一致，并且在大型文档系统中可以看到范围广泛的文件名。 作为管理员，您可以限制作者为他们在系统中创建的文件指定文件名。 对于每个新主题或映射文件，您可以选择自动指定基于UUID的文件名。

请按照以下说明进行操作： [配置覆盖](download-install-additional-config-override.md#) 创建配置文件。 在配置文件中，提供以下\(property\)详细信息以根据UUID配置自动文件名：

| PID | 属性键 | 属性值 |
|---|------------|--------------|
| `com.adobe.fmdita.xmleditor.config.XmlEditorConfig` | `xmleditor.uniquefilenames` | 布尔值\(true/false\)。<br> **默认值**： false |

>[!NOTE]
>
> 启用此选项后，作者在创建新主题或映射文件时，将不会看到指定文件名的选项。 可以从资产UI和Web编辑器创建新主题或映射文件。

**父主题：**[&#x200B;配置文件名](conf-file-names.md)
