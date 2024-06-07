---
title: 使用工具配置数据源连接器
description: 了解如何使用工具配置数据源连接器。
exl-id: d7cd412b-89ea-43a5-97b3-09944863bbee
feature: Web Editor Configuration
role: Admin
level: Experienced
source-git-commit: 873542cb2e8e1b7e80e0ecc113cae4f603b18592
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# 从用户界面配置数据源连接器

Experience Manager指南随附于 **数据源** 此工具可帮助您为数据源配置现成的连接器。 您可以设置JIRA、SQL(MySQL、PostgreSQL、Microsoft SQL Server、SQLite、MariaDB、H2DB)、AdobeCommerce、Elasticsearch和通用REST客户端连接器。


除了这些现成的连接器外，Experience Manager指南还为Salsify、Akeneo和Microsoft Azure DevOps Boards (ADO)数据源提供连接器。 您可以从以下位置下载并安装这些开源连接器 [Maven中央存储库](https://central.sonatype.com/search?q=com.adobe.aem.addon.guides). 然后，用户可以配置这些连接器。
了解如何 [安装开源连接器](#install-open-source-connector).



您还可以使用文件连接器连接到JSON数据文件。 从您的计算机中上传JSON文件或从Adobe Experience Manager资源中浏览该文件。 然后，使用生成器创建内容片段或主题。

要配置连接器，请执行以下步骤：

1. 选择 **Adobe Experience Manager** 单击顶部的链接，然后选择“工具”。
1. 选择 **指南** 工具列表中。
1. 选择 **数据源** 磁贴。 此 **数据源** 页面。 您可以查看连接的数据源。

   您可以在 **列表视图** 或 **平铺视图** 以列表或图块形式查看各种连接的数据源。

   <img src="./assets/data-sources-create-window.png" alt= "数据源页面上列出的数据源" width="800">

   *查看或创建数据源连接器。*
1. 单击&#x200B;**创建**。
1. 选择要为其创建连接器的数据库。 例如，Elasticsearch连接器。
   >[!NOTE]
   >
   >列出所有可用的现成数据库。

1. 单击&#x200B;**下一步**。
1. 根据数据库输入配置和连接详细信息。

   >[!TIP]
   >
   >* 将鼠标悬停在 <img src="./assets/info-details.svg" alt= "信息图标" width="25"> 在字段附近查看有关它的更多详细信息。
   > * 带*的字段为必填字段。 例如，您可以为Elasticsearch连接器输入以下详细信息。

   * **名称**：输入数据源的名称。
   * **身份验证类型**：从下拉列表中选择身份验证类型。 例如，基本的用户名 — 密码身份验证
   * **用户名**：输入您的用户名。
   * **密码**：输入您的用户名和密码。
   * **URL**：添加API URL。


1. 选择 **排除工厂模板** 用于排除工厂模板以用于生成主题和代码片段的选项。 它们将不会显示在 **数据映射模板** 中的下拉菜单  **添加内容片段生成器** 或 **添加主题生成器** 对话框。


1. 选择 **测试连接**. 您可以查看 **测试连接** 仅在添加所需的详细信息后启用按钮。 如果连接详细信息正确，请查看成功消息。 否则，您可能会看到一条错误消息。



1. 选择 **保存** 以保存连接器。     查看 **保存** 在填写所有详细信息且连接成功后启用按钮。


   如果连接器保存成功，则可以在页面上查看连接的数据源。

**连接到多个资源**

您可以根据某些Connectors的不同URL添加或使用多个资源，这些连接器包括Generic REST Client、Salsify、Akeneo和Microsoft Azure DevOps Boards (ADO)。 然后，与他们联系，使用生成器创建内容片段或主题。

执行以下步骤可创建资源：

1. 选择 ![“添加”图标](assets/Add_icon.svg) 在 **URL资源部分** 为每个URL添加资源。
1. 在中配置所有详细信息 **添加资源** 对话框。
1. 单击 **添加**.
1. 您可以编辑 ![编辑图标](assets/edit_pencil_icon.svg) 或删除 ![删除](assets/Delete_icon.svg) url资源列表中的资源。

1. 您还可以使用可用于数据源(如Salsify、Akeneo和Microsoft ADO)的默认资源。 将您不想为数据源配置的资源的选项切换为OFF。

这有助于从单个内容片段或主题中特定数据源的任何资源快速获取数据。



## 安装开源连接器{#install-open-source-connector}

要发布上存在的依赖项，请执行以下操作 [Maven中央存储库](https://central.sonatype.com/search?q=com.adobe.aem.addon.guides) 对于Cloud Service，您需要包含并嵌入开源连接器的依赖项。

1. 在中添加依赖项 `all/pom.xml`  在您的cloud manager Git项目代码中。 例如，您可以为Microsoft Azure DevOps Boards数据源连接器添加以下依赖项。


   ```
   <dependency>
       <groupId>com.adobe.aem.addon.guides</groupId>
       <artifactId>konnect-azure-devops</artifactId>
       <version>1.0.0</version>
       <type>jar</type>
   </dependency> 
   ```

1. 嵌入添加的依赖项。

       ```
       &lt;embedded>
       &lt;groupid>com.adobe.aem.addon.guides&lt;/groupid>
       &lt;artifactid>konnect-azure-devops&lt;/artifactid>
       &lt;type>jar&lt;/type>
       &lt;target>/apps/aemdoxonaemcsstageprogram-vendor-packages/content/install&lt;/target>
       &lt;/embedded>
       ```
   
1. 运行管道以应用Cloud Service中的更改。
连接器安装在您的环境中。


## 可用于连接器的功能

* 在 **列表视图** 或 **平铺视图**  以列表或图块形式查看各种连接的数据源。
* 选中单个连接器的复选框。 单击 **全选** 以选择所有连接器。 您可以单击 **取消全选** 当所有连接器都处于选中状态时。

<img src="./assets/data-sources-features.png" alt= "数据源页面上的数据源功能" width="800">

*编辑、重新连接、复制或删除数据源连接器。*

您可以对上的连接器使用以下特征 **数据源** 页面：

* **编辑**：编辑所选连接器的配置详细信息。

* **重新连接**：重新连接到已断开连接的连接器。

* **复制**：使用当前连接器作为基础创建新重复连接器。 缺省情况下，会创建带有后缀（如connectorname_1）的重复连接器。 例如，sample-elastic-search_1。
如果存在同名的连接器，则会查看错误。

* **删除**：删除选定的连接器。


配置数据源后，连接器将列在 **“数据源”面板** 在Web编辑器中。 然后，您可以连接到数据源并将内容片段插入到您的主题中。 有关详细信息，请查看 [插入数据源中的内容片段](../user-guide/web-editor-content-snippet.md).
