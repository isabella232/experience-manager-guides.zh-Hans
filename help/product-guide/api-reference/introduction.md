---
title: 简介
description: AEM Guides的API参考指南简介
role: Developer
feature: Introduction
exl-id: d8ee9cf7-1d67-4b4a-aa80-64e893a99463
source-git-commit: 26d0b3fd6b6d34fb2a86417179c8be672d40ad86
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# 简介 {#id1761C0007W7}

Adobe Experience Manager Guides \(以后称为 *AEM指南*\)是一个端到端的企业解决方案，它使Adobe Experience Manager \(AEM\)具备组件内容管理解决方案\(CCMS\)功能，可用于创建和交付基于DITA的内容。 客户可以使用AEM Guides API以编程方式访问AEM Guides工作流，以将其与其他企业应用程序集成。 Adobe合作伙伴还可以使用这些API来增强AEM Guides的价值主张，方法是扩展其功能或将其与其他应用程序或服务集成。

## AEM Guides API

AEM Guides API有两种格式：HTTP和Java。 这些API向应用程序开发人员公开AEM Guides的关键功能。 使用这些函数，开发人员可以创建自己的插件来扩展现成的工作流。 这些API可用于管理DITA内容的输出、使用DITA映射、将条件属性添加到文件夹级别配置文件以及将HTML和Words文档转换为DITA格式。

## 在本地Apache Maven存储库中安装JAR {#install-jar-local}

为了能够使用AEM Guides公开的JAR文件，您需要将其安装到本地Apache Maven存储库中。 执行以下步骤以在您的位置Maven存储库上安装JAR：

1. 在本地系统上提取AEM Guides包\(.zip\)文件的内容。

2. 在命令提示符下，导航到提取的内容路径中的以下文件夹：

   ```
   \jcr_root\libs\fmdita\osgi-bundles\install
   ```

3. 运行以下命令将API捆绑包安装到本地Maven存储库：

   ```
   mvn install:install-file -Dfile=api-X.x.jar -DgroupId=com.adobe.fmdita -DartifactId=api -Dversion=X.x -Dpackaging=jar**
   ```

   >[!NOTE]
   >
   > 在上述命令中，X.x应替换为Dfile和Dversion参数中的实际版本号。

4. \(*可选*\)在本地Maven项目的存储库中安装依赖项。 您可以通过在Maven项目中创建文件夹，然后运行 `mvn install` 上一步中给定的命令，带有以下附加参数：

   ```
   -DlocalRepositoryPath=<path_to_project_repository>
   ```

   接下来，要向Maven构建过程公开项目的本地存储库文件夹，请添加 `repository` 元素，如下所示：

   ```XML
   <repositories>
      <repository>
         <id>project-repository</id>
         <url>file://${project.basedir}/repository</url>
      </repository>
   </repositories>
   ```


此过程将API JAR安装到本地Maven存储库中。

## 在Maven项目中使用服务API JAR

在本地Maven存储库中安装API JAR后，执行以下步骤以在项目中使用JAR：

1. 将JAR添加到代码库，并将其提交到文件夹下的代码库存储库，如“依赖项”。 请注意，文件夹名称取决于您的代码基层次结构。

2. 按如下方式配置项目pom.xml文件：

   父项目的pom.xml文件：

   >[!IMPORTANT]
   >
   > 在以下代码片段中，应将X.x替换为实际版本号和API JAR的文件名。 此信息将与 [安装过程](#install-jar-local).

   ```XML
   <plugin>
   
       <groupId>org.apache.maven.plugins</groupId>
   
      <artifactId>maven-install-plugin</artifactId>
   
       <version>2.5.2</version>
   
       <configuration>
   
               <groupId>com.adobe.fmdita</groupId>
   
               <artifactId>api</artifactId>
   
               <version>X.x</version>
   
               <file>${basedir}/dependencies/fmdita/api-X.x.jar</file>
   
               <packaging>jar</packaging>
   
               <generatePom>true</generatePom>
   
       </configuration>
   
       <executions>
   
           <execution>
   
               <id>inst_fmdita</id>
   
                   <goals>
   
                       <goal>install-file</goal>
   
                   </goals>
   
                   <phase>clean</phase>
   
           </execution>
   
       </executions>
   </plugin>
   ```

   子模块的pom.xml文件：

   ```XML
   <plugin>
      <groupId>org.apache.maven.plugins</groupId>
   
      <artifactId>maven-install-plugin</artifactId>
   
      <configuration>
   
         <groupId>com.adobe.fmdita</groupId>
   
         <artifactId>api</artifactId>
   
         <version>3.6</version>
   
         <file>${basedir}/../dependencies/fmdita/api-3.6.jar</file>
   
         <packaging>jar</packaging>
   
         <generatePom>true</generatePom>
   
      </configuration>
   
      <executions>
   
         <execution>
   
            <id>inst_fmdita</id>
   
            <goals>
   
               <goal>install-file</goal>
   
            </goals>
   
            <phase>clean</phase>
   
         </execution>
   
      </executions>
   
   </plugin>
   ```


## 从公共Maven存储库配置并使用服务API JAR

执行以下步骤以配置和使用项目中的公共Maven存储库中的服务API JAR：

1. 要在项目中使用服务API JAR，请在pom.xml文件中配置AEM Guides公共Maven存储库。
2. 按如下方式在Maven的settings.xml文件中配置公共Maven存储库：

   ```XML
   <repository>
      <id>fmdita-public</id>
      <name>fmdita-public</name>
      <url>https://repo.aem-guides.com/repository/fmdita-public</url>
   </repository>
   ```

3. 设置存储库后，将服务API JAR作为项目依赖项添加到项目的pom.xml文件中。

   >[!NOTE]
   >
   > 使用与您在服务器上安装的AEM Guides包相同版本的API JAR。

4. 配置Maven依赖项，如下所示：

   ```XML
   <dependency>
      <groupId>com.adobe.fmdita</groupId>
      <artifactId>api</artifactId>
      <version>4.0</version>
   </dependency>
   ```


在项目的pom.xml文件中添加服务API JAR作为项目依赖项后，您可以在项目中构建和使用AEM Guides Java API。

## as a Cloud Service使用Maven Central repository for AEM Guides中的API JAR

对于AEM Guidesas a Cloud Service，API JAR已部署到Maven Central。 您无需任何设置即可使用API JAR。

>[!NOTE]
>
> API jar的命名约定已根据云加载项命名约定进行了更新。

要使用API JAR，您需要将依赖关系添加到项目的pom.xml，如下所示：

```XML
<dependency>
   <groupId>com.adobe.aem</groupId>
   <artifactId>aem-guides-sdk-api</artifactId>
   <version>2022.5</version>
</dependency>
```

>[!NOTE]
>
> 由于API JAR中的包仍然相同，因此无需更改代码即可在现有云项目中使用此API JAR。

## 其他资源

以下是AEM Guides的其他有用资源的列表，这些资源位于 [学习和支持](https://helpx.adobe.com/support/xml-documentation-for-experience-manager.html) 页面：

- 用户指南
- 安装和配置指南
- 快速入门指南
- [“帮助存档”页](https://helpx.adobe.com/xml-documentation-for-experience-manager/archive.html) \（访问旧版发行文档\）
