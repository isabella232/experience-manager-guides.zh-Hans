---
title: 用于转换工作流的REST API
description: 了解用于转换工作流的REST API
exl-id: f091782e-ab54-4db4-9018-9bcbff9da7b2
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# 用于转换工作流的REST API {#id175UB30E05Z}

以下REST API允许您将Word、HTML和InDesign文档转换为DITA格式。

## 转换Word文档

一种将Word文档转换为DITA格式的GET方法。

**请求URL**： http://*&lt;aem-guides-server>*： *&lt;port-number>*/bin/fmdita/conversion

**参数**： |名称|类型|必需|描述| --------------------------- |``operation``|字符串|是|要调用的操作的名称。 此参数的值为 ``word2dita``. <br> **注意：** 该值不区分大小写。 | |`inputFile`|字符串|是|AEM存储库中源Word文件的绝对路径。| |`destPath`|字符串|是|将保存转换的DITA文件的目标位置的绝对路径。| |`createRev`|布尔值|是|指定是否创建文件的修订版本\( `true`\)是否位于指定的目标\( `false`\)。 仅当目标位置包含转换文件的现有版本时，才考虑使用此选项。| |`style2tagMap`|字符串|是|用于转换的样式映射文件的绝对路径。|

**响应值**：返回HTTP 200 \(Successful\)响应。

## 转换HTML文档

一种将HTML文档转换为DITA格式的GET方法。

**请求URL**： http://*&lt;aem-guides-server>*： *&lt;port-number>*/bin/fmdita/conversion

**参数**： |名称|类型|必需|描述| --------------------------- |`operation`|字符串|是|要调用的操作的名称。 此参数的值为 ``html2dita``. <br> **注意：** 该值不区分大小写。| |`inputFile`|字符串|是|AEM存储库中源HTML文件的绝对路径。| |`destPath`|字符串|是|将保存转换的DITA文件的目标位置的绝对路径。| |`createRev`|布尔值|是|指定是否创建文件的修订版本\( `true`\)是否位于指定的目标\( `false`\)。 仅当目标位置包含转换文件的现有版本时，才考虑使用此选项。|

**响应值**：返回HTTP 200 \(Successful\)响应。

## 转换InDesign文档

一种将InDesign文档转换为DITA格式的GET方法。

**请求URL**： http://*&lt;aem-guides-server>*： *&lt;port-number>*/bin/fmdita/conversion

**参数**： |名称|类型|必需|描述| --------------------------- |``operation``|字符串|是|要调用的操作的名称。 此参数的值为 ``idml2dita``. <br> **注意：** 该值不区分大小写。| |`inputFile`|字符串|是|AEM存储库中源InDesign文件的绝对路径。| |`destPath`|字符串|是|将保存转换的DITA文件的目标位置的绝对路径。| |`createRev`|布尔值|是|指定是否创建文件的修订版本\( `true`\)是否位于指定的目标\( `false`\)。 仅当目标位置包含转换文件的现有版本时，才考虑使用此选项。|

**响应值**：返回HTTP 200 \(Successful\)响应。
