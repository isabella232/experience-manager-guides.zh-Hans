---
title: 配置文件名
description: 了解如何为上传到Adobe Experience Manager Assets的文件夹禁用后处理
feature: Filename Configuration
role: Admin
level: Experienced
source-git-commit: 532e7c562a233619a8c4b7cbdbaef44bc73eb4b2
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# 禁用文件夹的后处理

默认情况下，所有上传的资产都使用DAM更新资产工作流进行处理。 作为此工作流的一部分，Experience Manager指南会运行一项称为后处理的额外处理。 这还有助于生成UUID

将文件和文件夹上传到 *Adobe Experience Manager Assets* 服务器中，您还可以禁用后处理和UUID生成。


执行以下步骤可禁用给定路径的后处理或忽略文件夹的后处理：


1. 打开Adobe Experience Manager Web控制台配置页面。

   用于访问配置页面的默认URL为：

   ```http
   http://<server name>:<port>/system/console/configMgr
   ```

1. 搜索并单击 **com.adobe.fmdita.config.ConfigManager** 捆绑。

1. 选择 **后处理中忽略的路径** 选项，忽略文件夹以进行后处理。

   用于设置任何标准NODE_patches(多值OPTIONS)的字符串值，带有省略路径的字符串 `/` 在末尾)

   **默认值**： `/content/dam/projects/translation_output`

   >[!NOTE]
   >
   > 默认情况下，此属性处于禁用状态，并且地图功能板上提供翻译选项卡。

1. 选择 **已启用后处理的路径** 选项，启用后处理路径。

   用于设置任何标准NODE_patches(多值OPTIONS)的字符串值，带有省略路径的字符串 `/` 在末尾)

   **默认值**： `/content/dam/`

   >[!NOTE]
   >
   > 默认情况下，此属性处于禁用状态，并且地图功能板上提供翻译选项卡。


1. 单击&#x200B;**保存**。



## 启用或禁用后处理的规则

默认情况下，会对Experience ManagerDAM文件夹下的每个文件夹路径执行后处理。 根据以下规则为任何文件夹应用配置：

* 如果忽略父文件夹进行后处理，但启用了子文件夹，则子文件夹及其所有后续文件夹均被视为已启用。
* 如果为父项启用后处理，但忽略子项，则将忽略子项及其所有后续项。
* 如果ignored.post.processing.paths和enabled.post.processing.paths配置中存在相同的文件夹路径，则后处理时会将其忽略。
