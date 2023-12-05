---
title: 内部部署安装
description: 了解如何下载、安装和配置AEM指南。
exl-id: 90d5ad94-eb68-4d73-9b23-a1f3d4b802ba
source-git-commit: 02b33615669945cf65f70d6fd2de81bfd340a0ab
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# 内部部署安装 {#id175MC0P0S5Z}

Adobe Experience Manager Guides \(以后称为 *AEM指南*\)是一个功能强大、企业级组件内容管理解决方案\(CCMS\)。 它在Adobe Experience Manager中启用了本机DITA支持，使AEM能够处理基于DITA的内容创建和交付。 它使作者能够使用任何离线DITA创作工具(如Adobe FrameMaker或易于使用的内置Web编辑器)创建内容。

本指南提供了下载、安装和配置AEM Guides的说明。 在本指南中，您将找到根据组织创作和发布需求设置AEM Guides的详细说明。

本指南适用于以下类型的受众：

- 管理员，负责在Adobe Experience Manager上安装和管理AEM Guides。

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

- [将高级映射编辑器设置为默认值](conf-map-editor.md#id194GHE0I0CW)：本主题介绍如何配置高级映射编辑器作为映射文件的默认编辑器。

- [默认包含@navtitle属性](auto-add-navtitle.md#)：本主题介绍如何添加 `@navtitle` 默认情况下，属性为映射中的引用文件。

- [配置全局或文件夹级别的配置文件](conf-folder-level.md#)：本主题介绍创建文件夹配置文件和向特定用户授予权限的过程。

- [版本管理](version-management.md#)：本主题介绍如何为在Web编辑器中打开进行编辑的文件配置自动文件签出。

- [集成基于桌面的XML编辑器](integrate-desktop-editors.md#)：本主题介绍在外部XML编辑器中启用编辑文档所需的设置。

- [配置输出生成设置](conf-output-generation.md#)：本主题介绍可以进行的各种配置，用于自定义默认输出生成过程。

- [配置和自定义工作流](customize-workflows.md#)：本主题介绍用于自定义AEM Guides中提供的默认工作流的各种配置。

- [翻译内容](translation.md#)：本主题提供了指向AEM文档中的相关帮助文章的链接，以帮助您了解和配置翻译框架。 此外，了解如何启用基于组件的翻译工作流。

- [配置AEM Assets UI搜索](conf-dita-search.md#)：本主题介绍如何在Assets UI中配置DITA内容搜索并在搜索中添加自定义属性。


## 其他资源

以下是AEM Guides的其他有用资源的列表，这些资源位于 [学习和支持](https://helpx.adobe.com/support/xml-documentation-for-experience-manager.html) 页面：

- 用户指南
- API参考指南
- 快速入门指南
- [“帮助存档”页](https://helpx.adobe.com/xml-documentation-for-experience-manager/archive.html) \（访问旧版发行文档\）
