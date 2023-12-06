---
title: 升级AEM指南
description: 了解如何升级AEM Guides
exl-id: 57ae906f-69e3-4319-89f6-0fa9ddb7a3ff
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 升级AEM指南 {#id213BD050YPH}

1. 访问您的Cloud Manager的Git存储库。

1. 更新dox/dox.installer/pom.xml文件。

1. 将dox.version变量的值更新为Adobe提供的版本详细信息。

1. 提交更改并运行Cloud Manager管道以部署升级的包。


>[!NOTE]
>
> 有关使用CI/CD管道的更多详细信息，请参阅 [在AdobeCloud Manager中使用CI/CD管线](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/use-the-cicd-pipeline-in-cloud-manager-for-aem.html).

## 清除浏览器缓存

完成升级过程后，所有用户必须先清除浏览器缓存，然后才能使用AEM Guides的升级版本。

**父主题：**[&#x200B;下载并安装](download-install.md)
