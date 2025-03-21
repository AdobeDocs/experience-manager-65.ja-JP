---
title: アップグレード後のチェックおよびトラブルシューティング
description: アップグレード後に発生する可能性がある問題のトラブルシューティング方法について説明します。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
docset: aem65
feature: Upgrading
exl-id: ceac2b52-6885-496d-9517-5fc7291ad070
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: ht
source-wordcount: '1798'
ht-degree: 100%

---

# アップグレード後のチェックおよびトラブルシューティング{#post-upgrade-checks-and-troubleshooting}

## アップグレード後のチェック {#post-upgrade-checks}

[インプレースアップグレード](/help/sites-deploying/in-place-upgrade.md)の後に、次のアクティビティを実行してアップグレードを完了してください。AEM を 6.5 jar で起動し、アップグレードされたコードベースがデプロイされていることを前提としています。

* [ログでアップグレードの成功を確認](#main-pars-header-290365562)

* [OSGi バンドルの確認](#main-pars-header-1637350649)

* [Oak バージョンの確認](#main-pars-header-1293049773)

* [PreUpgradeBackup フォルダーの検査](#main-pars-header-988995987)

* [ページの初期検証](#main-pars-header-20827371)
* [AEM サービスパックの適用](#main-pars-header-215142387)

* [AEM 機能の移行](#main-pars-header-1434457709)

* [スケジュールされたメンテナンス設定の確認](#main-pars-header-1552730183)

* [レプリケーションエージェントの有効化](#main-pars-header-823243751)

* [スケジュール済みカスタムジョブの有効化](#main-pars-header-244535083)

* [テスト計画の実行](#main-pars-header-1167972233)

### ログでアップグレードの成功を確認 {#verify-logs-for-upgrade-success}

**upgrade.log**

以前は、インスタンスのアップグレード後の状態を調べるには、様々なログファイル、リポジトリの一部および Launchpad を慎重に調査する必要がありました。アップグレード後のレポートを生成すると、不具合があるアップグレードを稼動前に検出できることがあります。

この機能の主な目的は、アップグレードの成功を確認するために必要な、手動による解釈や複数のエンドポイントにわたる複雑な解析ロジックの必要性を減らすことです。このソリューションは、更新の成功または確認された失敗に外部の自動処理システムが対応するための明確な情報を提供することを目的としています。

具体的には、次のことが行われます。

* アップグレードフレームワークで検出されたアップグレードエラーは、単一のアップグレードレポートで一元管理されます。
* アップグレードレポートには、手動で対応する必要がある事項が記載されています。

これに対応するために、`upgrade.log` ファイルにログを生成する方法が変更されました。

アップグレード中にエラーが発生しなかったことを示すサンプルレポートを次に示します。

![1487887443006](assets/1487887443006.png)

アップグレードプロセスでインストールされなかったバンドルを示すサンプルレポートを次に示します。

![1487887532730](assets/1487887532730.png)

**error.log**

ターゲットバージョンの jar を使用した AEM の起動時および起動後に、error.log を注意深く確認してください。すべての警告やエラーを確認する必要があります。一般に、ログの先頭で問題を探すことをお勧めします。ログの後半で発生したエラーは、実際はファイルの前の方で発生した根本原因の副次的な影響である可能性があります。エラーや警告が繰り返し発生する場合は、以下の[アップグレードによる問題の分析](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade)を参照してください。

### OSGi バンドルの確認 {#verify-osgi-bundles}

OSGi コンソール `/system/console/bundles` に移動し、開始されていないバンドルがあるかどうかを確認します。いずれかのバンドルがインストール済み状態の場合は、`error.log` を調べて根本的な問題を特定します。

### Oak バージョンの確認 {#verify-oak-version}

アップグレード後に、Oak のバージョンが **1.10.2** に更新されていることを確認する必要があります。Oak バージョンを確認するには、OSGi コンソールに移動し、Oak バンドル（Oak Core、Oak Commons、Oak Segment Tar）に関連付けられているバージョンを調べます。

### PreUpgradeBackup フォルダーの検査 {#inspect-preupgradebackup-folder}

アップグレード時に、AEM はカスタマイズのバックアップを作成して、`/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>` の下に格納しようとします。このフォルダーを CRXDE Lite で表示するには、場合によって、[CRXDE Lite を一時的に有効にする](/help/sites-administering/enabling-crxde-lite.md)必要があります。

タイムスタンプがあるフォルダーには、`mergeStatus` という名前のプロパティがあり、`COMPLETED` という値である必要があります。**to-process** フォルダーは空になっている必要があり、**overwritten** ノードはアップグレード時に上書きされたノードを示しています。leftovers ノードの下のコンテンツは、アップグレード時に安全に統合できなかったコンテンツを示します。実装が（アップグレードされたコードパッケージによってまだインストールされておらず）いずれかの子ノードに依存している場合は、それらの子ノードを手動で統合する必要があります。

ステージング環境または実稼動環境の場合は、この作業の後に CRXDE Lite を無効にします。

### ページの初期検証 {#initial-validation-of-pages}

AEM の複数のページに対して初期検証を実行します。オーサー環境をアップグレードする場合は、開始ページとようこそページ（`/aem/start.html`、`/libs/cq/core/content/welcome.html`）を開きます。オーサー環境とパブリッシュ環境の両方で、アプリケーションページをいくつか開き、正しくレンダリングされるかどうかスモークテストを行います。問題が発生した場合は、`error.log` を調べてトラブルシューティングをおこないます。

### AEM サービスパックの適用 {#apply-aem-service-packs}

関連する AEM 6.5 サービスパックがリリースされている場合は、それらをすべて適用します。

### AEM 機能の移行 {#migrate-aem-features}

AEM の一部の機能では、アップグレード後に追加の手順が必要になります。これらの機能の完全なリストと、AEM 6.5 でそれらを移行する手順については、[コードとカスタマイズのアップグレード](/help/sites-deploying/upgrading-code-and-customizations.md)のページを参照してください。

### スケジュールされたメンテナンス設定の確認 {#verify-scheduled-maintenance-configurations}

#### データストアのガベージコレクションの有効化 {#enable-data-store-garbage-collection}

ファイルデータストアを使用する場合は、データストアのガベージコレクションタスクが有効になっていて、週別メンテナンスリストに追加されていることを確認します。手順については、[リビジョンクリーンアップ](/help/sites-administering/data-store-garbage-collection.md)を参照してください。

>[!NOTE]
>
>S3 カスタムデータストアのインストール環境の場合や、共有データストアを使用する場合、この手順はお勧めしません。

#### オンラインでのリビジョンクリーンアップの有効化 {#enable-online-revision-cleanup}

MongoMK または新しい TarMK セグメント形式を使用する場合は、リビジョンクリーンアップタスクが有効になっていて、日別メンテナンスリストに追加されていることを確認します。手順については、[リビジョンクリーンアップ](/help/sites-deploying/revision-cleanup.md)を参照してください。

### テスト計画の実行 {#execute-test-plan}

[コードとカスタマイズのアップグレード](/help/sites-deploying/upgrading-code-and-customizations.md)の&#x200B;**テスト手順**&#x200B;の節で定義されているとおりに、詳細なテスト計画を実行します。

### レプリケーションエージェントの有効化 {#enable-replication-agents}

パブリッシュ環境を完全にアップグレードして検証したら、オーサー環境でレプリケーションエージェントを有効にします。エージェントがそれぞれのパブリッシュインスタンスに接続できることを確認します。イベントの順序について詳しくは、[アップグレード手順](/help/sites-deploying/upgrade-procedure.md)を参照してください。

### スケジュール済みカスタムジョブの有効化 {#enable-custom-scheduled-jobs}

この時点で、コードベースの一部としてのスケジュール済みジョブを有効にすることができます。

## アップグレードに関する問題の分析 {#analyzing-issues-with-upgrade}

この節では、AEM 6.3 へのアップグレード手順で発生する可能性のある問題のシナリオをいくつか説明します。

これらのシナリオは、アップグレードに関連する問題の根本原因を追跡するのに役立ちます。また、プロジェクトや製品に固有の問題を特定するためにも役に立ちます。

### リポジトリ移行の失敗  {#repository-migration-failing-}

CRX2 から Oak へのデータ移行は、CQ 5.4 ベースのソースインスタンスから開始されるすべてのシナリオで実現可能です。`repository.xml` の準備を含むこのドキュメントのアップグレード手順に正確に従っていることを確認し、JAAS 経由でカスタム認証を起動していないことや、移行を始める前にインスタンスに不整合がないかをチェックしてあることを確認してください。

それでも移行が失敗する場合は、`upgrade.log` を調べることで、根本原因を解明できます。未知の問題の場合は、カスタマーサポートまで報告してください。

### アップグレードが実行されない {#the-upgrade-did-not-run}

準備手順を開始する前に、まず Java™ -jar aem-quickstart.jar コマンドを使用して、必ず&#x200B;**ソース**&#x200B;インスタンスを実行します。これは、quickstart.properties ファイルを正しく生成するために必要な手順です。このファイルがないと、アップグレードはうまくいきません。あるいは、ソースインスタンスのインストールフォルダーの `crx-quickstart/conf` の下を探して、このファイルが存在するかどうかを確認します。また、アップグレードを開始するために AEM を起動する際、Java™ -jar aem-quickstart.jar コマンドを使用して実行する必要があります。起動スクリプトから起動した場合、AEM はアップグレードモードで起動しません。

### パッケージとバンドルを更新できない  {#packages-and-bundles-fail-to-update-}

アップグレード時にパッケージがインストールされなかった場合は、パッケージに含まれるバンドルも更新されません。この種の問題は、データストアの設定ミスが原因で発生します。また、この問題は、error.log で **ERROR** メッセージや **WARN** メッセージとしても出現します。このような場合はほとんど、デフォルトのログインが機能しない可能性があるので、CRXDE を直接使用して設定の問題を調べ、見つけることができます。

### 一部の AEM バンドルがアクティブな状態に切り替わらない {#some-aem-bundles-are-not-switching-to-the-active-state}

起動しないバンドルがある場合は、未解決の依存関係がないかを確認してください。

この問題が発生し、その原因がパッケージのインストールの失敗にあり、その結果、バンドルがアップグレードされない場合は、新しいバージョンとの互換性がないと見なされます。この問題のトラブルシューティング方法について詳しくは、前述の&#x200B;**パッケージとバンドルを更新できない**&#x200B;を参照してください。

また、新規 AEM 6.5 インスタンスのバンドルリストとアップグレード後のバンドルリストを比較して、アップグレードされていないバンドルを検出することをお勧めします。この比較によって、`error.log` で検索すべき問題を絞り込むことができます。

### カスタムバンドルがアクティブ状態に切り替わらない {#custom-bundles-not-switching-to-the-active-state}

カスタムバンドルがアクティブ状態に切り替わらない場合は、変更後の API を読み込んでいないコードが存在する可能性が高くなります。これは、多くの場合、未解決の依存関係につながります。

削除された API は、以前のいずれかのリリースで廃止対象としてマークされているはずです。このような廃止の注記に、コードの直接移行に関する指示が含まれている場合があります。アドビでは、バージョン番号にできるだけ意味を持たせるようにしているので、バージョンが変わるときは、互換性を破る変更が行われている可能性があります。

また、問題の原因となった変更が必要かどうかを確認し、必要でない場合は、その変更を元に戻すことをお勧めします。さらに、パッケージエクスポートのバージョンが必要以上に増えていないかを確認し、意味のある厳密なバージョン定義に従ってください。

### Platform UI の不具合 {#malfunctioning-platform-ui}

アップグレード後に特定の UI 機能が正しく動作しない場合は、まずインターフェイスのカスタムオーバーレイを確認してください。一部の構造が変更され、オーバーレイを更新する必要があるか、オーバーレイが古くなっている可能性があります。

次に、クライアントライブラリに含まれているカスタムの追加拡張にまで追跡可能な JavaScript エラーが発生していないかを確認します。AEM レイアウトの問題を引き起こしている可能性があるカスタム CSS についても、同様の確認を行います。

最後に、JavaScript では対処できない設定ミスがないかを確認します。このような場合は、通常、拡張機能が不適切に非アクティブ化されています。

### カスタムコンポーネント、テンプレートまたは UI 拡張機能の不具合 {#malfunctioning-custom-components-templates-or-ui-extensions}

通常、これらの問題の根本原因は、起動されていないバンドルやインストールされていないパッケージによる問題と同じですが、異なる点は、最初にコンポーネントを使用した時点で問題が発生することです。

問題のあるカスタムコードへの対処方法としては、まずスモークテストを実行して原因を特定します。問題を特定したら、記事のこの[リンク]の節にあるレコメンデーションを参照して、問題の修正方法を確認します。

### /etc の下にカスタマイズが存在しない {#missing-customizations-under-etc}

`/apps` と `/libs` はアップグレードで適切に処理されますが、`/etc` の下の変更はアップグレード後に `/var/upgrade/PreUpgradeBackup` から手動で復元する必要がある場合があります。手動で統合する必要があるコンテンツについては、この場所を確認してください。

### error.log と upgrade.log の分析 {#analyzing-the-error.log-and-upgrade.log}

ほとんどの状況では、ログでエラーを調べて問題の原因を突き止める必要があります。ただし、アップグレードの場合は、古いバンドルが適切にアップグレードされていない場合があるので、依存関係の問題を監視する必要もあります。

そのための最適な方法は、現在発生している問題には関係がないと思われるメッセージをすべて削除して、error.log の情報を絞り込むことです。次のように grep などのツールを使用して実行できます。

```shell
grep -v UnrelatedErrorString
```

中には、即座に内容がわからないエラーメッセージもあります。その場合は、そのエラーメッセージが発生しているコンテキストを確認すると、エラーの発生場所の理解に役立ちます。以下のように使用して、エラーを区別することができます。

* `grep -B`（エラーの前の行を追加）

または

* `grep -A`（エラーの後の行を追加）

場合によっては、エラーが警告メッセージ内にも見つかることがあります。警告の状態につながる妥当なケースも存在し、それが実際にはエラーであるかどうかをアプリケーションで常に判断できるわけではないからです。これらの警告メッセージについても必ず確認してください。

### アドビサポートのご案内 {#contacting-adobe-support}

このページのアドバイスを実行しても問題が解決しない場合は、アドビサポートに連絡してください。当該の問題に対応するサポートエンジニアができるだけ多くの情報を得られるように、アップグレード時の upgrade.log ファイルを必ず含めてください。
