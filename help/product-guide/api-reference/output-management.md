---
title: 用于输出管理的REST API
description: 了解用于输出管理的REST API
exl-id: dab654f5-555d-4a89-bc94-55b1e938f255
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# 用于输出管理的REST API {#id175UB30E05Z}

以下REST API可用于管理AEM Guides中的输出。

## 获取DITA映射的所有输出预设 {#get-output-presets-dita-map}

一种POST方法，可检索为DITA映射配置的所有输出预设。

**请求URL**： http://*&lt;aem-guides-server>*： *&lt;port-number>*/bin/publishlistener

**参数**：\
|名称|类型|必需|描述| --------------------------- |`:operation`|字符串|是|要调用的操作的名称。 此参数的值为 `getalloutputs`.<br> **注意：** 该值不区分大小写。| |`sourcePath`|字符串|是|DITA映射文件的绝对路径。|

**响应值**：返回一个JSON输出预设对象数组，每个对象包含以下元素：

| 元素 | 描述 |
|-------|-----------|
| `outputName` | 输出预设的名称。 输出名称在其定义的DITA映射的范围内是唯一的。 |
| `outputType` | 使用此预设生成的输出类型，例如AEM Site、PDF、EPUB或其他。 可用的选项包括：<br>- AEMSITE <br>-PDF <br>-HTML5 <br>-EPUB <br> — 自定义 |
| `outputTitle` | 输出预设设置的描述性名称。 此值用于定义输出预设的“设置名称”属性的值。 |
| `ditaValPathList` | 用于生成所需输出的DITAVAL文件路径数组。 |
| `targetPath` | 发布或存储输出的路径。 |
| `siteName` | *\(对于AEM站点输出\)* AEM站点的名称。 |
| `templatePath` | *\(对于AEM站点输出\)* 用于生成所需输出的模板节点的路径。 |
| `searchScope` | 指定搜索操作的范围。 此参数的值必须设置为 `local`. |
| `generateTOC` | *\(对于AEM站点输出\)* 指定是否生成目录\(true\) \(false\)。 |
| `generateBreadcrumbs` | *\(对于AEM站点输出\)* 指定是否生成痕迹导航\(true\) \(false\)。 |
| `overwriteStrategy` | *\(对于AEM站点输出\)* 指定是否覆盖目标上的文件\(true\) \(false\)。 |
| `pdfGenerator` | 指定要使用的PDF生成引擎。 可能的值包括：<br>- DITAOT <br>- FMPS |

>[!NOTE]
>
> `DitaValPath` 元素不再受支持。

## 创建输出预设

一种为DITA映射创建新的输出预设的POST方法。

**请求URL**： http://*&lt;aem-guides-server>*： *&lt;port-number>*/bin/publishlistener

**参数**： |名称|类型|必需|描述| --------------------------- |`:operation`|字符串|是|要调用的操作的名称。 此参数的值为 ``createoutput``.<br> **注意：** 该值不区分大小写。| |`sourcePath`|字符串|是|DITA映射文件的绝对路径。| |`outputTitle`|字符串|是|输出预设设置的描述性名称。 此值用于定义输出预设的“设置名称”属性的值。<br> **注意：** 当创建新的输出预设时，后端系统从给定的标题驱动输出预设的唯一名称。| |`outputType`|字符串|是|使用此预设生成的输出类型，例如AEM Site、PDF、EPUB或其他。 可用的选项包括：<br>- AEMSITE <br>-PDF <br>-HTML5 <br>-EPUB <br> — 自定义|

**响应值**： 元素|描述| ------------------ |`outputName`|新创建的输出预设的唯一名称。 此名称派生自 `outputTitle` 参数|

## 保存输出预设

一种POST方法，用于保存输出预设中所做的更改。

**请求URL**： http://*&lt;aem-guides-server>*： *&lt;port-number>*/bin/publishlistener

**参数**： |名称|类型|必需|描述| --------------------------- |`:operation`|字符串|是|要调用的操作的名称。 此参数的值为 ``saveoutput``.<br> **注意：** 该值不区分大小写。| |`sourcePath`|字符串|是|DITA映射文件的绝对路径。| |`outputObj`|字符串|是|包含正在更新的输出预设属性的JSON对象。 此 `outputObj.outputName` 属性包含要更新的输出预设的名称。 有关JSON对象的格式，请参见 **响应值** 中的表 [获取DITA映射的所有输出预设](#get-output-presets-dita-map).|

**响应值**：返回HTTP 200 \(Successful\)响应。

## 获取特定的输出预设

一种POST方法，可检索现有的输出预设。

**请求URL**： http://*&lt;aem-guides-server>*： *&lt;port-number>*/bin/publishlistener

**参数**： |名称|类型|必需|描述| --------------------------- |`:operation`|字符串|是|要调用的操作的名称。 此参数的值为 `getoutput`. <br>**注意：** 该值不区分大小写。| |`sourcePath`|字符串|是|DITA映射文件的绝对路径。| |`outputName`|字符串|是|必须检索其详细信息的输出预设的名称。|

**响应值**： 元素|描述| ------------------ |`outputName`|输出预设的名称。 输出名称在其定义的DITA映射的范围内是唯一的。| |`outputType`|使用此预设生成的输出类型，例如AEM Site、PDF、EPUB或其他。 可用的选项包括：<br>- AEMSITE <br>-PDF <br>-HTML5 <br>-EPUB <br> — 自定义 <br>| |`outputTitle`|输出预设设置的描述性名称。 此值用于定义输出预设的“设置名称”属性的值。| |`ditaValPathList`|用于生成所需输出的DITAVAL文件路径数组。| |`targetPath`|发布或存储输出的路径。| |`siteName`|\(对于AEM站点输出\)AEM站点的名称。| |`siteTitle`|\(对于AEM站点输出\)AEM站点的标题。| |`templatePath`|\(对于AEM站点输出\)用于生成所需输出的模板节点的路径。| |`searchScope`|指定搜索操作的范围。 此参数的值必须设置为 `local`.| |`generateTOC`|\(对于AEM站点输出\)指定是否生成目录\(true\) \(false\)。| |`generateBreadcrumbs`|\(对于AEM站点输出\)指定是否生成痕迹导航\(true\)\(false\)。| |`overwriteFiles`|\(对于AEM站点输出\)指定是否覆盖目标位置的文件\(true\) \(false\)。| |`pdfGenerator`|指定要使用的PDF生成引擎。 可能的值包括：<br>- DITAOT <br>- FMPS|

>[!NOTE]
>
> `DitaValPath` 元素不再受支持。

## 生成输出

一种使用一个或多个输出预设生成输出的GET方法。

**请求URL**： http://*&lt;aem-guides-server>*： *&lt;port-number>*/bin/publishlistener

**参数**： |名称|类型|必需|描述| --------------------------- |`operation`|字符串|是|要调用的操作的名称。 此参数的值为 `GENERATEOUTPUT`.<br> **注意：** 值区分大小写。| |`source`|字符串|是|DITA映射文件的绝对路径。| |`outputName`|字符串|是|用于生成输出的输出预设的名称。 可以使用管道分隔符(“\|”\)指定多个输出预设，例如 `aemsite|pdfoutput`.|

**响应值**：返回HTTP 200 \(Successful\)响应。

## 生成增量输出

使用一个或多个输出预设为AEM Site生成增量输出的GET方法。

**请求URL**： http://*&lt;aem-guides-server>*： *&lt;port-number>*/bin/publishlistener

**参数**： |名称|类型|必需|描述| --------------------------- |`operation`|字符串|是|要调用的操作的名称。 此参数的值为 `INCREMENTALPUBLISH`. <br>**注意：** 值区分大小写。| |`contentPath`|JSON|是|DITA映射文件和主题文件的绝对路径以及输出预设的名称。 使用以下示例作为构建块：|

```XML
{
   {   
   "ditamap": 
      "/content/dam/sample/sample.ditamap",   
   "topics": [     
      "/content/dam/sample/topic1.xml",     
      "/content/dam/sample/topic2.xml"   
         ],   
   "fullMaps": [     
      "/content/dam/sample/submap.ditamap"   
      ],   
   "maps": [     
      "/content/dam/sample/keyspace.ditamap"   
      ],   
   "outputs": [     
      "aemsite"   
      ] 
   }
}
```

- 此 `ditamap` attribute采用用于生成输出的DITA映射的绝对路径。
- 此 `topics` 属性采用一系列已更新且需要重新发布的主题。
- 此 `fullMaps` 属性包含增量输出生成所需的映射文件\（如分块子映射\）的路径及其主题。
- 此 `maps` 属性包含映射文件的路径\（用于解析密钥空间引用\），这些文件在磁盘上提取，没有主题。
- 此 `outputs` attribute采用一系列用于生成输出的输出预设名称。

**响应值**：返回HTTP 200 \(Successful\)响应。

## 删除输出预设

一种删除输出预设的POST方法。

**请求URL**： http://*&lt;aem-guides-server>*： *&lt;port-number>*/bin/publishlistener

**参数**： |名称|类型|必需|描述| --------------------------- |`:operation`|字符串|是|要调用的操作的名称。 此参数的值为 `deleteoutput`.<br> **注意：** 该值不区分大小写。| |`sourcePath`|字符串|是|DITA映射文件的绝对路径。| |`outputName`|字符串|是|要删除的输出预设的名称。|

**响应值**：返回HTTP 200 \(Successful\)响应。
