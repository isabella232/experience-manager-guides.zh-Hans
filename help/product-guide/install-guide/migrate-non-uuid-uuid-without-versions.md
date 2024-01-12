---
title: 将不带版本的非UUID内容转换为UUID内容
description: 了解如何迁移不带版本的非UUID内容。
exl-id: 44b5660d-9961-4463-9686-53085249fb05
feature: Migration
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---

# 迁移不带版本的内容

>[!IMPORTANT]
>
> 如果打算忽略或不迁移资产版本，可以选择此迁移方法。


1. 使用AEM桌面应用程序等Adobe工具，直接从AEM Assets UI将资产从非UUID实例下载并上传到UUID实例。

1. 确保您启用了DAM更新资产工作流，并在导入内容以创建GUID后在所有资产上执行该工作流。
