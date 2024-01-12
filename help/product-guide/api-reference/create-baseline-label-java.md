---
title: 用于基线和标签的基于Java的API
description: 了解用于基线和标签的基于Java的API
exl-id: 0e2ba1bb-f5bf-44da-848a-a55385460c83
feature: Java-Based API Baseline
role: Developer
level: Experienced
source-git-commit: be06612d832785a91a3b2a89b84e0c2438ba30f2
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---

# 用于基线和标签的基于Java的API {#id175UB30E05Z}

以下基于Java的API允许您创建基线并向基线中的文件添加标签。 这些API以捆绑包形式提供。 您必须在代码中包含此捆绑包才能使用这些API。

捆绑包详细信息：

- 组ID： **com.adobe.fmdita**

- 工件ID： **api**

- 版本： **3.5**

- 包： **com.adobe.fmdita.api.baselines**

- 类详细信息：

  ```JAVA
  public class BaselineUtils extends Object
  ```

  此 **基线实用程序** 类包含用于创建基线以及将标签应用于基线中文件的方法。


## 创建基线

创建基线方法有两个版本 — 一个用于XML Documentation解决方案版本3.5，另一个用于3.5之前的版本\（包括版本3.4、3.3和3.2\）。 3.5版API允许使用映射文件中的标签、直接引用和间接引用创建基线。

API的另一个版本使用日期和时间创建基线。 保留此API是为了与使用XML Documentation解决方案3.4、3.3或3.2的系统保持向后兼容性。

**语法\（适用于版本3.5\）**：

```JAVA
public static String createBaseline(Session session, 
String sourcePath, 
String baselineTitle, 
String label, 
LinkedHashMap directContext, 
LinkedHashMap indirectContext) 
throws GuidesApiException
```

**参数**： 名称|类型|描述| --------文----------- |`session`|javax.jcr.Session|有效的JCR会话。 用户会话需要同时具有DITA映射的读取和写入权限以及基线中包含的所有引用文件的读取权限。| |`sourcePath`|字符串|AEM存储库中DITA映射文件的绝对路径。| |`baselineTitle`|字符串|基线的唯一标题。| |`label`|字符串|选择应用了给定标签的主题版本。| |`directContext`|LinkedHashMap&lt;string object=&quot;&quot;>|选择直接引用主题\(content\)的配置，按照映射中提到的顺序解析版本。 <br> 如果在迭代映射的所有键后未找到版本，则基线创建过程将失败。 <br> 如果HashMap为空\（发送空映射，默认为null映射\），则默认填充为： <br>`directContext.put("label", label);` <br> `directContext.put("latest", true);` <br> 如果您希望基线创建仅选取给定标签的版本，如果没有此类版本，则失败，请将 `label` 键和要在其中创建基线的标签。| |`indirectContext`|LinkedHashMap&lt;string object=&quot;&quot;>|选择间接引用主题\（引用的内容\）所依据的配置，按照映射中提到的顺序解析版本。 <br> 如果在迭代映射的所有键后未找到版本，则基线创建过程将失败。 <br> 如果HashMap为空\（发送空映射，默认为null映射\），则默认填充为： <br>`indirectContext.put("label", label);` <br>`indirectContext.put "pickAutomatically", null);` <br> 如果您希望它成为最新版本而不是自动选取版本，请替换： <br>`indirectContext.put("pickAutomatically", null);` <br> _替换为：_ <br>`indirectContext.put("latest", true)`|

**返回**：基线的名称，是JCR存储库中基线的节点名称。 新创建的基线的标题将显示在DITA映射的“基线”页上，供用户使用。

**例外**：丢弃 ``ItemExistExceptiom`` 已存在具有相同标题的基线。

**语法\（适用于版本3.4、3.3和3.2\）**

```JAVA
public static String createBaseline
(Session session, 
String sourcePath, 
String baselineTitle, 
Date versionDate) throws GuidesApiException
```

**参数**： 名称|类型|描述| --------文----------- |`session`|javax.jcr.Session|有效的JCR会话。 用户会话需要同时具有DITA映射的读取和写入权限以及基线中包含的所有引用文件的读取权限。| |``sourcePath``|字符串|AEM存储库中DITA映射文件的绝对路径。| |`baselineTitle`|字符串|基线的唯一标题。| |`versionDate`|日期|基线是使用此日期的主题版本\（直接从DITA映射中引用\）创建的。 指定日期 `d-MM-yyyy H:mm` 格式|

**返回**：基线的名称，是JCR存储库中基线的节点名称。 新创建的基线的标题将显示在DITA映射的“基线”页上，供用户使用。

**例外**：丢弃 ``RepositoryException.``

## 应用标签

此 ``applyLabel`` 方法将一个或多个标签应用于基线中的文件。

**语法**：

```JAVA
public static void applyLabel(Session session,
                  String sourcePath,
                  String baselineName,
                  String label)
                  throws RepositoryException, WorkflowException, Exception
```

**参数**： 名称|类型|描述| --------文----------- |`session`|javax.jcr.Session|有效的JCR会话。| |`sourcePath`|字符串|AEM存储库中DITA映射文件的绝对路径。| |``baselineName``|字符串|必须应用标签的基线节点的名称。 要获取基线节点的名称，您可以使用 [\#id185NFF0085Z](#id185NFF0085Z) 方法或检查CRXDE中DITA映射的基线节点。<br> **注意：** 标签应用于从基线中的映射文件直接引用的文件版本。| |`label`|字符串|应用于基线中文件的标签。 确保标签不包含以下字符：&amp;sol； &amp;comma； &amp;colon； &amp;comma； &amp;lbrack； &amp;comma； &amp;rbrack； &amp;comma； &amp;vert； &amp;comma； &amp;ast； <br> 如果要设置多个标签，请用逗号分隔标签；例如Label1， Label2.|

**例外**：丢弃 `RepositoryException`.

## 删除标签

此 ``deleteLabel`` 方法会从基线中的文件删除一个或多个标签。

**语法**：

```JAVA
public static Map
<String, String> deleteLabel(Session session, 
String sourcePath, 
String baselineName, 
String label) throws GuidesApiException
```

**参数**： 名称|类型|描述| --------文----------- |`session`|javax.jcr.Session|有效的JCR会话。| |`sourcePath`|字符串|AEM存储库中DITA映射文件的绝对路径。| |`baselineName`|字符串|必须从中删除标签的基线名称。 <br> **注意：** 从直接从基线中的映射文件引用的文件版本中删除标签。| |`label`|字符串|要从基线中的文件删除的标签。 <br> 如果要删除多个标签，请用逗号分隔标签；例如Label1， Label2.|

**返回**：映射和 *键：值* 对 `path:deletedlabels` 基线中的所有文件。

**例外**：丢弃 ``RepositoryException`, `VersionException`, `Exception``.
