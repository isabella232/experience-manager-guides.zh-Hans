---
title: 配置允许的特殊字符
description: 了解如何配置允许的特殊字符
exl-id: 3dd7752e-0836-480a-b1e1-6fa2099d404f
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# 配置允许的特殊字符 {#id20CIL600035}

利用Web编辑器，可插入一些现成的特殊字符。 但是，您可以自定义作者可以插入其文档中的特殊字符列表。 如果自定义特殊字符列表，则它会覆盖默认的特殊字符集。 只有您在配置中添加的特殊字符才可供作者使用。

执行以下步骤以覆盖默认的特殊字符列表：

1. 登录AEM并打开CRXDE Lite模式。

1. 创建 `symbols.json` 文件路径：

   ```json
   /apps/fmdita/xmleditor/
   ```

1. 在中添加特殊字符定义 `symbols.json` 文件为：

   ```json
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
