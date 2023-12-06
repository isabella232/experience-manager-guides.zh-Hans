---
title: 发行说明 | Adobe Experience Manager Guides（2023年9月版）中的升级说明和修复的问题
description: 了解错误修复以及如何升级到Adobe Experience Manager Guidesas a Cloud Service的2023年9月版
exl-id: 795b86a0-e763-404a-a4bb-35d3d2a42672
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '1486'
ht-degree: 0%

---

# Adobe Experience Manager Guidesas a Cloud Service2023年9月版

本发行说明涵盖了升级说明、兼容性矩阵，以及Adobe Experience Manager Guides版本2023年9月中修复的问题(后称为 *AEM Guidesas a Cloud Service*)。

有关新增功能和增强功能的更多信息，请参阅 [AEM Guidesas a Cloud Service版2023年9月版的新增功能](whats-new-2023.9.0.md).

## 升级到2023年9月版

通过执行以下步骤升级当前的AEM Guidesas a Cloud Service设置：

1. 查看Cloud Service的Git代码，并切换到在Cloud Service管道中配置的与要升级的环境对应的分支。
2. 更新 `<dox.version>` 中的属性 `/dox/dox.installer/pom.xml` Cloud ServiceGit代码的文件更改为2023.9.0.359。
3. 提交更改并运行Cloud Service管道，以升级到AEM Guidesas a Cloud Service的2023年9月版。

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

本部分列出了AEM Guides 2023年9月as a Cloud Service版本支持的软件应用程序的兼容性矩阵。

### FrameMaker和FrameMaker Publishing Server

| AEM Guides即云版本 | FMPS | FrameMaker |
| --- | --- | --- |
| 2023.09.0 | 不兼容 | 2022或更高版本 |
| | | |


### 氧气连接器

| AEM Guides即云版本 | 氧气连接器窗口 | 氧气连接器Mac | 在氧气窗口中编辑 | 在氧气Mac中编辑 |
| --- | --- | --- | --- | --- |
| 2023.09.0 | 3.1-uuid 17 | 3.1-uuid 17 | 2.3 | 2.3 |
|  |  |  |  |


### 知识库模板版本

| 组件包名称 | 组件版本 | 模板版本 |
|---|---|---|
| 适用于Cloud Service的AEM Guides组件内容包 | dxml-components.all-1.2.2 | aem-site-template-dxml.all-1.0.15 |

## 修复的问题

修复了多个区域中的错误如下：

### 创作

- 虽然已选中“解锁文件”选项和“不保存”选项，但不会在Web编辑器中解锁主题文件。 (12558)
- 无法在Web编辑器中签出文件，尽管选择了NO选项以在签入前放弃更改。 (12557)
- 在Web编辑器中，主工具栏中锁定和解锁文件图标的工具提示与存储库视图中显示的图标不一致。(12555)
- 在Web编辑器中，对于尚未在“映射视图”中签出的文件，将显示“取消签出”和“解锁”选项。 (12556)
- 无法在现有“topicref”链接中选择PDF资源。 (12477)。
- 在“存储库视图”中，使用搜索/筛选功能后无法拖动主题或图像。 (12396)
- 打开一个搜索的文件后，会在“查找和替换”面板中禁用搜索结果。 (12142)
- 侧键盘上的“8”数字键在AEM Guides编辑器中不起作用。 (12106)

- 前缀在Web编辑器的预览模式下重复。 (13133)
- `Choicetable` 行不显示或无法选择。 (12616)
- 使用自定义架构创建主题时，Web编辑器在特定情况下会引发验证错误。 (12576)
- 从映射模板创建映射时，复制主题模板引用不会在内容文件夹中创建副本。 (12150)
- DITA映射中的搜索框没有关闭按钮。 (11867)
- 在Web编辑器中保存长文件时， `DirtyChecker` 引发具有长栈栈跟踪的异常，并填充日志文件。 (11860)
- 创建DITA主题需要对相应的文件夹节点具有“删除”权限，但可以使用“写入”权限创建映射。 (11706)
- 当出现斜杠时，Web编辑器显示不正确的标题。 (10949)


### 管理

- DITA映射元数据属性中的“title”字段被覆盖 `<title>` 映射的元素。 (10702)
- 当主题ID与GUID不同时，内容引用是损坏的复制粘贴DITA文件。 (12614)
- 在动态基线中，不会从DITA映射的工作副本的直接引用中提取标签列表。 (11917)

### 发布

- 重命名本机PDF预设时，发布失败。 (12564)
- 复制本机PDF模板会复制到默认模板位置，而不是提供的自定义模板位置。 (12563)

- 本机PDF |包含多个Xref可将文本扩展到列宽之外。 (13004)
- 本机PDF |当主题和标题具有相同的ID时，会导致生成的PDF输出格式不正确。 (12644)
- 本机PDF |向父级添加输出类时 `<topicref>` dita映射中的元素并将自定义样式应用于outputclass时，该样式将应用于主题正文中的元素，包括节标题。(12166)
- 如果DITA映射具有多个ditavalref，则增量发布不起作用。 (12117)
- AEM站点 |在创建映射时，使用keydef指向作为变量的主题并添加processing-role=resource-only会创建一些意外页面。 (12099)
- 如果在AEM站点以外的任何输出中使用来自AEM DAM的任何资源，则元数据“jcr：createdBy”不会反映发布者的名称或上次修改DITA映射或主题的用户的名称。 (12090)
- AEM Sites | DITA映射的navtitle中带有主题头（包含不受支持的字符）会导致页面URL无效。 (11978)
- 本机PDF |在Frontmatter和Backmatter中支持topichead / topicmeta / navtitle时出现问题。 (11969)
- 本机PDF |为大型文档生成PDF非常耗时。 (11955)
- 本机PDF |在生成PDF输出时，重命名预设会引发NullPointerException。 (11889)
- 此 `<conref>` 内容未显示在PDF输出中。 (11131)
- 在中添加额外的空间 `<div>` 在页面布局编辑器中的创作视图和源视图之间切换的元素。 (10750)
- 在AEM Cloud Manager上复制的内容在发布实例上不可见。 (9564)

### 翻译

- 导出翻译的重命名基线的过程失败。 (12993)
- 将显示已翻译文件的标题来代替源文件的标题。 (11630)
