---
title: 配置单主题PDF生成
description: 了解如何配置单主题PDF生成
exl-id: 5b66fd3b-6450-49ce-b06e-d2d5bab37990
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# 配置单主题PDF生成 {#id22ADC70M0XA}

使用AEM Guides，可以生成单个主题的PDF或整个映射文件。 您可以使用本机PDF或DITA-OT方法以PDF格式发布主题。 使用本机PDF方法，根据W3C CSS3和CSS分页PDF标准生成功能丰富的媒体输出。 可以使用DITA-OT方法从映射操控板为映射生成PDF输出。

>[!NOTE]
>
> 本机PDF是在当前版本的AEM Guides中生成PDF的默认方法。

要在主题预览模式下通过DITA-OT启用旧PDF生成，请执行以下步骤：

1. 以管理员身份登录Adobe Experience Manager并下载用户界面配置文件。

1. 为此，请单击顶部的Adobe Experience Manager链接，然后选择 **工具**.
1. 选择 **指南** 从工具列表中，单击 **文件夹配置文件**.
1. 单击 **全局配置文件** 磁贴。
1. 选择 **XML编辑器配置** 选项卡，然后单击 **编辑** 顶部图标
1. 单击 **下载** 图标，用于在本地系统上下载ui\_config.json文件。 然后，您可以对文件进行更改，然后上传相同的更改。
1. 在 `ui_config.json` 文件，查找以下配置：

   ```
   {
                           "component": "button",
                           "variant": "action",
                           "quiet": true,
                           "icon": "filePDF",
                           "title": "Download as PDF",
                           "on-click": "EDITOR_SAVE_AS_PDF"
                           }
   ```

   并将其替换为

   ```
   {
                           "component": "button",
                           "icon": "filePDF",
                           "variant": "action",
                           "quiet": true, "title": "Export as PDF",
                           "on-click": "DOWNLOAD_TOPIC_PDF",
                           "show" : ["@isPreviewMode", "@isXmlMode"]
                           }
   ```

1. 保存文件并将其上传。

执行上述给定步骤后，如果从Web编辑器的“用户首选项”中选择相同的文件夹配置文件，则将在主题的预览模式下看到用于生成PDF的选项。

**父主题：**[&#x200B;自定义Web编辑器](conf-web-editor.md)
