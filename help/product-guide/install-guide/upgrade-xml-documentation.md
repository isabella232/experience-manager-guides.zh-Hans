---
title: 升级Adobe Experience Manager指南
description: 了解如何升级Adobe Experience Manager Guides
exl-id: f058b39f-7408-4874-942b-693e133886cf
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '4470'
ht-degree: 0%

---

# 升级Adobe Experience Manager指南 {#id224MBE0M0XA}

>[!NOTE]
>
> 按照特定于您的产品的许可版本的升级说明进行操作。

您可以将当前版本的《Experience Manager指南》升级到4.3.1版

- 如果您使用的是版本4.3.0、4.2或4.2.1，则可以直接升级到版本4.3.1。
- 如果您使用的是版本4.1或4.1.x ，则需要先升级到版本4.3.0、4.2或4.2.x ，然后再升级到版本4.3.1。
- 如果您使用的是版本4.0，则需要先升级到版本4.2，然后再升级到版本4.3.1。
- 如果您使用的是版本3.8.5，则在升级到版本4.2之前需要升级到版本4.0。
- 如果您使用的版本低于3.8.5，请参阅特定于产品的安装指南中的“升级Experience Manager指南”部分。


>[!NOTE]
>
> 在升级Experience Manager指南版本之前，必须安装AEM Service Pack。

有关更多详细信息，请参阅以下过程：

- [从3.8.5升级到版本4.0](#id2256DK003E1)
- [升级到版本4.2](#id22A3F500SXA)
- [升级到版本4.2.1](#upgrade-version-4-2-1)
- [升级到版本4.3.0](#upgrade-version-4-3)
- [升级到版本4.3.1](#upgrade-version-4-3-1)


>[!IMPORTANT]
>
> 在开始升级之前，请进行完整的系统备份以避免任何数据丢失。

## 从版本3.8.5升级到版本4.0 {#id2256DK003E1}

如果您使用的是Experience Manager指南版本3.8.5，则可以升级到Experience Manager指南版本4.0。 使用升级功能，您无需卸载以前版本的《Experience Manager指南》。

在运行进程之前，必须完成某些任务。 以下子部分将指导您完成先决条件、报告生成和迁移过程。 此外，安装Experience Manager指南4.0版后，您可以根据客户设置自定义各种配置。

>[!NOTE]
>
> 此升级过程仅适用于版本3.8.5到版本4.0。有关从版本3.4或更高版本升级到3.8.5的过程，请参阅 *《升级Experience Manager指南》* 特定产品的安装指南中的部分，请参见 [“帮助存档”页](https://helpx.adobe.com/xml-documentation-for-experience-manager/archive.html).

****前提条件****

在开始Experience Manager指南升级过程之前，请确保您具有：

1. 在打开供审阅的主题中导入审阅注释。
1. 已关闭所有活动审核。
1. 已关闭所有翻译任务。
1. 卸载安装在Experience Manager指南先前版本\（主要版本或修补程序版本\）顶部的Experience Manager指南热修复程序。

**安装版本4.0之前**

在安装版本4.0之前，请执行以下步骤：

1. 确保此时的《Experience Manager指南》版本为3.8.5。
1. 下载升级脚本包。 为此，请在上搜索“XML Documentation solution 4.0升级包” [Adobe软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 下载zip文件。
1. 通过包管理器将此包上传到AEM并安装此包。
1. 安装升级软件包后，请按照相同的顺序运行以下给定脚本，然后按照给定说明操作：

**检查升级兼容性API**

此API旨在评估当前系统状态，并报告是否可以进行升级。 要运行此脚本，请触发以下给定的端点：

| 终点 | /bin/dxml/upgrade/3xto4x/report |
| --- | --- |
| 请求类型 | **GET** 您可以使用Web浏览器，在该浏览器中，您以管理员身份登录到AEM实例。 |
| 预期响应 |  — 如果可以移动所有需要的节点，您将获得一个通过检查。 <br> — 如果目标位置中存在节点，您将收到相关错误。 清理存储库\（删除节点/var/dxml\）并重新安装升级包，然后再次触发此端点。 <br>**注意：** 这不是常见的错误，因为《3.xExperience Manager指南》之前未使用Target位置。 <br>  — 如果此脚本不成功，请不要继续，并报告给您的客户成功团队。 |

**系统数据迁移API**

此API用于迁移 **迁移映射** 部分。

1. 如果Check upgrade compatibility API失败，请勿执行此脚本\（不继续\）。
1. 一旦Check upgrade compatibility API返回成功，您就可以运行升级脚本了。

| 终点 | /bin/dxml/upgrade/3xto4x |
| --- | --- |
| 请求类型 | **POST** 此脚本是一个POST请求，因此应通过Postman等代理执行。 |
| 预期响应 |  — 迁移成功后，您可以安装XML Documentation解决方案版本4.0。<br> — 如果出现错误，请还原到最后一个检查点，并与您的客户成功团队共享错误日志以及API输出。 |

**迁移映射**：上述API将源位置下的所有数据迁移到目标位置。

| 源 | 目标 |
|------|------|
| /content/fmdita | /var/dxml |
| /content/dxml | /var/dxml |
| /etc/fmdita | /libs/fmdita |

## 安装版本4.0 {#id23598G006XA}

1. 仅当升级步骤成功时，才安装版本4.0。
1. 从下载4.0版本包 [Adobe软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)：

   - 如果您使用的是UUID版本的软件，请搜索“适用于AEM 6.5的XML Documentation解决方案的4.0 UUID版本”。
   - 如果您使用的是非UUID版本的软件，请搜索“适用于AEM 6.5的XML Documentation解决方案的4.0非UUID版本”。
使用CRX包管理器将包上传到现有AEM服务器实例并进行安装。

   >[!NOTE]
   >
   > 等待所有系统组件启动。

1. 安装包后清除浏览器缓存。
1. 如果在AEM创作实例上配置了Dispatcher，请执行以下步骤：
   - 确保在Dispatcher规则中处理以下内容：
   - URL模式/home/users/\*/preferences已列入白名单。
   - 不缓存URL模式/libs/cq/security/userinfo.json 。
1. 清除Dispatcher缓存\(以清除任何 `clientlibs` cached\)。

## 升级到版本4.2 {#id22A3F500SXA}

升级到4.2版取决于当前版本的《Experience Manager指南》。

如果您使用的是版本4.0、4.1或4.1.x，则可以直接升级到版本4.2。

****前提条件****

在开始Experience Manager指南4.2升级过程之前，请确保您具有：

1. 已升级到Experience Manager指南版本4.0、4.1或4.1.x。
1. 已关闭所有翻译任务。
1. 已将日志级别更改为 **信息** 对象 `com.adobe.fmdita.translationservices.TranslationMapUpgradeScript` 将这些日志附加到新日志文件中，例如， `logs/translation_upgrade.log.`

>[!NOTE]
>
> 您应该关闭所有活动审阅。 如果在升级到4.2时未关闭审阅任务，则旧版进行中的审阅任务将继续让用户访问旧版审阅页面，并且升级后创建的审阅任务将显示功能中的最新更新。

## 安装版本4.2 {#id2245IK0E0EV}

1. 从下载4.2版本包 [Adobe软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
1. 安装版本4.2包。
1. 完成软件包安装后，请等待日志中显示以下消息：

   `Completed the post deployment setup script`

   上述消息指示所有安装步骤均已完成。

   如果您遇到以下任何错误前缀，请将其报告给您的客户成功团队：

   - 部署后设置脚本出错
   - 移植翻译映射时出现异常
   - 无法为属性将翻译映射从v1端口转换为v2
1. 升级随版本4.2一起发布的氧气连接器插件\（如果需要\）。
1. 安装包后清除浏览器缓存。
1. 继续升级自定义项，如下一节所述。

## 安装版本4.2之后 {#id2326F02004K}

>[!IMPORTANT]
>
> 升级后的服务器上未显示高科技模板。 要在服务器上包含高科技模板，您可以复制该模板：源： /libs/fmdita/pdf/Hi-Tech目标： /content/dam/dita-templates/pdf

安装Experience Manager指南后，您可以将适用于从新安装的版本到安装的各种配置合并到一起。

>[!NOTE]
>
> 可以自定义dam-update-asset模型。 因此，如果已完成任何自定义设置，那么我们需要将自定义设置和Experience Manager指南同步到模型的工作副本中。

1. **DAM更新资产工作流\（后处理更改\）：**

1. 打开URL：

   ```http
   http://localhost:4502/libs/cq/workflow/admin/console/content/models.html
   ```

1. 选择 **DAM更新资产工作流**.
1. 单击 **编辑**.
1. 如果 **DXML后处理启动器** 组件存在，请确保自定义项已同步。
1. 如果 **DXML后处理启动器** 组件不存在，请执行以下步骤以插入该组件：

1. 单击 **插入组件** \(负责Experience Manager指南后期处理，这是该过程的最后一步\)。
1. 配置 **流程步骤** ，详情如下：

   **“常用”选项卡**

   **标题：** DXML后处理启动器

   **描述**：DXML后处理启动器步骤，这将触发用于修改/创建的资产的DXML后处理的sling作业

   **“流程”选项卡**

   - 选择 **DXML后处理启动器**&#x200B;从 **进程** 下拉框

   - 选择 **处理程序前进**

   - 选择 **完成**

1. 单击 **同步** 完成更改后显示在右上角。 您将收到成功通知。

   >[!NOTE]
   >
   > 刷新并验证最终工作流模型中是否存在自定义更改和Experience Manager指南后处理步骤。

1. 一次 **DAM更新资产工作流**&#x200B;经过验证，检查相应的启动器配置。 为此，请转到AEM Workflow界面并打开启动器。

   ```http
   http://localhost:4502/libs/cq/workflow/content/console.html
   ```

   查找并对以下两个启动器\（如果需要\）进行相应更改\（应该处于活动状态\） **DAM更新资产工作流**：

1. “ ”的启动器&#x200B;*节点已创建*“（表示） **DAM更新资产工作流** — 表示条件 `"jcr:content/jcr:mimeType!=video"`，则“通配”值应为：

   ```json
   /content/dam(/((?!/subassets|/translation_output).)*/)renditions/original
   ```

   - “excludeList”应具有 `"event-user-data:changedByWorkflowProcess"`.
   - “ ”的启动器&#x200B;*节点已修改*“（表示） **DAM更新资产工作流 —** 条件&quot;`jcr:content/jcr:mimeType!=video`“，
   - “通配”值应为：

   ```json
   /content/dam(/((?!/subassets|/translation_output).)*/)renditions/original
   ```

   - “excludeList”应具有 `"event-user-data:changedByWorkflowProcess"`.
1. 升级完成后，请确保验证并更新任何自定义项/叠加图，以匹配新的应用程序代码。 下面给出了一些示例：
   - 任何来自/libs/fmditor/libsis的叠加组件都应与新的产品代码进行比较，并且更新应在/apps下的叠加文件中完成。
   - 应审查产品中使用的任何clientlib类别是否有更改。 任何覆盖的配置\（见以下示例\）应与最新的配置进行比较，以获取最新的功能：
   - elementmapping.xml
   - ui\_config.json\（可能已在文件夹配置文件中设置\）
   - 已修改 `com.adobe.fmdita.config.ConfigManager`
   - 检查是否有任何自定义代码使用任何旧路径\(如 [迁移映射](#id2244LE040XA) 部分\) — 应更新为新路径，以便自定义项也能按预期工作。
1. 阅读有关当前版本中引入的任何新配置\(请选中 [发行说明](../release-info/release-notes-4.3.md)\)查看是否有任何功能受到影响，然后采取适当措施。 例如，可以使用4.0版中引入的“改进的文件和版本处理”，您需要启用该版本的配置。

## 为现有内容编制索引以使用新的查找和替换的步骤：

执行以下步骤来索引现有内容，并在映射级别使用新的查找和替换文本：

- 对服务器运行POST请求\（使用正确的身份验证\） - `http://<server:port\>/bin/guides/map-find/indexing`. \(可选：您可以传递映射的特定路径来进行索引，默认情况下，所有映射都将进行索引\|\|例如： `https://<Server:port\>/bin/guides/map-find/indexing?paths=<map\_path\_in\_repository\>`\)

- 该API将返回作业ID。 要检查作业的状态，可以将带有作业ID的GET请求发送到同一端点 — 

`http://<server:port\>/bin/guides/map-find/indexing?jobId=\{jobId\}`\(例如： `http://localhost:8080/bin/guides/map-find/indexing?jobId=2022/9/15/7/27/7dfa1271-981e-4617-b5a4-c18379f11c42`\)

- 作业完成后，上述GET请求将做出成功响应，并提及是否有任何映射失败。 可以从服务器日志中确认已成功编制索引的映射。

如果升级作业失败，并且错误日志显示以下错误：

“ *查询* 读取或遍历多于 *100000节点*. 为了避免影响其他任务，处理已停止。”

发生这种情况的原因是，没有为升级中使用的查询正确设置索引。 您可以尝试以下解决方法：

1. 在damAssetLucene Oak索引中，添加布尔值属性 `indexNodeName` 作为 `true` 在节点中。
   `/oak:index/damAssetLucene/indexRules/dam:Asset`
1. 在节点下添加名称为摘录的新节点。

   `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`
并在节点中设置以下属性：

   ```
   name - rep:excerpt
   propertyIndex - {Boolean}true
   notNullCheckEnabled - {Boolean}true
   ```

   的结构 `damAssetLucene` 应该类似于：

   ```
   <damAssetLucene compatVersion="{Long}2" async="async, nrt" jcr:primaryType="oak:QueryIndexDefinition" evaluatePathRestrictions="{Boolean}true" type="lucene">
   <indexRules jcr:primaryType="nt:unstructured">
     <dam:Asset indexNodeName="{Boolean}true" jcr:primaryType="nt:unstructured">
       <properties jcr:primaryType="nt:unstructured">
         <excerpt name="rep:excerpt" propertyIndex="{Boolean}true" jcr:primaryType="nt:unstructured" notNullCheckEnabled="{Boolean}true"/>
       </properties>
       </dam:Asset>
     </indexRules>
   </damAssetLucene>    
   ```


   （以及其他现有节点和属性）

1. 重新索引 `damAssetLucene` 索引(通过将重新索引标志设置为 `true` 在下面并等待它出现 `false` （这表示重新索引已完成）。 请注意，根据索引的大小，这可能需要几个小时。
1. 通过执行上述步骤，再次运行索引脚本。


## 升级到版本4.2.1 {#upgrade-version-4-2-1}

升级到4.2.1版取决于当前版本的《Experience Manager指南》。

如果您使用的是版本4.1、4.1.x或4.2，则可以直接升级到版本4.2.1。

>[!NOTE]
>
>后处理并编制索引可能需要几个小时。 我们建议您在非高峰时间启动升级过程。

****前提条件****

在开始Experience Manager指南4.2.1升级过程之前，请确保您具有：

1. 已升级到Experience Manager指南版本4.1、4.1.x或4.2。
1. 已关闭所有翻译任务。
1. 已将日志级别更改为 **信息** 对象 `com.adobe.fmdita.translationservices.TranslationMapUpgradeScript` 将这些日志附加到新日志文件中，例如， `logs/translation_upgrade.log.`

>[!NOTE]
>
> 您应该关闭所有活动审阅。 如果在升级到4.2时未关闭审阅任务，则旧版进行中的审阅任务将继续让用户访问旧版审阅页面，并且升级后创建的审阅任务将显示功能中的最新更新。

## 安装版本4.2.1

1. 从下载4.2.1版本包 [Adobe软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
1. 安装版本4.2.1包。
1. 您可以选择点击触发器以启动翻译图升级作业。 有关详细信息，请参阅 [通过Servlet启用脚本触发器](#enable-trigger-serverlet).


1. 完成软件包安装后，请等待日志中显示以下消息：

   `Completed the post deployment setup script`

   上述消息指示所有安装步骤均已完成。

   如果您遇到以下任何错误前缀，请将其报告给您的客户成功团队：

   - 部署后设置脚本出错
   - 移植翻译映射时出现异常
   - 无法为属性将翻译映射从v1端口转换为v2
1. 升级随版本4.2一起发布的氧气连接器插件\（如果需要\）。
1. 安装包后清除浏览器缓存。
1. 继续升级自定义项，如下一节所述。

### 通过Servlet启用脚本触发器{#enable-trigger-serverlet}

POST：

```
http://localhost:4503/bin/guides/script/start?jobType=translation-map-upgrade
```

响应：

```
{
"msg": "Job is successfully submitted and lock node is created for future reference",
"lockNodePath": "/var/dxml/executor-locks/translation-map-upgrade/1683190032886",
"status": "SCHEDULED"
}
```

在上述响应JSON中，键 `lockNodePath` 保存指向在存储库中创建的指向已提交作业的节点的路径。 作业完成后该节点会被自动删除，在此之前，您可以引用此节点以获取作业的当前状态。

示例日志：以下是触发脚本后日志文件中显示的日志示例。

```
04.05.2023 14:17:12.876 *INFO* [[0:0:0:0:0:0:0:1] [1683190032736] POST /bin/guides/script/start HTTP/1.1] com.adobe.dxml.common.executor.RunnableSynchronizedOTS Acquiring lock for job : translation-map-upgrade
04.05.2023 14:17:12.897 *INFO* [pool-59-thread-1] com.adobe.fmdita.xmltranslation.ots.TranslationMapUpgradeOTS Starting the thread to upgrade translation map from V1 to V2
04.05.2023 14:17:12.899 *INFO* [pool-59-thread-1] com.adobe.dxml.common.executor.RunnableSynchronizedOTS Initiating lock for node : /var/dxml/executor-locks/translation-map-upgrade/1683190032886
04.05.2023 14:17:12.901 *INFO* [pool-59-thread-1] com.adobe.fmdita.translationservices.TranslationMapUpgradeScript Starting porting of translation map from V1 to V2
04.05.2023 14:17:12.904 *INFO* [pool-59-thread-1] com.adobe.fmdita.translationservices.TranslationMapUpgradeScript Memory increase is of : 764 kB
04.05.2023 14:17:12.906 *INFO* [pool-59-thread-1] com.adobe.fmdita.translationservices.TranslationMapUpgradeScript Completed porting of translation map from V1 to V2
04.05.2023 14:17:12.907 *INFO* [pool-59-thread-1] com.adobe.dxml.common.executor.RunnableSynchronizedOTS Releasing lock for node : /var/dxml/executor-locks/translation-map-upgrade/1683190032886
04.05.2023 14:17:12.909 *INFO* [pool-59-thread-1] com.adobe.fmdita.xmltranslation.ots.TranslationMapUpgradeOTS Completed the thread to upgrade translation map from V1 to V2
```

查找 `com.adobe.fmdita.translationservices.TranslationMapUpgradeScript Completed porting of translation map from V1 to V2` 和 `com.adobe.fmdita.xmltranslation.ots.TranslationMapUpgradeOTS Completed the thread to upgrade translation map from V1 to V2` 然后再继续后续步骤。



## 安装版本4.2.1之后

>[!IMPORTANT]
>
> 升级后的服务器上未显示高科技模板。 要在服务器上包含高科技模板，您可以复制该模板：源： /libs/fmdita/pdf/Hi-Tech目标： /content/dam/dita-templates/pdf

安装Experience Manager指南后，您可以将适用于从新安装的版本到安装的各种配置合并到一起。

>[!NOTE]
>
> 可以自定义dam-update-asset模型。 因此，如果已完成任何自定义设置，那么我们需要将自定义设置和Experience Manager指南同步到模型的工作副本中。

1. **DAM更新资产工作流\（后处理更改\）：**

1. 打开URL：

   ```http
   http://localhost:4502/libs/cq/workflow/admin/console/content/models.html
   ```

1. 选择 **DAM更新资产工作流**.
1. 单击 **编辑**.
1. 如果 **DXML后处理启动器** 组件存在，请确保自定义项已同步。
1. 如果 **DXML后处理启动器** 组件不存在，请执行以下步骤以插入该组件：

1. 单击 **插入组件** \(负责Experience Manager指南后期处理，这是该过程的最后一步\)。
1. 配置 **流程步骤** ，详情如下：

   **“常用”选项卡**

   **标题：** DXML后处理启动器

   **描述**：DXML后处理启动器步骤，这将触发用于修改/创建的资产的DXML后处理的sling作业

   **“流程”选项卡**

   - 选择 **DXML后处理启动器**&#x200B;从 **进程** 下拉框

   - 选择 **处理程序前进**

   - 选择 **完成**

1. 单击 **同步** 完成更改后显示在右上角。 您将收到成功通知。

   >[!NOTE]
   >
   > 刷新并验证最终工作流模型中是否存在自定义更改和Experience Manager指南后处理步骤。

1. 一次 **DAM更新资产工作流**&#x200B;经过验证，检查相应的启动器配置。 为此，请转到AEM Workflow界面并打开启动器。

   ```http
   http://localhost:4502/libs/cq/workflow/content/console.html
   ```

   查找并对以下两个启动器\（如果需要\）进行相应更改\（应该处于活动状态\） **DAM更新资产工作流**：

1. “ ”的启动器&#x200B;*节点已创建*“（表示） **DAM更新资产工作流** — 表示条件 `"jcr:content/jcr:mimeType!=video"`，则“通配”值应为：

   ```json
   /content/dam(/((?!/subassets|/translation_output).)*/)renditions/original
   ```

   - “excludeList”应具有 `"event-user-data:changedByWorkflowProcess"`.
   - “ ”的启动器&#x200B;*节点已修改*“（表示） **DAM更新资产工作流 —** 条件&quot;`jcr:content/jcr:mimeType!=video`“”，“通配”值应为：

   ```json
   /content/dam(/((?!/subassets|/translation_output).)*/)renditions/original
   ```

   - `excludeList` 应该有 `"event-user-data:changedByWorkflowProcess"`.

1. 升级完成后，请确保验证并更新任何自定义项/叠加图，以匹配新的应用程序代码。 下面给出了一些示例：
   - 任何来自/libs/fmditor/libsis的叠加组件都应与新的产品代码进行比较，并且更新应在/apps下的叠加文件中完成。
   - 应审查产品中使用的任何clientlib类别是否有更改。 任何覆盖的配置\（见以下示例\）应与最新的配置进行比较，以获取最新的功能：
   - elementmapping.xml
   - ui\_config.json\（可能已在文件夹配置文件中设置\）
   - 已修改 `com.adobe.fmdita.config.ConfigManager`
   - 检查是否有任何自定义代码使用任何旧路径\(如 [迁移映射](#id2244LE040XA) 部分\) — 应更新为新路径，以便自定义项也能按预期工作。
1. 阅读有关当前版本中引入的任何新配置\(请选中 [发行说明](../release-info/release-notes-4.2.1.md)\)查看是否有任何功能受到影响，然后采取适当措施。 例如，可以使用4.0版中引入的“改进的文件和版本处理”，您需要启用该版本的配置。

## 为现有内容编制索引以使用新的查找和替换的步骤：

执行以下步骤来索引现有内容，并在映射级别使用新的查找和替换文本：

- 确保 `damAssetLucene` 索引已完成。 这可能需要几个小时，具体取决于服务器上存在的数据量。 您可以通过检查中的重新索引字段是否设置为false来确认重新索引已完成
  `http://<server:port>/oak:index/damAssetLucene`.  此外，如果您已在以下位置添加了任何自定义项： `damAssetLucene`中，您可能需要再次应用它们。

- 对服务器运行POST请求\（使用正确的身份验证\） - `http://<server:port\>/bin/guides/map-find/indexing`. (可选：您可以传递映射的特定路径来索引它们，默认情况下，所有映射都将索引\|\|例如： `https://<Server:port\>/bin/guides/map-find/indexing?paths=<map\_path\_in\_repository\>`)

- 您还可以传递根文件夹来索引特定文件夹（及其子文件夹）的DITA映射。 例如，`http://<server:port\>/bin/guides/map-find/indexing?root=/content/dam/test`。请注意，如果同时传递了路径参数和根参数，则只考虑路径参数。

- 该API将返回作业ID。 要检查作业的状态，可以将带有作业ID的GET请求发送到同一端点 —  `http://<server:port\>/bin/guides/map-find/indexing?jobId=\{jobId\}`\(例如： `http://localhost:8080/bin/guides/map-find/indexing?jobId=2022/9/15/7/27/7dfa1271-981e-4617-b5a4-c18379f11c42`\)


- 作业完成后，上述GET请求将做出成功响应，并提及是否有任何映射失败。 可以从服务器日志中确认已成功编制索引的映射。


## 升级到版本4.3.0 {#upgrade-version-4-3}

升级到4.3.0版取决于当前版本的《Experience Manager指南》。 如果您使用的是版本4.2或4.2.x ，则可以直接升级到版本4.3.0。

>[!NOTE]
>
>后处理并编制索引可能需要几个小时。 我们建议您在非高峰时间启动升级过程。

****前提条件****

在开始Experience Manager指南4.3.0升级过程之前，请确保您具有：

1. 已升级到《Experience Manager指南》版本4.2或4.2.x，并完成了各自的安装步骤。
1. 已关闭所有翻译任务。



## 安装版本4.3.0

1. 从下载4.3.0版本包 [Adobe软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
1. 安装版本4.3.0包。
1. 安装包后清除浏览器缓存。
1. 升级 `ui_config.json` 文件来自 **XML编辑器配置** 选项卡。


## 安装版本4.3.0之后

安装Experience Manager指南后，您可以将适用于从新安装的版本到安装的各种配置合并到一起。

## 后处理现有内容以使用断开链接报表的步骤


执行以下步骤后处理现有内容并使用新的断开链接报表：

1. （可选）如果系统中有超过100,000个dita文件，请更新 `queryLimitReads` 下 `org.apache.jackrabbit.oak.query.QueryEngineSettingsService` 设置为较大的值（任何大于现有资产数的值，例如200,000），然后重新部署。

   | PID | 属性键 | 属性值 |
   |---|---|---|
   | org.apache.jackrabbit.oak.query.QueryEngineSettingsService | queryLimitRead | 值： 200000 <br> 默认值： 100000 |

1. 执行以下API以对所有文件运行后处理：

   | 终点 | /bin/guides/reports/upgrade |
   |---|---|
   | 请求类型 | **POST**  此脚本是一个POST请求，因此应通过Postman等代理执行。 |
   | 预期响应 | 该API将返回作业ID。 要检查作业的状态，可以将带有作业ID的GET请求发送到同一端点。<br> 示例URL： `http://<server:port>/bin/guides/reports/upgrade` |

   | 终点 | /bin/guides/reports/upgrade |
   |---|---|
   | 请求类型 | **GET** |
   | 参数 | jobId：传递从上一个post请求收到的jobId。 |
   | 预期响应 |  — 作业完成后，GET请求将做出成功响应。 <br>  — 如果出现错误，请与客户成功团队共享错误日志以及API输出。  <br>示例URL： `http://<server:port>/bin/guides/reports/upgrade?jobId=2022/9/15/7/27/7dfa1271-981e-4617-b5a4-c18379f11c42_678` |


1. 恢复为默认或以前的现有值 `queryLimitReads` 如果您在步骤1中更改了它。


4.3.1

## 升级到版本4.3.1 {#upgrade-version-4-3-1}

升级到4.3.1版取决于当前版本的《Experience Manager指南》。 如果您使用的是版本4.3.0、4.2或4.2.1，则可以直接升级到版本4.3.1。

>[!NOTE]
>
>后处理并编制索引可能需要几个小时。 我们建议您在非高峰时间启动升级过程。

****前提条件****

在开始Experience Manager指南4.3.1升级过程之前，请确保您具有：

1. 已升级到《Experience Manager指南》版本4.3.0、4.2或4.2.1，并完成了各自的安装步骤。
1. 已关闭所有翻译任务。
1. 已将日志级别更改为 **信息** 对象 `com.adobe.fmdita.translationservices.TranslationMapUpgradeScript` 将这些日志附加到新日志文件中，例如， `logs/translation_upgrade.log`.


## 安装版本4.3.1

1. 从下载4.3.1版本包 [Adobe软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
1. 安装版本4.3.1包。
1. 您可以选择点击触发器以启动翻译图升级作业。 有关详细信息，请参阅 [通过Servlet启用脚本触发器](#enable-trigger-serverlet-4-3-1).


1. 完成软件包安装后，请等待日志中显示以下消息：

   `Completed the post deployment setup script`

   上述消息指示所有安装步骤均已完成。

   如果您遇到以下任何错误前缀，请将其报告给您的客户成功团队：

   - 部署后设置脚本出错
   - 移植翻译映射时出现异常
   - 无法为属性将翻译映射从v1端口转换为v2
1. 升级随版本4.2一起发布的氧气连接器插件\（如果需要\）。
1. 安装包后清除浏览器缓存。
1. 继续升级自定义项，如下一节所述。

### 通过Servlet启用脚本触发器{#enable-trigger-serverlet-4-3-1}

POST：

```
http://localhost:4503/bin/guides/script/start?jobType=translation-map-upgrade
```

响应：

```
{
"msg": "Job is successfully submitted and lock node is created for future reference",
"lockNodePath": "/var/dxml/executor-locks/translation-map-upgrade/1683190032886",
"status": "SCHEDULED"
}
```

在上述响应JSON中，键 `lockNodePath` 保存指向在存储库中创建的指向已提交作业的节点的路径。 作业完成后该节点会被自动删除，在此之前，您可以引用此节点以获取作业的当前状态。

示例日志：以下是触发脚本后日志文件中显示的日志示例。

```
04.05.2023 14:17:12.876 *INFO* [[0:0:0:0:0:0:0:1] [1683190032736] POST /bin/guides/script/start HTTP/1.1] com.adobe.dxml.common.executor.RunnableSynchronizedOTS Acquiring lock for job : translation-map-upgrade
04.05.2023 14:17:12.897 *INFO* [pool-59-thread-1] com.adobe.fmdita.xmltranslation.ots.TranslationMapUpgradeOTS Starting the thread to upgrade translation map from V1 to V2
04.05.2023 14:17:12.899 *INFO* [pool-59-thread-1] com.adobe.dxml.common.executor.RunnableSynchronizedOTS Initiating lock for node : /var/dxml/executor-locks/translation-map-upgrade/1683190032886
04.05.2023 14:17:12.901 *INFO* [pool-59-thread-1] com.adobe.fmdita.translationservices.TranslationMapUpgradeScript Starting porting of translation map from V1 to V2
04.05.2023 14:17:12.904 *INFO* [pool-59-thread-1] com.adobe.fmdita.translationservices.TranslationMapUpgradeScript Memory increase is of : 764 kB
04.05.2023 14:17:12.906 *INFO* [pool-59-thread-1] com.adobe.fmdita.translationservices.TranslationMapUpgradeScript Completed porting of translation map from V1 to V2
04.05.2023 14:17:12.907 *INFO* [pool-59-thread-1] com.adobe.dxml.common.executor.RunnableSynchronizedOTS Releasing lock for node : /var/dxml/executor-locks/translation-map-upgrade/1683190032886
04.05.2023 14:17:12.909 *INFO* [pool-59-thread-1] com.adobe.fmdita.xmltranslation.ots.TranslationMapUpgradeOTS Completed the thread to upgrade translation map from V1 to V2
```

查找 `com.adobe.fmdita.translationservices.TranslationMapUpgradeScript Completed porting of translation map from V1 to V2` 和 `com.adobe.fmdita.xmltranslation.ots.TranslationMapUpgradeOTS Completed the thread to upgrade translation map from V1 to V2` 然后再继续后续步骤。

## 安装版本4.3.1之后



安装Experience Manager指南后，您可以将适用于从新安装的版本到安装的各种配置合并到一起。

>[!NOTE]
>
> 可以自定义dam-update-asset模型。 因此，如果已完成任何自定义设置，那么我们需要将自定义设置和Experience Manager指南同步到模型的工作副本中。

1. **DAM更新资产工作流\（后处理更改\）：**

1. 打开URL：

   ```
   http://localhost:4502/libs/cq/workflow/admin/console/content/models.html 
   ```

1. 选择 **DAM更新资产工作流**.
1. 单击 **编辑**.
1. 如果 **DXML后处理启动器** 组件存在，请确保自定义项已同步。
1. 如果 **DXML后处理启动器** 组件不存在，请执行以下步骤以插入该组件：

1. 单击 **插入组件** \(负责Experience Manager指南后期处理，这是该过程的最后一步\)。
1. 配置 **流程步骤** ，详情如下：

   **“常用”选项卡**

   **标题：** DXML后处理启动器

   **描述**：DXML后处理启动器步骤，这将触发用于修改/创建的资产的DXML后处理的sling作业

   **“流程”选项卡**

   - 选择 **DXML后处理启动器**&#x200B;从 **进程** 下拉框

   - 选择 **处理程序前进**

   - 选择 **完成**

1. 单击 **同步** 完成更改后显示在右上角。 您将收到成功通知。

   >[!NOTE]
   >
   > 刷新并验证最终工作流模型中是否存在自定义更改和Experience Manager指南后处理步骤。

1. 一次 **DAM更新资产工作流** 经过验证，检查相应的启动器配置。 为此，请转到AEM Workflow界面并打开启动器。

   ```http
   http://localhost:4502/libs/cq/workflow/content/console.html
   ```

   查找并对以下两个启动器\（如果需要\）进行相应更改\（应该处于活动状态\） **DAM更新资产工作流**：

1. “ ”的启动器&#x200B;*节点已创建*“（表示） **DAM更新资产工作流** — 表示条件 `"jcr:content/jcr:mimeType!=video"`，则“通配”值应为：

   ```json
   /content/dam(/((?!/subassets|/translation_output).)*/)renditions/original
   ```

   - “excludeList”应具有 `"event-user-data:changedByWorkflowProcess"`.
   - “ ”的启动器&#x200B;*节点已修改*“（表示） **DAM更新资产工作流 —** 条件&quot;`jcr:content/jcr:mimeType!=video`“”，“通配”值应为：

   ```json
   /content/dam(/((?!/subassets|/translation_output).)*/)renditions/original
   ```

   - `excludeList` 应该有 `"event-user-data:changedByWorkflowProcess"`.

1. 升级完成后，请确保验证并更新任何自定义项/叠加图，以匹配新的应用程序代码。 下面给出了一些示例：
   - 任何来自/libs/fmditor/libsis的叠加组件都应与新的产品代码进行比较，并且更新应在/apps下的叠加文件中完成。
   - 应审查产品中使用的任何clientlib类别是否有更改。 任何覆盖的配置\（见以下示例\）应与最新的配置进行比较，以获取最新的功能：
   - elementmapping.xml
   - ui\_config.json\（可能已在文件夹配置文件中设置\）
   - 已修改 `com.adobe.fmdita.config.ConfigManager`


## 索引现有内容的步骤

>[!NOTE]
>
> 如果从4.3.0或4.2.1升级，则无需执行这些步骤。

执行以下步骤来索引现有内容，并在映射级别使用新的查找和替换文本：


- 对服务器运行POST请求\（使用正确的身份验证\） - `http://<server:port\>/bin/guides/map-find/indexing`. (可选：您可以传递映射的特定路径来索引它们，默认情况下，所有映射都将索引\|\|例如： `https://<Server:port\>/bin/guides/map-find/indexing?paths=<map\_path\_in\_repository\>`)


- 该API将返回作业ID。 要检查作业的状态，可以将带有作业ID的GET请求发送到同一端点 —  `http://<server:port\>/bin/guides/map-find/indexing?jobId=\{jobId\}`\(例如： `http://localhost:8080/bin/guides/map-find/indexing?jobId=2022/9/15/7/27/7dfa1271-981e-4617-b5a4-c18379f11c42`\)


- 作业完成后，上述GET请求将做出成功响应，并提及是否有任何映射失败。 可以从服务器日志中确认已成功编制索引的映射。

## 后处理现有内容以使用断开链接报表的步骤

>[!NOTE]
>
> 如果从4.3.0升级，则无需执行这些步骤

执行以下步骤后处理现有内容并使用新的断开链接报表：

1. （可选）如果系统中有超过100,000个dita文件，请更新 `queryLimitReads` 下 `org.apache.jackrabbit.oak.query.QueryEngineSettingsService` 设置为较大的值（任何大于现有资产数的值，例如200,000），然后重新部署。

   | PID | 属性键 | 属性值 |
   |---|---|---|
   | org.apache.jackrabbit.oak.query.QueryEngineSettingsService | queryLimitRead | 值： 200000 <br> 默认值： 100000 |

1. 执行以下API以对所有文件运行后处理：

   | 终点 | /bin/guides/reports/upgrade |
   |---|---|
   | 请求类型 | **POST**  此脚本是一个POST请求，因此应通过Postman等代理执行。 |
   | 预期响应 | 该API将返回作业ID。 要检查作业的状态，可以将带有作业ID的GET请求发送到同一端点。<br> 示例URL： `http://<server:port>/bin/guides/reports/upgrade` |

   | 终点 | /bin/guides/reports/upgrade |
   |---|---|
   | 请求类型 | **GET** |
   | 参数 | jobId：传递从上一个post请求收到的jobId。 |
   | 预期响应 |  — 作业完成后，GET请求将做出成功响应。 <br>  — 如果出现错误，请与客户成功团队共享错误日志以及API输出。  <br>示例URL： `http://<server:port>/bin/guides/reports/upgrade?jobId=2022/9/15/7/27/7dfa1271-981e-4617-b5a4-c18379f11c42_678` |


1. 恢复为默认或以前的现有值 `queryLimitReads` 如果您在步骤1中更改了它。



**父主题：**[&#x200B;下载并安装](download-install.md)
