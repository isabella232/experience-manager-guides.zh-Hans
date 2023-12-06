---
title: ePub预设
description: 了解如何从地图仪表板创建EPUB预设。 在AEM Guides中配置EPUB输出预设。
exl-id: b6fb5483-064e-4552-84c7-b6723b79d8c5
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 1%

---

# ePub {#id205BED020YT}

可以从地图仪表板创建EPUB预设。

>[!NOTE]
>
> 您可以选择使用DITA-OT或FMPS生成HTML5的方法\（如果系统管理员已配置它\）。

要打开EPUB的输出预设，请单击DITA映射文件，单击输出预设，然后单击EPUB选项。 以下选项可用于EPUB输出：

| ePub选项 | 描述 |
| --- | --- |
| 输出类型 | 要生成的输出类型。 要生成EPUB输出，请选择EPUB选项。 |
| 设置名称 | 为您正在创建的EPUB输出设置提供一个描述性名称。 例如，您可以指定 _内部客户输出_ 或 _最终用户输出_. |
| DITA-OT命令行参数 | 指定在生成输出时希望DITA-OT处理的其他参数。 有关DITA-OT中支持的命令行参数的详细信息，请参见 [DITA-OT文档](https://www.dita-ot.org/). |
| 使用以下方式生成EPUB | 选择DITA-OT以生成EPUB输出。 |
| 使用以下方式应用条件 | 选择以下选项之一：<br><br>* **未应用**：如果您不想对已发布的输出应用任何条件，请选择此选项。<br>* **DITAVal文件**：选择DITAVal文件以生成个性化内容。 可使用浏览对话框或键入文件路径来选择多个DITAVal文件。 使用文件名旁边的交叉图标可将其删除。 DITAVal文件将按指定的顺序进行计算，因此第一个文件中指定的条件优先于后续文件中指定的匹配条件。 您可以通过添加或删除文件来维护文件顺序。 如果将DITAVal文件移动到其他位置或将其删除，则不会从映射操控板中自动将其删除。 如果移动或删除了文件，则需要更新位置。 您可以将鼠标悬停在文件名上以查看存储该文件的AEM存储库中的路径。 您只能选择DITAVal文件，如果已选择任何其他文件类型，则会显示错误。 FrameMaker Publishing Server不支持多个DITAVAL文件。<br>* **条件预设**：从下拉列表中选择条件预设，以在发布输出时应用条件。 如果您在DITA映射控制台的条件预设选项卡中添加了条件，则该选项可见。 要了解有关条件预设的更多信息，请参阅 [使用条件预设](generate-output-use-condition-presets.md#id1825FL004PN). |
| 目标路径 | AEM存储库中存储EPUB输出的路径。 |
| 文件名 | 指定要用于保存EPUB输出的文件名。<br><br>**注意**：如果不提供文件名，则使用DITA映射的标题来生成最终EPUB输出文件名。 如果映射没有标题，则使用DITA映射的文件名命名最终EPUB输出。 使用系统中配置的规则清理文件名，以处理任何无效字符。 |
| 转换名称 | 指定要生成的输出类型。 如果您要使用自己的自定义插件（该插件集成在DITA-OT插件中）生成输出，则需要使用此插件。 例如，如果要生成XHTML输出，请指定 `xhtml`. 有关DITA-OT中可用的转换列表，请参见 [DITA-OT转换（输出格式）](http://www.dita-ot.org/2.3/user-guide/AvailableTransforms.md) OASIS DITA-OT用户指南中的。 |
| 清理DITA-OT临时文件 | 选择此选项可清除DITA-OT生成的临时文件。 可以在输出生成日志中找到DITA-OT存储临时文件的位置。<br><br>如果在通过DITA-OT生成输出时遇到错误，可以取消选择此选项以保留临时文件。 然后，您可以使用这些文件排除输出生成错误。 |
| 运行后期生成工作流 | 选择此选项时，将显示一个新的后期生成工作流下拉列表，其中包含在AEM中配置的所有工作流。 必须选择要在输出生成工作流完成后执行的工作流。<br><br>**注意**：有关创建自定义输出后生成工作流的更多信息，请参阅 _自定义输出后生成工作流_ 在as a Cloud Service安装和配置Adobe Experience Manager Guides中。 |
| 使用基线 | 如果已为所选DITA映射创建了基线，请选择此选项以指定要发布的版本。<br><br>请参阅 [使用基线](generate-output-use-baseline-for-publishing.md#id1825FI0J0PF) 了解更多详细信息。 |
| 属性 | 选择要作为元数据处理的属性。 这些属性是从DITA映射或书签文件的属性页面设置的。 从下拉列表中选择的属性列在“属性”字段的下方，并从下拉列表中删除。 设置后，这些属性也会复制到映射中的主题中。<br><br>**注意**：您还可以使用DITA-OT发布将元数据传递到输出。 有关详细信息，请参阅， [使用DITA-OT将元数据传递到输出](pass-metadata-dita-ot.md#id21BJ00QD0XA). |

**父主题：**[&#x200B;了解输出预设](generate-output-understand-presets.md)
