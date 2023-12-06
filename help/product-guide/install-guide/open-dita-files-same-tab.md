---
title: 在同一选项卡中打开DITA主题或映射文件
description: 了解如何在同一选项卡中打开DITA主题或映射文件
exl-id: 81ad2e18-3ea7-4cc1-8387-d703d1038a18
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# 在同一选项卡中打开DITA主题或映射文件 {#id223HI0P202H}

在某些工作流中，当您单击主题或映射文件的链接时，它将在新选项卡中打开。 这可能会导致在浏览器中打开许多选项卡，从而影响您的工作效率。 您可以更改在新选项卡中打开主题或映射文件的这种行为，并在当前选项卡中强制打开它。 为此，请执行以下配置更改：

1. 打开Adobe Experience Manager Web控制台配置页面。

   用于访问配置页面的默认URL为：

   ```http
   http://<server name>:<port>/system/console/configMgr
   ```

1. 搜索并单击 **com.adobe.fmdita.xmleditor.config.XmlEditorConfig** 捆绑。

1. 选择 **在同一选项卡中打开DITA主题/映射** 选项。

1. 单击&#x200B;**保存**。


此设置会影响以下位置，您可以从中访问主题或映射文件：

- 创建DITA主题\(在工作流结束时，当您单击 **打开主题** button\)

- 创建DITA映射\(在工作流结束时，当您单击 **打开地图** button\)

- DITA映射控制台中的“主题”选项卡

- DITA映射控制台中的“基线”选项卡

- DITA映射控制台中的“报表”选项卡


**父主题：**[&#x200B;自定义Web编辑器](conf-web-editor.md)
