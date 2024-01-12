---
title: 在Web编辑器中配置文件自动保存
description: 了解如何在Web编辑器中配置文件自动保存
exl-id: 23fe404c-c76d-43ba-9b28-c49ab1e524de
feature: Web Editor Configuration
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---

# 在Web编辑器中配置文件自动保存 {#id199CC0J0M5Z}

基于浏览器的编辑器中最常见的功能之一是，在特定时间段后能够保存数据。 AEM Guides的Web编辑器还支持在指定的时间间隔自动保存主题和映射文件。 触发此功能时，将保存主题或映射的工作副本。 不会创建主题或映射的新版本。 要创建新版本，您必须单击Web编辑器工具栏中的“保存修订版本”图标。

默认情况下，不会启用自动保存功能，您需要从configMgr启用此功能。 执行以下步骤以在Web编辑器中启用自动保存功能：

1. 打开Adobe Experience Manager Web控制台配置页面。

   用于访问配置页面的默认URL为：

   ```http
   http://<server name>:<port>/system/console/configMgr
   ```

1. 搜索并单击 **com.adobe.fmdita.xmleditor.config.XmlEditorConfig** 捆绑。

1. 在 *XmlEditorConfig* 设置，选择 **自动保存** 选项。

1. 在 **自动保存间隔** 字段，以秒为单位指定触发自动保存功能的时间间隔。

1. 单击&#x200B;**保存**。


**父主题：**[&#x200B;自定义Web编辑器](conf-web-editor.md)
