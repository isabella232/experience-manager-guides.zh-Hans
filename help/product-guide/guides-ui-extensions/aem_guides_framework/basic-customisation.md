---
title: 自定义应用程序
description: 自定义应用程序
role: User, Admin
source-git-commit: be06612d832785a91a3b2a89b84e0c2438ba30f2
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 自定义应用程序

我们的应用程序遵循MVC（模型、视图、控制器）结构

## 型号

模型定义各种属性并存储其值。 可使用语法从控制器访问存储在模型中的各种属性的值

```typescript
this.model.attributeName
```

对于在应用程序中自定义，所有新创建的属性都将添加到模型中的映射下。
要在模型中设置新属性，我们将在控制器中使用以下语法：

```typescript
this.model.extraProps.set("key", value)
```

要访问添加到模型中的属性，我们将使用以下语法：

```typescript
const value = this.model.extraProps.get("key")
```

## 查看

该视图定义应用程序的UI。 我们使用JSON文件来定义文件的视图。 在本例中，我们定义组件和css（如组件外的示例中所提供），并渲染存储在模型中的值。
在我们的应用程序中，每个视图都使用JSON进行定义。 JSON通过其唯一ID进行引用，该ID称为 `id`.

## 控制器

控制器用于处理事件和处理数据。 控制器用于从服务器获取和发送数据，是UI上显示的内容与存储在后端上的内容之间的接口。

- 要在初始化时设置值，我们使用 `init` 函数。
- 要将方法添加到控制器，请使用以下语法：

```typescript
methodName: function(args){
    // functionality
}
```

此 `methodName` 此处用作 `key` 在JSON（视图）或其他函数中引用方法

- 要在控制器中调用方法，请使用语法

```typescript
this.next('methodName', args)
```

## 示例

现在，我们通过一个简单的示例来演示这3个组件如何彼此进行交互。
我们将添加一个按钮，该按钮可在单击时切换其标签值

### 查看示例

下面我们定义了一个按钮的JSON，该按钮显示在变量名称下存储在模型中的动态文本 `buttonLabel`.
在此示例中，单击按钮将更改其标签。

```JSON
{
    "component": "button",
    "label": "@extraProps.buttonLabel",
    "variant": "cta",
    "on-click": "switchButtonLabel",
}
```

### 模型示例

这种情况下， `extraProps.buttonLabel` 保存按钮的标签

### 控制器示例

```typescript
  controller: {
    init: function () {
      this.model.extraProps.set("buttonLabel", "Submit")
    },

    switchButtonLabel(){
        const buttonLabel = this.model.extraProps.get("buttonLabel") === "Submit"? "Cancel" : "Submit"
        this.model.extraProps.set("buttonLabel", buttonLabel)
    }
  }
```

以下GIF显示了正在运行的上述代码
![basic_customization](imgs/basic_customisation.gif "基本自定义按钮")
