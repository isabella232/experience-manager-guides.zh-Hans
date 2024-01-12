---
title: 按钮
description: 按钮
role: User, Admin
source-git-commit: be06612d832785a91a3b2a89b84e0c2438ba30f2
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 5%

---


# 按钮

要显示按钮，我们使用组件button。
JUI中的按钮组件表示html `<button/>`.

```js title="buttonJSON.js"
const buttonJSON = {
  "component": "button",//tells the component name
  "label": "Yes, login",//tells the text for the button
  "variant": "cta",//tells the variants for the button which  provides default styles
  "on-click": "done",//tells what function to run after user clicks the button
};
```

这将生成一个带有标签的按钮 `Yes, login`. 其他属性包括但不限于variant、label、on-click。
> **_注意：_**  此 `on-<events>` 是调用控制器中命令的语法。

呈现的按钮将如下所示：

![按钮](imgs/yes_login_button.png "按钮")
