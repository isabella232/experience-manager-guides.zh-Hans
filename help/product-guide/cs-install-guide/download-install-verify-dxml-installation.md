---
title: 验证AEM Guides的安装
description: 了解如何验证AEM Guides的安装
exl-id: 4e566c57-a522-4605-bc70-47155f20b429
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# 验证AEM Guides的安装 {#id213BD030FBE}

安装AEM Guides后，您需要验证安装是否成功。 执行以下步骤来验证安装：

1. 访问Cloud Service的开发人员控制台。

   有关访问开发人员控制台的详细信息，请参阅 [开发人员控制台访问](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html) 请参阅AEM文档。

1. 访问AEM中的OSGi包列表。

   有关访问捆绑包的详细信息，请参阅 [包](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#bundles) 请参阅AEM文档。

1. 在捆绑列表中搜索fmdita并检查其状态。

   状态应显示 *活动* 成功部署的包。 如果有任何捆绑包不处于“活动”状态，请检查AEM日志以解决安装问题。


**父主题：**[&#x200B;下载并安装](download-install.md)
