---
title: 本机PDF | 为本机PDF发布配置JVM标记
description: 为本机PDF发布配置JVM标记
exl-id: d5432913-4b5a-48e7-9467-7f6c6e0adbe4
feature: Output Generation
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 1%

---

# 为本机PDF发布配置JVM标记

本机PDF发布会启动单独的JVM进程来生成PDF。 您可能需要调整此JVM的配置以支持不同的场景。 例如，要运行较大的工作负载，应增加派生的JVM进程可用的最大栈大小。

执行以下步骤以配置AEM Guides本机PDF发布JVM标记：

1. 打开Adobe Experience Manager Web控制台配置页面。

   用于访问配置页面的默认URL为：

   ```http
   http://<server name>:<port>/system/console/configMgr
   ```

1. 搜索并选择 *com.adobe.fmdita.config.ConfigManager* 捆绑。

1. 更新属性 **本机pdf的Java命令行选项** (*native.pdf.java.opts*)，以传递任何标准JVM标记。



1. 单击&#x200B;**保存**。
