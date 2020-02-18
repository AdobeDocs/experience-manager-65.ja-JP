---
title: AEM の基盤とリポジトリ
description: Adobe Experience Manager 6.3 AEM プラットフォームとリポジトリ固有のリリースノート
uuid: 70626eda-c514-44bd-9f28-ff7abdc22f53
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 66ecf4c5-6d0f-4586-880d-7d1c8a5a5614
docset: aem65
translation-type: tm+mt
source-git-commit: 4dc4a518c212555b7833ac27de02087a403d3517

---


# AEM の基盤とリポジトリ{#aem-foundation-repository}

## 変更点の一覧 {#list-of-changes}

### リポジトリ {#repository}

* Adobe Experience Manager 6.5 の基盤は、アップデートバージョンの OSGi ベースのフレームワーク（Apache Sling および Apache Felix）と Java コンテンツリポジトリの Apache Jackrabbit Oak 1.10.2 上に構築されています。
* Please see [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) and [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt) for a full overview of fixed issues.

>[!CAUTION]
>
>* AEM 6.3 以降の新しいバージョンの Oak セグメント Tar では、リポジトリを移行する必要があります。この手順は、古いバージョンの TarMK からアップグレードする場合、または別のタイプの格納機能から新しい Segment Tar に切り替える場合に必須です。新しい Segment Tar のメリットについて詳しくは、[Oak Segment Tar への移行に関する FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar) を参照してください。
>



### Java サポート {#java-support}

* 既にサポートされている Java 8 に加えて、Java 11 を新しくサポートします。
* 最適なパフォーマンスを得るには、デフォルトの GC 値を他の値に置き換えてください。詳しくは、](/help/sites-deploying/custom-standalone-install.md)インストールとアップデート[の節を参照してください。
* Java 11 および Java 8 のメンテナンスアップデートが Oracle から公開されない場合は、AEM 関連プロジェクトで使用するお客様向けにアドビが配布します。

### OSGi {#osgi}

* OSGi PromisesおよびConverterユーティリティライブラリの追加

### プロジェクトとワークフロー {#projects-and-workflows}

* 6.4 で導入された新しいワークフローモデルエディターが改善され、「コピー」や「公開」などの新しい操作、ワークフローステップでの変数のサポート、強化された OR および AND 分割が追加されました。

### 検索 {#searching}

* Oak 内の検索では動的ファセットをサポートするようになりました。例えば、アセット検索のフィルターレールに結果の予測量が表示されます。
* QueryBuilder は、動的ファセットを使用して結果を返すように拡張されました。

### セキュリティ {#security}

* 管理者ユーザーのパスワードの有効期限が追加されました。

### ユーザーインターフェイス {#user-interface}

UI に対して様々な機能強化がおこなわれ、生産性と使いやすさが向上しました。

* AEM 6.5 には、ユーザーとグループの新しい権限管理 UI が導入されています。この UI を使用すると、CRXDE に移動しなくても、すべての権限と制限を容易に表示および設定することができます。
* 列表示では、画面上に表示されるエントリのみを読み込み、それ以外のエントリはユーザーがスクロールを開始した場合にのみ読み込まれるようになりました。リストおよびカード表示では、AEM 6.0 以降、この機能が既に実装されています（AEM 6.4 で改善されました）。
* 列表示には、該当する場合、ページ／アセットのワークフローステータスが含まれるようになりました。
* 「すべてを&#39;選択」アクションを使用すると、同じフォルダー内のすべてのページ／アセットに対してアクションを手軽に実行することができます。
* 「すべてを選択」アクションは、読み込まれたページ／アセットだけでなく、すべてのページ／アセットに対してアクションを実行しようとします。バルクアクションを処理できるようにアクションがアップグレードされていない場合は、警告ダイアログが表示されます。

>[!CAUTION]
>
>* クラシック UI の機能がさらに強化される予定はありません。AEM 6.5 にはクラシック UI が含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用し続けることができます。Note that Classic UI remains fully supported while being deprecated [Read more](/help/sites-deploying/ui-recommendations.md).
>



### アップグレード {#upgrade}

* アップグレード手順は 6.5 でもほぼ変わりません。
* 6.4 で導入された下位互換性、アップグレードの複雑さの評価、持続可能なアップグレードの機能を引き続きサポートしています。必要に応じて、これらの分野でバージョン固有の更新がおこなわれてきました。
* パターン検出パッケージが簡素化され、利用可能なソースバージョンごとに、6.5 へのアップグレードを評価するパッケージが 1 つ用意されるようになりました。
* Please see the [Upgrade documentation](/help/sites-deploying/upgrade.md) for more details on upgrade procedure.

### Web サーバー {#web-server}

* Quickstart配布では、Eclipse Jetty 9.4.15をサーブレットエンジンとして使用します（AEM 6.4は9.3.22に付属）。

