---
title: 配置查询的LimitReads数
description: 了解如何为查询配置LimitReads的数量
exl-id: f6010cc3-5fec-4ec7-adf7-5ad3c9bd8879
feature: Web Editor Configuration
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 2%

---

# 配置查询的LimitReads数 {#id231RC0HL0ID}

要增加查询一次可读取的节点数，请执行以下步骤：

1. 打开Adobe Experience Manager Web控制台JMX页面。

   用于访问配置页面的默认URL为：

   ```http
   http://<server name>:<port>/system/console/jmx
   ```

1. 搜索并单击 **Queryenginesettings**.

1. 更改属性值 **限制读取** 属性。

1. 单击&#x200B;**保存**。


当增加此属性值时，它有助于为较大的DITA映射生成报告。

**父主题：**[&#x200B;自定义Web编辑器](conf-web-editor.md)
