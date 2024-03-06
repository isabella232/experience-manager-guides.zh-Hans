---
title: 发行说明 | 修复了Adobe Experience Manager Guides 2024.2.0版本中的问题
description: 了解Adobe Experience Manager Guidesas a Cloud Service2024.2.0版本中的错误修复。
source-git-commit: 3da78dd90bd219809d0a47bcdc2775b2c5ba29e1
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# 修复了2024.2.0版本中的问题

本文介绍Adobe Experience Manager Guidesas a Cloud Service2024.2.0版本中各个方面修复的错误。

有关新增功能和增强功能的详细信息，请查看 [2024.2.0版本中的新增功能](whats-new-2024-2-0.md).

了解 [2024.2.0版的升级说明](upgrade-instructions-2024-2-0.md).



## 创作

- 编辑器中的拼写检查不允许选择建议。 (15045)
- 全局导航按钮不起作用，无法加载仪表板。 (14968)
- 在Web编辑器中，下载映射功能在可以下载时无法触发弹出通知。 (14626)
- 在Web编辑器中，下载映射功能无法下载带有基线的映射。 (14622)
- 2023年10月版的《Experience Manager指南》as a Cloud Service出现DTD错误无效。 (14482)
- 将词汇表主题从存储库拖到词汇表映射中会创建 `topicref`. (10767)
- 片段的预览屏幕已冻结。 (14840)
- 标签来自 `labels.json` 文件在Web编辑器中以随机顺序显示。 (10508)

## 发布

- 在本机PDF发布中，条件预设中的自定义属性不适用于本机PDF发布。 (14943)
- 在本机PDF发布中，无法解析2023年12月版的Adobe Experience Manager Guides的关键引用。 (15085)
- AEM Sites发布失败，并导致下列文件的范围错误： `xref` 到以“HTTP”开头的DITA文件。 (15154)
- 无法从添加自定义模板 **输出** 选项卡。 (14846)
- **AEM站点** 由于模板路径为空，预设无法正常工作。 (14804)
- 对于主题包含MathML方程式的DITA映射，AEM站点重新生成失败。 (14790)
- 在本机PDF发布中，PDF生成过程在获取依赖关系时抛出错误 `Node.js` 发布。 (14445)
- AEM预设不允许选择模板位于 `/content` Web编辑器中的层次结构。 (14260)
- 在AEM Sites输出中，的样式或换行符丢失 `<lines>` 具有子元素的元素。 (12542)
- 自定义元数据在最终输出中不可用。 (12116)
- 在本机PDF发布中，无法使用DITA映射元数据属性来填充PDF文件输出的元数据。 (15159)



## 管理

- **基线筛选器** 文件无法在Web编辑器中使用文件名。 (13486)
- 禁用父DITA map的索引以获取更好的性能可能会影响某些功能的功能。(12213)


## 审查

- 右键单击上下文菜单不起作用 **Accept** 或 **拒绝** 跟踪更改。 (14607)
- 在2023年12月版的Adobe Experience Manager Guides中，在审核屏幕中切换以关闭DITA主题不起作用。 (14537)
- 自定义审核工作流的电子邮件模板不适用于叠加。 (13954)

## 已知问题

Adobe发现了2024.2.0版本的以下已知问题：

- 对于重复的DITA文件，版本1.0不会显示在UI上。
- 为任何预设启用微服务后，资产元数据的传播在2024.2.0版本中不起作用。

