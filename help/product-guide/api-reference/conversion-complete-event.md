---
title: 转换过程事件处理程序
description: 了解转换过程事件处理程序
exl-id: 8033935d-2113-4e39-ab74-b7431b89f948
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 转换过程事件处理程序 {#id175UB30E05Z}

AEM Guides会公开用于在文档转换过程完成后执行任何后处理操作的com/adobe/fmdita/conversion/complete事件。 只要将非DITA文档迁移到DITA文件格式，就会触发此事件。 例如，如果您运行Word到DITA转换或InDesign到DITA转换过程，则在转换过程结束后调用此事件。

您需要创建一个AEM事件处理程序来读取此事件中可用的属性并进行进一步处理。

活动详情说明如下：

**事件名称**：

```HTTP
com/adobe/fmdita/conversion/complete 
```

**参数**：\
名称|类型|描述| --------文----------- |`status`|字符串|所执行操作的返回状态。 可能的选项有： — 成功：转换过程已成功完成。 <br>  — 已完成，但出现错误：转换过程已完成，但有一些错误。 <br> — 失败：转换过程由于某个致命错误而失败。| |`filePath`|字符串|AEM存储库中源文件\（待转换\）的绝对路径。| |`outputPath`|字符串|将保存转换的DITA文件的目标位置的绝对路径。| |`logPath`|字符串|将保存转换日志的节点的绝对路径。|
