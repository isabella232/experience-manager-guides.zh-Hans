---
title: 批量激活完成事件处理程序
description: 了解批量激活完成事件处理程序
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---

# 批量激活完成事件处理程序

Experience Manager指南公开 `com/adobe/fmdita/replication/complete` 用于在批量激活过程完成后执行任何操作的事件。 每当批量激活过程完成时，就会触发此事件。 例如，如果您运行批量激活地图的AEM站点预设，则会在激活过程结束后调用此事件。


您需要创建一个AEM事件处理程序来读取此事件中可用的属性并进行进一步处理。

活动详情说明如下：

**事件名称**：

```
com/adobe/fmdita/replication/complete 
```

**参数**： 名称|类型|描述| --------文----------- |`path`|字符串|触发此事件的文件的路径。 <br> 例如， `/content/output/sites/ditamap1-ditamap`. <br> 它是序列化为JSON数组的路径的列表。| |`messageType`|字符串|消息的类型。 <br>可能的选项： `REPLICATION`| |`action`|字符串|这是执行的操作。 <br>可能的选项： `BulkReplicate`| |`user`|字符串|启动操作的用户。| |`result`|字符串|批量激活的结果。 它是一个序列化的JSON对象： <br>`{"success":boolean,"code":integer,"message":"" }`| |`agentId`|字符串|复制中使用的agentId。 例如：`"publish"`。| |`importMode`|字符串|在激活中使用的导入模式。 可能的选项包括： <br>`REPLACE, MERGE, UPDATE`.|


**示例事件侦听器**：

```XML
@Component(service = EventHandler.class,
        immediate = true,
        property = {
                EventConstants.EVENT_TOPIC + "=" + "com/adobe/fmdita/replication/complete",
        })
 
public class SampleEventHandler implements EventHandler {
 
    protected final Logger log = LoggerFactory.getLogger(this.getClass());
 
    @Override
    public void handleEvent(final Event event) {
        Map<String, String> properties = new HashMap<>();
        properties.put("paths", (String) event.getProperty("paths"));
        properties.put("messageType", (String) event.getProperty("messageType"));
        properties.put("action", (String) event.getProperty("action"));
        properties.put("result", (String) event.getProperty("result"));
        properties.put("user", (String) event.getProperty("user"));
        properties.put("agentId", (String) event.getProperty("agentId"));
        properties.put("importMode", (String) event.getProperty("importMode"));
 
        String eventTopic = event.getTopic();
        log.debug("eventTopic {}", eventTopic);
        for(Map.Entry entry:properties.entrySet()) {
            log.debug(entry.getKey() + " : " + entry.getValue());
        }
 
    }
}
```
