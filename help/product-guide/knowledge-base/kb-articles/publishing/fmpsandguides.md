---
title: AEM Guides中的使用FrameMaker Publishing Server(FMPS)发布
description: 使用AEM Guides通过FMPS发布
exl-id: 05d4d876-f83b-473c-bf31-14d6565e80e2
source-git-commit: eb3fe92d36bc58a11e47f786a10d5938e2ed0184
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# AEM Guides中的使用FrameMaker Publishing Server(FMPS)发布

如果您希望获得高质量的自动发布功能，AEM Guides与FrameMaker Publishing Server集成可能是您的解决方案。\
文章可帮助您设置和运行带有AEM Guides的FMPS。

## FMPS与AEM Guides的兼容性

- 与4.1 AEM Guides的兼容性： [4.1兼容性矩阵](https://experienceleague.adobe.com/docs/experience-manager-guides-learn/tutorials/release-info/release-notes/on-prem-release-notes/release-notes-4.1.html?lang=en/#compatibility-matrix)
- 与4.0 AEM Guides的兼容性： [4.0兼容性矩阵](https://helpx.adobe.com/xml-documentation-for-experience-manager/release-note/release-notes-xml-documentation-solution-4-0.html/#Compatibility%20matrix)
- 最新版本： [最新版本信息](https://experienceleague.adobe.com/docs/experience-manager-guides-learn/tutorials/release-info/latest-release-info.html?lang=en)

## 安装

有关AEM Guides和FMPS的安装与配置，请参阅以下内容

### AEM指南

安装和配置请参阅： [4.1安装和配置](https://helpx.adobe.com/content/dam/help/en/xml-documentation-solution/4-1-2/Adobe-Experience-Manager-Guides_Installation-Configuration-Guide_EN.pdf)

### FMPS

对于FMPS安装，您可以参考给定的 [YouTube链接](https://www.youtube.com/watch?v=2deelyM5VA8&amp;t) 或 [FMPS安装和配置](https://help.adobe.com/en_US/framemaker/server/index.html#t=fmps-user-guide%2Finstall_config_fmps.html%23install_config_fmps&amp;rhtocid=_2)

## 所需的配置

FrameMaker Publishing Server(FMPS)可用于生成DITA内容。 FMPS支持多种输出格式。 在Web控制台中修改“com.adobe.fmdita.config.ConfigManager捆绑包”的以下属性，将AEM Guides配置为使用FMPS。

要打开Web控制台，请转到URL Access http://\&lt;server name=&quot;&quot;>：\&lt;port>/system/console/configMgr。

**配置属性及其说明** [4.1安装和配置](https://helpx.adobe.com/content/dam/help/en/xml-documentation-solution/4-1-2/Adobe-Experience-Manager-Guides_Installation-Configuration-Guide_EN.pdf#page=89)

## 正在运行测试：

使用FMPS，您可以自动发布 **PDF，响应式HTML5**、和 **埃布** 用于DITA和FM资产。

从“使用生成PDF”菜单中，选择“FrameMaker Publishing Server”。

用户可以提供“settings File(.sts)”和“ditaval”。 根据您提供的条件，使用域进行筛选。

- **设置文件**：一个FrameMaker/FMPS发布设置文件，其中包含您希望FMPS在发布时遵循的所有设置。 例如，使用自定义模板创建输出，创建“标记和出血”(PDF)，以及使用TOC创建PDF。
- **FMPS预设：** 它是预定义的ditaval和设置文件组合。 用户可以预先创建FMPS预设，而不是提供单独的视图和设置文件，可以重复使用这些预设来满足发布需求。

**注意：** 如果您未选择任何设置或FMPS预设，则FMPS会使用默认系统设置进行发布。

如果您选择了FMPS预设，并且还从AEM提供了自定义设置或Ditaval文件，则会发生冲突。 在这种情况下，FMPS预设优先于自定义设置或二进制文件。

### 使用FMPS的基线发布：

您可以使用FMPS2020.0.2或更高版本发布已创建的基线。

**开始使用的FMPS设置文件（.sts文件）示例：** [FMPS设置文件示例](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:ef750752-7a7e-4e51-923e-6b7d9861ed54) （解压缩此文件）

## 常见问题解答和疑难解答：

- ### FMPS发布失败，出现“超时异常”

>检查并增加/system/console/configMgr/com.adobe.fmdita.config.ConfigManager中的“FMPS超时”（秒）值

- ### 无法在下拉列表中获取FMPS预设

>确保在服务器上创建了预定义的FMPS预设，并且您的连接设置正确。

- ### 发布时我收到空白PDF

>如果您使用的是UUID，请确保您已在FrameMaker编辑首选项中选中“使用基于UUID的引用”，并反之选中非UUID AEM指南的引用。

- ### 我的设置/对话框未应用于最终发布的输出

>确认您未同时选择FMPS预设和设置/Diaval文件。 使用FrameMaker手动检查输出。

- ### 未从FMPS发布基线

>FMPS2020.0.2或更高版本与基线发布兼容。
>确保正确创建了基线；要进行检查，请转到“映射仪表板 — 主题 — 下载映射”并选择“使用基线”。
- ### 从FMPS发布任务所花费的时间比其他引擎多

>从FMPS发布时，理想的固定标头时间约为3 - 4分钟；如果您认为时间更长，请联系FMPS管理员或联系Adobe支持部门。

## 其他资源：

[FMPS学习和支持](https://helpx.adobe.com/support/framemaker-publishing-server.html)

[AEM Guides学习和支持](https://helpx.adobe.com/in/support/xml-documentation-for-experience-manager.html)

[FrameMaker和FMPS社区](https://community.adobe.com/t5/framemaker/ct-p/ct-framemaker?page=1&amp;sort=latest_replies&amp;lang=all&amp;tabid=all)

[AEM Guides社区](https://experienceleaguecommunities.adobe.com/t5/experience-manager-guides/ct-p/aem-xml-documentation)
