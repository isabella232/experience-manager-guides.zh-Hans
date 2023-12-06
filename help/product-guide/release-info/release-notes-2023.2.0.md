---
title: 发行说明 | Adobe Experience Manager Guidesas a Cloud Service，2023年2月版
description: Adobe Experience Manager Guidesas a Cloud Service2月版
exl-id: c639b136-11ed-4a8b-a595-4bb5da879747
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# 2023年2月版Adobe Experience Manager Guidesas a Cloud Service

本发行说明涵盖了升级说明、兼容性矩阵，以及Adobe Experience Manager Guides版本2023年2月中修复的问题(后称为 *AEM Guidesas a Cloud Service*)。

有关新增功能和增强功能的更多信息，请参阅 [AEM Guidesas a Cloud Service版2023年2月版的新增功能](whats-new-2023.2.0.md).

## 升级到2023年2月版

通过执行以下步骤升级当前的AEM Guidesas a Cloud Service设置：
1. 查看Cloud Service的Git代码，并切换到在Cloud Service管道中配置的与要升级的环境对应的分支。
2. 更新 `<dox.version>` 中的属性 `/dox/dox.installer/pom.xml` Cloud ServiceGit代码的文件更改为2023.2.235。
3. 提交更改并运行Cloud Service管道，以升级到AEM Guidesas a Cloud Service的2023年2月版。

## 索引现有内容的步骤(仅当使用的版本早于9月份的AEM Guidesas a Cloud Service版本时)

执行以下步骤来索引现有内容，并在映射级别使用新的查找和替换文本：

* 对服务器运行POST请求（使用正确的身份验证） —  `http://<server:port>/bin/guides/map-find/indexing`.
(可选：您可以传递映射的特定路径来对其进行索引，默认情况下，所有映射都将进行索引 ||示例： `https://<Server:port>/bin/guides/map-find/indexing?paths=<map_path_in_repository>`)

* 该API将返回作业ID。 要检查作业的状态，可以将带有作业ID的GET请求发送到同一端点 —  `http://<server:port>/bin/guides/map-find/indexing?jobId={jobId}`
(例如：http://&lt;_localhost：8080_>/bin/guides/map-find/indexing？jobId=2022/9/15/7/27/7dfa1271-981e-4617-b5a4-c18379f11c42_678)

* 作业完成后，上述GET请求将做出成功响应，并提及是否有任何映射失败。 可以从服务器日志中确认已成功编制索引的映射。

## 兼容性矩阵

本部分列出了AEM Guides 2023年2月as a Cloud Service版本支持的软件应用程序的兼容性矩阵。

### FrameMaker和FrameMaker Publishing Server

| AEM Guides即云版本 | FMPS | FrameMaker |
| --- | --- | --- |
| 2023.02.0 | 不兼容 | 2022或更高版本 |
| | | |

*从2020.2开始的FMPS版本支持在AEM中创建的基线和条件。

### 氧气连接器

| AEM Guides即云版本 | 氧气连接器窗口 | 氧气连接器Mac | 在氧气窗口中编辑 | 在氧气Mac中编辑 |
| --- | --- | --- | --- | --- |
| 2023.02.0 | 2.8-uuid-8 | 2.8-uuid-8 | 2.3 | 2.3 |
|  |  |  |  |

## 修复的问题

修复了多个区域中的错误如下：

### 创作

* 在Web编辑器html中进行的更改会导致以下问题 `<dl>` 和 `<dlentry>`. (11024)
* 某些属性不会被视为条件属性，从而导致出现问题。 (10895)
* 三个或更高级别嵌套 `<indexterm>` 未嵌套在本机PDF导出中。 (10799)
* 从“创作”视图切换到“源”视图时，内容在任务正文中消失。 (10735)
* 审核评论在审核任务中放置错误。 (10625)
* **还原** 或 **重做** 在某些文件上无法正常工作。 (10373)
* 在复制和粘贴操作中，自定义元数据未保留。 (10367)
* XML编辑器中的“撤消”选项会将用户带到页面顶部。 (10091)
* 对资产执行复制和粘贴操作后，将删除节点属性。 (10053)
* mimetype是为DITA资产创建和更新进行硬编码的。 (8979)
* 对于通过Assets UI上传的文件，版本历史记录中的版本创建者名称是“fmdita-serviceuser”。 (8910)
* 在云上安装AEM Guides时，无法复制和粘贴内容片段。 (11315)
* 使用自定义架构加载内容时，浏览器（Web编辑器）冻结。 (11211)

### 管理

* 复制DITA映射资产（从资产UI ）会导致复制的资产中出现错误的基线。 (11218)
* 对于大于AEM所允许限制（默认为2 GB）的文件，上传时不会显示警告消息。 (10817)
* Web编辑器 — 基线 | Latest列的行为在Web编辑器的新基线仪表板中是不同的。 (10808)
* 翻译 |由于/libs/fmdita/i18n/ja.json无效，翻译作业未开始。 (10543)
* 翻译 |从翻译仪表板（人工翻译）创建的范围翻译项目发生错误。 (10526)
* 翻译 |对于资产位于活动翻译项目中的整个语言文件夹，后处理将被阻止。 (10332)
* 如果在基线编辑器中更改并保存了版本，则会为任何资产显示多个弹出窗口。 (10399)
* 会话泄露发生在 `com.day.cq.search.impl.builder.QueryBuilderImpl.createResourceResolver(QueryBuilderImpl.java:210)`. (10279)

### 发布

* 主题重新生成不适用于某些场景。 (10635)
* Publishlistener不在信息日志中显示请求的数据，并且还包含一些垃圾日志。( 10567)
* 本机PDF |使用“添加到文件夹配置文件”选项创建输出预设时，PDF生成失败，出现空指针异常。 (10950)
* 本机PDF |旋转表标题时出现问题。 (10555)
* 本机PDF |嵌套 `<indexterm>` 未嵌套在本机PDF导出中。 (10521)
* 本机PDF |附录中的嵌套topicref全部转换为临时HTML中的h1。 (10454)
* 对于使用FrameMaker Publishing Server2020生成的PDF，基线发布失败。 (10551)
* 本机PDF |添加 `xref` 对于图像，不会在生成的PDF上渲染图像。 (11346)
* 本机PDF |图像标记向所有图像添加display-inline属性。 (10653)
* 本机PDF |缺省情况下，在生成的输出中隐藏草稿注释。 (10560)
* 本机PDF |不对topichead授予navtitle。 (10509)
