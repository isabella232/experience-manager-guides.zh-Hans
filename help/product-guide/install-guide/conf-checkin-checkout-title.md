---
title: 配置签入和签出图标的标题
description: 了解如何配置签入和签出图标的标题
exl-id: a8888a17-e819-4fa2-bb6f-cafe1002803a
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 配置签入和签出图标的标题

AEM Guides允许您在Web编辑器中配置签入和签出图标的标题。 执行以下步骤来配置检入和检出图标的标题：

1. 以管理员身份登录Adobe Experience Manager以下载用户界面配置文件。
1. 单击顶部的Adobe Experience Manager链接，然后选择 **工具**.
1. 选择 **指南** 从工具列表中，单击 **文件夹配置文件**.
1. 单击 **全局配置文件** 磁贴。
1. 选择 **XML编辑器配置** 选项卡，然后单击 **编辑** 图标。
1. 在 **XML编辑器UI配置** 部分，单击 **下载** 图标以下载 `ui_config.json` 文件。
1. 在 `ui_config.json` 文件，更改“顶栏”部分中的标题。 您可以更改以下值：

   ```json
   //Change title to "Check out" instead of "Lock"
           "title": "Check out"
   
   //Change title to "Check in" instead of "@checkOutBy
            "title": "Check in"
   ```

1. 保存文件并将其上传。
