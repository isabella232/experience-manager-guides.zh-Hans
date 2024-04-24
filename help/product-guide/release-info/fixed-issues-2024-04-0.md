---
title: 发行说明 | 修复了Adobe Experience Manager Guides 2024.4.0版本中的问题
description: 了解Adobe Experience Manager Guidesas a Cloud Service2024.04.0版本中的错误修复。
source-git-commit: 9d1b0bea20b2fe3ae8fb2ee7cf4387cf7271562d
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---


# 修复了2024.04.0版本中的问题

本文介绍Adobe Experience Manager Guidesas a Cloud Service2024.04.0版各个方面修复的错误。

有关新增功能和增强功能的详细信息，请查看 [2024.04.0版本中的新增功能](whats-new-2024-04-0.md).

了解 [2024.04.0版的升级说明](upgrade-instructions-2024-04-0.md).

## 创作

- 此 **复制** 函数无法复制Adobe Experience Manager as a Cloud Service中的空文件夹。 (15353)
- Web编辑器无法上传.pptx文件。 (14837)
- 在Web编辑器中查找文本时，按Enter键光标将返回到搜索文本的第一次出现。 (14820)
- 自动保存会导致多个问题，它会重新定位光标，并需要手动单击文档。 (14253)
- 打开通过全局找到的文件后，搜索结果将被禁用 **查找和替换**. (12142)
- 在源视图中， `</conbody>` 偶尔会插入不正确的位置。 (11305)
- 在XML编辑器中，工具提示功能无法更新“源”字段。 (15847)
- 此 **共享UUID链接** 功能不适用于Adobe Experience Manager中的图像。 (15598)
- 中出现重叠文本问题 `<reltable>` 和 `<fig>` 标记之间。 (15238)
- 出现闪烁问题的位置 **属性** 面板。 (15237)
- 删除内容中的字符或单词时，光标在块元素之间跳转。 (15224)
- 此 **属性** 面板不会显示在Web编辑器的“源”视图中。 (14387)
- 在Web编辑器的标记末尾编辑时，会添加不需要的不间断空格。 (11786)
- 在更正DITA文件中的拼写错误时，内容将被删除。 (11610)


## 发布

- 在以下情况下，AEM站点输出生成失败： **删除孤立站点** 选项。 (15896)
- 将文件添加到映射集合时，编辑功能不起作用。 (15813)
- 在JSON输出中，来自DITA映射或主题的元数据无法传播到JSON输出文件。 (15713)
- 重命名预设时，本机PDF发布失败。 (15662)
- 此 **源路径** 发布的AEM站点输出中的属性不正确。 (15502)
- 语言变量选择和自定义在本地PDF输出预设中无法正常工作。 (15399)
- 使用具有大型样式表或布局的PDF时，本机模板生成失败。 (15344)
- 在以下情况下，已发布输出中的内容无法正确呈现 `<conref>` 与绝对路径一起使用。
- 由于AEM Sites URL与 `fmdita rewriter` 和 `ResourceResolver`. (14793)
- 此 **processing-role=&quot;resource-only&quot;**， **search=&quot;no&quot;**、和 **chunk=&quot;to-content&quot;** 在AEM Sites输出中，属性分别显示为irasely 。 (14442)
- 如果在任何文件夹配置文件的文件夹路径中设置了包含2k个映射的文件夹，则应用于输出预设的更改将失败。(14852)

## 管理

- 未关闭 **资源解析程序** 导致2023年10月版的《Experience Manager指南》as a Cloud Service出现会话计数增加和PathNotFoundException错误。 (15604)
- 功能标记 **fmdita.useapproval** 未按预期工作。 (15310)
- 使用Java API创建基线不适用于2023年6月版的Experience Manager指南as a Cloud Service。 (14787)
- 此 `/bin/fmdita/import` 当上传的资产超过500 MB时，API无限期地停留在待处理请求中。 (14743)

## 审查

- 删除审阅节点会中断在Adobe Experience Manager Guides中打开和查看注释的功能。 (15366)
- 在Web编辑器中，审阅面板加载缓慢。 (14680)

## 翻译

- **接受翻译** 无法完成临时文件的翻译。 (14665)

