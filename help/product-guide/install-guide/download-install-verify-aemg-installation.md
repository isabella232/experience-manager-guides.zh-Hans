---
title: 验证AEM Guides的安装
description: 了解如何验证AEM Guides的安装
exl-id: 8e0afe18-5675-4c7e-b216-6de1a752bd01
feature: Installation
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 验证AEM Guides的安装 {#id213BD030FBE}

安装AEM Guides后，您需要验证安装是否成功。 执行以下步骤来验证安装过程：

1. 登录AEM实例并导航到AEM Web Console“包”页面。 用于访问捆绑包的默认URL为：

   ```http
   http://<server name>:<port>/system/console/bundles
   ```

   此时将显示捆绑包列表。

1. 通过在过滤文本框中输入fmdita来过滤捆绑列表，然后按 **输入**.

   捆绑包列表经过筛选，以显示AEM Guides安装的捆绑包。 如果安装成功，则所有已安装的捆绑包都将具有 **状态** 之 **活动**.

   如果任何捆绑包中没有 **活动** 状态，然后检查AEM日志以解决安装问题。


>[!IMPORTANT]
>
> 您可以考虑使用许多性能优化建议来提高系统性能。 请参阅 [Recommendations优化性能](download-install-recommend-perf-optimiz.md#) 以了解详细信息。

**父主题：**[&#x200B;下载并安装](download-install.md)
