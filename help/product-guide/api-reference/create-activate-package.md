---
title: 用于创建和激活包的 REST API
description: 了解用于创建和激活包的 REST API
exl-id: 90686f77-a769-44bc-90eb-116cf9d0341e
feature: Rest API Packages
role: Developer
level: Experienced
source-git-commit: b95a64ca2e8ebffebec3d8ff8704f76f7faceca2
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# 用于创建和激活包的 REST API {#id198CF0260Y4}

以下REST API允许您创建和激活CRX包。

## 创建并激活包

创建和激活CRX包的POST方法。

**请求网址**：
http://*&lt;aem-guides-server\>*： *&lt;port-number\>*/bin/fmdita/activate&lt;/port-number\>&lt;/aem-guides-server\>

**参数**：
请求查询由 JSON 规则字符串组成。 POST 请求的内容类型必须设置为 `application/json; charset=UTF-8`。

**示例**：
以下示例显示了使用 curl 命令的 API 调用：

```XML
curl -u <*username*>:<*password*> -H "Content-Type: application/json; charset=UTF-8"  -k -X POST -d "{[JSON rules string](create-activate-package-java.md#example-create-activate-package-id198JH0B905Z)}" http://<*aem-guides-server*>:<*port-number*>/bin/fmdita/activate
```


**可选参数**

`activationTarget`

**有效值**

`preview` 或 `publish` 用于云服务和 `publish` 本地软件

- 对于云服务，如果参数包含无效值，则包激活将失败。

- 对于本地软件，如果参数包含无效值，则会记录错误，并使用默认值 . `publish`

如果未定义可选参数 ， `activationTarget`它将使用云服务和本地软件的默认发布代理激活。



以下示例显示了使用带有可选参数的 curl 命令的 API 调用：


    &#39;&#39;&#39;XML
    
    curl -u &lt;*username*>：&lt;*password*> -H “内容类型： application/json;charset=UTF-8“ -k -X POST -d ”{[JSON rules string]（create-activate-package-java.md#example-create-activate-package-id198JH0B905Z）}“ http://&lt;*aem-guides-server*>：&lt;*port-number*>/bin/fmdita/activate？activationTarget=&#39;&lt;validActivationTargetValue>&#39;
    &#39;&#39;&#39;&#39;
&lt;/validActivationTargetValue>&lt;/*port-number*>&lt;/*aem-guides-server*>&lt;/*password*>&lt;/*username*>