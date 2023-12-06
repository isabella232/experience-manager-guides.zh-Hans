---
title: 在Web编辑器中配置翻译功能
description: 了解如何在Web编辑器中配置翻译功能
exl-id: e25473c3-9a84-4658-87c9-6fd72bcaa2b6
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# 在Web编辑器中配置翻译功能 {#id21BONI0J0YR}

Web编辑器提供强大的翻译功能，可将您的内容翻译成多种语言。

您可以使用 **管理** 选项卡，以翻译您的内容。 默认情况下，此选项卡可用。

要隐藏 **管理** 选项卡中，执行以下步骤：

1. 登录 **Adobe Experience Manager** 作为管理员。
1. 单击 **Adobe Experience Manager** 在顶部链接，然后选择 **工具**.
1. 选择 **指南** 从工具列表中，单击 **文件夹配置文件**.
1. 单击 **全局配置文件** 磁贴。
1. 单击 **XML编辑器配置**.
1. 单击 **编辑** 图标。
1. 下载 `ui\_config.json` 文件。从下载的文件中删除以下代码片段：

   ```json
   {
       "component":"tab",
       "id":"workflow",
       "title":"Manage",
       "on-click":"APP_MODE_CHANGE",
       "items":
       [
           {
               "component":"label",
               "label":"Manage"
           }
       ]
   },
   ```

1. 上传更新的ui\_config.json文件。

请注意 **管理** 过滤器不再可用。

**父主题：**[&#x200B;自定义Web编辑器](conf-web-editor.md)
