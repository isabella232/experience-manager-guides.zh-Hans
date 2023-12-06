---
title: 关于本指南
description: 了解本指南
exl-id: cdd40267-3f0c-40d2-acbc-2ebe43633c2f
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 2%

---

# 关于本指南 {#id175MC0P0S5Z}

Adobe Experience Manager Guides \(以后称为 *AEM指南*\)是一个功能强大、基于云的企业级组件内容管理解决方案\(CCMS\)。 它在Adobe Experience Manager中启用了本机DITA支持，使AEM能够处理基于DITA的内容创建和交付。 它使作者能够使用易于使用的内置Web编辑器创建内容并将其发布为各种输出格式。

本指南提供了下载、安装和配置AEM Guides的说明。 在本指南中，您将找到根据组织创作和发布需求设置AEM Guides的详细说明。

本指南适用于以下类型的受众：

- 管理员，负责安装和管理AEM Guides。

- 发布者，负责运行发布任务以生成各种格式的输出。


## 内容结构

本指南中的信息组织如下：

- [关于本指南](#id175MC0P0S5Z)：本主题介绍了本指南、目标受众以及本指南中信息的组织方式。

- [下载并安装](download-install.md#)：本主题介绍如何下载、安装或升级AEM Guides。

- [用户管理和安全性](user-admin-sec.md#)：本主题介绍AEM中用户和身份验证的核心概念以及AEM Guides创建的默认用户组。

- [使用自定义DITA-OT和DITA专业化](dita-ot-specialization.md#)：本主题介绍如何配置自定义DITA-OT插件和使用DITA专业化。

- [配置文档状态](customize-doc-state.md#)：本主题介绍如何为DITA文档配置自定义状态。

- [迁移现有内容](migrate-content.md#)：本主题介绍如何在AEM存储库中载入现有内容。

- [配置文件名](conf-file-names.md#)：本主题介绍如何配置设置以自动分配文件名并定义有效文件名字符的正则表达式。

- [配置主题和映射模板](conf-template-tags.md#)：本主题介绍如何配置主题和映射模板以满足您的创作需求。 了解AEM中的标记系统以及如何配置标记以用于AEM Guides。

- [自定义Web编辑器](conf-web-editor.md#)：本主题介绍您可以在Web编辑器中进行的各种自定义设置，以增强其功能。

- [默认包含@navtitle属性](auto-add-navtitle.md#)：本主题介绍如何添加 `@navtitle` 默认情况下，属性为映射中的引用文件。

- [配置全局或文件夹级别的配置文件](conf-folder-level.md#)：本主题介绍创建文件夹配置文件和向特定用户授予权限的过程。

- [版本管理](version-management.md#)：本主题介绍如何为在Web编辑器中打开进行编辑的文件配置自动文件签出。

- [配置输出生成设置](conf-output-generation.md#)：本主题介绍可以进行的各种配置，用于自定义默认输出生成过程。

- [配置和自定义工作流](customize-workflows.md#)：本主题介绍用于自定义AEM Guides中提供的默认工作流的各种配置。

- [翻译内容](translation.md#)：本主题提供了指向AEM文档中的相关帮助文章的链接，以帮助您了解和配置翻译框架。 此外，了解如何启用基于组件的翻译工作流。

- [配置AEM Assets UI搜索](conf-dita-search.md#)：本主题介绍如何在Assets UI中配置DITA内容搜索并在搜索中添加自定义属性。


## Adobe Experience Manager概述\(AEM\)

[Adobe Experience Manager \(AEM\)](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html) 是一个用于构建网站、移动应用程序和表单的综合性内容管理解决方案。 AEM可帮助您管理营销内容和资源。 AEM可as a Cloud Service使用。 AEMas a Cloud Service通过将AEM Content Management System与AEM Digital Asset Management的强大功能结合起来，帮助您向客户提供以内容为导向的个性化体验。以下为一些可帮助您开始使用并部署到AEMas a Cloud Service的关键资源：

- [Experience Manageras a Cloud Service概述](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/home.html?lang=en)
- [迁移到AEMas a Cloud Service历程快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/getting-started.html?lang=en)
- [开始载入Experience Manageras a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/home.html?lang=enhttps://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html?lang=en)
- [实施 AEM as a Cloud Service 的应用程序](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/home.html?lang=en)
- [部署到 AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=en)
- [Assetsas a Cloud Service指南](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/home.html?lang=cn)

## 其他资源

以下是AEM Guides的其他有用资源的列表，这些资源位于 [学习和支持](https://helpx.adobe.com/support/xml-documentation-for-experience-manager.html) 页面：

- 用户指南
- API参考指南
