---
title: 配置允许的特殊字符
description: 了解如何配置允许的特殊字符
exl-id: 7ff4305f-71bb-4155-b8e5-911cea6f0ad9
feature: Web Editor Configuration
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# 配置允许的特殊字符 {#id20CIL600035}

利用Web编辑器，可插入一些现成的特殊字符。 但是，您可以自定义作者可以插入其文档中的特殊字符列表。 如果自定义特殊字符列表，则它会覆盖默认的特殊字符集。 只有您在配置中添加的特殊字符才可供作者使用。

执行以下步骤以覆盖默认的特殊字符列表：

1. 创建 `symbols.json` 文件，该文件位于Cloud Manager的Git存储库中的以下位置：

   ```
   /apps/fmdita/xmleditor/
   ```

1. 在中添加特殊字符定义 `symbols.json` 文件为：

   ```
   {"symbols": [{"label": "Arrows",
      "items": [
      {   "name": "←",   "title": "Left Arrow"   } 
      ,   
      {   "name": "↑",   "title": "Up Arrow"      } 
      ]   
      }   ]   }
   ```


的结构 `symbols.json` 文件说明如下：

- `"label": "Arrows"`：这会指定特殊字符的类别。 在代码片段中，名为的类别 `"Arrows"` 已定义。
- `"items"`：此属性定义类别中特殊字符的集合。
- `"name": "←", "title": "Left Arrow"`：这是特殊字符的定义。 它从 `"name"` 标签，不可更改。 名称后跟特殊字符。 此 `"title"` 是特殊字符的名称或标题，作为该特殊字符的工具提示显示。

  您可以在一个类别中定义多个特殊字符定义。


**父主题：**[&#x200B;自定义Web编辑器](conf-web-editor.md)
