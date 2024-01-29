---
title: 发行说明 | Adobe Experience Manager Guides（2024年2月版）中的升级说明和修复的问题
description: 了解错误修复以及如何升级到Adobe Experience Manager Guidesas a Cloud Service的2024年2月版。
source-git-commit: a04b1aa28bda0c0da1770eaff8b385721e20654d
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 0%

---

# 2024年2月版Adobe Experience Manager Guidesas a Cloud Service

本发行说明涵盖了升级说明、兼容性矩阵，以及Adobe Experience Manager Guidesas a Cloud Service(以后称为 *Experience Manager指南as a Cloud Service*)。

有关新增功能和增强功能的详细信息，请查看 [2024年2月版《Experience Manager指南》as a Cloud Service的新增功能](whats-new-2024.02.0.md).

## 升级到2024年2月版

通过执行以下步骤升级当前的Experience Manager指南as a Cloud Service设置：

1. 查看Cloud Service的Git代码，并切换到在Cloud Service管道中配置的与要升级的环境对应的分支。
2. 更新 `<dox.version>` 中的属性 `/dox/dox.installer/pom.xml` Cloud ServiceGit代码的文件更改为2024.02.0.15。
3. 提交更改并运行Cloud Service管道，以升级到2024年2月版的《Experience Manager指南》as a Cloud Service。

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

1. 对服务器运行POST请求（使用正确的身份验证） —  `http://<server:port>/bin/guides/map-find/indexing`. (可选：您可以传递映射的特定路径来索引它们，默认情况下，所有映射都将索引|| 例如： `https://<Server:port>/bin/guides/map-find/indexing?paths=<path of the MAP in repository>`)

1. 该API将返回作业ID。 要检查作业的状态，可以将带有作业ID的GET请求发送到同一端点 —  `http://<server:port>/bin/guides/map-find/indexing?jobId={jobId}`(例如： `http://localhost:8080/bin/guides/reports/upgrade?jobId=2022/9/15/7/27/7dfa1271-981e-4617-b5a4-c18379f11c42_678`)

1. 作业完成后，先前的GET请求会成功响应。 如果作业由于某个原因失败，则可以从服务器日志中看到失败。

1. 如果在步骤1中更改了queryLimitReads的值，请将其恢复为缺省值或上一个现有值。

## 处理步骤 `'fmdita rewriter'` 冲突

Experience Manager指南具有 [**自定义sling重写器**](../cs-install-guide/conf-output-generation.md#custom-rewriter) 用于处理在交叉映射的情况下生成的链接的模块（两个不同映射的主题之间的链接）。

如果您的代码库中有另一个自定义sling重写器，请使用 `'order'` 值大于50，因为Experience Manager指南sling重写器使用 `'order'` 50.  要覆盖此值，您需要一个大于50的值。 有关详细信息，请查看 [输出重写管道](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html).

在此升级过程中，由于 `'order'` 值从1000更改为50，您需要将现有的自定义重写器（如果有）与 `'fmdita-rewriter'`.


## 兼容性矩阵

本部分列出了2024年2月版Experience Manager指南as a Cloud Service支持的软件应用程序的兼容性矩阵。

### FrameMaker和FrameMaker Publishing Server

| 《Experience Manager指南as a Cloud版》 | FMPS | FrameMaker |
| --- | --- | --- |
| 2024.02.0 | 不兼容 | 2022或更高版本 |
| | | |


### 氧气连接器

| 《Experience Manager指南as a Cloud版》 | 氧气连接器窗口 | 氧气连接器Mac | 在氧气窗口中编辑 | 在氧气Mac中编辑 |
| --- | --- | --- | --- | --- |
| 2024.02.0 | 3.1-uuid.17 | 3.1-uuid.17 | 2.3 | 2.3 |
|  |  |  |  |


### 知识库模板版本

| 组件包名称 | 组件版本 | 模板版本 |
|---|---|---|
| 用于Cloud Service的Experience Manager指南组件内容包 | dxml-components.all-1.2.2 | aem-site-template-dxml.all-1.0.15 |

## 修复的问题

修复了多个区域中的错误如下：

### 创作

- 编辑器中的拼写检查不允许选择建议。 (15045)
- 全局导航按钮不起作用，无法加载仪表板。 (14968)
- 在Web编辑器中，下载映射功能在可以下载时无法触发弹出通知。 (14626)
- 在Web编辑器中，下载映射功能无法下载带有基线的映射。 (14622)
- Experience Manager指南as a Cloud Service版本2310中的DTD错误无效。 (14482)
- 将词汇表主题从存储库拖到词汇表映射中会创建 `topicref`. (10767)
- 重新安装Adobe Experience Manager Guides版本4.3.1后，将卸载Web编辑器。 (14519)
- 4.3.1版本的安装程序遇到过滤器冲突，导致覆盖 `apps/cq/core/content/projects/properties`. (14517)
- 片段的预览屏幕已冻结。 (14840)

### 发布

- 在本机PDF发布中，条件预设中的自定义属性不适用于本机PDF发布。 (14943)
- 无法从添加自定义模板 **输出** 选项卡。 (14846)
- **AEM站点** 由于模板路径为空，预设无法正常工作。 (14804)
- 对于主题包含MathML方程式的DITA映射，AEM站点重新生成失败。 (14790)
- 在本机PDF发布中，PDF生成过程在获取依赖关系时抛出错误 `Node.js` 发布。 (14445)
- AEM预设不允许选择模板位于 `/content` Web编辑器中的层次结构。 (14260)
- 在AEM Sites输出中，的样式或换行符丢失 `<lines>` 具有子元素的元素。(12542)
- 自定义元数据在最终输出中不可用。 (12116)
- 升级到版本4.3.1时，本机PDF节点中会出现一些异常。 (14492)


### 管理

- **基线筛选器** 文件无法在Web编辑器中使用文件名。 (13486)
- 禁用父DITA map的索引以获取更好的性能可能会影响某些功能的功能。(12213)
- 标签来自 `labels.json` 文件在Web编辑器中以随机顺序显示。 (10508)

### 审查

- 右键单击上下文菜单不起作用 **Accept** 或 **拒绝** 跟踪更改。 (14607)
- 在Adobe Experience Manager Guides 4.3.1版中，在审阅屏幕中切换以关闭DITA主题不起作用。 (14537)
- 自定义审核工作流的电子邮件模板不适用于叠加。 (13954)

## 已知问题

Adobe已为2024年2月版本发现以下已知问题：

- 对于重复的DITA文件，版本1.0不会显示在UI上。
