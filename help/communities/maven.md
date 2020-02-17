---
title: コミュニティでの Maven の使用
seo-title: コミュニティでの Maven の使用
description: AEM Communities API jar と AEM Uber API jar
seo-description: AEM Communities API jar と AEM Uber API jar
uuid: ea37a89a-db6c-4018-8ab9-f5717e6c0421
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a726c904-aadd-4678-be84-9e05808ab8be
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# コミュニティでの Maven の使用 {#using-maven-for-communities}

## 概要 {#overview}

AEM Communitiesドキュメントのこのセクションには、次の内容に加えて、以下のセクションが含まれます。

* [Apache Maven を使用して AEM プロジェクトをビルドする方法](../../help/sites-developing/ht-projects-maven.md)

現在、個々のアーティファクトに代わる 2 つの「uber」アーティファクトがあります。

* AEM [Communities API jar](#communities-api-jar-artifact)
* AEM [Uber API jar](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

## Communities API jar アーティファクト {#communities-api-jar-artifact}

AEM Communities API jar の GAV の例を次に示します。

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
```

指定したバージョンが、AEM Communities用にインストールされたCommunitiesパッケージバージョンに対応していることを確認します。 インストールされているバージョン番号を確認するには：

1. 管理者権限でログインします。
2. Browse to [Package Manager](../../help/sites-administering/package-manager.md). For example, [http://localhost:4502/crx/packmgr/](http://localhost:4502/crx/packmgr/)

3. パッケージ *cq-socialcommunities-pkg-1.x.xxx* を探します。
4. パッケージ名からバージョンを抽出します。
   * AEM 6.3 の最初のバージョンは、バージョン 1.11.170 です。
   * 機能パックはバージョン 1.12.xxx になります。

>[!NOTE]
>
>コミュニティのリリースを常に最新に保つことをお勧めします。
>
>最新バージョンを確認するには、[最新リリース](deploy-communities.md#latest-releases)の節を参照してください。

## Maven 依存関係の例 {#maven-dependency-example}

Uber API jar より前に Communities API jar を指定する必要があります。

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
