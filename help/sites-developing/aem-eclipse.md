---
title: AEM Developer Tools for Eclipse
description: AEM Developer Tools for Eclipse
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
exl-id: 00473769-c447-4966-a71e-117c669e0151
source-git-commit: 4fd5e9a1bc603202ee52e85a1c09125b13cec315
workflow-type: ht
source-wordcount: '788'
ht-degree: 100%

---

# AEM Developer Tools for Eclipse {#aem-developer-tools-for-eclipse}

![AEM Developer Tools for Eclipse 用の円形の画像モチーフ。](do-not-localize/chlimage_1-9.png)

## 概要 {#overview}

AEM Developer Tools は、Apache License 2 に従ってリリースされた [Apache Sling 向け Eclipse プラグイン](https://sling.apache.org/documentation/development/ide-tooling.html) をベースとする Eclipse プラグインです。

このツールは、AEM 開発を容易にする次のような機能を提供します。

* Eclipse Server Connector による AEM インスタンスとのシームレスな統合。
* コンテンツと OSGI バンドルの同期。
* コードのホットスワップ機能を備えたデバッグサポート。
* 固有のプロジェクト作成ウィザードからの AEM プロジェクトの簡単なブートストラップ
* JCR プロパティの容易な編集。

## 要件 {#requirements}

AEM Developer Tools を使用する前に、以下の手順を実行します。

* [Eclipse IDE for Java™ EE Developers](https://www.eclipse.org/downloads/packages/release/luna/r/eclipse-ide-java-ee-developers) をダウンロードしてインストールします。AEM Developer Tools は現在、Eclipse Kepler 以降をサポートします。

* AEM バージョン 5.6.1 以降で使用できます。
* [Eclipse に関する FAQ](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F) の説明に従って、`eclipse.ini` 設定ファイルを編集し、ヒープメモリが 1 GB 以上になるように Eclipse を設定します。

>[!NOTE]
>
>macOS では、**Eclipse.app** を右クリックし、「**パッケージの内容を表示**」を選択して、`eclipse.ini` を探します。

## AEM Developer Tools for Eclipse のインストール方法 {#how-to-install-the-aem-developer-tools-for-eclipse}

前述の[要件](#requirements)を満たしたら、次の手順でプラグインをインストールできます。

1. **AEM Developer Tools** の web サイト（`https://eclipse.adobe.com/aem/dev-tools/`）を参照します。

1. **インストール用リンク**&#x200B;をコピーします。

   または、インストール用リンクを使用する代わりにアーカイブをダウンロードできます。この方法ではオフラインインストールが可能ですが、自動アップデート通知は受け取れません。

1. Eclipse で、**ヘルプ**&#x200B;メニューを開きます。
1. 「**Install New Software**」をクリックします。
1. 「**Add...**」をクリックします。
1. 「**Name**」に「AEM Developer Tools」と入力します。
1. 「**Location**」にインストール用 URL をコピーします。
1. 「**OK**」をクリックします。
1. 「**AEM**」プラグインと「**Sling**」プラグインの両方をオンにします。
1. 「**Next**」をクリックします。
1. 「**次へ**」をクリックします。
1. 使用許諾契約書に同意し、「**Finish**」をクリックします。
1. 「**Yes**」をクリックして、Eclipse を再起動します。

## 既存プロジェクトの読み込み方法 {#how-to-import-existing-projects}

>[!NOTE]
>
>[AEM からダウンロードした際に Eclipse でバンドルを操作する方法](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407)を参照してください。

## AEM パースペクティブ {#the-aem-perspective}

AEM Development Tools for Eclipse には、AEM プロジェクトおよびインスタンスを完全にコントロールできるパースペクティブが同梱されています。

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## サンプルのマルチモジュールプロジェクト {#sample-multi-module-project}

AEM Developer Tools には、Eclipse でのプロジェクト設定を素早く習得できる、サンプルのマルチモジュールプロジェクトが付属しています。また、AEM のいくつかの機能のベストプラクティスガイドとしても役立ちます。プロジェクトのアーキタイプについて詳しくは、[こちら](https://github.com/adobe/aem-project-archetype)を参照してください。

サンプルプロジェクトを作成するには、次の手順を実行します。

1. **File**／**New**／**Project** メニューで、「**AEM**」セクションを参照して、「**AEM Sample Multi-Module Project**」を選択します。

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 「**次へ**」をクリックします。

   >[!NOTE]
   >
   >m2eclipse がアーキタイプカタログをスキャンする必要があるので、この手順にはしばらく時間がかかることがあります。

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. メニューから「**com.adobe.granite.archetypes：sample-project-archetype：（最も大きい数字）**」を選択して、「**次へ**」をクリックします。

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. サンプルプロジェクトの&#x200B;**名前**、**グループ ID** および&#x200B;**アーティファクト ID** を入力します。いくつかの高度なプロパティを設定することもできます。

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. 次に、Eclipse の接続先となる AEM サーバーを設定します。

   デバッガー機能を使用するには、AEM をデバッグモードで起動します。コマンドラインに以下を追加するなどして、デバッグモードで起動できます。

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. 「**終了**」をクリックします。プロジェクト構造が作成されます。

   >[!NOTE]
   >
   >新規インストールでは（より具体的には、Maven の依存関係をダウンロードしたことがない場合は）、プロジェクトを作成するとエラーが表示されることがあります。その場合は、[無効なプロジェクト定義の解決](#resolving-invalid-project-definition)で説明されている手順に従ってください。

## トラブルシューティング {#troubleshooting}

### 無効なプロジェクト定義の解決 {#resolving-invalid-project-definition}

無効な依存関係およびプロジェクト定義を解決するには、次の手順を実行します。

1. 作成したプロジェクトをすべて選択します。
1. 右クリックします。**Maven** メニューで「**Update Projects**」を選択します。
1. 「**スナップショット／リリースの強制更新**」をオンにします。
1. 「**OK**」をクリックします。Eclipse は必要な依存関係のダウンロードを試みます。

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

AEM のデプロイメントに適したバージョンを追加してください。

## 詳細情報 {#more-information}

Apache Sling IDE tooling for Eclipse の公式 web サイトでは、次の有益な情報を参照できます。

* [**Apache Sling IDE tooling for Eclipse** ユーザーガイド](https://sling.apache.org/documentation/development/ide-tooling.html)。このドキュメントでは、全体のコンセプト、AEM Development Tools がサポートするサーバー統合およびデプロイメント機能について説明します。
* [トラブルシューティング情報](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)
* [既知の問題リスト](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)

次の公式の [Eclipse](https://www.eclipse.org/) ドキュメントは、環境の設定に役立ちます。

* [Eclipse 使用の手引き](https://eclipseide.org/getting-started/)
* [Eclipse Luna ヘルプシステム](https://help.eclipse.org/latest/index.jsp)
* [Maven 統合（m2eclipse）](https://www.eclipse.org/m2e/)
