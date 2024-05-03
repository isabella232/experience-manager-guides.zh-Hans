---
title: 为自定义Dita类型配置图标
description: 了解如何为自定义Dita类型定义图标，以便在AEM中的不同UI中显示其图标
source-git-commit: ce2f5e4ab6b05fbce7b8384ff59091ebf9bab7be
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# 为自定义Dita（主题或映射）类型配置图标


## 问题陈述

利用AEM Guides中使用的自定义架构，您可以创建自定义主题或映射类型，并且您可能会注意到自定义主题/映射在Web编辑器或Assets UI中未显示图标。 请参阅屏幕快照以供参考  (../assets/authoring/custom-ditatype-icon-notshown.png)

因此，要为自定义主题/映射类型分配图标，您必须执行以下操作：
- 查找自定义主题/映射类型
- 编写样式以为自定义类型添加所需的图标


我们可以实施上述步骤以在Web编辑器（存储库视图）和资产UI中显示图标。 以下是这两个步骤的步骤


## 在Web编辑器视图中显示自定义主题/映射的图标

步骤1 ：确定自定义dita主题/ap的dita类型 — 在Web编辑器中打开存储库视图>在浏览器中打开开发人员控制台 — Inspect所列主题/映射旁边的图标空间 — 检查分配给自定义主题的类 — 查看屏幕快照  (../assets/authoring/custom-ditatype-icon-knowditatype.png)有关详细信息 — 我们将使用此类为此分配图标和写入css

步骤2：创建css并将图标分配给此dita类型 — 在/apps下创建客户端库，例如您在所需路径下创建cq：ClientLibraryFolder — 将类别“apps.fmdita.xml_editor.page”添加到其中 — 在此目录下创建文件夹“assets”，并添加您想要用于自定义dita类型的所有图标 — 在client library文件夹下添加css文件，例如“tree-icons.css” — 向其添加以下代码

```
            .tree-item-icon {
                &.custommaptype {
                    background-image: url('assets/custommap.svg')
                }
                &.customtopictype {
                    background-image: url('assets/customtopic.svg')
                }
            }
```

     — 在client library文件夹下添加css.txt，并添加对刚刚创建的“tree-icon.css”的引用
     — 保存/部署这些更改
参阅屏幕快照  (../assets/authoring/custom-ditatype-icon-define-webeditor-styles.png)以了解更多详细信息。

最终输出如屏幕快照中所示  (../assets/authoring/custom-ditatype-icon-webeditor-showstyles.png)


## 在Assets UI中显示自定义主题/映射图标

步骤1：确定自定义dita主题/映射的dita类型 — 已在前面方法步骤1中进行了说明

步骤2：创建Javacscript以定义要为自定义主题/映射类型的自定义dita类型加载哪些图标 — 在/apps下创建客户端库，例如您在所需路径下创建cq：ClientLibraryFolder — 向其添加以下属性： - &quot;categories&quot;（多值字符串）值，如&quot;dam.gui.admin.coral&quot; - &quot;dependencies&quot;（多值字符串）值，如&quot;libs.fmdita.versioncontrol&quot; — 在此/apps目录下创建文件&quot;/libs/fmdita/clientlibs/clientlibs/xmleditor/clientlib-dam/topic_type.js&quot;的副本 — 编辑复制的&quot;topic_type.js&quot;，并在变量&quot;下更改/添加customtopictopicontypeNameNameNameName map” — 您还可以更改图像文件夹的路径，方法是将变量“parentImagePath”的值更改为存储自定义图标的位置 — 在client library文件夹下创建名为js.txt的文件并添加对“topic_type.js”的引用 — 保存/部署这些更改参考屏幕快照  (../assets/authoring/custom-ditatype-icon-define-assetsui-styles.png)以了解更多详细信息。

最终输出将如屏幕快照中所示  (../assets/authoring/custom-ditatype-icon-assetsui-showstyles.png)