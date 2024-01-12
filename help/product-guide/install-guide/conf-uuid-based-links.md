---
title: 配置基于UUID的链接的显示
description: 了解如何配置基于UUID的链接的显示
exl-id: ab1b0ecf-cb50-4fcd-b36e-d16a8c396054
feature: Web Editor Configuration
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# 配置基于UUID的链接的显示 {#id2035G20M0QN}

默认情况下，在Web编辑器中使用“插入引用”或“插入重用内容”选项创建链接时，将使用引用内容的UUID创建链接。 此 **链接** 可以将引用内容的属性\（在“属性”面板中\）配置为显示引用内容的相对文件路径或UUID。 此显示由 **启用UUID** 选项。 默认情况下，此功能处于打开状态，这意味着引用内容的UUID显示在“属性”面板中。

执行以下步骤以在Web编辑器中显示引用内容的相对路径或UUID：

1. 打开Adobe Experience Manager Web控制台配置页面。

   用于访问配置页面的默认URL为：

   ```http
   http://<server name>:<port>/system/console/configMgr
   ```

1. 搜索并单击 **com.adobe.fmdita.xmleditor.config.XmlEditorConfig** 捆绑。

1. 在 *XmlEditorConfig* 设置， **启用UUID** 选项默认处于启用状态。 这意味着引用内容的UUID显示在 **链接** 属性面板中的属性。

   如果要显示链接内容的相对路径，请取消选择 **启用UUID** 选项。

1. 单击&#x200B;**保存**。


**父主题：**[&#x200B;自定义Web编辑器](conf-web-editor.md)
