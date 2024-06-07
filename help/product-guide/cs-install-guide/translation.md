---
title: 翻译内容
description: 了解如何翻译内容
exl-id: 5af78233-343e-47ba-b60c-b7f4789e2406
feature: Translation
role: Admin
level: Experienced
source-git-commit: bcb61127f5f69ac39860a90eac2e1a56ecd1de31
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 9%

---

# 翻译内容 {#id181GB0400UI}

自动翻译页面内容、资产和用户生成的内容，以创建和维护多语言网站。 要自动化翻译工作流，您可以将翻译服务提供商与 AEM 集成并创建项目以将内容翻译成多种语言。AEM 支持人工翻译工作流和机器翻译工作流。

- 人工翻译：内容将发送给您的翻译提供商并由专业翻译人员进行翻译。 完成后，将返回翻译的内容并将其导入 AEM。当您的翻译提供商与AEM集成时，内容会在AEM和翻译提供商之间自动交换

- 机器翻译：机器翻译服务将立即翻译您的内容


翻译内容涉及以下步骤：

1. 将AEM与您的 [翻译服务提供商](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/reusing-content/translation/integration-framework.html?lang=en) 和创建翻译集成框架配置。

1. 将语言母版页面关联到翻译服务和框架配置。

1. 识别类型 [要翻译的内容](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/reusing-content/translation/rules.html?lang=en).

1. 通过创作语言母版并创建语言副本的根页面来[准备内容以进行翻译](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/reusing-content/translation/preparation.html?lang=en)。

1. 创建 [翻译项目](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/reusing-content/translation/managing-projects.html?lang=en) 收集要翻译的内容并准备翻译过程。

1. 将翻译项目用于 [管理内容翻译](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/reusing-content/translation/managing-projects.html?lang=en) 进程。


如果翻译服务提供商不提供连接器来与AEM集成，则AEM支持以XML格式手动导出和导入已翻译内容。

>[!TIP]
>
> 请参阅 *翻译* 部分，了解翻译内容的最佳实践。

## 在DITA映射仪表板上配置翻译选项卡

要在DITA map操控板上隐藏翻译选项卡，请执行以下步骤：

1. 请按照以下说明进行操作： [配置覆盖](download-install-additional-config-override.md#) 创建配置文件。
1. 在配置文件中，提供以下\（属性\）详细信息以在映射功能板上配置翻译选项卡：

   | PID | 属性键 | 属性值 |
   |---|------------|--------------|
   | `com.adobe.fmdita.config.ConfigManager` | `tabs.translation` | 布尔值\( true/ false\)。<br> **默认值**： `true` |

   >[!NOTE]
   >
   > 默认情况下，此配置处于启用状态，并且翻译选项卡在映射功能板上不可用。


## 配置基于组件的翻译工作流

如果翻译供应商的连接器不支持DITA内容，则需要启用基于组件的翻译工作流。 启用后，可翻译内容将作为资产元数据发送。 但是，连接器需要支持此工作流的资产元数据翻译才能正常工作。

根据设置中使用的翻译工作流，应配置基于组件的翻译工作流选项。 请按照以下说明进行操作： [配置覆盖](download-install-additional-config-override.md#) 创建配置文件。 在配置文件中，提供以下\（属性\）详细信息以配置基于组件的翻译工作流：

| PID | 属性键 | 属性值 |
|---|------------|--------------|
| `com.adobe.fmdita.config.ConfigManager` | `component.translation` | 布尔型： <br>  — 如果您使用人工翻译，则 *禁用* \( `false`\) **基于组件的翻译工作流** 选项。 <br>  — 如果您使用的是机器翻译，则 *启用\( `true`\)* 该 **基于组件的翻译工作流** 选项。 |



## 配置旧版翻译工作流

建议您使用最新的翻译工作流，该工作流可提高性能。 但是，如果您要使用旧版翻译工作流，则可以对其进行配置。

请按照以下说明进行操作： [配置覆盖](download-install-additional-config-override.md#) 创建配置文件。 在配置文件中，提供以下（属性）详细信息以配置旧版翻译工作流：




| PID | 属性键 | 属性值 |
|---|------------|--------------|
| `com.adobe.fmdita.config.ConfigManager` | `translation.workflow.version.legacy` | 布尔型： <br>  — 如果您使用最新的翻译工作流，则 *禁用* \( `false`\) **运行旧版翻译工作流** 选项。 默认情况下，将启用最新的翻译工作流。 <br>  — 如果您使用旧版翻译，则 *启用\( `true`\)* 该 **运行旧版翻译工作流** 选项。 |



>[!NOTE]
>
> 如果您使用的是翻译连接器，请确保已按照 *[配置翻译集成框架](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/reusing-content/translation/integration-framework.html?lang=en)* Adobe Experience Manager主题。

>[!IMPORTANT]
>
> 设置翻译配置后，请确保在语言文件夹上设置适当的云配置。

## 配置临时语言副本的后处理

启动翻译工作流时，系统会创建源内容的临时语言副本。 您可以选择对这些临时文件启用或禁用后处理操作。 在后处理操作中，解析来自文件的传入和传出引用，设置文档状态以及其他操作。 如果对这些临时文件启用后处理，则翻译过程可能需要更长的时间才能完成。 因此，建议禁用后处理选项。

请按照以下说明进行操作： [配置覆盖](download-install-additional-config-override.md#) 创建配置文件。 在配置文件中，提供以下\(property\)详细信息以配置临时语言副本的后处理：

| PID | 属性键 | 属性值 |
|---|------------|--------------|
| `com.adobe.fmdita.config.ConfigManager` | `postprocess.temporary.langcopies` | 布尔型： <br>  — 如果不想对临时文件运行后处理操作，则 *禁用* \( false\) **后处理语言副本** 选项。<br>  — 如果要对临时文件运行后处理操作，则 *启用* \( true\) **后处理语言副本** 选项。<br> **默认值**： false |

