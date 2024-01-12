---
title: 为AEM站点输出配置有效文件名
description: 了解如何为AEM站点输出配置有效文件名
exl-id: 05215bec-653b-4563-83c6-a1bb16200469
feature: Filename Configuration
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 1%

---

# 为AEM站点输出配置有效文件名 {#id214GK0X0KXA}

与DITA主题允许的有效文件名字符列表类似，您还可以为AEM Site输出配置有效文件名字符列表。 URL中不允许使用的一些已知字符包括： ``'<>`@$``. 这些字符配置为自动转换为下划线»`_`&quot;当在生成AEM Site输出文件名时发现这些地址。

请按照以下说明进行操作： [配置覆盖](download-install-additional-config-override.md#) 创建配置文件。 在配置文件中，提供以下\(property\)详细信息以在AEM Site输出中设置有效字符：

| PID | 属性键 | 属性值 |
|---|------------|--------------|
| `com.adobe.fmdita.common.SanitizeNodeNameImpl` | `aemsite.DisallowedFileNameChars` | 在AEM Site输出文件名中添加要替换为下划线的字符。 <br> **默认值**： ``'<\>\`@$`` |

**父主题：**[&#x200B;配置文件名](conf-file-names.md)
