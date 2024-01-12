---
title: Recommendations优化性能
description: 学习Recommendations以实现性能优化
exl-id: 92ac1f81-2f51-44b0-82c3-56b39e8f3027
feature: Performance Optimization
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Recommendations优化性能 {#id213BD0JG0XA}

对于性能优化，请考虑以下几点：

- 要优化内容和索引体验，请参阅 [优化内容搜索和索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html) 请参阅AEM文档。

- 使用自定义DITA-OT进行发布时修补Xerces Jar。 这是一个强制性配置，具体取决于您的用例。 仅当使用自定义DITA-OT发布输出时，才需要此更改。

  *必需的配置*：将自定义DITA-OT包中的Xerces Jar文件替换为附带的OOTB文件。 默认的OOTB xercesImpl-2.11.0.jar文件在/libs/fmdita/dita\_resources/DITA-OT.zip文件中提供。 确保重命名xercesImpl-2.11.0.jar文件以匹配要替换的旧Xerces Jar文件。 这可以在运行时完成。

  此更改可减少发布时间和内存使用率，同时发布包含大量主题的DITA映射。


**父主题：**[&#x200B;下载并安装](download-install.md)
