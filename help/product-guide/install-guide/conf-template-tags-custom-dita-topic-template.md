---
title: 配置自定义DITA主题模板
description: 了解如何配置自定义DITA主题模板
exl-id: a9b2c479-7bf6-4c62-addd-fdfe74dc1f69
feature: Template Configuration
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 2%

---

# 配置自定义DITA主题模板 {#id16A7G0O02TD}

AEM Guides附带以下DITA主题模板：

- 主题

- 任务

- 概念

- 引用

- 术语表

- 疑难解答

- 空白


可根据创作要求使用任意这些模板来创建主题模板。 空白DITA模板不包含与其它模板类似的任何结构或元素。 如果模板是高度自定义的并且不基于任何常规DITA主题模板，则可以使用“空白”模板作为基础。

要自定义DITA主题模板并将其用于创作，您需要执行以下三个主要任务：

1. *\（可选\）* [配置自定义DITA模板文件夹路径](#id191LCF0095Z)

1. [创建自定义创作模板](conf-folder-level.md#id1917D0EG0HJ)

1. 将自定义模板添加到全局或文件夹级别的配置文件中，如 [配置创作模板](conf-folder-level.md#id1889D0IL0Y4) 部分


## 配置自定义DITA模板文件夹路径 {#id191LCF0095Z}

AEM Guides允许您配置文件夹以存储自定义的DITA映射和模板。 默认情况下，模板文件存储在DAM的以下文件夹中：

`/content/dam/dita-templates/`

要管理主题和映射模板文件，有专用的文件夹用于存储主题和映射模板。 默认情况下，所有主题模板都存储在 `/content/dam/dita-templates/topics`

文件夹。 所有映射模板都存储在 `/content/dam/dita-templates/maps` 文件夹。

作为管理员，您可以选择在默认文件夹中创建自定义映射或主题模板，或者创建自己的文件夹来存储自定义模板。 如果您计划使用默认文件夹，则可以跳过此过程。

要为自定义DITA主题模板配置文件夹，请执行以下步骤：

>[!IMPORTANT]
>
> 如果要使用默认文件夹存储自定义模板，则可以跳过此过程。

1. 打开Adobe Experience Manager Web控制台配置页面。

   用于访问配置页面的默认URL为：

   ```http
   http://<server name>:<port>/system/console/configMgr
   ```

1. 搜索并单击 *com.adobe.fmdita.config.ConfigManager* 捆绑。

1. 在 **模板位置** 属性，指定存储自定义模板的位置。

1. 单击&#x200B;**保存**。


如果DAM中存在指定的位置，则所有默认映射和主题模板都将复制到该文件夹中。 如果该位置不存在，则使用所有默认映射和主题模板创建文件夹。

**父主题：**[&#x200B;配置主题和映射模板](conf-template-tags.md)
