---
title: 发行说明 | 修复了Adobe Experience Manager Guides 4.3.1.5版本中的问题
description: 了解Adobe Experience Manager Guides 4.3.1.5版本中的错误修复
role: Leader
source-git-commit: 485f88e2e8724d1dc28deac13d677734fcc15c25
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 2%

---


# 修复了4.3.1.5版本中的问题


本文介绍Adobe Experience Manager Guides 4.3.1.5版本中各个方面修复的错误。



了解 [4.3.1.5版本的升级说明](../release-info/upgrade-instructions-4-3-1-5.md).


## 创作

- 在中的内联元素之间添加空格 `<codeblock>` 导致生成的输出中出现换行符。 (15247)
- 从“插入元素”对话框添加元素时出现体验问题。 (15108)

## 发布

- 错误日志显示有关使用外部范围发布内容的信息不正确。 (15242)
- 指向以开头的DITA文件的内部链接 `HTTP` 会被视为外部链接，导致范围错误。 (15155)
- DITA映射的AEM站点重新生成失败。 (14369)

## 管理

- **fmditaTopicrefs** 属性显示相对路径而不是绝对路径。 (15341)

