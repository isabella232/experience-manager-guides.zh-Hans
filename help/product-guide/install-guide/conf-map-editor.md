---
title: 将高级映射编辑器设置为默认值
description: 了解如何将高级映射编辑器设置为默认值
exl-id: ecc023f6-48eb-4afd-97a2-4b3cdd5a8991
feature: Web Editor Configuration
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# 将高级映射编辑器设置为默认值 {#id181AI0003PN}

AEM Guides附带基本映射编辑器和高级映射编辑器。 基本映射编辑器为您提供了创建映射文件所需的所有功能。 高级映射编辑器功能更丰富，并且集成在Web编辑器中。 高级映射编辑器允许作者使用易于使用的界面创建和编辑DITA映射文件。

默认情况下，每当创建新映射文件时，都会在“基本映射编辑器”中打开该文件。 通过启用默认打开“高级映射编辑器”的设置，可以更改此行为。

执行以下步骤，使高级映射编辑器成为映射文件的默认编辑器：

1. 打开Adobe Experience Manager Web控制台配置页面。

   用于访问配置页面的默认URL为：

   ```http
   http://<server name>:<port>/system/console/configMgr
   ```

1. 搜索并单击 **com.adobe.fmdita.xmleditor.config.XmlEditorConfig** 捆绑。

1. 选择 **隐藏基本映射编辑器** 选项。

   选中此选项后，用户将看不到用户界面中任何位置的“基本映射编辑器”链接。 默认情况下，映射文件将在高级映射编辑器中打开。
