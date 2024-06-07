---
title: 发行说明 | Adobe Experience Manager Guides 4.4.0版本的升级说明
description: 了解如何升级到Adobe Experience Manager Guides的4.4.0版本
role: Leader
exl-id: 884178b6-7a72-471a-a6e3-238a543fb227
source-git-commit: 47c06dcc30b34780cbd26ded1ca400a5056a59ba
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 5%

---

# 4.4.0版（2024年1月）的升级说明

本文介绍Adobe Experience Manager Guides 4.4.0版的升级说明和兼容性矩阵。

有关新功能和增强功能的更多信息，请查看 [4.4.0 版本中的新增功能](../release-info/whats-new-4-4.md)。

有关此版本中已修复的问题的列表，请查看 [修复了4.4.0版本中的问题](../release-info/fixed-issues-4-4.md).




## 兼容性矩阵

本部分列出了Experience Manager指南4.4.0版本支持的软件应用程序的兼容性矩阵。

### Adobe Experience Manager

**4.4.0非UUID**
版本6.5 Service Pack 20、19、18或17

**4.4.0 UUID**
版本6.5 Service Pack 20、19、18或17


有关更多详细信息，请查看 [技术要求](../install-guide/download-install-technical-requirements.md) On-Premise Installation and Configuration Guide中的部分。

### FrameMaker和FrameMaker Publishing Server

| 发行版本 | FMPS 2022 | FMPS 2020 | Fm 2022 | Fm 2020 |
| --- | --- | --- | --- | --- |
| 4.4.0（非UUID） | 2022或更高版本 | 2020.2或更高版本* | 2022或更高版本 | 2020.3或更高版本 |
| 4.4.0 (UUID) | 2022或更高版本 | 2020.2或更高版本* | 2022或更高版本 | 2020.4或更高版本 |
| | | | |

*从2020.2开始的FMPS版本支持在AEM中创建的基线和条件。

### 氧气连接器

| 发行版本 | 氧气连接器窗口 | 氧气连接器Mac | 在氧气窗口中编辑 | 在氧气Mac中编辑 |
| --- | --- | --- |--- |--- |
| 4.4.0（非UUID） | 2.7-regular-1 | 2.7-regular-1 | 1.6 | 1.6 |
| 4.4.0 (UUID) | 3.4-uuid-1 | 3.4-uuid-1 | 2.3 | 2.3 |
|  |  |   |



### 知识库模板版本

| 组件包名称 | 组件版本 | 模板版本 |
|---|---|---|
| 用于Cloud Service的Experience Manager指南组件内容包 | dxml-components.all-1.2.2 | aem-site-template-dxml.all-1.0.15 |



## 升级到Experience Manager指南的4.4.0版本


您可以轻松地将指南的当前版本升级到4.4.0版。在继续升级到版本4.4.0的《Experience Manager指南》之前，您必须考虑以下几点：


- 如果您使用的是版本4.3.1、4.3.0或4.2.1（修补程序4.2.1.3），则可以直接升级到版本4.4.0。
- 如果您使用的是版本4.2、4.1或4.1.x，则在升级到版本4.4.0之前，需要升级到版本4.3.1、4.3.0或4.2.1（修补程序4.2.1.3）。
- 如果您使用的是版本4.0，则需要先升级到版本4.2，然后再升级到版本4.3.x。
- 如果您使用的是版本3.8.5，则在升级到版本4.2之前需要升级到版本4.0。
- 如果您使用的版本低于3.8.5，请参阅产品特定安装指南中的“升级Experience Manager指南”部分，该指南位于 [Adobe Experience Manager Guides帮助PDF存档](https://helpx.adobe.com/xml-documentation-for-experience-manager/archive.html).



>[!NOTE]
>
>在升级Experience Manager指南版本之前，必须安装AEM Service Pack。

有关详细信息，请查看 [内部部署版本的升级说明](../install-guide/upgrade-xml-documentation.md) Experience Manager指南。
