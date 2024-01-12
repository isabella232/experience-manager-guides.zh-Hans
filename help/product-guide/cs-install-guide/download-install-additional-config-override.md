---
title: 配置覆盖
description: 了解如何配置覆盖
exl-id: dc5f81f7-5b0a-4d12-a944-ba66b0239d5c
feature: Installation
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# 配置覆盖 {#id216IFC003XA}

要进行任何配置更新，应使用以下通用方法：

1. 访问您的Cloud Manager的Git存储库。

1. 在以下位置创建新的JSON文件：

   src/main/content/jcr\_root/apps/fmditaCustom/config/

1. 使用以下格式命名文件：

   $\{PID\}.cfg.json

   其中，PID是配置的进程ID。

1. 使用以下格式在JSON文件中添加属性：

   ```
   {
      "aem.adminuname": "updatedUserjson",
      "valid.characters": "[-a-zA-Z0-9_@$]",
      "dita.serialization": true
   }
   ```

1. 提交更改并运行Cloud Manager管道以部署更新的配置。


**父主题：**[&#x200B;下载并安装](download-install.md)
