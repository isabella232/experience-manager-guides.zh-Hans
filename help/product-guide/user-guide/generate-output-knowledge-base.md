---
title: 知识库
description: 了解如何从Web编辑器和地图仪表板创建知识库预设。 在AEM Guides中配置知识库输出预设。
source-git-commit: 899b493709ee7f1fb31789e4afc3e985fa2505f7
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 1%

---

# 知识库 {#knowledge-base}

您可以创建 **知识库** Web编辑器中的预设：

在“存储库”面板中，打开DITA映射文件 **映射视图**，然后在 **输出** 选项卡，选择+图标以创建输出预设，然后选择 **知识库** 从 **类型** 中的下拉菜单 **新的输出预设** 对话框。 您可以命名预设，然后使用选择要生成输出的目标 **Adobe Experience Manager**， **Salesforce**，或 **ServiceNow**.




## 知识库配置{#knowledge-base-configuration}


在Web编辑器中，以下配置位于下 **常规** 和 **文章** 选项卡。 您还可以配置以下各项的设置： **知识库** 您已选择作为目标， **Adobe Experience Manager**， **Salesforce**，或 **ServiceNow**.


### 常规

| 知识库选项 | 描述 |
| --- | --- |
| 使用以下方式应用条件 | 选择以下选项之一：<br><br>* **未应用**：如果您不想对已发布的输出应用任何条件，请选择此选项。<br>* **DITAVAL文件**：选择DITAVAL文件以生成个性化内容。 您可以使用浏览对话框或键入文件路径来选择多个DITAVAL文件。 使用文件名旁边的交叉图标可将其删除。 DITAVAL文件将按指定的顺序进行计算，因此第一个文件中指定的条件优先于后续文件中指定的匹配条件。 您可以通过添加或删除文件来维护文件顺序。 如果将DITAVAL文件移动到其他位置或将其删除，则不会自动将其从预设中删除。 如果移动或删除了文件，则需要更新位置。 您可以将鼠标悬停在文件名上以查看存储该文件的Adobe Experience Manager存储库中的路径。 您只能选择DITAVAL文件，如果选择了任何其他文件类型，则会显示错误。<br>* **条件预设**：从下拉列表中选择条件预设，以在发布输出时应用条件。 如果您在DITA映射控制台的条件预设选项卡中添加了条件，则该选项可见。 要了解有关条件预设的更多信息，请查看 [使用条件预设](generate-output-use-condition-presets.md#id1825FL004PN). |
| 使用基线 | 如果已为所选DITA映射创建了基线，请选择此选项以指定要发布的版本。<br><br>视图 [使用基线](generate-output-use-baseline-for-publishing.md#id1825FI0J0PF) 以了解更多详细信息。 |
| 后期生成工作流 | 选择此选项时，将显示一个新的生成后工作流下拉列表，其中包含在Adobe Experience Manager中配置的所有工作流。 必须选择要在输出生成完成后执行的工作流。<br><br>**注意**：详细了解如何 [自定义输出后生成工作流](../cs-install-guide/customize-workflows.md#id17A6GI004Y4) Cloud Service的《安装和配置指南》中的部分。 |

### ServiceNow

| ServiceNow选项 | 描述 |
| --- | --- |
| 发布配置文件 | 使用下拉菜单从管理员配置的ServiceNow连接配置文件中进行选择。 要详细了解管理员如何创建发布配置文件，请查看 **编辑器设置** 中的功能描述 [左侧面板](./web-editor-features.md#id2051EA0M0HS) 部分。 |
| 知识库 | 使用此字段选择所需的ServiceNow知识库。 您可以在ServiceNow站点中配置知识库，以根据权限存储内容。 可以将此DITA映射中的文章发布到这些知识库。 |
| 类别和子类别 | 类别类似于用于查找和分类ServiceNow Knowledge Base文章的分层树。 添加类别和子类别，将目录的主题和子主题发布到ServiceNow站点上的该类别和子类别中。 |

### Salesforce

| Salesforce选项 | 描述 |
| --- | --- |
| 发布配置文件 | 使用下拉菜单从管理员配置的Salesforce连接配置文件中进行选择。 要详细了解管理员如何创建发布配置文件，请查看 **编辑器设置** 中的功能描述 [左侧面板](./web-editor-features.md#id2051EA0M0HS) 部分。 |
| 记录类型 | 根据基于用户配置文件的可见性设置，使用下拉菜单从Salesforce中设置的记录类型中进行选择。 Salesforce记录类型是一种为该对象分组多种类型记录的方法。 它们定义出版物的组织方式。 例如，您可以选择常见问题解答记录类型，并根据常见问题解答页面布局和字段进行发布。 |
| 文章内容字段 | 每个记录类型模板可以有不同的字段和唯一的布局。 使用这些字段可根据文章类型输入特定信息。 例如，您可以查看常见问题解答文章的标题、答案和方程式。 |
| 类别 | 从下拉列表中选择一个类别，以在Salesforce站点上发布该类别中目录的主题。 |

您还可以在Salesforce和ServiceNow预设中查看以下选项： | 选项 | 描述 | | — | — | |从文章正文中删除主题标题。|选择此选项可从已发布输出中的文章中删除主题标题。 | |上传为草稿 | 选择此选项可上传主题，以将其共享为草稿，然后再提供给用户。| |上传图像| 如果希望主题中的任何图像包含在已发布的输出中，请选择此选项。| |上传链接的文档| 选择此选项可在已发布输出中包括主题中链接的文档。|


### Adobe Experience Manager

>[!NOTE]
>
>如果管理员已配置Adobe Experience Manager知识库预设，则可以使用该预设。 有关详细信息，请查看 [从Web编辑器中基于文章的发布](../install-guide/configure-article-based-publishing.md) 安装和配置指南中的部分。

| Adobe Experience Manager选项 | 描述 |
| --- | --- |
| 使用文章路径 | 选择此选项以查看 **文章路径** 包含知识库模板的文件夹的URL。 |
| 文章路径 | 如果选择该选项，将显示此字段 **使用文章路径**. 浏览以选择Adobe Experience Manager存储库中存储输出的知识库网站。 |
| 站点 | 使用此字段选择所需的Adobe Experience Manager知识库。 您可以在Adobe Experience Manager站点中配置知识库，以根据权限存储内容。 可以将此DITA映射中的文章发布到这些知识库。 |
| 类别 | 从下拉列表中选择一个类别，以在AdobeExperience Manager站点上发布该类别中目录的主题。 |
| 区域模板和文章模板 | 这些是用于组织输出内容的结构组件。 这些是在Adobe Experience Manager站点模板中预定义的。 |
| 后期生成工作流 | 选择此选项时，将显示一个新的生成后工作流下拉列表，其中包含在Adobe Experience Manager中配置的所有工作流。 必须选择要在输出生成工作流完成后执行的工作流。<br>详细了解如何 [自定义输出后生成工作流](../install-guide/customize-workflows.md#id17A6GI004Y4) 安装和配置指南中的部分。 |
>[!TIP]
> 
>选择 **刷新** ![刷新图标](images/navtitle-refresh-icon.svg) 根据您选择的知识库模板在字段中填充相应的模板。

### 文章

此选项卡显示映射的树或分层视图。 选择要发布到知识库的主题。 展开目录节点并选择要发布的主题。

**父主题：** [了解输出预设](generate-output-understand-presets.md)
