---
title: 使用DITA映射的REST API
description: 了解用于DITA映射的REST API
exl-id: 6277e52d-1b05-4dd7-8d2b-4b94f329e2d7
feature: Rest API DITA Map
role: Developer
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# 使用DITA映射的REST API {#id175UB30E05Z}

以下REST API允许您在AEM Guides中使用DITA映射。

## 下载具有依赖项的DITA映射

一种GET方法，用于下载DITA映射及其所有依赖项，如映射和主题中使用的引用主题、子映射、图像和DTD。

**请求URL**： http://*&lt;aem-guides-server>*： *&lt;port-number>*/bin/fmdita/exportditamap

**参数**： |名称|类型|必需|描述| --------------------------- |`ditamap`|字符串|是|AEM存储库中DITA映射文件的绝对路径。| |`baseline`|字符串|是|用于检索版本化内容的基线的标题。 <br> **注意：** 值区分大小写。 |

**响应值**：一个.zip文件，其内容会写入响应的输出流中。

## 启动具有依赖项的DITA映射的导出

一种POST方法，用于启动对DITA映射及其所有依赖项（如映射和主题中使用的引用主题、子映射、图像和DTD）的导出。 稍后可以查询状态，并在完成后检索下载URL。

**请求URL**： http：*//&lt;aem-guides-server>： &lt;port-number>/bin/dxml/async-export*

**参数**： |名称|类型|必需|描述| --------------------------- |`ditamap`|字符串|是|AEM存储库中DITA映射文件的绝对路径。| |`baseline`|字符串|否|用于检索版本化内容的基线的标题。 <br> **注意：** 值区分大小写。| |`flatFS`|Boolean|No|\(Optional\)如果设置为true，则在ZIP文件中返回文件的平面结构。 例如，如果DITA映射引用多个文件夹中的内容，则所有引用的文件都将提取到单个文件夹中。 如果存在同名文件，则通过添加数字后缀来重命名这些文件。 所有引用\（在DITA映射和主题中\）都会自动处理，因为它们会根据平面文件夹结构中文件的新位置进行更新。 如果设置为false，则文件夹结构将保持不变。 如果DITA映射从多个位置引用文件，则所有这些位置也会在ZIP文件中创建。 恢复ZIP文件时，会在目标位置创建精确的文件夹结构。 <br> 此参数的默认值为false。|

**响应值**： 元素|描述| ------------------ |`status`|所执行操作的返回状态。 可能的选项包括：“已启动”、“失败”、“进行中”、“成功”、“缺失”、“已删除”| |`jobId`|作业的唯一ID。 以后可用于查询状态。| |errorMessage|失败时作业的错误消息\（如果状态为FAILED、MISSING或DELETED\）。| |`filePath`|ZIP文件的路径。 仅当作业已完成且状态为“成功”时，它才会出现。 这可用于下载ZIP文件。|

## 查询导出DITA映射状态

一种GET方法，可检索DITA映射及其所有依赖项的导出状态。 如果状态为STARTED或INPROGRESS，可以间隔轮询直到轮询完成\（成功或出错\）。

**请求URL**： http：*//&lt;aem-guides-server>： &lt;port-number>/bin/dxml/async-export*

**参数**
|名称|类型|必需|描述| --------------------------- |`jobId`|字符串|是|启动导出作业时检索到的作业ID。|

**响应值**： 元素|描述| ------------------ |`status`|导出作业的状态。 可能的选项包括：“已启动”、“失败”、“进行中”、“成功”、“缺失”、“已删除”| |`jobId`|作业的唯一ID。 以后可用于查询状态。| |`errorMessage`|失败时作业的错误消息\（如果状态为“失败”、“缺失”或“已删除”\）。| |`filePath`|ZIP文件的路径。 仅当作业已完成且状态为“成功”时，它才会出现。 这可用于下载ZIP文件。|
