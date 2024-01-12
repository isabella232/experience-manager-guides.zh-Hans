---
title: 配置主题和内容片段模型之间的基于JSON的映射。
description: 了解如何配置主题和内容片段模型之间的基于JSON的映射。
exl-id: 21446bcb-e7df-4823-acc3-1fdc7473f0d1
feature: Output Generation
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 创建主题和内容片段之间的映射

AEM Guides提供了在主题和内容片段模型之间创建基于JSON的映射的功能。 您可以使用此映射将主题中部分或所有元素中存在的内容发布到内容片段。

1. 要下载 *contentFragmentMapping.json*&#x200B;中，以管理员身份登录Adobe Experience Manager。
1. 选择顶部的Adobe Experience Manager链接，然后选择 **工具**.
1. 从工具列表中选择“参考线”，然后选择 **文件夹配置文件**.
1. 选择 **全局配置文件** 磁贴。
1. 选择 **XML编辑器配置** 选项卡，然后选择 **编辑** 图标。
1. 选择 **下载** 图标以下载 *contentFragmentMapping.json*  文件。 然后，您可以对文件进行更改，然后上传相同的更改。

1. 您需要遵循以下验证操作：

   1. 它应该是一个JSON文件
   2. 它应包含一个至少包含一个对象的数组，每个对象应包含以下内容：


      `"name": string `

      `"mapping": array`

      映射的每个对象必须包含以下内容：

      `"modelField": string`

      `"xpath": string`

      `"outputType": string`
1. 保存文件并将其上传。

示例文件：

```
[
  {
    "mapping": [
      {
        "modelField": "title",
        "xpath": "/topic[1]/title[1]",
        "outputType": "textContent"
      },
      {
        "modelField": "shortdesc",
        "xpath": "/topic[1]/shortdesc[1]",
        "outputType": "textContent"
      },
      {
        "modelField": "topicData",
        "xpath": "/topic[1]/body[1]",
        "outputType": "outerHTML"
      }
    ],
    "name": "Full Topic"
  },
  {
    "mapping": [
      {
        "modelField": "title",
        "xpath": "/topic[1]/title[1]",
        "outputType": "textContent"
      },
      {
        "modelField": "shortdesc",
        "xpath": "/topic[1]/shortdesc[1]",
        "outputType": "textContent"
      },
      {
        "modelField": "heroImage",
        "xpath": "/topic[1]/body[1]/p[1]/image[1]",
        "outputType": "outerHTML"
      },
      {
        "modelField": "dataTable",
        "xpath": "/topic[1]/body[1]/table[1]",
        "outputType": "outerHTML"
      }
    ],
    "name": "Sample Example with XPath"
  }
]
```

您可以使用默认映射发布整个主题。 选择 `Full Topic` 中的下拉菜单的映射 **发布为内容片段** 对话框并在内容片段模型中具有“topicData”字段。
