---
title: 配置数据源连接器
description: 了解如何配置数据源连接器
exl-id: bd1188e1-0e1d-4e70-928a-10251c3d529d
feature: Web Editor Configuration
role: Admin
level: Experienced
source-git-commit: 0513ecac38840a4cc649758bd1180edff1f8aed1
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# 配置数据源连接器

AEM Guides为JIRA和SQL (MySQL、PostgreSQL、SQL Server、SQLite)数据库提供现成的连接器。 也可以通过扩展缺省接口来添加其它连接器。 以下配置可帮助您轻松添加各种数据源。 添加后，您可以在Web编辑器中查看数据源。

执行以下步骤来配置数据源连接器，然后从Web编辑器使用它：

## 配置连接器

您可以通过上传JSON文件来配置现成连接器。 您可以使用以下示例安装文件为Jira和SQL (MySQL、PostgreSQL、SQL Server、SQLite)数据库设置连接器。

Jira使用用户名和密码进行基本身份验证的示例设置文件：

```
{
	"connectorClazz": "com.adobe.guides.konnect.definitions.ootb.connector.rest.JiraConnector",
	"configName": "Jira",
	"templateFolders": ["/content/dam/dita-templates/konnect/jira"],
	"connectionConfig": {
		"configClazz": "com.adobe.guides.konnect.definitions.ootb.config.rest.BasicAuthRestConfig",
		"configData": {
			"username": "jirausername",
			"password": "jirapassword",
			"url": "https://jira.corp.adobe.com/rest/api/latest/search"
		}
	}
}
```

例如，另存为 `jira.json`.

Jira带令牌的基本身份验证的示例设置文件：

```
{
	"connectorClazz": "com.adobe.guides.konnect.definitions.ootb.connector.rest.JiraConnector",
	"configName": "Jira",
	"templateFolders": ["/content/dam/dita-templates/konnect/jira"],
	"connectionConfig": {
		"configClazz": "com.adobe.guides.konnect.definitions.ootb.config.rest.BasicAuthRestConfig",
		"configData": {
			"token": "jiraauthtoken",
			"url": "https://jira.corp.adobe.com/rest/api/latest/search"
		}
	}
}
```

例如，另存为 `jira.json`.

Jira基本身份验证的示例设置文件，其中包含具有“Basic”关键字的令牌：

```
{
	"connectorClazz": "com.adobe.guides.konnect.definitions.ootb.connector.rest.JiraConnector",
	"configName": "Jira",
	"templateFolders": ["/content/dam/dita-templates/konnect/jira"],
	"connectionConfig": {
		"configClazz": "com.adobe.guides.konnect.definitions.ootb.config.rest.BasicAuthRestConfig",
		"configData": {
			"token": "Basic jiraauthtoken",
			"url": "https://jira.corp.adobe.com/rest/api/latest/search"
		}
	}
}
```

例如，另存为 `jira.json`.

MySql基本身份验证的示例安装文件：

```
{
	"connectorClazz": "com.adobe.guides.konnect.definitions.ootb.connector.sql.MySqlConnector",
	"configName": "MySQL",
	"templateFolders": ["/content/dam/dita-templates/konnect/sql"],
	"connectionConfig": {
		"configClazz": "com.adobe.guides.konnect.definitions.ootb.config.sql.UserPassSqlConfig",
		"configData": {
			"username": "admin",
			"password": "admin",
			"driver": "com.mysql.jdbc.Driver",
			"connectionString": "jdbc:mysql://host.corp.adobe.com:3306/plm"
		}
	}
}
```

例如，另存为 `mysql.json`.

PostgreSQL基本身份验证的示例设置文件：

```
{
	"connectorClazz": "com.adobe.guides.konnect.definitions.ootb.connector.sql.PostgreSqlConnector",
	"configName": "PostgreSQL",
	"templateFolders": ["/content/dam/dita-templates/konnect/sql"],
	"connectionConfig": {
		"configClazz": "com.adobe.guides.konnect.definitions.ootb.config.sql.UserPassSqlConfig",
		"configData": {
			"username": "admin",
			"password": "admin",
			"driver": "org.postgresql.Driver",
			"connectionString": "jdbc:postgresql://host:port/database"
		}
	}
}
```

例如，另存为 `postgres.json`.

MS SQL Server基本身份验证的示例安装文件：

```
{
	"connectorClazz": "com.adobe.guides.konnect.definitions.ootb.connector.sql.MsSqlServerConnector",
	"configName": "MSSQLServer",
	"templateFolders": ["/content/dam/dita-templates/konnect/sql"],
	"connectionConfig": {
		"configClazz": "com.adobe.guides.konnect.definitions.ootb.config.sql.UserPassSqlConfig",
		"configData": {
			"username": "admin",
			"password": "admin",
			"driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
			"connectionString": "jdbc:sqlserver://10.10.10.10\\SQLEXPRESS01:1433;database=TutorialDB;encrypt=false;trustServerCertificate=true"
		}
	}
}
```

例如，另存为 `mssqlserver.json`.

SQLite基本身份验证的示例安装文件：

```
{
	"connectorClazz": "com.adobe.guides.konnect.definitions.ootb.connector.sql.SqliteConnector",
	"configName": "SQLiteServer",
	"templateFolders": ["/content/dam/dita-templates/konnect/sql"],
	"connectionConfig": {
		"configClazz": "com.adobe.guides.konnect.definitions.ootb.config.sql.UserPassSqlConfig",
		"configData": {
			"username": "admin",
			"password": "admin",
			"driver": "org.sqlite.JDBC",
			"connectionString": "jdbc:sqlite:sample.db"
		}
	}
}
```

例如，另存为 `sqqlite.json`.

### 自定义连接器配置

AEM Guides允许您自定义配置文件中的某些值以满足用户的需求。

| 属性名称 | 描述 |
|---|---|
| 配置名称 | 用户可以指定配置名称来帮助识别连接器 |
| templateFolders | 将从其中获取模板的文件夹的列表 |

根据为运行Connector而选择的配置类定制其他字段。

## 将文件上传到AEM中的某个位置

将文件上传到AEM Assets中的某个位置。

例如，  `/content/dam/jira.json`

## 使用REST API创建配置

您可以使用REST API注册配置。 有关更多详细信息，请查看 *用于注册数据源连接器的REST API* 部分(Adobe Experience Manager Guides的API参考)。

配置数据源后，连接器将列在Web编辑器中的数据源面板下。 然后，您可以连接到数据源并将内容片段插入到您的主题中。 有关详细信息，请查看 [插入数据源中的内容片段](../user-guide/web-editor-content-snippet.md).
