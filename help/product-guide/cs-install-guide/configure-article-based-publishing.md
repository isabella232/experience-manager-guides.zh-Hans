---
title: 安装用于基于文章的发布的包
description: 了解如何安装包以进行基于文章的发布
exl-id: d83fc1a9-0822-47f0-8099-22a74b9ced2a
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# 安装用于基于文章的发布的包 {#id21BNL02052Z}

AEM Guides提供了与Web编辑器集成的强大的基于文章的发布功能。 使用此功能，您可以同时发布一个或多个主题。 在地图编辑器中打开地图后，您可以导航到输出选项卡以创建预设，然后选择一个或多个主题以生成输出。 您可以使用基于文章的发布功能递增地生成一个或多个主题的输出，或以逐篇文章的方式将内容发布到知识库平台。 有关详细信息，请参阅， *从Web编辑器部分基于文章的发布* （在用户指南中）。

要创建用于发布基于文章的输出的AEM站点，请执行以下步骤：

1. 下载 **适用于Cloud Service的XML Documentation组件内容包** 来自您的 [Adobe软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html).
1. 打开AEM包管理器。 访问包管理器的默认URL为： `https://<hostname>/crx/packmgr/index.jsp`
1. 上传用于Cloud Service的XML Documentation组件内容包，然后安装它。
1. 下载 `Knowledge-base-template-for-article-based-publishing-for-cloud-service.zip` 来自您的文件 [Adobe软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html).
1. 在全局导航中，选择 **站点**.
1. 在站点UI中，单击 **创建** 按钮进行标记。
1. 选择 **从模板创建站点** 从 **创建** 下拉菜单。
1. 单击 **导入** 按钮，然后选择 `Knowledge-base-template-for-article-based-publishing-for-cloud-service.zip` 已在您的系统上下载。 导入站点模板后，该模板将列在底部。

   >[!NOTE]
   >
   > 您只需在第一次导入ZIP文件即可。 导入后，站点模板即可在列表中找到。

   选择 **用于基于文章的发布的知识库模板** 创建AEM站点并单击 **下一个** 在右上角。

1. 输入 **网站标题** 和 **站点名称** 并单击 **创建** 在右上角。 AEM站点是使用Tragopan站点模板创建的。 \(Tragopan站点是一个示例知识库AEM站点，其中包含用于类别、分区和文章页面的模板。\)

   >[!NOTE]
   >
   > 您可以使用同一模板创建多个AEM站点。


您可以使用AEM站点通过Web编辑器中的输出预设发布文章。

**父主题：**[&#x200B;自定义Web编辑器](conf-web-editor.md)
