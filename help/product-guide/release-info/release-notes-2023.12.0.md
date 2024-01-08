---
title: 发行说明 | Adobe Experience Manager Guides（2023年12月版）中的升级说明和修复的问题
description: 了解错误修复以及如何升级到Adobe Experience Manager Guidesas a Cloud Service的2023年12月版。
source-git-commit: eb3fe92d36bc58a11e47f786a10d5938e2ed0184
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 1%

---

# 2023年12月版Adobe Experience Manager Guidesas a Cloud Service

本发行说明涵盖了升级说明、兼容性矩阵，以及Adobe Experience Manager Guidesas a Cloud Service(以后称为 *Experience Manager指南as a Cloud Service*)。

有关新增功能和增强功能的详细信息，请查看 [2023年12月版《Experience Manager指南》as a Cloud Service的新增功能](whats-new-2023.12.0.md).

## 升级到2023年12月版

通过执行以下步骤升级当前的Experience Manager指南as a Cloud Service设置：

1. 查看Cloud Service的Git代码，并切换到在Cloud Service管道中配置的与要升级的环境对应的分支。
2. 更新 `<dox.version>` 中的属性 `/dox/dox.installer/pom.xml` Cloud ServiceGit代码的文件更改为2023.12.0.15。
3. 提交更改并运行Cloud Service管道，以升级到2023年12月版的《Experience Manager指南》as a Cloud Service。

## 通过servlet启用脚本触发器的步骤

(仅限您使用的版本早于2023年6月发布的《Experience Manager指南》as a Cloud Service)

完成安装后，您可以选择点击触发器以启动翻译作业：

POST：

```
http://localhost:4503/bin/guides/script/start?jobType=translation-map-upgrade
```

响应：

```
{
"msg": "Job is successfully submitted and lock node is created for future reference",
"lockNodePath": "/var/dxml/executor-locks/translation-map-upgrade/1683190032886",
"status": "SCHEDULED"
}
```

在上一个响应JSON中，键 `lockNodePath` 保存指向在存储库中创建的指向已提交作业的节点的路径。 作业完成后会自动将其删除，然后您可以引用此节点以获取作业的状态。

请等待此作业完成，然后再继续后续步骤。

>[!NOTE]
>
> 您应该检查节点是否仍然存在，以及作业的状态。

```
GET
http://<aem_domain>/var/dxml/executor-locks/translation-map-upgrade/1683190032886.json
```

## 后处理现有内容以使用断开链接报表的步骤

(仅限您使用的版本早于2023年6月发布的《Experience Manager指南》as a Cloud Service)

执行以下步骤对现有内容进行后处理，并使用新的断开链接报表：

1. （可选）如果系统中有超过100,000个DITA文件，请更新 `queryLimitReads` 和 `queryLimitInMemory` 下 `org.apache.jackrabbit.oak.query.QueryEngineSettingsService` 设置为较大的值（任何大于现有资产数的值，例如200,000），然后重新部署。

   - 请按照 *配置覆盖* 安装和配置Adobe Experience Manager Guidesas a Cloud Service的部分，以创建配置文件。
   - 在配置文件中，提供以下（属性）详细信息以配置 `queryLimitReads` 和 `queryLimitInMemory` 选项：

     | PID | 属性键 | 属性值 |
     |---|---|---|
     | org.apache.jackrabbit.oak.query.QueryEngineSettingsService | queryLimitRead | 值：200000默认值：100000 |
     | org.apache.jackrabbit.oak.query.QueryEngineSettingsService | queryLimitInMemory | 值：200000默认值：100000 |

1. 对服务器运行POST请求（使用正确的身份验证） —  `http://<server>//bin/guides/reports/upgrade`.

1. API返回jobId。 要检查作业的状态，可以将带有作业ID的GET请求发送到同一端点 —  `http://<server>/bin/guides/reports/upgrade?jobId= {jobId}`
(例如： `http://localhost:8080/bin/guides/reports/upgrade?jobId=2022/9/15/7/27/7dfa1271-981e-4617-b5a4-c18379f11c42_678`)

1. 作业完成后，先前的GET请求会成功响应。 如果作业由于某个原因失败，则可以从服务器日志中看到失败。

1. 恢复为默认或以前的现有值 `queryLimitReads` 如果您在步骤1中更改了它。

## 为现有内容编制索引以使用“报表”选项卡下的新查找和替换以及主题列表的步骤：

(仅限您使用的版本早于2023年6月发布的《Experience Manager指南》as a Cloud Service)

执行以下步骤来索引现有内容，并在报表选项卡下的映射级别和主题列表中使用新的查找和替换文本：

1. 对服务器运行POST请求（使用正确的身份验证） —  `http://<server:port>/bin/guides/map-find/indexing`. (可选：您可以传递映射的特定路径来索引它们，默认情况下，所有映射都将索引|| 例如： `https://<Server:port>/bin/guides/map-find/indexing?paths=<map_path_in_repository>`)

1. 您还可以传递根文件夹来索引特定文件夹（及其子文件夹）的DITA映射。 例如，`http://<server:port>/bin/guides/map-find/indexing?root=/content/dam/test`。请注意，如果同时传递了路径参数和根参数，则只考虑路径参数。

1. API返回jobId。 要检查作业的状态，可以将带有作业ID的GET请求发送到同一端点 —  `http://<server:port>/bin/guides/map-find/indexing?jobId={jobId}`(例如： `http://localhost:8080/bin/guides/map-find/indexing?jobId=2022/9/15/7/27/7dfa1271-981e-4617-b5a4-c18379f11c42_678`)


1. 作业完成后，先前的GET请求会做出成功响应，并提及是否有任何映射失败。 可以从服务器日志中确认已成功编制索引的映射。

## 处理步骤 `'fmdita rewriter'` 冲突

Experience Manager指南具有 [**自定义sling重写器**](../cs-install-guide/conf-output-generation.md#custom-rewriter) 用于处理在交叉映射的情况下生成的链接的模块（两个不同映射的主题之间的链接）。

如果您的代码库中有另一个自定义sling重写器，请使用 `'order'` 值大于50，因为Experience Manager指南sling重写器使用 `'order'` 50.  要覆盖此值，您需要一个大于50的值。 有关详细信息，请查看 [输出重写管道](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html).

在此升级过程中，由于 `'order'` 值从1000更改为50，您需要将现有的自定义重写器（如果有）与 `'fmdita-rewriter'`.


## 兼容性矩阵

本部分列出了2023年12月as a Cloud ServiceExperience Manager指南所支持软件应用程序的兼容性矩阵。

### FrameMaker和FrameMaker Publishing Server

| 《Experience Manager指南as a Cloud版》 | FMPS | FrameMaker |
| --- | --- | --- |
| 2023.12.0 | 不兼容 | 2022或更高版本 |
| | | |


### 氧气连接器

| 《Experience Manager指南as a Cloud版》 | 氧气连接器窗口 | 氧气连接器Mac | 在氧气窗口中编辑 | 在氧气Mac中编辑 |
| --- | --- | --- | --- | --- |
| 2023.12.0 | 3.3-uuid.5 | 3.3-uuid.5 | 2.3 | 2.3 |
|  |  |  |  |


### 知识库模板版本

| 组件包名称 | 组件版本 | 模板版本 |
|---|---|---|
| 用于Cloud Service的Experience Manager指南组件内容包 | dxml-components.all-1.2.2 | aem-site-template-dxml.all-1.0.15 |

## 修复的问题

修复了多个区域中的错误如下：



### 创作

- 此 **标题** 在Web编辑器选项卡中，在点(.)之后被截断 字符。(14372)
- 未更新资产UI中重复映射名称的错误消息。 (14320)
- 拖放资产期间，版本创建逻辑中出错。 (14291)
- 可重用内容会跳过元素ID。 (14213)
- 要隐藏的设置控件 **语言变量** 下的面板 **输出** 缺少选项卡。 (14194)
- 在“布局”视图中使用专用架构添加新引用或主题时，Web编辑器会引发应用程序错误。 (14094)
- 指向的锚点链接 `<dlentry>` 或 `<dt>` 元素无法显示链接文本。 (13543)
- 此 **收藏夹** Web编辑器中的收藏集加载失败。 (13495)
- 如果使用带有空格的唯一ID创建引文，则会显示不可点击的链接。 (13447)
- 在 **布局** 查看书图，使用 **右移** 使选定的章节成为子元素不起作用。 (12567)
- 在Google Chrome和Microsoft Edge浏览器中，XML编辑器的预览窗口被截断。 (10755)
- Web编辑器无法将元素包装在可能的父元素中。 (8791)

### 发布

- Fmdita组件的硬编码路径为 `delegator.jsp`，防止叠加AEM Sites组件。 (13993)
- 本机PDF发布输出中PDFReactor的标记视图无法按预期工作。 (13622)
- AEM站点发布在提交到数据存储区以获取具有作用域对等链接的大型映射时遇到问题。 (13531)
- 无法使用Experience Manager指南批量发布仪表板激活站点。 (13439)
- 元素标签本地化在AEM Sites输出中无法正常工作。 (12144)
- 缺失 **ditaval** 通过Web编辑器UI创建的文件夹配置文件级别输出预设中的选项。 (11903)

### 管理

- 由于大型节点，AEM云环境遇到MongoWrite异常。 (13509)

### 翻译

- 此 **接受/拒绝** 自动批准的人工翻译会错误地显示按钮。 (14318)
- 在将非英语DITA文件转换为AEM页面时出现国际化(i18n)问题。 (14286)
- 已翻译内容无法从临时翻译项目同步，并且DITA XML编辑器翻译向导显示不正确 **进行中** 已批准作业的状态。 (9938)

### 辅助功能

- 无法在创作画布用户界面中导航，因为焦点被困在主题编辑器中。 (13517)

## 已知问题

Adobe已发现2023年12月版本的以下已知问题：
- 升级到2023年12月版本时，会间歇性地出现“获取无效的DTD错误”。