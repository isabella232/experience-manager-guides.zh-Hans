---
title: 如何添加 [!DNL AEM Guides] 敬您的 [!DNL AEM as a Cloud Service] 环境
description: 了解如何添加 [!DNL AEM Guides] 敬您的 [!DNL AEM as a Cloud Service] 环境
exl-id: a1e020c2-360c-4d71-b5fd-8179d9ceacda
feature: Installation
role: Leader
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# [!DNL AEM Guides] as a Cloud Service部署

了解如何添加 [!DNL Guides] 敬您的 [!DNL AEM as a Cloud Service] 环境。

## 通过Cloud Manager Git管道手动部署

如果您已购买 [!DNL AEM Guides] 与2022年3月29日之前as a Cloud Service，请按照以下部署说明操作：

* 如果您是全新开始的，则可以替换自动生成的代码 [!UICONTROL Cloud Manager] 使用已集成XML插件的以下存储库中的代码：https://github.com/Adobe-TCS/XML-documentation-for-AEMaaCS

* 如果您在中已经签入了自定义项 [!UICONTROL Cloud Manager] git存储库，您可以参考以下存储库，了解如何在现有代码中添加XML插件的说明：https://github.com/Adobe-TCS/DoX-Installer-for-AEMaaCS

## 通过Cloud Manager部署

如果您是已购买的客户 [!DNL AEM Guides] 与在2022年3月29日或之后as a Cloud Service，请按照以下说明添加 [!DNL Guides] 敬您的 [!DNL AEM as a Cloud Service] 环境：

1. 登录 [!UICONTROL Cloud Manager].

1. 编辑要配置的程序 [!DNL AEM Guides].

1. 切换到 **[!UICONTROL 解决方案和加载项]** 选项卡。

1. 在 **[!UICONTROL 解决方案和加载项]** 表，单击 **[!UICONTROL 资产]**.

1. 选择 **[!UICONTROL 指南]** 并选择 **[!UICONTROL 保存]**.

您已成功配置程序以自动配置AEM Guides解决方案。

![配置AEM Guides解决方案](assets/addon-configuration.png)

>[!NOTE]
>
>安装 [!DNL AEM Guides] 在集成程序下的任何环境中，必须运行与该环境关联的管道。 在CM Git代码库中无需额外配置即可安装 [!DNL AEM Guides].
