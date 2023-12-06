---
title: 后处理事件处理程序
description: 了解后处理事件处理程序
exl-id: 3b105ff5-02d4-40e3-a713-206a7fcf18b2
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 1%

---

# 后处理事件处理程序 {#id175UB30E05Z}

AEM Guides会公开用于执行任何后处理操作的com/adobe/fmdita/postprocess/complete事件。 只要对DITA文件执行操作，就会触发此事件。 对DITA文件执行的以下操作会触发此事件：

>[!NOTE]
>
> 没有为AEM 6.1中的删除操作触发此事件。

- 上传
- 创建
- 修改
- 删除

您需要创建一个AEM事件处理程序来读取此事件中可用的属性并进行进一步处理。

活动详情说明如下：

**事件名称**：

```
com/adobe/fmdita/postprocess/complete 
```

**参数**： 名称|类型|描述| --------文----------- |`path`|字符串|触发此事件的文件的路径。 通常，这是已对其执行操作的文件。| |`status`|字符串|所执行操作的返回状态。 可能的选项包括： - <br> — 成功：后处理操作已成功完成。 <br> — 已完成，但出现错误：后处理操作已完成，但有一些错误。 <br> — 失败：后处理操作失败，因为发生了一些致命错误。| |`message`|字符串|如果状态为COMPLETED WITH ERRORS或FAILED，则此参数包含有关错误或失败原因的详细信息。| |`operation`|字符串|对文件执行的后处理操作。 可能的选项包括：<br> — 添加 <br> — 更新 <br> — 删除|
