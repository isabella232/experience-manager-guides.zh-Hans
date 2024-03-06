---
title: 配置用于创作的智能建议
description: 了解如何为创作配置智能建议
source-git-commit: 1cdad275651b78d794ebc3f4ad9ead266ebeb0bd
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 1%

---

# 为创作配置AI支持的智能建议

作为管理员，您可以为作者配置智能建议功能。 智能建议服务由基于Adobe IMS身份验证的身份验证来保护。 将您的环境与Adobe基于令牌的安全身份验证工作流集成，并开始使用新的智能建议功能。 以下配置可帮助您添加 **人工智能配置** 选项卡到文件夹配置文件。 添加后，您可以在Web编辑器中使用智能建议功能。

## 在Adobe Developer控制台中创建IMS配置

执行以下步骤可在Adobe Developer控制台中创建IMS配置：
1. Launch [Adobe Developer控制台](https://developer.adobe.com/console).
1. 成功登录到开发人员控制台后，您将看到 **主页** 屏幕。 此 **主页** 在屏幕中，您可以轻松查找信息和快速链接，包括指向项目和下载的顶部导航链接。
1. 要创建新的空项目，请选择  **创建新项目** 从  **快速入门** 链接。
   ![快速入门链接](assets/conf-ss-quick-start.png) {width="550" align="left"}
   *创建新项目。*

1. 选择  **添加API**  从  **项目** 屏幕。  此 **添加API** 屏幕。 此屏幕显示了可用于开发应用程序的Adobe产品和技术的所有可用API、事件和服务。

1. 选择 **I/O管理API** 以将其添加到您的项目。
   ![IO管理API](assets/confi-ss-io-management.png)
   *将I/O管理API添加到您的项目中。*

1. 新建 **OAuth凭据** 并保存它。
   ![配置API中的OAuth凭据拼贴](assets/conf-ss-OAuth-credential.png) {width="3000" align="left"}
   *为API配置OAuth凭据。*

1. 在  **项目** 选项卡，选择 **OAuth服务器到服务器** 选项，然后选择新创建的凭据。

1. 选择 **OAuth服务器到服务器** 查看项目凭据详细信息的链接。

   ![连接的凭据](assets/conf-ss-connected-credentials.png) {width="800" align="left"}

   *连接到项目以查看凭据详细信息。*
1. 复制CLIENT_ID和CLIENT_SECRET密钥。

您现在已配置OAuth身份验证详细信息。 请随时使用这两个键，因为下一节需要用到它们。

### 将IMS配置添加到环境

执行以下步骤以将IMS配置添加到环境：

1. 打开Experience Manager，然后选择包含要配置的环境的程序。
1. 切换到 **环境** 选项卡。
1. 选择要配置的环境名称。 这应该会将您导航到“环境信息”页面。
1. 切换到 **配置** 选项卡。
1. 添加CLIENT_ID和CLIENT_SECRET密钥，如下面的屏幕快照所示。 请确保您使用的名称和配置与下面高亮显示的名称和配置相同。
   ![环境配置](assets/conf-ss-environment.png) {width="800" align="left"}
   *添加环境配置详细信息。*




将IMS配置添加到环境后，执行以下步骤以使用OSGi将这些属性与AEM Guides链接：

1. 在您的Cloud Manager Git项目代码中，添加以下两个给定的文件(对于文件内容，请查看 [附录](#appendix))。

   * `com.adobe.fmdita.ims.service.ImsOauthUserAccountHeadersImpl.cfg.json`
   * `com.adobe.fmdita.smartsuggest.service.SmartSuggestConfigurationConsumer.cfg.json`
1. 确保新添加的文件包含在您的 `filter.xml`.
1. 提交并推送您的Git更改。
1. 运行管道以在环境中应用更改。

完成此操作后，您应该能够使用智能建议功能。



## 附录 {#appendix}

**文件**：
`com.adobe.fmdita.ims.service.ImsOauthUserAccountHeadersImpl.cfg.json`

**内容**：

```
{
  "client.id": "$[secret:CLIENT_ID]",
  "client.secret": "$[secret:CLIENT_SECRET]",
  "ims.url": "https://ims-na1.adobelogin.com"
}
```

**文件**： `com.adobe.fmdita.smartsuggest.service.SmartSuggestConfigurationConsumer.cfg.json`

**内容**：

```
{
  "smart.suggestion.flag":true,
  "conref.inline.threshold":0.6,
  "conref.block.threshold":0.7,
  "emerald.url":"https://adobeioruntime.net/apis/543112-smartsuggest/emerald/v1",
  "instance.type":"prod"
}
```

## 智能建议配置详细信息

| 关键值 | 描述 | 允许的值 | 默认值 |
|---|---|---|---|
| smart.suggestion.flag | 控制是否启用智能建议 | true/false | false |
| conref.inline.threshold | 控制为用户当前键入的标记获取的建议精确度/回调度的阈值。 | 从–1.0到1.0的任何值。 | 0.6 |
| conref.block.threshold | 控制在整个文件中为标记获取的建议精确度/回调度的阈值。 | 从–1.0到1.0的任何值。 | 0.7 |
| emerald.url | 翡翠矢量数据库的端点 | [https://adobeioruntime.net/apis/543112-smartsuggest/emerald/v1](https://adobeioruntime.net/apis/543112-smartsuggest/emerald/v1) | [https://adobeioruntime.net/apis/543112-smartsuggest/emerald/v1](https://adobeioruntime.net/apis/543112-smartsuggest/emerald/v1) |
| instance.type | AEM实例的类型。 请确保对于已配置智能建议的每个AEM实例而言，这是唯一的。 用例是在暂存环境中使用“instance.type”=“stage”测试该功能，与此同时，该功能也在“prod”上配置。 | 标识环境的任意唯一键。 仅 *字母数字* 值是允许的。 “dev”/“stage”/“prod”/“test1”/“stage2” | &quot;prod&quot; |

配置完毕后，智能建议图标将显示在Web编辑器的右侧面板中。 编辑主题时，可以查看智能建议列表。 有关详细信息，请查看 [用于创作的基于AI的智能建议](../user-guide/authoring-ai-based-smart-suggestions.md) Experience Manager部分。
