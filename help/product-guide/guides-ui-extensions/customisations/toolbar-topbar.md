---
title: 顶部栏和工具栏
description: 自定义标题栏和工具栏
role: User, Admin
source-git-commit: be06612d832785a91a3b2a89b84e0c2438ba30f2
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---


# 自定义标题栏和工具栏

要自定义 `topbar` 和 `toolbar`，我们将使用id： `topbar` 或 `toolbar`，并遵循相同的视图，控制器结构。

以下是工具栏自定义的简单示例。 在此，我们删除了 `Insert Numbered List` 按钮，并替换了 `Insert Paragraph` 按钮创建自定义自定义点击处理程序。

```js title = toolbar_customisation.js
const toolbarExtend = {
    id: "toolbar",
    view: {
        items: [
            {
                component: "div",
                target: {
                    key:"title",value: "Insert Numbered List",                    
                    viewState: VIEW_STATE.REPLACE
                }
            },
            {
                {
                    "component": "button",
                    "icon": "textParagraph",
                    "variant": "action",
                    "quiet": true,
                    "title": "Insert Paragraph",
                    "on-click": "INSERT_P"
                },

                target: {
                    key:"title",value: "Insert Paragraph",                    
                    viewState: VIEW_STATE.REPLACE
                }
            },
        ]
    },
    controller: {

        INSERT_P(){
            this.next("AUTHOR_INSERT_ELEMENT",  "p" )
        }
    }
}
```
