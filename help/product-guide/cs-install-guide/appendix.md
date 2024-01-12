---
title: 附录
description: 了解如何准备InDesign文档以进行迁移
exl-id: 71b09039-b220-45f3-b334-c23f5b09dadc
feature: InDesign File Conversion, Troubleshooting
role: Admin
level: Experienced
source-git-commit: be06612d832785a91a3b2a89b84e0c2438ba30f2
workflow-type: tm+mt
source-wordcount: '2852'
ht-degree: 0%

---

# 附录 {#id195AD0L60Y4}

## AEM Guides疑难解答

安装和配置AEM Guides后，即可对这些问题进行故障诊断。

## 验证引用

您可以运行给定的脚本来验证引用。 这些脚本可帮助您识别损坏的引用，然后对其进行修补或修复。

- `/bin/fmdita/validatebtree?operation=validate`  — 报告任何损坏的内容引用，但不会修复它们。

- `/bin/fmdita/validatebtree?operation=patch`  — 列出断开的内容引用和修补程序或对其进行修复。


**验证脚本**

使用以下步骤，使用产品包中提供的验证脚本检查引用：

1. 运行验证脚本\[`/bin/fmdita/validatebtree?operation=validate`\]以检查是否存在任何新的断开引用。
1. 如果验证脚本报告任何错误，可以使用修补程序脚本对其进行修补程序。
1. 记录以下提供的详细信息，并在必要时与客户成功团队分享：
1. 
   - 验证脚本打印的日志
- “”的包`/content/fmdita/references`&quot;
- 任何其他所需的详细信息，具体取决于所报告的情景

**修补程序脚本**

使用产品包中提供的修补程序脚本，执行以下步骤来修补任何损坏的引用：

1. 运行修补程序脚本 `[/bin/fmdita/validatebtree?operation=patch]` 修复损坏的参照。 脚本执行需要几分钟时间，并在执行过程中打印日志。 执行完成后，它将打印&quot;`Done`”在末尾。

>[!NOTE]
>
> 建议您复制并保存日志以供参考。

1. 成功执行修补程序脚本后，可以执行以下检查：
1. 
   - 检查新节点»`references_backup_<timestamp>"` 已创建于 `/content/fmdita`
- 检查引用是否已修复

**Logger**

您还可以为此脚本执行创建一个单独的日志程序，如下所示：

- 在类&#39;&#39;上添加记录器`adobe.fmdita.common.BTreeReferenceValidator`&quot;
- 将其设置为 `DEBUG`

创建的日志文件将记录与脚本执行相关的所有信息，并在浏览器会话超时同时从浏览器触发脚本的情况下很有用。

## 准备InDesign文件进行转换 {#id195DBF0045Z}

InDesign为作者提供了一组丰富的功能，用于创建吸引人且复杂的文档。 通常，这意味着文档的各个部分会以可视方式放置在页面上，但不尝试在这些文本框架之间提供任何流向。 当&#39;*阅读顺序*&#x200B;未定义文本框架的&#39;，IDML文件将包含可能未遵循任何有意义的顺序的文章。 最终结果将是一个或多个DITA主题，其中包含以随机顺序排列的段落、表格和图形。

虽然可以在DITA编辑器中将DITA内容编辑为合理的顺序，但在创建IDML文件之前修复InDesign文件要容易得多。 可以在不改变源文档外观的情况下完成此操作。 通过正确定义阅读顺序，它还有助于使源文档可访问。

***串连文本框架***

InDesign使用术语 *&#39;线程&#39;* 用于将一个帧链接到另一个帧的过程。 有关线程化文本框架的更多详细信息，请参见 *[线程文本](https://helpx.adobe.com/in/indesign/using/threading-text.html)* InDesign文档的主题。

***重叠帧***

有些InDesign文档出于布局原因使用无线程重叠框架。 将此内容合并到主线程中可能非常困难。 最佳选项可能是在DITA环境中编辑结果。

***InDesign故事***

InDesign文档中的每个线程内容流都称为&#39;*story*’。 为获得最佳结果，建议限制文章数量。 但是，在DITA输出中可能不需要文档的某些部分。 例如，页脚很少需要，但如果处理不当，它们可能会出现在主题的中间。

排除文档中不需要的文本的最简单方法是为其指定一个特殊的 *段落标记* 仅用于不需要的内容。 例如，不要重复使用 *\[基本段落\]* 对于页脚，创建专用的 *页脚* 标记之前。 然后在MapStyle文件中，只需设置 *页脚* 要删除的段落如下：

```
<paraRule style="Footer" local="0" refactor="drop">
   <attributeRules createID="false"/>
</paraRule>
```

***映射到DITA文档类型***

源文档必须具有至少一个可以标记主题开头的段落样式或元素。 文档通常使用 *标题1* 作为文档中顶级标题的名称。 然后，您可以创建从该样式到特定DITA doctype的映射。 如果您的文档井然有序，并且使用 *标题1* 始终不变，那么你会得到很好的结果。

***多个DITA文档类型***

如果某些 *标题1* 段落需要转换为其他DITA文档类型，然后复制InDesign的段落样式。 为这些样式提供一个易于识别的名称，例如 *Heading1\_genTask* 或 *Heading1\_疑难解答* 视情况而定。 然后，设置mapStyle文件，如下所示：

```
<doctypes>
   <doctypeParaRule style="Heading1" local="0" mapToDoctype="concept">
      <attributeRules createID="true"/>
   </doctypeParaRule>
   <doctypeParaRule style="Heading1_genTask" local="0" mapToDoctype=" generalTask">
      <attributeRules createID="true"/>
   </doctypeParaRule>
   <doctypeParaRule style="Heading1_troubleshooting" local="0"mapToDoctype=" troubleshooting">
      <attributeRules createID="true"/>
   </doctypeParaRule>
</doctypes>
```

***结构化InDesign文档***

InDesign与XML的关系很松散。 虽然文档可以包含XML DTD，并且主故事可能对该DTD有效，但也可以创建一些内容是XML但不包含DTD的混合文档。 这些是成功转换为DITA的不希望出现的情况。 如果文档包含XML部件，请尝试将输出保存为XML，并查看结果是否可接受。 如果不包含，则DITA内容也将包含无效内容，或者可能完全失败。

***表格格式***

从InDesign表格式规则转换为DITA中的等效表格式是一个复杂的过程。 这是因为与DITA中使用的Oasis \(CALS\)表模型提供的基本选项相比，源文件中提供了丰富的格式功能。 提供了垂直和水平文本对齐方式，并且提供了类似的结果，尽管两端对齐的文本始终根据文本方向对齐，而InDesign则允许两端对齐和两端对齐的文本。

InDesign对列和行分隔符的处理，再次比Oasis表格模型的基本选项要强大得多。 InDesign提供四种单元格边框 — 边框类型\（实心或图案\）、边框粗细、边框颜色、边框色调、边框间隙颜色和边框间隙色调。 所有这些都必须向下映射到每个单元格右侧和底部的边框\(entry element\)，其中唯一选项为0或1 — 隐藏边框或显示边框。

InDesign的边界裁定可以应用于以下级别：

- 表格样式
- 单元格样式
- 每个单元格上的本地覆盖

InDesign到DITA的转换过程应用以下边界规则：

- 表样式将映射到 `colspec/@colsep` 垂直规则的属性。 水平规则映射到 `row/@rowsep` 属性。 在这两种情况下，如果未定义边框，则不会创建属性。
- 单元格样式将映射到 `entry/@colsep` 和 `entry/@rowsep` 属性。 这些值将覆盖任何表样式派生的边框规则。
- 局部覆盖将格式设置直接应用于单元格，并覆盖表格样式和单元格样式。

***交替图案***

InDesign表样式允许列和单元格直排遵循交替模式。 虽然该功能支持转换，但只有当一个模式组映射为显示正线\(1\)，而另一个模式组映射为隐藏正线\(0\)时，转换的结果才明显。

## 准备映射文件以InDesign到DITA迁移 {#id194AF0003HT}

正确的DITA转换需要一个与源文档内容匹配的映射文件。 对于非结构化InDesign文档，这意味着需要映射所有可用的段落样式和字符样式。 对于XML结构化InDesign文档，必须映射其关联DTD中的所有元素。

非结构化和结构化InDesign文档的映射文件是不同的。 这是因为将非结构化源内容转换为DITA的处理要求更加复杂。

下面给出了映射文件的示例：

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE styleMap SYSTEM "mapStyle.dtd">
<styleMap xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="mapStyle.xsd" >
   <doctypes>
      <mapDoctypeParaRule root="itpx:stories" mapToDoctype="map">
         <attributeRules createID="true">
            <addNew name="outputclass" value="map"/>
         </attributeRules>
      </mapDoctypeParaRule>
      <doctypeParaRule style="Heading 1" local="0" mapToDoctype="concept">
         <attributeRules createID="true"/>
      </doctypeParaRule>
      <doctypeParaRule style="Heading A" local="0" mapToDoctype="topic">
         <attributeRules createID="true"/>
      </doctypeParaRule>
   </doctypes>
   <wrappingRules>
      <wrap elements="li+" context="number" wrapper="ol">
         <attributeRules createID="true"/>
      </wrap>
      <wrap elements="li+" context="bullet" wrapper="ul">
         <attributeRules createID="true"/>
      </wrap>
   </wrappingRules>
   <paragraphStyleRules>
      <paraRule style="Heading 2" local="0"  mapTo="p">
         <attributeRules createID="true"/>
      </paraRule>
      <paraRule style="Heading 3" local="0"  mapTo="p">
         <attributeRules createID="true"/>
      </paraRule>
      <paraRule style="List Paragraph" local="p[-|-|-|-|-|b|-|-]" context="bullet" mapTo="li">
         <attributeRules createID="true"/>
      </paraRule>
      <paraRule style="List Paragraph" local="p[-|-|-|-|-|n|-|-]" context="number" mapTo="li">
         <attributeRules createID="true"/>
      </paraRule>
      <paraRule style="List Paragraph" local="0" context="bullet" mapTo="li">
         <attributeRules createID="true"/>
      </paraRule>
      <paraRule style="Normal" local="0"  mapTo="p">
         <attributeRules createID="true"/>
      </paraRule>
      <paraRule style="Normal" local="p[-|-|-|-|-|b|-|-]" context="bullet" mapTo="li">
         <attributeRules createID="true"/>
      </paraRule>
      <paraRule style="Title" local="0"  mapTo="p">
         <attributeRules createID="true"/>
      </paraRule>
   </paragraphStyleRules>
   <characterStyleRules>
      <charRule style="Bold" local="0" mapTo="b">
         <attributeRules createID="false"/>
      </charRule>
      <charRule style="Code" local="0" mapTo="codeph">
         <attributeRules createID="false"/>
      </charRule>
      <charRule style="[No character style]" local="c[Bold|-|-|-|-|-|-|-]" mapTo="b">
         <attributeRules createID="false"/>
      </charRule>
      <charRule style="[No character style]" local="c[Italic|-|-|-|-|-|-|-]" mapTo="i">
         <attributeRules createID="false"/>
      </charRule>
   </characterStyleRules>
</styleMap>
```

映射文件是一个具有简单结构的XML文件，其中列出了所有源段落样式和字符样式代码。 文件内容说明如下：

**样式映射**

在 `styleMap` 元素，您可以指定两个可选属性 —  `@map_date` 和 `@map_version` 用于记录映射文件的版本。

**文档类型**

此 `doctypes` 元素列出支持的DITA映射和主题映射。

**映射文档类型段落规则**

此 `mapDoctypeParaRule` 元素是必需的。 不得编辑此元素的属性，因为源XML的根元素始终映射到DITA映射的根 `map` 元素。

**文档类型段落规则**

此 `doctypeParaRule` 元素是必需的。 这为转换过程提供了一种识别新主题开始位置的方法。 通常 `@style` 属性单独用于 `@local` 属性设置为0。 但是，如果所选样式上始终存在本地格式覆盖，则必须为每个样式添加规则及其本地覆盖。 这很容易识别生成的映射文件中可以找到以下内容或类似内容的地方：

```
<paraRule style="Heading 1" local="0" mapTo="p">
   <attributeRules createID="true"/>
</paraRule>
<paraRule style="Heading 1" local="p[Italic|-|-|-|-|-|-|-]" mapTo="p">
   <attributeRules createID="true"/>
</paraRule>
```

在上例中，有两种 `paraRule` 元素 `@style` =“标题1”。 简单地说，创建一个等效项 `doctypeParaRule` 元素和 `@mapToDoctype` 属性集。

中使用的属性 `doctypeParaRule` 详情如下：

- `@style`：源InDesign文档中样式的名称。
- `@local`：请参阅 [\#id194CG0V005Z](#id194CG0V005Z).
- `@mapToDoctype`：所有有效项的枚举列表中DITA主题类型的名称 `doctypes`.

**元素封装规则**

元素封装规则定义根据一组属性值将传入文档中的元素封装或移动到预定义元素中的方式。

***`wrap`元素***

这是一个可选元素。 此 `wrap` 元素列出将封装或移动的元素。 封装通常用于必须为一系列元素指定公共父元素的情况。 例如，多个 `li` 元素封装在 `ol` 元素。 此外， `wrap` 可用于移动元素，例如插图和表格的标题。

中使用的属性 `wrap` 详情如下：

- `@element`：元素名称后的加号显示，名称相同的所有相邻元素将封装在 `@wrapper`属性。
- `@wrapper`：包装元素的名称。
- `@context`：提供进一步细化给定元素包装方式的方法。 以下示例说明映射一系列规则的方法 `li` 已排序列表中的元素 `ol` 或无顺序列表 `ul` 根据 `@context` 值\(上下文定义于 `paraRule` 元素\)：

  ```
  <wrap elements="li+" context="number" wrapper="ol">
     <attributeRules createID="true"/>
  </wrap>
  <wrap elements="li+" context="bullet" wrapper="ul">
     <attributeRules createID="true"/>
  </wrap>
  ```


以下示例说明如何创建 `fig` 元素来自 `title` 和 `image` 元素：

- `@elements`：用逗号列出和分隔的元素将封装在 `@wrapper` 属性。 由于通常在图像下方包含图标题，因此标题将为 `title` 紧跟在后面的元素 `image`.

  以下换行规则：

  ```
  <wrap elements="title, image" context="FigTitle" wrapper="fig">
     <attributeRules createID="true"/>
  </wrap>
  ```

  转换以下中间XML：

  ```
  <image href="Links/myImage.png" scale="59">
     <title>IDML2DITA workflow</title>
  ```

  转换为以下有效的DITA图结构：

  ```
  <fig id="id397504">
     <title>IDML2DITA workflow</title>
     <image href="Links/myImage.png" scale="59">
  </fig>
  ```

- `@wrapper`：包装元素的名称。
- `@context`：提供进一步细化给定元素包装方式的方法\(上下文定义在 `paraRule` 元素\)。

以下示例说明如何移动 `title` 转换为 `table`：

- `@elements`：和 `title` 元素之前或之后紧接的元素 `table` 将封装在 `@wrapper` 属性。 XPath样式谓词可以将title元素的位置标识为 `[before]` 或 `[after]`.

  示例：以下换行规则：

  ```
  <wrap elements="title[before]" context="TableTitle" wrapper="table">
     <attributeRules createID="true"/>
  </wrap>
  ```

  转换以下中间XML：

  ```
  <title>IDML2DITA workflow</title>
  <table id="id289742" outputclass="BasicTable">
     <tgroup cols="2">
        <colspec colname="0" colwidth="0.7*">
           <colspec colname="1" colwidth="0.3*">
  ```

  在此有效的DITA图结构中：

  ```
  <table id="id289742" outputclass="BasicTable">
     <title>IDML2DITA workflow</title>
     <tgroup cols="2">
        <colspec colname="0" colwidth="0.7*">
           <colspec colname="1" colwidth="0.3*">
  ```

- `@wrapper`：包装元素的名称。

- `@context`：提供进一步细化给定元素包装方式的方法\(上下文定义在 `paraRule` 元素\)。


**段落样式规则**

此 `paragraphStyleRule` 元素如下所述：

** `paraRule` 元素**

此 `paraRule` 元素是必需的。 这会指定所有段落样式的映射规则。 在InDesign文档中，所有文本都包含在“段落样式”的子结构中，即使没有任何样式的段落也被命名 `\[No paragraph style\]`. 方括号，表示内置InDesign样式名称。

>[!NOTE]
>
> 方括号表示内置InDesign样式名称。

中使用的属性 `paraRule` 详情如下：

- `@style`：源InDesign文档中样式的名称。
- `@local`：请参阅 [\#id194CG0V005Z](#id194CG0V005Z).
- `@mapTo`：DITA目标元素的名称。

- `@context`：此属性用于链接到特定的 **换行** 规则是否提供了多个包装器选择。 示例： `li` 元素可以封装在 `ol`，或 `ul` 元素。 要标识不同的列表类型，可以使用特定的样式名称或 `@local` 属性，其中可显示以下内容：
   - `local="p[-|-|-|-|-|b|-|-]"` 其中&#39;`b`&#39;在字段6中，表示项目符号列表项。 在本例中，设置 `@context` 到&#39;`bullet`’。
   - `local="p[-|-|-|-|-|n|-|-]"` 其中&#39;`n`字段6中的&#39;表示编号列表项。 在本例中，设置 `@context` 到&#39;`number`’。

- `@commentOut`：此属性允许以XML注释封装目标元素，以便信息不会丢失，但用户可以手动处理。 如果无法强制源内容符合DITA结构规则，这将很有用。

- `@refactor`：此可选属性可以选择两个值：

- `unwrap`：删除匹配的元素，同时保留其内容。

- `drop`：删除匹配的元素及其所有内容。


**字符样式规则**

此 `charRule` 元素如下所述：

>[!NOTE]
>
> 内置字符样式将没有映射 `[No character style]` 时间 `local="0"`，因为这些变量在预处理期间会被删除。

***`charRule`元素***

这是一个可选元素。

这些是所有字符样式的映射规则。 在InDesign文档中，所有文本都包含在字符样式的子元素中。

中使用的属性 `charRule` 详情如下：

- `@style`：源InDesign文档中样式的名称。
- `@local`：请参阅 [\#id194CG0V005Z](#id194CG0V005Z).
- `@mapTo`：DITA目标元素的名称。
- `@refactor`：此可选属性可以选择两个值：
   - `unwrap`：删除匹配的元素，同时保留其内容。

   - `drop`：删除匹配的元素及其所有内容。


**属性规则**

此元素可以是以下元素上下文的子元素：

- `mapDoctypeParaRule`
- `mapDoctypeElemRule`
- `doctypeParaRule`
- `doctypeElemRule`
- `paraRule`
- `charRule`
- `elementRule`

属性规则的用途是管理匹配元素的属性。

根据上下文，以下属性可用 `attributeRules` 元素：

- `@createID`：为匹配的元素生成唯一ID。 允许的值 `true` 或 `false`. 在所有上下文中均可用。
- `@copyAll`：仅从结构化源文件的源XML内容中复制所有属性。 允许值为 `true` 或 `false`. 可用于上下文 `mapDoctypeParaRule`， `mapDoctypeElemRule`， `doctypeElemRule` 和 `elementRule`.


中使用的属性 `attributeRules` 详情如下：

>[!NOTE]
>
> 此元素可以包含多个子元素。

- `addNew`：向匹配的元素添加新属性。 可用于所有上下文。 它具有两个属性：
   - `@name`：必须是合法的XML名称，最好对DITA上下文有效。
   - `@value`：可以是文本或简单的XPath表达式。
- `copyAtt`：将单个属性复制到目标，但可以选择在此过程中重命名该属性。 此值不会更改。 可用于上下文 `mapDoctypeParaRule`， `mapDoctypeElemRule`， `doctypeElemRule` 和 `elementRule`. 当此元素存在时， `@copyAllAtts` 假定值为 `false`. 它具有两个属性：
   - `@name`：必须是源XML元素上存在的属性的名称。
   - `@mapTo`：必须是合法的XML名称，最好对DITA上下文有效。

**本地格式代码**

在任何InDesign文档中，段落样式和字符样式都可以包含数百种不同的格式覆盖。 这些属性中的大多数在转换过程中没有发挥任何有用的作用。 但是，我们已确定了一组核心格式特征，这些特征确实会影响文档的语义，并且需要影响转换过程。

此 `@local` 属性以特殊分隔格式显示，其中提供了8个字段以及前缀，以显示格式覆盖的类型。 下面列出了格式化代码字段：

- 前缀 **p** 对于para样式本地覆盖或 **c** 用于字符样式本地覆盖。
- **字体样式** ，即系列名称和属性，例如“***加粗斜体***’。
- **字体大小** 以点为单位。
- **字符位置** 用于上标或下标。
- **下** 用于下划线。
- **罢工** 用于删除线。
- **列表代码** 将列表类型标识为项目符号或编号 — 并不总是由InDesign使用。
- **项目符号代码** 列出文档中所有已定义的项目符号类型。
- **编号代码** 列出文档中所有已定义的编号样式。

谨慎使用此功能会丢失本地格式，这有助于提高从样式化内容传输到DITA的质量。 此示例可以解析为项目符号列表中表示16pt斜体文本： `p[Italic|16|-|-|-|b|-|-]`.

**结构映射**

结构映射文件类似于样式映射文件，其结构非常简单，列出了所有源元素和相关属性类型。 两个属性， `@map_date` 和 `@map_version` 提供用于记录要使用的映射文件的版本。

**文档类型**

此 `doctypes` 元素列出支持的DITA映射和主题映射。

**映射文档类型元素规则**

此 `mapDoctypeElemRule` 元素是必需的。 不得编辑此元素的属性，因为源XML的根元素始终映射到DITA映射的根 `map` 元素。

**元素封装规则**

请参阅 [\#id194CG600NY4](#id194CG600NY4).

**`elementRules`元素**

这将列出所有 [\#id194CGC00SHS](#id194CGC00SHS)元素。

**`elementRule`元素**

此 `elementRule` 元素是必需的。 这些是所有源元素的映射规则。 虽然InDesign文档不包含非结构化样式元素，但结构化内容将忽略这些元素，除非“***混合模式***&#x200B;已启用&#39;处理。

中使用的属性 `elementRule` 详情如下：

- `@elementName`：源InDesign文档中元素的名称。

- `@local`：请参阅 [\#id194CG0V005Z](#id194CG0V005Z). \（仅适用于混合文档\）。

- `@mapTo`：DITA目标元素的名称。

- `@refactor`：此可选属性可以选择两个值：

   - `unwrap`：删除匹配的元素，同时保留其内容。

   - `drop`：删除匹配的元素及其所有内容。

- `@context`：当有多个包装器选择可用时，此属性用于链接到特定的包装规则。 示例： `li` 元素可以封装在 `ol`，或 `ul` 元素。

- `@commentOut`：此属性允许以XML注释封装目标元素，以便信息不会丢失，但用户可以手动处理。 如果无法强制源内容符合DITA结构规则，这将很有用。
