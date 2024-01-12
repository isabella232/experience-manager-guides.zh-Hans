---
title: 自定义
description: 自定义审核应用程序
role: User, Admin
source-git-commit: be06612d832785a91a3b2a89b84e0c2438ba30f2
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# 自定义审核应用程序

为了简化审阅应用程序的自定义，我们提供了一些挂钩，如下所述：

## Review-Comment

- id： `review_comment`
- 挂钩： `this.updateExtraProps`：

如讨论内容 [此处](../../aem_guides_framework/basic-customisation.md)，自定义期间添加的任何新属性将遵循 `this.model.extraProps`. 方法 `updateExtraProps` 用于向审阅注释添加属性，以及在服务器上处理所添加属性的更新和存储。

### 使用示例

例如，您要添加字段 `commentRationale` 和 `severity` 到您的意见中去。
让我们更新 `commentRationale` “这是一个重要的句子。” 和 `severity` “严重”时。
可以使用语法执行此操作：

```typescript
 this.updateExtraProps(
        {'commentRationale': 'This is an important sentence.',
        'severity': 'CRITICAL'}
      )
```

上述代码片段将处理值的更新和保存。 通过定义视图，保存的值可以在UI中呈现。

```JSON
{
    "component" : "label",
    "label": "@extraProps.commentRationale"
}
```

## 内联审核面板

- id： `inline_review_panel`

1. 挂钩： `onNewCommentEvent`
挂钩 `onNewCommentEvent` 用于引发新注释或回复事件或调用方法。
中收到的参数 `onNewCommentEvent` 包括：
   - 事件：已调度的评论/回复事件。
   - newComment：布尔值如果调度的事件是新注释事件，即 `highlight`， `insertion`， `deletion`， `sticky note comment`
   - newReply：布尔值：如果调度的事件是新回复事件。

2. 挂钩： `sendExtraProps`

如果要扩展 `event` 并发送 `extraProps` 内联审阅面板中的。 下面我们将解释这两个钩子的用法。

### 内联审阅面板示例

假设我们要发送一个extraProp `userInfo`，每次发送新评论或回复时。 现在，这将通过内联审阅面板完成，但我们没有对新生成评论的commentId的引用，因此要实现此目的，我们可以编写以下代码。

```typescript
    onNewCommentEvent(args){
      const events = _.get(args, "events")
      const currTopicIndex = tcx.model.getValue(tcx.model.KEYS.REVIEW_CURR_TOPIC) || this.model.currTopicIndex || "0"
      const event = _.get(_.get(events, currTopicIndex), '0')
      const newComment = _.get(args, 'newComment')
      const newReply = _.get(args, 'newReply')
      if ((newComment || newReply) && event) {
        this.next('setUserInfo', event)
      }
    },
```

在上述代码片段中，我们正在检查已调度的事件是新注释还是回复。 如果出现新的评论或回复，我们将调用方法 `setUserInfo`

```typescript
    setUserInfo(event) {
      this.loader?.getUserInfo(event.user).subscribe(userData => {
        const extraProps = {
          "userFirstName": userData?.givenName || '',
          "userLastName": userData?.familyName || '',
          "userTitle": userData?.title || '',
          "userJobTitle": userData?.jobTitle || '',
          'userEmail': userData?.email || '',
        }
        const data = {... event, extraProps}
        this.sendExtraProps(
          data
        )
      })
    },
```

在上述方法中，我们将扩展事件以发送extraProp，包括用户的名字、电子邮件、标题等。 通过此方式扩展事件可确保使用正确的commentId发送extraProp，并确保它们附加到正确的注释中。

挂钩 `updateExtraProps` 固有地调用挂接 `sendExtraProps`，那么什么时候使用什么？

我们使用 `updateExtraProps` 在 `review_comment` 控制者，该控制者已拥有该评论的 `id` 因此你只需提一下 `extraProps.`

此 `inline_review_panel` 但是，无法访问评论的id，因此无论您何时需要从内联审核面板调度事件， `sendExtraProps` 会很方便的。
