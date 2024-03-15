---
title: 发行说明 | Adobe Experience Manager Guides 2024.2.0版本中的升级说明和修复的问题
description: 了解兼容性矩阵以及如何升级到Adobe Experience Manager Guides的2024.2.0版本as a Cloud Service。
source-git-commit: 9022b8fbae9ff9eba962ca75e25c1f1137b008f8
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 0%

---

# 2024.2.0版的升级说明

本文介绍Adobe Experience Manager Guidesas a Cloud Service2024.2.0版的升级说明和兼容性矩阵。

有关新增功能和增强功能的详细信息，请查看 [2024.2.0版本中的新增功能](whats-new-2024-2-0.md).

有关此版本中已修复的问题的列表，请查看 [修复了2024.2.0版本中的问题](fixed-issues-2024-2-0.md).


## 兼容性矩阵

本部分列出了2024.2.0版Experience Manager指南as a Cloud Service支持的软件应用程序的兼容性矩阵。

### FrameMaker和FrameMaker Publishing Server

| 《Experience Manager指南as a Cloud版》 | FMPS | FrameMaker |
| --- | --- | --- |
| 2024.2.0 | 不兼容 | 2022或更高版本 |
| | | |


### 氧气连接器

| 《Experience Manager指南as a Cloud版》 | 氧气连接器窗口 | 氧气连接器Mac | 在氧气窗口中编辑 | 在氧气Mac中编辑 |
| --- | --- | --- | --- | --- |
| 2024.2.0 | 3.5-uuid 1 | 3.5-uuid 1 | 2.3 | 2.3 |
|  |  |  |  |


### 知识库模板版本

| 组件包名称 | 组件版本 | 模板版本 |
|---|---|---|
| 用于Cloud Service的Experience Manager指南组件内容包 | dxml-components.all-1.2.2 | aem-site-template-dxml.all-1.0.15 |

## 升级到2024.2.0版

在升级Experience Manageras a Cloud Service的当前（最新）版本时，“Experience Manager指南”会自动升级。


如果您之前尚未针对现有版本对《Experience Manager指南》执行以下操作，请as a Cloud Service执行以下步骤：

### 通过servlet启用脚本触发器的步骤

(仅当您在2023年6月Experience Manager指南as a Cloud Service版本之前的版本上时)

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

### 后处理现有内容以使用断开链接报表的步骤

(仅当您在2023年6月Experience Manager指南as a Cloud Service版本之前的版本上时)

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

### 为现有内容编制索引以使用“报表”选项卡下的新查找和替换以及主题列表的步骤：

(仅当您在2023年6月Experience Manager指南as a Cloud Service版本之前的版本上时)

执行以下步骤来索引现有内容，并在报表选项卡下的映射级别和主题列表中使用新的查找和替换文本：

1. 对服务器运行POST请求（使用正确的身份验证） —  `http://<server:port>/bin/guides/map-find/indexing`. (可选：您可以传递映射的特定路径来索引它们，默认情况下，所有映射都将索引|| 例如： `https://<Server:port>/bin/guides/map-find/indexing?paths=<path of the MAP in repository>`)

1. 该API将返回作业ID。 要检查作业的状态，可以将带有作业ID的GET请求发送到同一端点 —  `http://<server:port>/bin/guides/map-find/indexing?jobId={jobId}`(例如： `http://localhost:8080/bin/guides/reports/upgrade?jobId=2022/9/15/7/27/7dfa1271-981e-4617-b5a4-c18379f11c42_678`)

1. 作业完成后，先前的GET请求会成功响应。 如果作业由于某个原因失败，则可以从服务器日志中看到失败。

1. 如果在步骤1中更改了queryLimitReads的值，请将其恢复为缺省值或上一个现有值。

### 处理步骤 `'fmdita rewriter'` 冲突

Experience Manager指南具有 [**自定义sling重写器**](../cs-install-guide/conf-output-generation.md#custom-rewriter) 用于处理在交叉映射的情况下生成的链接的模块（两个不同映射的主题之间的链接）。

如果您的代码库中有另一个自定义sling重写器，请使用 `'order'` 值大于50，因为Experience Manager指南sling重写器使用 `'order'` 50.  要覆盖此值，您需要一个大于50的值。 有关详细信息，请查看 [输出重写管道](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html).

在此升级过程中，由于 `'order'` 值从1000更改为50，您需要将现有的自定义重写器（如果有）与 `'fmdita-rewriter'`.



