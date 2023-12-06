---
title: 发行说明 | Adobe Experience Manager Guides（2023年7月版）中的升级说明和修复的问题
description: 了解错误修复以及如何升级到Adobe Experience Manager Guidesas a Cloud Service的2023年7月版
exl-id: f1765c6a-cb8e-4a06-a6f4-f5c225b6bc88
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 1%

---

# 2023年7月版Adobe Experience Manager Guidesas a Cloud Service

本发行说明涵盖了升级说明、兼容性矩阵，以及2023年7月版Adobe Experience Manager Guides(以后称为 *AEM Guidesas a Cloud Service*)。

有关新增功能和增强功能的更多信息，请参阅 [AEM Guidesas a Cloud Service版2023年7月版的新增功能](whats-new-2023.7.0.md).

## 升级到2023年7月版

通过执行以下步骤升级当前的AEM Guidesas a Cloud Service设置：

1. 查看Cloud Service的Git代码，并切换到在Cloud Service管道中配置的与要升级的环境对应的分支。
2. 更新 `<dox.version>` 中的属性 `/dox/dox.installer/pom.xml` Cloud ServiceGit代码的文件更改为2023.7.0.314。
3. 提交更改并运行Cloud Service管道，以升级到AEM Guidesas a Cloud Service的2023年7月版本。

## 通过servlet启用脚本触发器的步骤

(仅限您使用的版本早于2023年6月发布的AEM Guidesas a Cloud Service)

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

在上一个响应JSON中，键 `lockNodePath` 保存指向在存储库中创建的指向已提交作业的节点的路径。 作业完成后该节点会被自动删除，在此之前，您可以引用此节点以获取作业的当前状态。

请等待此作业完成，然后再继续后续步骤。

>[!NOTE]
>
> 您应该检查节点是否仍然存在，以及作业的状态。

```
GET
http://<aem_domain>/var/dxml/executor-locks/translation-map-upgrade/1683190032886.json
```

## 后处理现有内容以使用断开链接报表的步骤

(仅限您使用的版本早于2023年6月发布的AEM Guidesas a Cloud Service)

执行以下步骤后处理现有内容并使用新的断开链接报表：

1. （可选）如果系统中有超过100,000个dita文件，请更新 `queryLimitReads` 下 `org.apache.jackrabbit.oak.query.QueryEngineSettingsService` 设置为较大的值（任何大于现有资产数的值，例如200,000），然后重新部署。

   - 请按照以下说明进行操作： *配置覆盖* 安装和配置Adobe Experience Manager Guidesas a Cloud Service的部分，以创建配置文件。
   - 在配置文件中，提供以下（属性）详细信息以配置queryLimitReads选项：

     | PID | 属性键 | 属性值 |
     |---|---|---|
     | org.apache.jackrabbit.oak.query.QueryEngineSettingsService | queryLimitRead | 值：200000默认值：100000 |

1. 对服务器运行POST请求（使用正确的身份验证） —  `http://<server:port>//bin/guides/reports/upgrade`.

1. 该API将返回作业ID。 要检查作业的状态，可以将带有作业ID的GET请求发送到同一端点 —  `http://<server:port>/bin/guides/reports/upgrade?jobId= {jobId}`
(例如： `http://localhost:8080/bin/guides/map-find/indexing?jobId=2022/9/15/7/27/7dfa1271-981e-4617-b5a4-c18379f11c42_678`)

1. 作业完成后，先前的GET请求将做出成功响应。 如果作业由于某个原因失败，则可以从服务器日志中看到失败。

1. 恢复为默认或以前的现有值 `queryLimitReads` 如果您在步骤1中更改了它。

## 为现有内容编制索引以使用“报表”选项卡下的新查找和替换以及主题列表的步骤：

(仅限您使用的版本早于2023年6月发布的AEM Guidesas a Cloud Service)

执行以下步骤来索引现有内容，并在报表选项卡下的映射级别和主题列表中使用新的查找和替换文本：

1. 对服务器运行POST请求\（使用正确的身份验证\） - `http://<server:port\>/bin/guides/map-find/indexing`. (可选：您可以传递映射的特定路径来索引它们，默认情况下，所有映射都将索引\|\|例如： `https://<Server:port\>/bin/guides/map-find/indexing?paths=<map\_path\_in\_repository\>`)

1. 您还可以传递根文件夹来索引特定文件夹（及其子文件夹）的DITA映射。 例如，`http://<server:port\>/bin/guides/map-find/indexing?root=/content/dam/test`。请注意，如果同时传递了路径参数和根参数，则只考虑路径参数。

1. 该API将返回作业ID。 要检查作业的状态，可以将带有作业ID的GET请求发送到同一端点 —  `http://<server:port\>/bin/guides/map-find/indexing?jobId=\{jobId\}`\(例如： `http://localhost:8080/bin/guides/map-find/indexing?jobId=2022/9/15/7/27/7dfa1271-981e-4617-b5a4-c18379f11c42`\)


1. 作业完成后，先前的GET请求将做出成功响应，并提及是否有任何映射失败。 可以从服务器日志中确认已成功编制索引的映射。

## 兼容性矩阵

本部分列出了AEM Guides 2023年7月as a Cloud Service版本支持的软件应用程序的兼容性矩阵。

### FrameMaker和FrameMaker Publishing Server

| AEM Guides即云版本 | FMPS | FrameMaker |
| --- | --- | --- |
| 2023.07.0 | 不兼容 | 2022或更高版本 |
| | | |


### 氧气连接器

| AEM Guides即云版本 | 氧气连接器窗口 | 氧气连接器Mac | 在氧气窗口中编辑 | 在氧气Mac中编辑 |
| --- | --- | --- | --- | --- |
| 2023.07.0 | 2.9-uuid-2 | 2.9-uuid-2 | 2.3 | 2.3 |
|  |  |  |  |


## 修复的问题

修复了多个区域中的错误如下：

### 创作

- 内联/显示属性不会显示在Web编辑器的“布局”视图中。 (12498)
- 如果存在，则在用于AEM Guides的氧气插件中上传文件在Cloud Service中将不起作用！ 文件名中的。 (12207)
- 使用可编辑模板时，DITA映射发布速度非常慢。 (12075)
- 全局配置文件UI配置与文件夹配置文件不匹配。 (11970)
- 复制和粘贴DITA文件时会破坏内容引用。 (11959)
- 安装AEM Guides后无法在列视图中编辑内容片段。 (7342)
- 当未包装的xref位于子元素标记下时，内容丢失。 (12532)

### 发布

- 当docstate从右侧面板的“文件”属性更改为“结束状态”时，审批工作流不起作用。 (11026)
