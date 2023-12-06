---
title: 将带有版本的非UUID内容转换为UUID内容
description: 了解如何使用版本迁移非UUID内容。
exl-id: 9387e0d1-906c-4e5c-a7a0-0ed1600f5eb6
source-git-commit: 5e0584f1bf0216b8b00f00b9fe46fa682c244e08
workflow-type: tm+mt
source-wordcount: '1287'
ht-degree: 1%

---

# 使用版本迁移非UUID内容

执行以下步骤，将具有版本的非UUID内容迁移到UUID内容。

## 兼容性矩阵

| 当前AEM Guides版本（非UUID） | 迁移到UUID所需的版本 | 支持的升级路径 |
|---|---|---|
| 3.8.5 | 4.0非UUID | 安装4.1 (UUID)并运行迁移 |
| 4.0、4.0.x、4.1或4.1.x | 与当前的非UUID相同 | 安装4.1 (UUID)并运行迁移 |
| 4.2或更高版本 | NA | 尚不受支持 |

## 必需的包

1. **版本清除**： `com.adobe.guides.version-purge-1.0.11.zip` （可选）
1. **预迁移**： `com.adobe.guides.pre-uuid-migration-1.0.7.zip`
1. **迁移**： `com.adobe.guides.uuid-upgrade-1.0.17`
1. **迁移后**： `com.adobe.guides.post-uuid-migration-1.0.2.zip`


## 预迁移

1. （可选）对内容执行版本清除以删除不必要的版本并加快迁移过程。 要在版本4.1上执行版本清除（4.0上不支持），请安装包 `com.adobe.guides.version-purge-1.0.11.zip`，并使用此URL转到用户界面 `http://<server-name> /libs/fmdita/clientlibs/xmleditor_version_purge/page.html`.

   >[!NOTE]
   >
   >此实用程序不删除基线或审阅中使用的任何版本，也不具有任何标签。
1. 安装预迁移包(`com.adobe.guides.pre-uuid-migration-1.0.7.zip`)。

1. 运行以下查询以获取一个报告，其中提供了迁移所需的估计时间(ETA)，并会报告是否存在任何存在无法迁移的内容问题的文件。

>[!NOTE]
>
>您需要管理员权限才能执行迁移。


| 终结点 URL | 请求类型 | 查询参数 | 预期结果 |
|---|---|---|---|
| `/bin/guides/pre_uuid_upgrade` <br> <br>**例如**： http://localhost:4502/bin/guides/pre_uuid_upgrade?root=/content/dam | GET | **根**：根文件夹<br> **值**： `/content/dam` 整个存储库。 | 将创建一个迁移前报表(.csv)，其中列出文件数、总版本和错误。 <br><br> **示例输出**：<br>根文件夹： /content/dam <br>文件总数：2697 <br>总版本：10380 <br>有错误的文件数： 28 <br>详细报告将通过AEM CRX提供，网址为 `/content/uuid-pgrade/UuidMigrationReport_1688400131039.csv` |

如果系统中存在许多DITA文件，此步骤可能会失败。 要解决此问题，请通过增加值 *内存中读取限制(queryLimitReads)* 在Apache Jackrabbit查询引擎设置服务中，从中100000取一个大于系统中存在的DITA资产总数的数字。

## 迁移

### 步骤1：更新配置

1. 请确保可用空间至少是AEM （crx-quickstart目录）在迁移期间占用空间的10倍。 完成迁移后，可以通过运行压缩回收大部分磁盘空间(请参阅 [修订版清理](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=en))。

1. 启用 *启用后处理工作流启动器* 在 `com.adobe.fmdita.config.ConfigManager` 和 *启用版本后处理* 在 `com.adobe.fmdita.postprocess.version.PostProcessVersionObservation.`

1. 在非UUID版本上安装受支持发行版的UUID版本。 例如，如果您使用的是4.0非UUID内部版本或4.1非UUID内部版本，则需要安装UUID版本4.1。

1. 安装新的包以进行uuid迁移(`com.adobe.guides.uuid-upgrade-1.0.17`)。

1. 禁用以下工作流和在上运行的任何其他工作流 `/content/dam` 在中使用启动器 `http://localhost:4502/libs/cq/workflow/content/console.html`.

   * DAM更新资产工作流
   * DAM元数据写回工作流

1. 禁用 *启用后处理工作流启动器* 在 `com.adobe.fmdita.config.ConfigManager` 和禁用 *启用版本后处理* 在 `com.adobe.fmdita.postprocess.version.PostProcessVersionObservation`.

1. 禁用属性启用验证(`validation.enabled`)。

1. 确保 `uuid.regex` 属性文件夹在中已正确设置 `com.adobe.fmdita.config.ConfigManager`. 如果为空，则将其设置为默认值 —  `^GUID-(?<id>.*)`.
1. 为添加单独的日志程序 `com.adobe.fmdita.uuid.upgrade.UuidUpgrade` 浏览器响应也位于 `/content/uuid-upgrade/logs`.

### 步骤2：运行脚本并验证

先对包含较小数据的文件夹运行给定查询，然后再对其运行 `/content/dam`.

>[!TIP]
>
>您可以检查文件夹中的所有文件是否都已正确升级，以及所有功能是否仅对该文件夹起作用。

| 终结点 URL | 请求类型 | 查询参数 | 预期结果 |
|---|---|---|---|
| `/bin/guides/uuid_upgrade`<br><br> **例如**： `http://localhost:4502/bin/guides/uuid_upgrade?root=/content/dam/test` | GET | **根**：根文件夹 <br>**值**：适用于整个存储库的/content/dam 。<br><br>**ignoreImageVersion**<br> **值**： true/false(忽略图像版本的处理。 默认值为false) | 包含文件列表的迁移报告已成功迁移、升级失败、升级出现错误，以及所用总时间。 <br><br> **示例输出**： <br> [信息] 文件列表失败：0 <br>[信息] 不适用。 文件升级成功： 2241 <br>[信息] 不适用。 已升级但出现错误的文件数： 28 <br>[信息] 不适用。 无法升级的文件数： 0 <br> [信息] 所用总时间：0:37:03.131 |

>[!NOTE]
>
> 内容迁移可以在文件夹级别或整个文件夹级别运行 `/content/dam` 或在同一文件夹中（重新运行迁移）。

此外，确保也针对所有媒体资产（例如您在DITA内容中使用的图像和图形）执行内容迁移也很重要。

#### 基线迁移

对已迁移的文件夹运行查询以迁移其中的基线。

| 终结点 URL | 请求类型 | 查询参数 | 预期结果 |
|---|---|---|---|
| `/bin/guides/baseline_uuid_upgrade`<br><br> **例如**： ` http://localhost:4502/bin/guides/baseline_uuid_upgrade?root=/content/dam/test` | GET | **根**：根文件夹 <br> **值**：适用于整个存储库的/content/dam 。 <br><br> **ignoreImageVersion**<br> **值**： true/false <br>(忽略图像版本的处理。 默认值为false) <br><br> **doReviews** <br> **值**： true/false <br> (是否必须升级审阅。 默认值为false。) 包含文件列表的迁移报告已成功迁移、升级失败、升级出现错误，以及所用总时间。 <br> <br> **示例输出**：<br>[信息] 文件列表失败 <br> [信息] 不适用。 个文件已成功升级2241<br> [信息] 不适用。 个文件，共个文件，错误为28<br>[信息] 不适用。 个文件（共个），升级失败0<br>[信息] 所用总时间：0:37:03.131 |


### 步骤3：恢复配置

成功迁移服务器后，启用后处理、标记和以下工作流（包括迁移期间最初禁用的所有其他工作流）以继续在服务器上工作。

* DAM更新资产工作流
* DAM元数据工作流

>[!NOTE]
>
>如果某些文件在迁移前未处理或损坏，则它们在迁移前会损坏，甚至在迁移后也会保持损坏状态。

## 迁移验证

1. 安装post uuid迁移包(`com.adobe.guides.post-uuid-migration-1.0.2.zip`)。

1. 运行以下查询以验证在迁移期间没有导致任何链接断开的错误。 此脚本将识别是否存在之前未断开但现在由于任何原因已断开的任何链接。

   | 终结点 URL | 请求类型 | 查询参数 | 预期结果 |
   |---|---|---|---|
   | `/bin/guides/get_broken_links` <br> <br> **例如**：<br>`http://localhost:4502/bin/guides/get_broken_links` | GET | NA | 包含已损坏UUID的文件总数及其相应文件路径的迁移报告。 <br> <br> **示例输出**：<br>[调试] 检查内容中是否使用了所有这些通用唯一标识符。<br>[调试] 可能具有中断的UUID的文件总数：0 <br>[调试] 可能具有中断的UUID的路径：0 |

1. 迁移完成后，可以通过运行压缩回收大部分磁盘空间(请参阅 `https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=en`)。

## 增量内容迁移

1. 要将增量内容从活动服务器（非UUID）迁移到当前uuid服务器，请在非UUID服务器上安装预迁移脚本。

1. 对整个数据集（或子文件夹）运行以下查询，以识别并导出在给定时间戳之后修改的所有文件：时间戳使用ISO8601格式表示日期和时间( YYYY-MM-DDTHH:mm:ss.SSSZ)并允许部分表示，如YYYY-MM-DD。

   | 终结点 URL | 请求类型 | 查询参数 | 预期结果 |
   |---|---|---|---|
   | `/bin/guides/data_export`<br><br>**例如**： <br> `http://localhost:4502/bin/guides/data_export?timestamp=2023-07-11&root=/content/dam` | GET | **时间戳** <br> **值**： YYYY-MM-DD<br><br> **根**：根文件夹 <br> **值**： `/content/dam` 整个存储库。 | 在/var/dxml/exports中创建包含增量内容的zip文件。 <br> <br>**示例**： dataexport_1689761491218.zip（创建文件） |

1. 下载由脚本导出的zip文件。 响应的最后一行应给出所生成zip文件（存储在系统的/var/dxml/exports中）的路径。

1. 在资产UI中，将zip文件上传到uuid服务器。

1. 确保uuid服务器上安装了迁移后软件包。

1. 运行以下给定查询，将增量内容从上传的zip文件导入到系统中。 查询应包括已上传zip文件的路径，以正确识别并处理数据。

   | 终结点 URL | 请求类型 | 查询参数 | 预期结果 |
   |---|---|---|---|
   | `/bin/guides/data_import`<br> **例如**：`http://localhost:4502/bin/guides/data_import?path=/content/dam/dataexport_1689344927551.zip&createVersion=true` | POST | **path**<br> **值**： `/content/dam/filename.zip`（上传的文件位置） **createVersion** <br> **值**： true/false<br>（createVersion的默认值为false）。 | 文件将上载到所需的内容路径。<br><br>**示例**： `dataexport_1689761491218.zip`<br><br> (上一步中导出的同一文件将上传到中的所需路径 `/content/dam`)。 |

1. 如果新文件不存在，脚本将创建新文件；如果修改了现有文件，脚本将覆盖现有文件。

>[!NOTE]
>
> 在服务器上进行的版本历史记录和任何其他更改（如工作流和审核）需要手动更新。
