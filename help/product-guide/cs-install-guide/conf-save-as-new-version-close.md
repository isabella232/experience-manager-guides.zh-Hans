---
title: 配置关闭时另存为新版本的提示
description: 了解如何配置关闭时另存为新版本的提示
exl-id: 9029b671-8ff8-45eb-b27e-ab89bd09e7ed
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 1%

---

# 配置关闭时另存为新版本的提示 {#id222HBI00XXA}

当用户尝试关闭在Web编辑器中打开的文件时 **关闭** 文件选项卡上的按钮或 **关闭** 选项，如果文件具有未保存的数据或未保存的版本，将出现一个对话框。 如果未保存该版本，则提示用户将文件另存为新版本。

请按照以下说明进行操作： [配置覆盖](download-install-additional-config-override.md#) 创建配置文件。 在配置文件中，提供以下\(property\)详细信息以配置关闭时另存为新版本的提示：

| PID | 属性键 | 属性值 |
|---|------------|--------------|
| `com.adobe.fmdita.xmleditor.config.XmlEditorConfig` | `xmleditor.savenewversion` | 布尔值\( true/ false\)。 <br>  **默认值**： true |

启用此配置后， **另存为新版本** 该复选框在对话框中默认处于选中状态。

有关更多详细信息，请参阅 *文件关闭并保存方案* 部分(位于使用Adobe Experience Manager Guidesas a Cloud Service指南中)。

**父主题：**[&#x200B;自定义Web编辑器](conf-web-editor.md)
