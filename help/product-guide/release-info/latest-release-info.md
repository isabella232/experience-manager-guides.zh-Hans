---
title: AEM Guides版本
description: 最新的 AEM Guides 版本和必备 AEM 版本
exl-id: 780697a9-bdc6-40c2-b258-64639fe30f88
source-git-commit: eb3fe92d36bc58a11e47f786a10d5938e2ed0184
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 1%

---

# [!DNL AEM Guides] 版本

[!DNL Adobe Experience Manager Guides] 是部署在AEM上的应用程序。 这是一个功能强大、企业级组件内容管理解决方案(CCMS)，可在Adobe Experience Manager中启用原生DITA支持，使AEM能够处理基于DITA的内容创建和交付。

AEM Guides包有两种变体可用 — UUID内部版本和非UUID内部版本。

## UUID和非UUID内部版本

UUID和非UUID内部版本之间的主要区别如下：

|  | 非UUID版本 | UUID版本 |
|---|---|---|
| **资产识别** | 所有资源都使用存储库中资源的路径进行标识。 | 所有资产均使用其UUID（首次上传资产时系统生成的唯一ID）进行标识。 |
| **引用创建** | 所有内容引用都是根据其路径创建的。 | 所有内容引用都是基于其UUID创建的。 |

### UUID构建的优势

* UUID安装的性能更高：
   * 参照是独立于路径的：参照管理系统在参照基于UUID而不是路径创建时可识别链接。
   * 移动/更新操作高效：即使资产迁移到存储库中的其他路径，UUID仍保持不变。 因此，在移动/更新操作中，无需处理即可修补资源之间的引用。
* UUID构建具有前瞻性，因为我们也将此框架用于AEM Guides的云设置。


### 在两个内部版本之间进行选择

* 如果您是新客户，我们建议您使用UUID内部版本。
* 如果您是现有客户，则可以选择迁移到UUID内部版本，因为现在可以从非UUID内部版本迁移到UUID内部版本。 欲知更多详情，请参见 *非UUID到UUID内容迁移* 中的部分 **安装和配置Adobe Experience Manager Guides。**

>[!NOTE]
>
>* 在首次设置时，客户将需要在UUID和非UUID模式之间进行选择（如果您需要帮助，请联系客户成功经理，帮助您根据用例做出决策）。
>* 从一种版本的AEM Guides升级到较新版本时，客户将需要确保选择相同的模式（UUID/非UUID）以匹配其现有模式。 非UUID内部版本不应直接升级到UUID内部版本。 从非UUID内部版本迁移到UUID内部版本将需要内容迁移。

**升级内部版本**

当您从旧版本升级到新版本时 [!DNL AEM Guides]中，您可能需要执行迁移脚本。 有关升级说明，请参阅发行说明和特定于版本的文档。

并非所有升级路径都直接受支持。 例如，只有从版本3.8直接升级到版本4.0才可行。如果您使用的版本低于3.8，请参阅特定于版本的文档以了解升级说明 [帮助存档](https://helpx.adobe.com/xml-documentation-for-experience-manager/archive.html).
请联系您的客户成功经理以验证升级路径。

**[!DNL AEM Guides]内部版本**

以下列表包含最新的 [!DNL AEM Guides] 可用于在AMS或内部部署上安装的包、相应的AEM版本（先决条件）、包的下载链接以及其他有用信息。 建议仅使用的最新内部版本 [!DNL AEM Guides]. 如果由于某种原因，您需要访问旧版本，请联系您帐户的客户成功经理。

>[!NOTE]
>
>联系您的客户成功经理以访问 [!DNL AEM Guides] AEM内部版本as a Cloud Service。

| [!DNL AEM Guides] 版本 | 发行说明 | AEM先决条件 | 生成下载链接 |
|---|---|---|---|
| **AEM Guides 4.3.0** | [4.3.1发行说明](./release-notes-4.3.1.md)<br><br>[4.3.0发行说明](./release-notes-4.3.md) | **非UUID和UUID 4.3.1** <br>AEM 6.5 SP18、SP17、SP16、SP15或SP14 <br><br>   Java：11或8 <br><br> **非UUID和UUID 4.3.0** <br>AEM 6.5 SP18、SP17、SP16、SP15或SP14 <br><br>   Java：11或8 | **非UUID AEM 6.5** <br> [4.3.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-3-1%2Fcom.adobe.fmdita-6.5-4.3.1.390.zip) <br> [4.3.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-3%2Fcom.adobe.fmdita-6.5-4.3.0.347.zip)<br> **UUID AEM 6.5** <br> [4.3.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-3-1%2Fcom.adobe.fmdita-6.5-uuid-4.3.1.390.zip)<br>[4.3.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-3%2Fcom.adobe.fmdita-6.5-uuid-4.3.0.347.zip) |
| **AEM Guides 4.2** | [4.2.1发行说明](https://experienceleague.adobe.com/docs/experience-manager-guides-learn/tutorials/release-info/release-notes/on-prem-release-notes/42-release/42-release-notes/release-notes-4.2.1.html?lang=en)<br> <br> [4.2发行说明](https://experienceleague.adobe.com/docs/experience-manager-guides-learn/tutorials/release-info/release-notes/on-prem-release-notes/42-release/42-release-notes/release-notes-4.2.html?lang=en) | **非UUID和UUID 4.2.1**<br><br> AEM 6.5 SP15、SP14、SP13或SP12 <br><br>Java：11或8 <br><br>**非UUID和UUID 4.2**<br><br> AEM 6.5 SP15、SP14、SP13或SP12 <br><br>Java：11或8<br><br> | **非UUID**： <br> **AEM 6.5** <br>[4.2.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-2-1%2F4-2-1-non-uuid%2Fcom.adobe.fmdita-6.5-4.2.1.270.zip)<br>[4.2](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-2%2F4-2-non-uuid%2Fcom.adobe.fmdita-6.5-4.2.229.zip)<br><br> **UUID** <br>**AEM 6.5** <br>[4.2.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-2-1%2F4-2-1-uuid%2Fcom.adobe.fmdita-6.5-uuid-4.2.1.270.zip)<br>[4.2](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-2%2F4-2-uuid%2Fcom.adobe.fmdita-6.5-uuid-4.2.229.zip)<br> |
| **AEM Guides 4.1** | [4.1.x发行说明](https://experienceleague.adobe.com/docs/experience-manager-guides-learn/tutorials/release-info/release-notes/on-prem-release-notes/release-notes-4.1.html) | **非UUID和UUID 4.1.2**<br><br> AEM 6.5 SP13、SP12、SP11或SP10 <br>Java：11或8 <br><br>**非UUID和UUID 4.1**<br><br> AEM 6.5 SP13、SP12、SP11或SP10 | **非UUID**： <br> **AEM 6.5** <br>[4.1.3](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-1-3%2F4-1-3-non-uuid%2Fcom.adobe.fmdita-6.5-sp-4.1.3.2.zip)<br>[4.1.2](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-1-2%2F4-1-2-non-uuid%2Fcom.adobe.fmdita-6.5-sp-4.1.2.11.zip)<br>[4.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-1%2F4-1-non-uuid%2Fcom.adobe.fmdita-6.5-4.1.159.zip)<br><br> **UUID** <br>**AEM 6.5** <br>[4.1.3](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-1-3%2F4-1-3-uuid%2Fcom.adobe.fmdita.uuid-6.5-sp-4.1.3.2.zip)<br>[4.1.2](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-1-2%2F4-1-2-uuid%2Fcom.adobe.fmdita.uuid-6.5-sp-4.1.2.11.zip)<br>[4.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-1%2F4-1-uuid%2Fcom.adobe.fmdita-6.5-uuid-4.1.159.zip) |
| **AEM Guides 4.0** | [4.0.x发行说明](https://helpx.adobe.com/xml-documentation-for-experience-manager/release-note/release-notes-xml-documentation-solution-4-0.html) | **非UUID和UUID 4.0.3**<br> AEM 6.5 SP12、SP11、SP10或SP9 <br>Java：11或8 <br><br> <br>**非UUID和UUID 4.0.2** <br> AEM 6.5 SP12、SP11、SP10或SP9 <br>Java：11或8 <br><br> **非UUID和UUID 4.0** <br> AEM 6.5 SP11、SP10或SP9 | **非UUID**： <br> **AEM 6.5** <br>[4.0.3](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-0-3%2F4-0-2-non-uuid%2Fcom.adobe.fmdita-6.5-hotfix-4.0.3.1.zip)<br>[4.0.2](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-0-2%2F4-0-2-non-uuid%2Fcom.adobe.fmdita-6.5-sp-4.0.2.10.zip)  <br> [4.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/aemdox/4-0/4-0-non-uuid/com.adobe.fmdita-6.5-4.0.70.zip)  <br><br> **UUID** <br>**AEM 6.5**  <br>[4.0.3](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-0-3%2F4-0-3-uuid%2Fcom.adobe.fmdita.uuid-6.5-hotfix-4.0.3.1.zip) <br>[4.0.2](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faemdox%2F4-0-2%2F4-0-2-uuid%2Fcom.adobe.fmdita.uuid-6.5-sp-4.0.2.10.zip)<br> [4.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/aemdox/4-0/4-0-uuid/com.adobe.fmdita-6.5-uuid-4.0.70.zip) |
| **AEM Guides 3.8.5** <br> 3.8.5是3.8之上的SP版本。 <br>由于3.8.5 SP包含关键修补程序，因此不能单独安装3.8版本。 <br>客户必须先安装3.8，然后再安装SP 3.8.5。 | [3.8.x发行说明](https://helpx.adobe.com/xml-documentation-for-experience-manager/release-note/release-notes-xml-documentation-solution-3-8.html) | **非UUID** <br> AEM 6.5 SP9或SP8 <br> AEM 6.4 SP8 <br> AEM 6.3 SP3 <br><br> **UUID** <br> AEM 6.5 SP9或SP8 | **非UUID**： <br> **AEM 6.5** <br> [3.8.5sp](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/aemdox/3-8-5/com.adobe.fmdita-6.5-hotfix-3.8.5.2.zip) <br>[3.8](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/aemdox/3-8/com.adobe.fmdita-6.5-3.8.166.zip)<br> **AEM 6.4** <br> [3.8.5sp](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/aemdox/3-8-5/com.adobe.fmdita-6.4-hotfix-3.8.5.1.zip) <br>[3.8](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/aemdox/3-8/com.adobe.fmdita-6.4-3.8.166.zip) <br> **AEM 6.3** <br> [3.8.5sp](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/aemdox/3-8-5/com.adobe.fmdita-6.3-hotfix-3.8.5.1.zip) <br>[3.8](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/aemdox/3-8/com.adobe.fmdita-6.3-3.8.166.zip) <br><br> **UUID** <br>**AEM 6.5** <br> [3.8.5sp](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/aemdox/3-8-5uuid/com.adobe.fmdita.uuid-6.5-hotfix-3.8.5.2.zip) <br> [3.8](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/aemdox/3-8uuid/com.adobe.fmdita.uuid-6.5-3.8.168.zip) |
