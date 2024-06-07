---
title: 配置主题和体验片段模板之间基于JSON的映射。
description: 了解如何配置主题和体验片段模板之间基于JSON的映射。
feature: Output Generation
role: Admin
level: Experienced
source-git-commit: f252537d15d7e8f8651dddb0ae635905705e4adf
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# 创建主题和体验片段之间的映射

Adobe Experience Manager Guides提供了在主题和体验片段模板之间创建基于JSON的映射的功能。 您可以使用此映射将主题中部分或所有元素中存在的内容发布到体验片段。

1. 要下载 *experienceFragmentMapping.json*&#x200B;中，以管理员身份登录Adobe Experience Manager。
1. 选择顶部的Adobe Experience Manager链接，然后选择 **工具**.
1. 从工具列表中选择“参考线”，然后选择 **文件夹配置文件**.
1. 选择要配置的配置文件拼贴。 您可以为全局或文件夹级别的配置文件配置映射。 例如，选择 **全局配置文件** 磁贴。
1. 选择 **XML编辑器配置** 选项卡，然后选择 **编辑** 图标。
1. 选择 **下载** 图标以下载 *experienceFragmentMapping.json*  文件。 然后，您可以对文件进行更改，然后上传相同的更改。

1. 您需要遵循以下验证操作：

   1. 它应该是一个JSON文件
   2. 它应包含一个至少包含一个对象的数组，每个对象应包含以下内容：


      `"template": string `

      `"mapping": array`

      映射的每个对象必须包含以下内容：

      `"name": string`

      `"class": string`

      `"resourceType": string`

      `"attributeMap": array`


1. 保存文件并将其上传。

Experience Manager指南将完整主题转换为HTML，然后可以映射到体验片段中使用的核心组件。 例如，中的内容 `<p>` 标记可以映射为在体验片段中创建文本组件。
* `name`：指定HTML元素。 例如， `<div>`， `<img>`
* `class`：指定与HTML元素对应的DITA元素标记。 例如， `<p>` `<image>`
* `resourceType`：指定适用于体验片段中使用的组件的资源类型。 例如， `wcm/foundation/components/text` 是wcm的resourceType `text` 组件。
* `attributeMap`：为组件提供其他信息，例如文本组件是否应呈现为 `RichText` 或包含 `fileReference` 图像组件的。




示例文件：

```
[
  {
    "template": "default",
    "mapping": [
      {
        "name": "#element",
        "resourceType": "wcm/foundation/components/text",
        "attributeMap": [
          {
            "from": "outerHTML",
            "to": "text"
          },
          {
            "value": true,
            "to": "textIsRich"
          }
        ]
      }
    ]
  },
  {
    "template": "/conf/we-retail/settings/wcm/templates/experience-fragment-web-variation",
    "mapping": [
      {
        "name": "div",
        "class": "title",
        "resourceType": "wcm/foundation/components/text",
        "attributeMap": [
          {
            "from": "outerHTML",
            "to": "text"
          },
          {
            "value": true,
            "to": "textIsRich"
          }
        ]
      },
      {
        "name": "h1, h2, h3, h4, h5, h6",
        "resourceType": "wcm/foundation/components/text",
        "attributeMap": [
          {
            "from": "outerHTML",
            "to": "text"
          },
          {
            "value": true,
            "to": "textIsRich"
          }
        ]
      },
      {
        "name": "div",
        "class": "p",
        "resourceType": "wcm/foundation/components/text",
        "attributeMap": [
          {
            "from": "outerHTML",
            "to": "text"
          },
          {
            "value": true,
            "to": "textIsRich"
          }
        ]
      },
      {
        "name": "img",
        "class": "image",
        "resourceType": "wcm/foundation/components/image",
        "attributeMap": [
          {
            "from": "outerHTML",
            "to": "fileReference"
          }
        ]
      },
      {
        "name": "#element",
        "resourceType": "wcm/foundation/components/text",
        "attributeMap": [
          {
            "from": "outerHTML",
            "to": "text"
          },
          {
            "value": true,
            "to": "textIsRich"
          }
        ]
      }
    ]
  }
]
```



从Web编辑器发布体验片段时，选择 `Template` 从的下拉菜单中 **生成体验片段** 对话框中的模板可用映射 **映射** 字段。 如果模板不存在自定义映射，则会列出默认映射。 您可以使用默认映射将整个主题发布为体验片段。

有关详细信息，请查看 [发布体验片段](../user-guide/publish-experience-fragment.md).

