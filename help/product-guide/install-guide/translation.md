---
title: AEM Guides中的翻译内容
description: 了解如何翻译内容
exl-id: 0d3a909c-3499-4ef4-b033-02e412dae959
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 9%

---

# 翻译内容 {#id181GB0400UI}

自动翻译页面内容、资产和用户生成的内容，以创建和维护多语言网站。 要自动化翻译工作流，您可以将翻译服务提供商与 AEM 集成并创建项目以将内容翻译成多种语言。AEM 支持人工翻译工作流和机器翻译工作流。

- 人工翻译：内容将发送给您的翻译提供商并由专业翻译人员进行翻译。 完成后，将返回翻译的内容并将其导入 AEM。当您的翻译提供商与AEM集成时，内容会在AEM和翻译提供商之间自动交换

- 机器翻译：机器翻译服务将立即翻译您的内容


翻译内容涉及以下步骤：

1. 将AEM与您的 [翻译服务提供商](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/tc-tic.html#ConnectingtoaTranslationServiceProvider) 和创建 [翻译集成框架配置](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/tc-tic.html#CreatingaTranslationIntegrationConfiguration).

1. 将语言母版页面与 [翻译服务和框架配置](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/tc-tic.html#ConfiguringPagesforTranslation).

1. 识别类型 [要翻译的内容](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/tc-rules.html).

1. 通过创作语言母版并创建语言副本的根页面来[准备内容以进行翻译](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/tc-prep.html)。

1. 创建 [翻译项目](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/tc-manage.html) 收集要翻译的内容并准备翻译过程。

1. 将翻译项目用于 [管理内容翻译](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/tc-manage.html) 进程。


如果翻译服务提供商不提供连接器来与AEM集成，则AEM支持以XML格式手动导出和导入已翻译内容。

>[!TIP]
>
> 请参阅 *翻译*&#x200B;最佳实践指南中的部分，以了解有关翻译内容的最佳实践。

## 在DITA映射仪表板上配置翻译选项卡

默认情况下，“隐藏翻译选项卡”选项未启用，您需要从configMgr中启用它。 要在DITA map操控板上隐藏翻译选项卡，请执行以下步骤：

1. 打开Adobe Experience Manager Web控制台配置页面。

   用于访问配置页面的默认URL为：

   ```http
   http://<server name>:<port>/system/console/configMgr
   ```

1. 搜索并单击 **com.adobe.fmdita.config.ConfigManager** 捆绑。

1. 选择 **隐藏翻译选项卡** 选项，以在映射仪表板上隐藏翻译选项卡。

   >[!NOTE]
   >
   > 默认情况下，此属性处于禁用状态，并且地图功能板上提供翻译选项卡。

1. 单击&#x200B;**保存**。

## 配置基于组件的翻译工作流

如果翻译供应商的连接器不支持DITA内容，则需要启用基于组件的翻译工作流。 启用后，可翻译内容将作为资产元数据发送。 但是，连接器需要支持此工作流的资产元数据翻译才能正常工作。

根据设置中使用的翻译工作流，基于组件的翻译工作流选项应配置如下：

1. 打开Adobe Experience Manager Web控制台配置页面。

   用于访问配置页面的默认URL为：

   ```http
   http://<server name>:<port>/system/console/configMgr
   ```

1. 搜索并单击 **com.adobe.fmdita.config.ConfigManager** 捆绑。

1. 配置 **基于组件的DITA翻译工作流** 选项（根据您的设置）：

   - 如果您使用人工翻译，则 *禁用* 该 **基于组件的翻译工作流** 选项。

   - 如果您使用的是机器翻译，则 *启用* 该 **基于组件的翻译工作流** 选项。

   >[!NOTE]
   >
   > 如果您使用的是翻译连接器，请确保已按照 *[配置翻译集成框架](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/tc-tic.html)* AEM主题。

1. 单击&#x200B;**保存**。


>[!IMPORTANT]
>
> 设置翻译配置后，请确保在语言文件夹上设置适当的云配置。

## 配置临时语言副本的后处理

启动翻译工作流时，系统会创建源内容的临时语言副本。 您可以选择对这些临时文件启用或禁用后处理操作。 在后处理操作中，解析来自文件的传入和传出引用，设置文档状态以及其他操作。 如果对这些临时文件启用后处理，则翻译过程可能需要更长的时间才能完成。 因此，建议禁用后处理选项。

默认情况下，“临时文件的后处理”选项处于禁用状态。 可以通过执行以下步骤来配置此选项：

1. 打开Adobe Experience Manager Web控制台配置页面。

   用于访问配置页面的默认URL为：

   ```http
   http://<server name>:<port>/system/console/configMgr
   ```

1. 搜索并单击 **com.adobe.fmdita.config.ConfigManager** 捆绑。

1. 配置 **后处理语言副本** 选项（根据您的设置）：

   - \(*默认*\)如果不想对临时文件运行后处理操作，则 *禁用* 该 **后处理语言副本** 选项。

   - 如果要对临时文件运行后处理操作，则 *启用* 该 **后处理语言副本** 选项。

1. 单击&#x200B;**保存**。
