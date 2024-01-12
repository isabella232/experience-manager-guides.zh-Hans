---
title: 在Web编辑器中配置文件自动保存
description: 了解如何在Web编辑器中配置文件自动保存
exl-id: 4d99c3d8-cf6a-4cf3-aaec-9009a0376c1e
feature: Web Editor Configuration
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 1%

---

# 在Web编辑器中配置文件自动保存 {#id199CC0J0M5Z}

基于浏览器的编辑器中最常见的功能之一是，在特定时间段后能够保存数据。 AEM Guides Web Editor还支持在指定的时间间隔自动保存主题和映射文件。 触发此功能时，将保存主题或映射的工作副本。 不会创建主题或映射的新版本。 要创建新版本，您必须单击Web编辑器工具栏中的“保存修订版本”图标。

默认情况下，不会启用自动保存功能，您需要使用配置文件启用该功能。

请按照以下说明进行操作： [配置覆盖](download-install-additional-config-override.md#) 创建配置文件。 在配置文件中，提供以下\(property\)详细信息以配置文件的自动保存和自动保存时间间隔：

| PID | 属性键 | 属性值 |
|---|------------|--------------|
| `com.adobe.fmdita.xmleditor.config.XmlEditorConfig` | `xmleditor.autosave` | 布尔值\(true/false\)。<br> **默认值**： false |
| `xmleditor.autosaveinterval` | 以秒为单位指定触发自动保存功能的时间间隔。 |

**父主题：**[&#x200B;自定义Web编辑器](conf-web-editor.md)
