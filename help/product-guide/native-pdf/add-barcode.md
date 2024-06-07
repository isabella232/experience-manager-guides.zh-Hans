---
title: 本机PDF发布功能 | 添加条形码
description: 了解如何添加条形码。
source-git-commit: a766353908829ab433173f8fd003ecad0c9d1bf1
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---


# 向PDF输出添加条形码

条形码是一种机器可以读取的数据模式。 客户可以使用条形码扫描仪或智能手机摄像头扫描条形码。 产品详细信息、库存编号或网站URL等编码信息可能会有所帮助。 添加条形码可帮助您轻松捕获数据，增强客户体验，并有助于更好的数据管理和安全性。

您可以为条形码创建样式。 并用于在页面布局中插入条形码。 您可以按所需的页面布局将样式应用于条形码示例。


本教程可帮助您在PDF输出中添加条形码。

## 生成条形码的步骤

要生成条形码，请执行以下步骤：

### 更新模板的CSS以渲染条形码值

修改 `layout.css` 文件以在PDF生成期间呈现条形码。 支持各种条形码类型，如“qrcode”和“pdf417”。  有关详细信息，请查看 [条形码类型](#barcode-types).



```css
...
.barcode { 
-ro-replacedelement: barcode;   
-ro-barcode-type: code128;   
-ro-barcode-size: 100%;   
-ro-barcode-content: content();   
object-fit: contain;   
margin-top: 2mm;
 
}
...
```

### 使用CSS样式生成条形码

您可以通过不同的方式生成条形码。 以下是一些示例：

**示例 1**

在模板标题中添加条形码占位符并应用样式：

1. 编辑 **模板** > **页面布局**
1. 选择页面布局。 例如，您可以选择“后盖”页面布局，其中包含页眉或页脚。
1. 将以下范围添加到要插入条形码的位置。

   `<span class="barcode">Sample barcode</span></p>`。

   >[!NOTE]
   >
   > 使用您在中定义的相同类名 `layout.css`.

1. 替换 `<Sample barcode>` 使用您希望条形码扫描仪读取的值……

使用包含页面布局的模板生成输出PDF时，您可以查看条形码。 执行上述步骤后，可以使用条形码生成PDF输出。

以下屏幕截图在PDF输出中显示一个条形码示例。

<img src="./assets/barcode-output-sample.png" alt="带有条形码的示例输出" width="700" border="2px">

**示例 2**

修改 `Common.plt` 中的文件 **基本** 用于在项目标题后添加条形码的模板。

要为ISBN编号创建条形码，请添加ISBN编号。 然后使用ISBN编号生成条形码。

```html
...

  <div data-region="header">
    <p class="chapter-header"><span data-field="project-title" data-format="default">Project Title</span> </p>
    <p><span class="barcode">978-1-56619-909-4</span></p>
  </div>
} 
...
```

**示例 3**

要使用映射元数据创建条形码，请执行以下操作：

使用中存在的任意元数据 `<topicmeta>` 要显示为条形码的DITA映射元素。 确保使用正确的XPath。 例如，您可以添加 `<resourceid>` 在 `<topicmeta>` DITA映射的。

在以下示例中，资源ID用作生成条形码的主输入。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE map PUBLIC "-//OASIS//DTD DITA Map//EN" "technicalContent/dtd/map.dtd">
<map id="GUID-3c330691-4dac-4020-904a-d2d6246aeeb1-en">
  <title>Barcode Sample</title>
  <topicmeta>
    <resourceid id="7a5bda1c-b1db-4fd8-8763-a731e2e8abba">
    </resourceid>
  </topicmeta>
  <topicref href="GUID-139f6c64-bea3-4f17-8b22-ee131557e249-en.dita" type="topic">
  </topicref>
</map>  
```



您可以在页面布局中使用资源ID，如下所示：


```html
  <div data-region="header">
    <p class="chapter-header"><span data-field="project-title" data-format="default">Project Title</span> </p>
    <p><span class="barcode" data-field="metadata" data-format="default" data-subtype="//resourceid/@id">Resource ID (barcode)</span></p>
  </div>
} 
```

## 条形码类型 {#barcode-types}

一些常用的条形码如下：

| 类型 | -ro-barcode-type | 其他详细信息 |
| ---| --- | --- |
| QR代码 | qrcode | 根据ISO/IEC 18004：2015的二维码条码符号。 |
| 代码128 | 代码128 | ISO/IEC 15417：2007中定义的代码128条码符号。 |
| 代码32 | 代码32 | 代码32，也称为意大利军码。 |
| 代码49 | 代码49 | ANSI/AIM-BC6-2000中的代码49。 |
| 代码11 | 代码11 |                            |
| 代码93 | 代码93 |                            |
| 代码16k | 代码16k |                            |
| PDF417 | pdf417 | PDF417/MicroPDF417条码符号符合ISO/IEC 15438：2006和ISO/IEC 24728：2006。 |
| 第3个代码（共9个） | 代码39 | 根据ISO/IEC 16388：2007,9条码符号的代码3。 |
| MSI Plessey | msiplessey |                            |
| 渠道代码 | channelcode | 根据ANSI/AIM BC12-1998编写通道代码。 |
| Codabar | codabar | 根据BS EN 798:1996，代码代码符号学。 |
| EAN-8 | ean-8 | 根据BS EN 797:1996的EAN条码符号。 |
| EAN-13 | ean-13 | 根据BS EN 797:1996的EAN条码符号。 |
| UPC-A | upc-a | 根据BS EN 797:1996的UPC条码符号。 |
| UPC-E | upc-e | 根据BS EN 797:1996的UPC条码符号。 |
| Ean/UPC附加模块 | 加载项 | 根据BS EN 797:1996，EAN/UPC附加条码符号。 |
| Telepen | 电话笔 | 也称为TelepenAlpha。 |
| GS1数据库/数据库14 | 数据库 | GS1 DataBar符合ISO/IEC 24724：2011。 |
| GS1数据库已扩展/数据库已扩展14 | 数据库扩展 | GS1 DataBar根据ISO/IEC 24724：2011扩展。 |
| GS1数据库有限公司 | 数据库限制 | GS1 DataBar根据ISO/IEC 24724：2011受限。 |
| POSTNET（邮政数字编码技术） | postnet | 美国邮政局使用的POSTNET（邮政数字编码技术）条形码符号。 |
| Pharmazentralnummer (PZN-8) | pzn8 | 德国制药业使用的基于代码39的符号学。 |
| Pharmacode | pharmacode |                            |
| 代码块F | codablockf | 根据AIM Europe的符号“统一符号规范Codablock F”，1995年。 |
| Logmars | logmars | 美国国防部使用的LOGMARS（自动标记和读取符号的物流应用）标准。 |
| Aztec Runes | aztec-runes | 根据ISO/IEC 24778：2008附件A的Aztec Runes条码符号。 |
| Aztec代码 | aztec-code | 根据ISO/IEC 24778：2008，Aztec代码条码符号。 |                            |
| 数据矩阵 | 数据矩阵 | 数据矩阵ECC 200条码符号根据ISO/IEC 16022：2006。 |
| 代码1 | code-one |                            |



