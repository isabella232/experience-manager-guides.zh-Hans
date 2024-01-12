---
title: 根据UUID配置自动文件名
description: 了解如何根据UUID配置自动文件名
exl-id: 2a599228-6d46-494f-a57a-96c3f30e073a
feature: Filename Configuration
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 根据UUID配置自动文件名 {#id205QG070D5Z}

默认情况下，在创建主题或映射文件时，作者也可以选择指定文件名。 作者可以根据自己的要求自由分配文件名。 但是，这可能会导致不一致，并且在大型文档系统中可以看到范围广泛的文件名。 作为管理员，您可以限制作者为他们在系统中创建的文件指定文件名。 对于每个新主题或映射文件，您可以选择自动指定基于UUID的文件名。

执行以下步骤，自动为系统中创建的所有新文件指定基于UUID的文件名：

1. 打开Adobe Experience Manager Web控制台配置页面。

   用于访问配置页面的默认URL为：

   ```http
   http://<server name>:<port>/system/console/configMgr
   ```

1. 搜索并单击 *com.adobe.fmdita.xmleditor.config.XmlEditorConfig* 捆绑。

1. 选择 **使用基于UUID的系统文件名** 选项。

1. 单击&#x200B;**保存**。


>[!NOTE]
>
> 默认情况下，此选项处于关闭状态。 启用此选项后，作者在创建新主题或映射文件时，将不会看到指定文件名的选项。 可以从资产UI和Web编辑器创建新主题或映射文件。

**父主题：**[&#x200B;配置文件名](conf-file-names.md)
