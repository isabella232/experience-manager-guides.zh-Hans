---
title: 用于注册数据源连接器的REST API
description: 了解用于注册数据源连接器的REST API
exl-id: e2811892-c3cf-41f5-94d8-c2b37823a53a
feature: Rest API Data Source
role: Developer
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---

# 用于注册数据源连接器的REST API {#id236LG0Y0CXA}

以下REST API允许您注册数据源连接器。

## 注册数据源连接器

注册数据源连接器的GET方法。

**请求URL**：
`http://server:port/bin/guides/v1/konnect/config/register?path=<uploaded file path>`

**参数**： |名称|类型|必需|描述| --------------------------- |`path`|字符串|是|指向AEM存储库中路径的字符串。 它可以是 `/content/dam or /var/dxml`.|

**示例**：\
`http://host:4502/bin/guides/v1/konnect/config/register?path=/var/dxml/konnect/jira.json`
