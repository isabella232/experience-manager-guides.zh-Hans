---
title: 使用NativePDF的TOC（目录）发布
description: 使用NativePDF发布Dita书签的目录和其他书签
feature: Native PDF Output
author: Pulkit Nagpal(punagpal)
role: User, Admin
exl-id: c551f0a8-f973-4c5a-bd34-f52890a91342
source-git-commit: 7638f3634ad45bbadda64ec6e3f706cbb65d696c
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# 在PDF发布中生成书签映射的目录

## 设置书图

包括 `<toc>`  元素：在书签的 `<frontmatter>`元素，找到 `<booklists>` 元素。  嵌套 `<toc>` 元素内部 `<booklists>` 如下所示：

```
<frontmatter>
  <booklists>
    <toc/>  <figurelist/>
    <tablelist/>
  </booklists>
</frontmatter>
```

DITA规范允许将TOC和书签放在 `<backmatter>` 部分。


```
<backmatter>
    <booklists>
      <toc/>
      <figurelist/>
      <indexlist/>
    </booklists>
  </backmatter>
```

书签的目录结构、前件图表和表表结构、后件索引表结构。

```
<bookmap>
  <title>My Bookmap Title </title>
  <frontmatter>
    <booklists>
      <toc/>
      <figurelist/>
      <tablelist/>
    </booklists>
  </frontmatter>

  <chapter href="chapter1.ditamap">
  <chapter href="chapter2.ditamap">
  </chapter>

  <backmatter>
    <booklists>
      <indexlist/>
    </booklists>
  </backmatter>
</bookmap>
```

目录和书签列表会根据书签映射中定义的结构自动生成。

设置书签后，使用本机PDF生成PDF输出。 它处理书签图结构和引用，包括目录和书签。

## TOC设计及其在PDF中的顺序

本机PDF功能提供了一种方便的方法来定制目录的布局和设计。

您可以通过目录的分页布局和通过layout.css的样式来控制设计。

目录和其他PDF中的书签顺序仅基于书签映射的结构。

![toc](../assets/publishing/toc.png)


## 常见问题解答

- ### 如何在PDF中包含Ditamap的目录

Ditamap本身并不像书签那样直接具有目录(TOC)。 但是，在定义内容结构时，Ditamap起着关键作用，并间接有助于目录生成过程。

如果要发布Ditamap，则本机PDF提供自动生成目录和书签列表的功能，您可以在本机PDF设置中启用/禁用在ditamap上生成目录。

![启用禁用目录](../assets/publishing/pageorder.png)

## 其他资源：

- [本机PDF设计页面布局文档](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/install-guide/on-prem-ig/output-gen-config/config-native-pdf-publish/design-page-layout)
- [本机PDF要点 — 预先录制的专家讲座](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/knowledge-base/expert-session/native-pdf-publishing-essentials-feb23)

<br>
<br>

在AEM Guides社区上发帖 [论坛](https://experienceleaguecommunities.adobe.com/t5/experience-manager-guides/ct-p/aem-xml-documentation) 以进行任何查询。



