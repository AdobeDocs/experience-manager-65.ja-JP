---
title: AEM Foundationとリポジトリ
description: Adobe Experience Managerプラットフォームおよびリポジトリのリリースノートです。
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 55%

---


# AEM Foundation and Repository {#aem-foundation-repository}

## 変更について  {#list-of-changes}

### リポジトリ {#repository}

* Adobe Experience Manager 6.5 の基盤は、アップデートバージョンの OSGi ベースのフレームワーク（Apache Sling および Apache Felix）と Java コンテンツリポジトリの Apache Jackrabbit Oak 1.10.2 上に構築されています。
* 修正された問題の概要については、[Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt)、[Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt)および[Apache Jackrabbit Oar v. 1.1.1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt)を参照してください。

>[!CAUTION]
>
>AEM 6.3 以降の新しいバージョンの Oak セグメント Tar では、リポジトリを移行する必要があります。この手順は、古いバージョンの TarMK からアップグレードする場合、または別のタイプの格納機能から新しい Segment Tar に切り替える場合に必須です。新しい Segment Tar のメリットについて詳しくは、[Oak Segment Tar への移行に関する FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar) を参照してください。

### Java サポート {#java-support}

* Java 11および既にサポートされているJava 8の新しいサポート。
* 最適なパフォーマンスを得るには、デフォルトの GC 値を他の値に置き換えてください。詳しくは、](/help/sites-deploying/custom-standalone-install.md)インストールとアップデート[の節を参照してください。
* Java 11およびJava 8のメンテナンスアップデートは、Oracleで公開されていない場合、AEM関連のプロジェクトでのお客様の利用を目的として、Adobeから配布されます。

### OSGi {#osgi}

* OSGi Promises and Converterユーティリティライブラリが追加されました。

### プロジェクトとワークフロー {#projects-and-workflows}

* 6.4で導入された新しいワークフローモデルエディターが強化され、コピーと公開、ワークフローステップでの変数のサポート、強化された`OR`分割、`AND`分割などの操作が追加されました。

### 検索 {#searching}

* Oak 内の検索では動的ファセットをサポートするようになりました。例えば、アセット検索のフィルターレールに、結果の予測量が表示されます。
* QueryBuilderが拡張され、動的ファセットを結果に提供するようになりました。

### セキュリティ {#security}

* 管理者ユーザーのパスワードの有効期限が追加されました。

### ユーザーインターフェイス {#user-interface}

UI に対して様々な機能強化がおこなわれ、生産性と使いやすさが向上しました。

* AEM 6.5 には、ユーザーとグループの新しい権限管理 UI が導入されています。この UI を使用すると、CRXDE に移動しなくても、すべての権限と制限を容易に表示および設定することができます。
* 列表示では、画面上に表示されるエントリのみを読み込み、それ以外のエントリはユーザーがスクロールを開始した場合にのみ読み込まれるようになりました。リストおよびカード表示では、AEM 6.0 以降、この機能が既に実装されています（AEM 6.4 で改善されました）。。
* 列表示に、該当する場合にページ/アセットのワークフローステータスが含まれるようになりました。
* 「すべて選択」アクションを使用すると、同じフォルダ内のすべてのページ/アセットに対して、簡単にアクションを実行できます。
* 「すべてを選択」アクションは、読み込まれたページ／アセットだけでなく、すべてのページ／アセットに対してアクションを実行しようとします。バルクアクションを処理するようにアクションをアップグレードしない場合は、警告が表示されます。

>[!CAUTION]
>
>Adobeでは、クラシックUIの機能をさらに強化することはできません。 Experience Manager6.5には、下位互換性を確保するためのクラシックUIが含まれています。 従来のUIは、非推奨の[詳細情報](/help/sites-deploying/ui-recommendations.md)を読む間も、引き続き完全にサポートされます。

### アップグレード {#upgrade}

* アップグレード手順は 6.5 でもほぼ変わりません。
* 6.4 で導入された下位互換性、アップグレードの複雑さの評価、持続可能なアップグレードの機能を引き続きサポートしています。必要に応じて、これらの分野でバージョン固有の更新がおこなわれてきました。
* パターン検出パッケージが簡素化され、利用可能なソースバージョンごとに、6.5 へのアップグレードを評価するパッケージが 1 つ用意されるようになりました。
* アップグレード手順について詳しくは、[アップグレードドキュメント](/help/sites-deploying/upgrade.md)を参照してください。

### Web サーバー {#web-server}

* Quickstart配布版では、Eclipse Jetty 9.4.15をサーブレットエンジンとして使用します(9.3.22に付属のAEM 6.4)。
