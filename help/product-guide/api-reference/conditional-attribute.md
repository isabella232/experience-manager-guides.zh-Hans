---
title: 用于条件属性的REST API
description: 了解用于条件属性的REST API
exl-id: 1f0e023a-422c-47b9-917f-b0d80090471c
feature: Rest API Conditional Attributes
role: Developer
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# 用于条件属性的REST API {#id175UB30E05Z}

以下REST API允许您在文件夹配置文件中添加条件属性。

## 在文件夹级别的配置文件中添加条件属性

一种POST方法，用于将条件属性添加到给定的文件夹级配置文件。

**请求URL**：\
http://*&lt;aem-guides-server>*： *&lt;port-number>*/bin/fmdita/folderprofiles

**参数**：\
|名称|类型|必需|描述| --------------------------- |`:operation`|字符串|是|要调用的操作的名称。 此参数的值为 ``ADDATTRIBUTEPROFILES``. <br> **注意：** 该值不区分大小写。| |`profilename`|字符串|是|必须添加条件属性的文件夹级别配置文件的显示名称。| |`conditionalprofiles`|JSON数组|是|由条件属性名称和值组成的JSON数组。 以下示例代码片段显示了具有两个属性的JSON数组 —  `platform` 和 `product` 为其分配了多个值。|

```JSON
[  {    name: "platform",    
        values: [       
                {value: "win", label: "Windows"},       
                {value: "mac", label: "Mac OS"}    
                ]},
                {    
                    name: "product",    
                    values: [      
                        {value: "aem_1", label: "AEM 6.1"},     
                        {value: "aem_4,  label: "AEM 6.4"}  
                        ]  
                }]
```

**响应值**：\
返回HTTP 200 \(Successful\)响应。
