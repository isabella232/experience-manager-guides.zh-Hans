---
title: 在AEMaaCS上发布基准的指南
description: 了解AEM Cloud上发布的系统限制。
exl-id: 2cb4dfa4-dafc-409a-8d29-dbb00fabeae5
feature: Publishing
role: User, Admin
source-git-commit: be06612d832785a91a3b2a89b84e0c2438ba30f2
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 8%

---

# AEM Guides在AEMaaCS上发布基准

目前，AEM Guides云服务在发布指南团队正在积极努力解决的地图大小方面存在某些限制。

指南团队引入了一项可扩展的发布微服务，以支持大型地图和多个并发发布。 要了解有关新发布微服务的更多信息，请参阅 [发布微服务架构](publish-microservice-architecture-and-performance.md)

要为任何AEM云环境配置新的发布服务，请参阅 [配置新的基于微服务的发布](configure-microservices.md)


## 执行环境

    AEM版本： 2023.5.11983.20230511T173830Z
    指南加载项版本：2023.6.0
    AEM站点模板：AEM Guides OOTB模板
    DITA-OT版本： 3.5.4
    发布工作流类型：拆分发布工作流
    微服务支持的输出：本机PDF、PDF(Dita-OT)

## 输出层代号

| 输出类型 | 映射大小（主题引用） | 执行时间（秒） | 发布微服务 |
|---------------|------------------------------|----------------------------|-----------------------|
| AEM站点 | 3500 | 5220 | 否 |
| 本机PDF | 3500 | 780 | 是 |
| PDF(DITA-OT) | 11000 | 960 | 是 |
| HTML5 | 3500 | 240 | 否 |
| 自定义 | 300 | 300 | 否 |

## 要记住的要点

- AEM Site通过在生成期间分别呈现多个cq：Page节点和拼合文件，来创建这些节点和拼合文件。 因此，建议您避免运行大型的多次AEM Site并发发布，因为这会增加系统的负担。
- AEM站点生成时间取决于所使用的模板。 如果使用复杂模板，执行时间可能会增加。
- 自定义发布执行时间用于示例自定义输出。 自定义发布时间完全取决于客户自己的转换逻辑。
