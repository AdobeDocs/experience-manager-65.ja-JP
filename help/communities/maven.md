---
title: コミュニティでの Maven の使用
description: Communities で使用するAdobe Experience Manager Uber API jar について説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3df90511-e43e-442b-bf73-44c22c1886b7
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 7%

---

# コミュニティでの Maven の使用 {#using-maven-for-communities}

## 概要 {#overview}

Adobe Experience Manager（AEM） Communities のドキュメントのこの節は、次の機能に追加されています。

* [Apache Maven を使用したAEM プロジェクトの構築](../../help/sites-developing/ht-projects-maven.md).

個々のアーティファクトを置き換える「uber」アーティファクトは 1 つだけです。

* AEM [Uber API jar](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

>[!NOTE]
>
>AEM 6.4 以降、Communities API は明示的にはリリースされません。 すべての Communities API が Uber jar 自体に含まれるようになりました。
>
>最新の Communities リリースに関する最新情報を入手してください。
>
>を参照してください。 [最新リリース](deploy-communities.md#latest-releases) 最新のバージョンを識別できるセクションです。

## Maven 依存関係の例 {#maven-dependency-example}

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.7</version>
    <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>を参照してください。 [AEM Uber jar リポジトリ](https://mvnrepository.com/artifact/com.adobe.aem/uber-jar) 最新の Uber jar アーティファクトを特定できます。

<!--
There are now two "uber" artifacts that replace individual artifacts:

* AEM [Communities API jar](#communities-api-jar-artifact)
* AEM [Uber API jar](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

## Communities API Jar Artifact {#communities-api-jar-artifact}

Following is an example of a GAV for the AEM Communities API jar:

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>

```

Ensure thet the version specified corresponds with the Communities package version installed for AEM Communities. To verify the installed version number:

1. Log in with adminstrative privileges.
1. Browse to [Package Manager](../../help/sites-administering/package-manager.md). For example, [http://localhost:4502/crx/packmgr/](http://localhost:4502/crx/packmgr/)

1. Locate the package: `cq-socialcommunities-pkg-1.x.xxx`
1. Extract the version from the package name:
   * First version for AEM 6.3 is version 1.11.170.
   * Feature packs is versions 1.12.xxx.

>[!NOTE]
>
>It is recommended to keep up-to-date with the most recent Communities release.
>
>Visit the [Latest Releases](deploy-communities.md#latest-releases) section to identify the most recent version.

## Maven Dependency Example {#maven-dependency-example}

The Communities API jar must be specified before the Uber API jar.

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.3.0</version>
    <scope>provided</scope>
    <classifier>apis</classifier>
</dependency>
```
-->
