---
title: AEM Developer Tools for Eclipse
seo-title: AEM Developer Tools for Eclipse
description: 'null'
seo-description: 'null'
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 82%

---


# AEM Developer Tools for Eclipse{#aem-developer-tools-for-eclipse}

![](do-not-localize/chlimage_1-9.png)

## 概要 {#overview}

AEM Developer Tools for Eclipse は、Apache License 2 に従ってリリースされた [Apache Sling 向け Eclipse プラグイン](https://sling.apache.org/documentation/development/ide-tooling.html) をベースとする Eclipse プラグインです。

このツールは、AEM 開発を容易にする次のような機能を提供します。

* Eclipse Server Connector による AEM インスタンスとのシームレスな統合。
* コンテンツと OSGI バンドルの同期。
* コードのホットスワップ機能によるデバッグのサポート。
* 固有の Project Creation Wizard からの AEM プロジェクトのシンプルなブートストラップ。
* JCRプロパティの簡単な編集。

## 要件 {#requirements}

AEM Developer Toolsを使用する前に、次の操作を行う必要があります。

* [Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar) をダウンロードしてインストールします。AEM Developer Toolsは、現在EclipseKepler以降をサポートしています

* AEMバージョン5.6.1以降で使用可能
* Configure your eclipse installation to ensure that you have at least 1 gigabyte of heap memory by editing your `eclipse.ini` configuration file as described in the [Eclipse FAQ](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>On macOS, you need to right-click on **Eclipse.app** and then select **Show Package Contents** in order to find your `eclipse.ini`**.**

## AEM Developer Tools for Eclipse のインストール方法 {#how-to-install-the-aem-developer-tools-for-eclipse}

Once you have fulfilled the [requirements](#requirements) above, you can install the plugin as follows:

1. [**AEM** Developer Tools Web サイト](https://eclipse.adobe.com/aem/dev-tools/)にアクセスします。

1. **インストール用リンク**&#x200B;をコピーします。

   または、インストール用リンクを使用する代わりに、アーカイブをダウンロードすることもできます。この方法ではオフラインインストールが可能ですが、自動アップデート通知は受けられません。

1. Eclipse で、**Help** メニューを開きます。
1. 「**Install New Software**」をクリックします。
1. 「**Add...**」をクリックします。
1. 「**Name**」に「AEM Developer Tools」と入力します。
1. 「**Location**」にインストール用 URL をコピーします。
1. 「**OK**」をクリックします。
1. 「**AEM**」プラグインと「**Sling**」プラグインの両方をオンにします。
1. 「**次へ**」をクリックします。
1. 「**次へ**」をクリックします。
1. 使用許諾契約書に同意し、「**Finish**」をクリックします。
1. 「**Yes**」をクリックして、Eclipse を再起動します。

## 既存プロジェクトの読み込み方法 {#how-to-import-existing-projects}

>[!NOTE]
>
>See [How to work with a bundle in Eclipse when it was downloaded from AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## AEM パースペクティブ {#the-aem-perspective}

AEM Development Tools for Eclipse には、AEM プロジェクトおよびインスタンスを完全にコントロールできるパースペクティブが同梱されています。

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## サンプルのマルチモジュールプロジェクト {#sample-multi-module-project}

AEM Developer Tools for Eclipse には、サンプルのマルチモジュールプロジェクトが同梱されています。このプロジェクトは、Eclipse でのプロジェクト設定を手早くおこなうために役立つだけでなく、いくつかの AEM 機能に対するベストプラクティスガイドの役割も果たします。[プロジェクトのアーキタイプについて詳しくは、こちらを参照してください。](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype) 

次の手順を実行して、サンプルプロジェクトを作成します。

1. **File**／**New**／**Project**&#x200B;メニューで、「**AEM**」セクションを参照して、「**AEM Sample Multi-Module Project**」を選択します。

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 「**次へ**」をクリックします。

   >[!NOTE]
   >
   >m2eclipse がアーキタイプカタログをスキャンする必要があるので、この手順にはしばらくかかることがあります。

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. メニューから「**com.adobe.granite.archetypes：sample-project-archetype：（最も大きい数字）**」を選択して、「**Next**」をクリックします。

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. サンプルプロジェクトの&#x200B;**名前**、**グループ ID** および&#x200B;**アーティファクト ID** を入力します。いくつかの高度なプロパティを設定することもできます。

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. 次に、Eclipse が接続する AEM サーバーを設定します。

   デバッガー機能を使用するには、AEM をデバッグモードで起動する必要があります。コマンドラインに以下を追加するなどして、デバッグモードで起動できます。

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. 「**Finish**」をクリックします。プロジェクト構造が作成されます。

   >[!NOTE]
   >
   >新規インストールでは（より具体的には、Maven の依存関係をダウンロードしたことがない場合は）、プロジェクトを作成するとエラーが表示されることがあります。この場合は、[無効なプロジェクト定義の解決](#resolving-invalid-project-definition)で説明されている手順に従ってください。

## トラブルシューティング {#troubleshooting}

### 無効なプロジェクト定義の解決 {#resolving-invalid-project-definition}

無効な依存関係およびプロジェクト定義を解決するには、次の手順を実行します。

1. 作成したプロジェクトをすべて選択します。
1. 右クリックします。**Maven** メニューで「**Update Projects**」を選択します。
1. 「**Force Updates of Snapshot/Releases**」をオンにします。
1. 「**OK**」をクリックします。Eclipse が必要な依存関係のダウンロードを試みます。

### JSP ファイルでのタグライブラリのオートコンプリートの有効化 {#enabling-tag-library-autocompletion-in-jsp-files}

適切な依存関係がプロジェクトに追加されていれば、タグライブラリのオートコンプリートはデフォルトで機能します。必要な tld ファイルと TagExtraInfo ファイルが含まれていない AEM Uber Jar を使用する場合、既知の問題が 1 つ存在します。

この問題を回避するには、org.apache.sling.scripting.jsp.taglib アーティファクトを AEM Uber Jar より前のクラスパスに配置します。Maven プロジェクトの場合は、pom.xml 内で、Uber Jar より前に次の依存関係を配置します。

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

使用する AEM のデプロイメントに適したバージョンを追加してください。

## 詳細情報 {#more-information}

Apache Sling IDE tooling for Eclipse の公式 Web サイトでは、次の役立つ情報を参照できます。

* 『[**Apache Sling IDE tooling for Eclipse** ユーザーガイド](https://sling.apache.org/documentation/development/ide-tooling.html)』。このドキュメントは、全体のコンセプト、AEM Development Tools がサポートするサーバー統合およびデプロイメント機能について説明するものです。
* [トラブルシューティング情報](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)
* [既知の問題リスト](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)

次の公式の [Eclipse](https://eclipse.org/) ドキュメントは、環境の設定に役立ちます。

* [Eclipse 使用の手引き](https://eclipse.org/users/)
* [Eclipse Luna ヘルプシステム](https://help.eclipse.org/luna/index.jsp)
* [Maven 統合（m2eclipse）](https://www.eclipse.org/m2e/)

