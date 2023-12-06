---
title: 配置和自定义工作流
description: 了解如何配置和自定义工作流
exl-id: a5742082-cc0b-49d9-9921-d0da1b272ea5
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 1%

---

# 配置和自定义工作流 {#id181AI0OJ0RO}

通过工作流，您可以自动化Adobe Experience Manager \(AEM\)活动。 工作流包含一系列按特定顺序执行的步骤。 您可以定义要在每个步骤中执行的不同活动。 例如，您可以在创建主题审阅时向组中的所有审阅人发送电子邮件通知。 或者，在输出生成任务完成时向发布者发送通知。

有关AEM中工作流的详细信息，请参阅：

- [管理工作流实例](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html)

- 应用和参与工作流： [使用项目工作流](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/projects/workflows.html).


本主题中的部分将指导您逐步完成AEM Guides中提供的默认工作流中可以进行的各种自定义设置。

## 自定义审核工作流 {#id176NE0C00HS}

每个组织的内容创作团队都以特定的方式工作，以满足其业务要求。 有些组织设有专门的编辑人员，而有些其他组织则设有自动编辑审查系统。 例如，在组织中，典型的创作和发布工作流程可能包括以下任务 — 每当作者完成创作内容时，它会自动发送给审阅人，审阅完成后会发送给发布者，以生成最终输出。 在AEM中，您可以采用流程的形式组合对内容和资产执行的活动并将其映射到AEM工作流。 有关AEM中工作流的详细信息，请参阅 [管理工作流](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html) 请参阅AEM文档。

AEM Guides允许您自定义默认的审阅工作流。 您可以将以下四个与自定义审阅相关的流程用于其他创作或发布工作流。

- **创建审核**：此进程准备创建审阅任务所需的元数据。 例如，它将为审阅人分配审阅权限、将主题的状态设置为审阅、设置审阅时间表等。 在四个流程中，这是必须包含在自定义工作流中的唯一强制流程。 在工作流中，您可以选择包括或排除其他三个流程。

- **分配审阅任务**：此进程创建审阅任务，并将任务通知发送给发起者和审阅者。

- **发送审核电子邮件**：此进程向发起者和审阅者发送审阅电子邮件。

- **计划作业以关闭审阅**：此过程可确保审查过程在到达截止日期时完成。


创建自定义审阅工作流时，第一项任务是设置“创建审阅”进程所需的元数据。 为此，您可以创建一个ECMA脚本。 下面提供了分配元数据的ECMA脚本示例：

```javascript
var workflowdata=workItem.getWorkflowData();
workflowdata.getMetaDataMap().put("initiator","admin");
workflowdata.getMetaDataMap().put("operation","AEM_REVIEW");
workflowdata.getMetaDataMap().put("orgTopics","/content/dam/xml-solution/review.xml");
workflowdata.getMetaDataMap().put("payloadJson","{\"base\":\"/content/dam/xml-solution\",\"asset\":[\"/content/dam/xml-solution/review.xml\"],\"referrer\":\""}");
workflowdata.getMetaDataMap().put("deadline","2017-06-27T13:19:00.000+05:30");
workflowdata.getMetaDataMap().put("title","Review through custom workflow");
workflowdata.getMetaDataMap().put("description","Initiate this review process using the AEM workflow");
workflowdata.getMetaDataMap().put("assignee","user-one", "user-two");
workflowdata.getMetaDataMap().put("status","1");
workflowdata.getMetaDataMap().put("projectPath","/content/projects/review");
workflowdata.getMetaDataMap().put("startTime", System.currentTimeMillis());
```

您可以在中创建此脚本 `/etc/workflows/scripts` 节点。 下表描述了此ECMA脚本所分配的属性：

| 属性 | 类型 | 描述 |
|--------|----|-----------|
| `initiator` | 字符串 | 启动审阅任务的用户的用户ID。 |
| `operation` | 字符串 | 静态值设置为 `AEM_REVIEW`. |
| `orgTopics` | 字符串 | 共享以供审核的主题路径。 指定多个以逗号分隔的主题。 |
| `payloadJson` | JSON对象 | 指定以下值： -   `base`：包含已发送以供审阅的主题的父文件夹的路径。 <br> -   `asset`：发送以供审阅的主题路径。 <br> -   `referrer`：将其留空。 |
| `deadline` | 字符串 | 指定时间 `yyyy-MM-dd'T'HH:mm:ss.SSSXXX` 格式。 |
| `title` | 字符串 | 输入审核任务的标题。 |
| `description` | 字符串 | 输入审核任务的说明。 |
| `assignee` | 字符串 | 要向其发送主题以供审阅的用户的用户ID。 |
| `status` | 整数 | 静态值设置为1。 |
| `startTime` | 长整型 | 使用 `System.currentTimeMillis()` 函数以获取当前系统时间。 |

创建脚本后，请在调用工作流中的创建审阅进程之前调用该脚本。 然后，根据您的要求，您可以调用其他审阅工作流流程。

### 从清除配置中删除审核工作流

要提高工作流引擎性能，您可以定期从AEM存储库中清除已完成的工作流实例。 如果您使用默认的AEM配置，则会在特定时间段后清除所有已完成的工作流实例。 这也会导致所有审阅工作流从AEM存储库中清除。

您可以通过从自动清除配置中删除审核工作流模型\(information\)来阻止自动清除审核工作流。 您需要使用 **AdobeGranite工作流清除配置** 从自动清除列表中删除审阅工作流模型。

在 **AdobeGranite工作流清除配置**，确保至少列出一个可安全清除的工作流。 例如，您可以使用由AEM Guides创建的以下任何工作流：

- /etc/workflow/models/publishditamap/jcr：content/model
- /etc/workflow/models/post-dita-project-creation-tasks/ jcr：content/model

在中添加工作流 **AdobeGranite工作流清除配置** 确保AEM仅清除配置中列出的那些工作流。 这会阻止AEM清除审阅工作流信息。

有关配置的更多详细信息 **AdobeGranite工作流清除配置**，请参见 *管理工作流实例* 请参阅AEM文档。

### 自定义电子邮件模板

许多AEM Guides工作流都使用电子邮件通知。 例如，如果您启动审阅任务，则会向审阅人发送电子邮件通知。 但是，要确保电子邮件通知已发送，您必须在AEM中启用此功能。 要在AEM中启用电子邮件通知，请参阅文章 [发送电子邮件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) 请参阅AEM文档。

AEM Guides包含一组您可自定义的电子邮件模板。 执行以下步骤可自定义这些模板：

1. 使用包管理器进行下载 `/libs/fmdita/mail` 文件。

   >[!NOTE]
   >
   > 请勿将默认配置文件中的任何自定义设置用于 ``libs`` 节点。 您必须创建一个由 ``libs`` 中的节点 ``apps`` 节点并更新以下文件中的所需文件： ``apps`` 仅节点。

1. 邮件文件夹包含以下可自定义的模板：

   | 模板文件名 | 描述 |
   |-----------------|-----------|
   | closereview.html | 此电子邮件模板在关闭审核任务时使用。 |
   | createreview.html | 创建新审阅任务时使用此电子邮件模板。 |
   | reviewapproval.css | 此CSS文件包含电子邮件模板的样式。 |


## 自定义输出后生成工作流 {#id17A6GI004Y4}

AEM Guides使您能够灵活地指定输出后生成工作流程。 您可以对使用AEM Guides生成的输出执行一些后处理任务。 例如，您可能希望在生成的AEM Site输出中应用一些CQ标记，或者在PDF输出中设置某些属性，或者在生成输出后向一组用户发送电子邮件。

您可以创建新的工作流模型以用作输出后生成工作流。 触发输出后生成工作流时，输出生成工作流通过工作流元数据映射共享上下文信息，您可以使用这些上下文信息对生成的输出执行处理。 下表描述了作为元数据共享的上下文信息：

| 属性 | 类型 | 描述 |
|--------|----|-----------|
| ``outputName`` | 字符串 | 用于生成输出的输出预设的名称。 |
| `generatedPath` | 字符串 | DAM中存储生成的输出的路径。 |
| `outputType` | com.adobe.fmdita.output.OutputType | 输出预设的类型。 |
| `outputTitle` | 字符串 | 输出预设的标题。 |
| `outputHistoryPath` | 字符串 | 历史记录节点的存储库路径。 |
| `isSuccess` | 布尔值 | 描述输出生成过程的最终状态（成功或失败）的标志。 |
| `logPath` | 字符串 | DAM中保存输出生成日志的路径。 |
| `generatedTime` | 长整型 | 触发输出生成过程的时间。 |
| `initiator` | 字符串 | 触发输出生成工作流的用户的用户ID。 |

要利用输出生成元数据，您可以创建ECMA脚本或OSGi捆绑包。 下面给出了使用元数据的ECMA脚本示例：

>[!NOTE]
>
> 您可以在中创建此脚本 ``/etc/workflows/scripts`` 节点。

```javascript
var session = workflowSession.getSession(); // Obtain session object to read/write the repository.
var payload = workItem.getWorkflowData().getPayload().toString(); // Get the workflow payload (the ditamap file on which the generation was triggered)
var metadata = workItem.getWorkflowData().getMetaDataMap(); // Get the workflow metadata object
var generatedPath = metadata.get("generatedPath"); // supplied by AEM Guides
var username = metadata.get("initiator"); // supplied by AEM Guides
var successful = metadata.get("isSuccess"); // supplied by AEM Guides
var title = metadata.get("outputTitle"); // supplied by AEM Guides
var subject = "Output Generation Finished";
var message = "Generation of output " + title + " just finished " + 
(successful ? "successfully. " : "unsuccessfully. ");
    message += "It was triggered by " + username;    
if (successful) {
    message += "<br/><br/>The path to the generated output is " + 
generatedPath;
}
/*
    MailerAPI.sendMail("dl-docs-authors", subject, message);
*/
```

创建脚本后，在工作流中调用自定义脚本。 然后，根据您的要求，您可以调用其他工作流进程。 设计自定义工作流后，调用 *最终确定帖子生成* 作为工作流进程的最后一步。 此 *最终确定帖子生成* 步骤可确保输出生成任务的状态更新为 *已完成* 在输出生成过程完成时。 创建自定义输出后生成工作流后，您可以将其配置为使用任何输出生成预设。 在中选择所需的工作流 *运行后期生成工作流* 所需的预设的属性。 使用配置的输出预设运行输出生成任务时，任务状态\（在“输出”选项卡中\）将更改为 *后处理*.
