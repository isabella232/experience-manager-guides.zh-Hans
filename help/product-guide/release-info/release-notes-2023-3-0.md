---
title: 发行说明 | Adobe Experience Manager Guidesas a Cloud Service，2023年3月版
description: Adobe Experience Manager Guidesas a Cloud Service3月版
exl-id: 6a0bba92-7d7d-4b20-ad46-0eacc91268da
feature: Release Notes
role: Leader
source-git-commit: 6d8c01f20f7b59fed92c404561b647d9ebecb050
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# 2023年3月版Adobe Experience Manager Guidesas a Cloud Service

本发行说明涵盖了升级说明、兼容性矩阵，以及2023年3月版Adobe Experience Manager Guides中修复的问题(后称为 *AEM Guidesas a Cloud Service*)。

有关新增功能和增强功能的更多信息，请参阅 [AEM Guidesas a Cloud Service版2023年3月版的新增功能](whats-new-2023-3-0.md).

## 升级到2023年3月版

通过执行以下步骤升级当前的AEM Guidesas a Cloud Service设置：

1. 查看Cloud Service的Git代码，并切换到在Cloud Service管道中配置的与要升级的环境对应的分支。
1. 更新 `<dox.version>` 中的属性 `/dox/dox.installer/pom.xml` Cloud ServiceGit代码的文件更改为2023.3.242。
1. 提交更改并运行Cloud Service管道，以升级到AEM Guidesas a Cloud Service的2023年3月版。

## 索引现有内容的步骤(仅当使用的版本早于9月份的AEM Guidesas a Cloud Service版本时)

执行以下步骤来索引现有内容并在映射级别使用新的查找和替换文本：

* 对服务器运行POST请求（使用正确的身份验证） —  `http://<server:port>/bin/guides/map-find/indexing`.
(可选：您可以传递映射的特定路径来对其进行索引，默认情况下，所有映射都将进行索引 || 示例： `https://<Server:port>/bin/guides/map-find/indexing?paths=<map_path_in_repository>`)

* 该API将返回作业ID。 要检查作业的状态，可以将带有作业ID的GET请求发送到同一端点 —  `http://<server:port>/bin/guides/map-find/indexing?jobId={jobId}`
(例如：http://&lt;_localhost：8080_>/bin/guides/map-find/indexing？jobId=2022/9/15/7/27/7dfa1271-981e-4617-b5a4-c18379f11c42_678)

* 作业完成后，上述GET请求将做出成功响应，并提及是否有任何映射失败。 可以从服务器日志中确认已成功编制索引的映射。

## 兼容性矩阵

本部分列出了AEM Guides 2023年3月as a Cloud Service版本支持的软件应用程序的兼容性矩阵。

### FrameMaker和FrameMaker Publishing Server

| AEM Guides即云版本 | FMPS | FrameMaker |
| --- | --- | --- |
| 2023.03.0 | 不兼容 | 2022或更高版本 |
| | | |


### 氧气连接器

| AEM Guides即云版本 | 氧气连接器窗口 | 氧气连接器Mac | 在氧气窗口中编辑 | 在氧气Mac中编辑 |
| --- | --- | --- | --- | --- |
| 2023.03.0 | 2.9-uuid-2 | 2.9-uuid-2 | 2.3 | 2.3 |
|  |  |  |  |

## 修复的问题

修复了多个区域中的错误如下：

* 下载PDF过程在Web编辑器中无法正常工作。 (11496)
* JSON输出 | 将属性值映射为的元数据 `"value in spaces and double quotes"` 会导致发布错误。 (11438)
* 在YouTube格式下，插入音频和视频多媒体文件失败 **插入多媒体** 图标。 (11320)
* 使用具有专门化标题元素的模板创建映射时，会发生验证错误。 (11212)
* 本机PDF | 表标题中的脚注导致PDF输出中相应页脚中的粗体和居中对齐文本。 (10610)
>[!NOTE]
>
>要反映本机PDF更改，请删除位于/content/dam/dita-templates的PDF文件夹，然后升级到最新内部版本。 (10610)

### 有变通方法的已知问题

Adobe已发现AEM Guides 2023年3月as a Cloud Service版的以下已知问题。

* 用户无法保存或创建重复资源的版本。

**解决方法**：在对该重复资产进行任何更改之前，请从Assets UI重新处理该资产。
