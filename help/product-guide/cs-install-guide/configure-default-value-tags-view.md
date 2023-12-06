---
title: 配置标记视图的默认值
description: 了解如何为标记视图配置默认值
exl-id: 3ab75101-4c23-4e45-bfcf-76c1f5b92c96
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# 配置标记视图的默认值 {#id223GN0M0NDC}

AEM Guides允许您在Web编辑器中配置“标记视图”的默认状态，这有助于在默认情况下为新用户的会话打开或关闭标记视图。执行以下步骤来配置“标记视图”的默认值：

1. 以管理员身份登录Adobe Experience Manager以下载用户界面配置文件。
1. 单击顶部的Adobe Experience Manager链接，然后选择 **工具**.
1. 选择 **指南** 从工具列表中，单击 **文件夹配置文件**.
1. 单击 **全局配置文件** 磁贴。
1. 选择 **XML编辑器配置** 选项卡，然后单击 **编辑** 图标。
1. 在 **XML编辑器UI配置** 部分，单击 **下载** 图标以下载 `ui_config.json` 文件。
1. 在 `ui_config.json` 文件，通过更改defaultValues部分来更改默认标记视图状态，如下所示：

```
"defaultValues":
                {
                "tagsView": true
                }
```

1.) 保存文件并将其上传。

>[!NOTE]
>
> 用户在Web编辑器中启用/禁用标记视图的首选项优先于此默认值。 因此，如果用户从Web编辑器启用标记视图，则即使跨会话，该视图也会保持启用状态。

**父主题：**[&#x200B;自定义Web编辑器](conf-web-editor.md)
