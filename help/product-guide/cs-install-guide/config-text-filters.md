---
title: 配置文本过滤器
description: 了解如何配置文本过滤器
exl-id: 0963606c-010e-4a72-b7bf-850b86b34a84
feature: Web Editor Configuration
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# 配置文本过滤器 {#id21BPD0FK0XA}

AEM Guides提供了在AEM存储库选定路径上的文件中搜索文本的功能。 您可以使用过滤器搜索从存储库面板中搜索文件或浏览文件。 在Web编辑器中工作时，需要使用文件浏览对话框插入图像、引用或键引用等元素。

默认情况下，您可以使用一些增强型过滤器来搜索AEM存储库中的文件。 您可以筛选选定路径中存在的所有DITA文件或非DITA文件。 您还可以在DITA元素的属性中搜索特定值。 您还可以查找由指定用户签出的文件。

>[!NOTE]
>
> 您还可以配置全局配置文件并添加更多用于搜索的过滤器。

执行以下步骤来配置文本过滤器：

1. 以管理员身份登录Adobe Experience Manager。
1. 单击顶部的Adobe Experience Manager链接，然后选择 **工具**.
1. 选择 **指南** 从工具列表中，单击 **文件夹配置文件**.
1. 单击 **全局配置文件** 磁贴。
1. 单击 **XML编辑器配置**.
1. 单击 **编辑** 图标。
1. 单击 **下载** 图标，用于在本地系统上下载ui\_config.json文件。 然后，您可以对文件进行更改，然后上传相同的更改。
   1. 在文件中配置过滤器。 您还可以添加自定义筛选条件，如下例所示：

      以下代码段显示了如何添加过滤选项“DITA文件”、“非DITA”、“DITA元素”和“由文件签出”。 它还包含一个自定义筛选条件 — 标记。

      ```
       "operation":"like"
                                      },
                                      {
                                      "title":"Checked out by",
                                      "property":"jcr:content/cq:drivelock",
                                      "operation":"like",
                                      "itemConfig":{
                                      "component":"textfield",
                                      "placeholder":"Checked out by"
                                      },
                                      "children":[
                                      {
                                      "title":"Check out"
                                      }
                                      ]
                                      },
                                      {
                                      "title":"Tags",
                                      "property":"jcr:content/metadata/cq:tags",
                                      "itemConfig":{
                                      "component":"textfield",
                                      "placeholder":"Enter Tag"
                                      },
                                      "children":[
                                      {
                                      "title":"Tags"
                                      }
                                      ]
                                      }
                                      ]
      ```

      在上述代码片段中，第一个过滤器用于DITA文件。 过滤器定义采用以下参数：

      ****标题****：过滤器的显示名称。 此标题将作为筛选选项显示在文件浏览对话框中。

      ****属性****：与文件元数据匹配的属性。 例如，要仅允许属性中包含dita\_class元数据的文件，属性过滤器会将“jcr：content/metadata/dita\_class”作为其值。

      ****操作&#x200B;**：**指定“存在”以匹配属性参数中指定的值的存在

1. 上载更新的ui\_config.json文件，该文件包含添加的过滤器。

配置的筛选器在筛选器面板中可用。

**父主题：**[&#x200B;自定义Web编辑器](conf-web-editor.md)
