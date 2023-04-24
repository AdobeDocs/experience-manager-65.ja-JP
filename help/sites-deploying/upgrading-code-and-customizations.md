---
title: コードのアップグレードとカスタマイズ
seo-title: Upgrading Code and Customizations
description: AEMでのカスタムコードのアップグレードについて詳しく説明します。
seo-description: Learn more about upgrading custom code in AEM.
uuid: dec11ef0-bf85-4e4e-80ac-dcb94cc3c256
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 59780112-6a9b-4de2-bf65-f026c8c74a31
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: a36a310d-5943-4ff5-8ba9-50eaedda98c5
source-git-commit: a296e459461973fc2dbd0641c6fdda1d89d8d524
workflow-type: tm+mt
source-wordcount: '2115'
ht-degree: 20%

---

# コードのアップグレードとカスタマイズ{#upgrading-code-and-customizations}

アップグレードを計画する際は、実装の次の領域を調べ、対処する必要があります。

* [コードベースのアップグレード](#upgrade-code-base)
* [6.5 のリポジトリ構造への準拠](#align-repository-structure)
* [AEM のカスタマイズ](#aem-customizations)
* [手順のテスト](#testing-procedure)

## 概要 {#overview}

1. **パターン検出**  — アップグレード計画で説明されているとおりにパターン検出を実行し、詳細は [このページ](/help/sites-deploying/pattern-detector.md). Target バージョンのAEMで使用できない API/バンドルに加えて対処する必要がある領域の詳細を含む、パターン検出レポートが表示されます。 パターン検出レポートに、コード内の非互換性が示されます。 存在しない場合は、デプロイメントは既に 6.5 と互換性があります。 6.5 の機能を使用するために新しい開発を行うこともできますが、互換性を維持するためだけに必要なわけではありません。 互換性が報告されない場合は、互換モードで実行を選択し、新しい 6.5 機能または互換性に対する開発を遅らせることができます。 または、アップグレード後に開発を行うことにし、手順 2 に進むこともできます。 詳しくは、 [AEM 6.5 の後方互換性](/help/sites-deploying/backward-compatibility.md) を参照してください。

1. **6.5 のコードベースの開発** - Target バージョンのコードベース専用のブランチまたはリポジトリを作成します。アップグレード前の互換性の情報を使用して、更新するコードの領域を計画します。
1. **6.5 Uber jar でコンパイル** - 6.5 uber jar を指すようにコードベース POM を更新し、それに対してコードをコンパイルします。
1. **AEM カスタマイズの更新*** - *AEM のカスタマイズまたは拡張を更新して、6.5 で機能することを検証し、6.5 コードベースに追加する必要があります。UI 検索フォーム、Assets のカスタマイズ、/mnt/overlay を使用するすべてのものを含みます。

1. **6.5 環境へのデプロイ** - AEM 6.5 のクリーンなインスタンス（オーサー + パブリッシュ）を開発環境と QA 環境で立ち上げる必要があります。更新したコードベースと、現在の実稼動環境にある代表的なコンテンツのサンプルをデプロイする必要があります。
1. **QA 検証とバグ修正** - QA では、6.5 のオーサーインスタンスとパブリッシュインスタンスの両方でアプリケーションを検証する必要があります。検出されたすべてのバグを修正して、6.5 コードベースにコミットする必要があります。必要に応じて、すべてのバグが修正されるまで、Dev-Cycle を繰り返します。

アップグレードを続行する前に、AEMのターゲットバージョンに対して完全にテストされた、安定したアプリケーションコードベースが必要です。 テストでの観察に基づいて、カスタムコードを最適化する方法が存在する場合があります。 例えば、リポジトリの走査、検索を最適化するためのカスタムインデックス作成、JCR での順序なしノードの使用などを避けるために、コードのリファクタリングを含めることができます。

新しいAEMバージョンで動作するようにコードベースとカスタマイズをオプションでアップグレードする以外に、 6.5 は、 [このページ](/help/sites-deploying/backward-compatibility.md).

上記および下の図に示すように、 [パターン検出](/help/sites-deploying/pattern-detector.md) 最初の手順では、アップグレードの全体的な複雑さを評価できます。 また、互換性モードで実行するか、カスタマイズを更新してAEM 6.5 のすべての新機能を使用するかを決定する際にも役立ちます。 詳しくは、 [AEM 6.5 の後方互換性](/help/sites-deploying/backward-compatibility.md) ページを参照してください。
[ ![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## コードベースのアップグレード {#upgrade-code-base}

### バージョン管理での 6.5 コード用の専用ブランチの作成 {#create-a-dedicated-branch-for-6.5-code-in-version-control}

AEMの実装に必要なすべてのコードと設定は、何らかの形式のバージョン管理を使用して管理する必要があります。 バージョン管理の専用のブランチを作成して、AEMのターゲットバージョンのコードベースに必要な変更を管理する必要があります。 AEMのターゲットバージョンに対するコードベースの反復テストと、それ以降のバグ修正は、このブランチで管理されます。

### AEM Uber Jar バージョンの更新 {#update-the-aem-uber-jar-version}

AEM Uber Jar では、すべての AEM API を単一の依存関係として Maven プロジェクトの `pom.xml` に含めます。AEM API の依存関係を個々に含めるのではなく、Uber Jar を単一の依存関係として含めることが常にベストプラクティスです。 コードベースをアップグレードする場合、AEMのターゲットバージョンを指すように Uber Jar のバージョンを変更します。 Uber Jar が存在する前のバージョンのAEMでプロジェクトが開発された場合は、個々のAEM API の依存関係をすべて削除します。 AEMのターゲットバージョン用の Uber Jar を 1 つ含めて置き換えます。 新しいバージョンの Uber Jar に対してコードベースを再コンパイルします。 AEMのターゲットバージョンと互換性があるように、非推奨の API またはメソッドを更新します。

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### 管理リソースリゾルバーの使用を停止します {#phase-out-use-of-administrative-resource-resolver}

を通じた管理セッションの使用 `SlingRepository.loginAdministrative()` および `ResourceResolverFactory.getAdministrativeResourceResolver()` は、AEM 6.0 より前のコードベースで広く使用されていました。これらのメソッドは、アクセスのレベルが広すぎるので、セキュリティ上の理由から非推奨（廃止予定）となっています。 [今後のバージョンの Sling では、これらのメソッドは削除されます](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). 代わりに Service Users を使用するコードをリファクタリングすることを強くお勧めします。 サービスユーザーおよび [管理セッションを段階的に廃止する方法は、こちらを参照してください。](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions).

### クエリと Oak インデックス {#queries-and-oak-indexes}

コードベースでのクエリの使用は、コードベースのアップグレードの一環として、完全にテストする必要があります。 Jackrabbit 2(6.0 より前のバージョンのAEM) からアップグレードするお客様にとって、このテストは特に重要です。Oak はコンテンツを自動的にインデックス化せず、カスタムインデックスを作成する必要があるからです。 AEM 6.x バージョンからアップグレードする場合、標準提供の Oak インデックス定義が変更され、既存のクエリに影響を与える可能性があります。

クエリのパフォーマンスを分析および検査するには、次のツールを使用できます。

* [AEM インデックスツール](/help/sites-deploying/queries-and-indexing.md)

* [運用診断ツール - クエリパフォーマンス](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

<!-- URL is 404 as of 04/24/23; commenting out * [Oak Utils](https://oakutils.appspot.com/). This is an open source tool that is not maintained by Adobe. -->

### クラシック UI オーサリング {#classic-ui-authoring}

クラシック UI のオーサリングは、AEM 6.5 で引き続き利用できますが、非推奨（廃止予定）となっています。 詳細はこちらをご覧ください [ここ](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release). アプリケーションがクラシック UI オーサー環境で実行されている場合は、AEM 6.5 にアップグレードして、引き続きクラシック UI を使用することをお勧めします。 その後、複数の開発サイクルにわたって完了するために、タッチ UI への移行を個別のプロジェクトとして計画できます。 AEM 6.5 でクラシック UI を使用するには、複数の OSGi 設定をコードベースにコミットする必要があります。 設定の実行方法の詳細については、を参照してください。 [ここ](/help/sites-administering/enable-classic-ui.md).

## 6.5 のリポジトリ構造との整合 {#align-repository-structure}

アップグレードを容易にし、アップグレード中に設定が上書きされることを防ぐため、6.4 ではリポジトリの構造が見直され、コンテンツと設定が分離されました。

したがって、複数の設定を移動して、の配下にないようにする必要があります。 `/etc` 過去の事件と同じように AEM 6.4 への更新で確認および対応が必要な、リポジトリの再構築に関する懸念の完全なセットを確認するには、 [AEM 6.4 におけるリポジトリの再構築](/help/sites-deploying/repository-restructuring.md).

## AEM のカスタマイズ  {#aem-customizations}

AEMのソースバージョンでAEMオーサリング環境をカスタマイズしている場合は、すべて識別する必要があります。 特定されたら、各カスタマイズをバージョン管理または少なくともコンテンツパッケージの一部としてバックアップすることをお勧めします。 すべてのカスタマイズは、実稼動環境のアップグレード前に、対象バージョンのAEMを実行する QA またはステージング環境でデプロイおよび検証する必要があります。

### 一般的なオーバーレイ {#overlays-in-general}

/libs の下のノードやファイルを/apps の下の追加のノードでオーバーレイすることで、標準の機能でAEMを拡張するのが一般的な方法です。 これらのオーバーレイは、バージョン管理で追跡し、AEMのターゲットバージョンに対してテストする必要があります。 ファイル（JS、JSP、HTL など）がオーバーレイされている場合、AEMのターゲットバージョンでの回帰テストを容易にするために、拡張された機能についてコメントを残すことをAdobeがお勧めします。 一般的なオーバーレイについて詳しくは、 [ここ](/help/sites-developing/overlays.md). 特定のAEMオーバーレイの手順については、以下を参照してください。

### カスタム検索フォームのアップグレード  {#upgrading-custom-search-forms}

カスタム検索ファセットを正しく機能させるには、アップグレード後に手動で調整する必要があります。 詳しくは、[カスタム検索フォームのアップグレード](/help/sites-deploying/upgrading-custom-search-forms.md)を参照してください。

### Assets UI のカスタマイズ {#assets-ui-customizations}

>[!NOTE]
>
>この手順は、AEM 6.2 より前のバージョンからのアップグレードに対してのみ必要です。

Assets デプロイメントをカスタマイズしたインスタンスをアップグレードする準備をしておく必要があります。 このアクションは、カスタマイズされたすべてのコンテンツが新しい 6.4 ノード構造と互換性を持つようにするために必要です。

Assets UI のカスタマイズを準備するには、次の手順を実行します。

1. アップグレードしようとしているインスタンスで、次の場所に移動してCRXDE Liteを開きます： *https://server:port/crx/de/index.jsp*

1. 次のノードに移動します。

   * `/apps/dam/content`

1. コンテンツノードの名前をに変更します。 **content_backup** ウィンドウの左側にあるエクスプローラペインを右クリックし、を選択します。 **名前を変更**.

1. ノードの名前を変更したら、以下に content という名前のノードを作成します。 `/apps/dam` 名前付き **コンテンツ** ノードタイプをに設定します。 **sling:Folder**.

1. のすべての子ノードを移動 **content_backup** 新しく作成されたコンテンツノードに移動するには、エクスプローラーペインで各子ノードを右クリックし、「 」を選択します。 **移動**.

1. を削除します。 **content_backup** ノード。

1. `/apps/dam` の下にある、正しいノードタイプ `sling:Folder` で更新されたノードは、理想的にはバージョン管理に保存してコードベースでデプロイするか、少なくともコンテンツパッケージとしてバックアップする必要があります。

### 既存アセットのアセット ID の生成 {#generating-asset-ids-for-existing-assets}

既存のアセットのアセット ID を生成するには、AEMインスタンスをアップグレードしてAEM 6.5 を実行する際に、アセットをアップグレードします。この手順は、 [アセットインサイト機能](/help/assets/asset-insights.md). 詳しくは、[埋め込みコードの追加](/help/assets/use-page-tracker.md#add-embed-code)を参照してください。

アセットをアップグレードするには、JMX コンソールで Associate Asset IDs パッケージを設定します。リポジトリ内のアセットの数によっては、`migrateAllAssets` に長い時間がかかることがあります。Adobeの内部テストでは、TarMK 上の125000アセットについて約 1 時間を見積もります。

![1487758945977](assets/1487758945977.png)

アセット全体のサブセットに対してアセット ID が必要な場合は、`migrateAssetsAtPath` API を使用します。

その他すべての目的には、`migrateAllAssets()` API を使用してください。

### InDesign スクリプトのカスタマイズ {#indesign-script-customizations}

Adobe では、カスタムスクリプトを `/apps/settings/dam/indesign/scripts` に配置することを推奨しています。InDesignスクリプトのカスタマイズの詳細については、を参照してください。 [ここ](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### ContextHub 設定の復元 {#recovering-contexthub-configurations}

ContextHub 設定は、アップグレードの影響を受けます。既存の ContextHub 設定の復元方法については、[こちら](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading)を参照してください。

### ワークフローのカスタマイズ {#workflow-customizations}

不要な機能を追加または削除するのは、標準のワークフローを編集する一般的な方法です。 カスタマイズ対象として一般的なワークフローは、[!UICONTROL DAM アセットの更新]ワークフローです。カスタム実装に必要なすべてのワークフローは、アップグレード中に上書きされる可能性があるので、バックアップしてバージョン管理に保存する必要があります。

### 編集可能なテンプレート {#editable-templates}

>[!NOTE]
>
>この手順は、AEM 6.2 の編集可能テンプレートを使用した Sites のアップグレードでのみ必要です。

編集可能テンプレートの構造は、AEM 6.2 と 6.3 の間で変更されました。6.2 以前からアップグレードする場合や、編集可能テンプレートを使用してサイトコンテンツを構築する場合は、 [レスポンシブノードのクリーンアップツール](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration). このツールは実行するためのものです **後** コンテンツをクリーンアップするためのアップグレード。 オーサー層とパブリッシュ層の両方で実行します。

### CUG 実装の変更 {#cug-implementation-changes}

閉じられたユーザーグループの実装は、以前のバージョンのAEMでのパフォーマンスと拡張性の制限に対処するために、大幅に変更されました。 CUG の以前のバージョンは 6.3 で廃止され、新しい実装はタッチ UI でのみサポートされます。 6.2 以前からアップグレードする場合は、新しい CUG 実装に移行する手順を確認できます [ここ](/help/sites-administering/closed-user-groups.md#upgradetoaem63).

## 手順のテスト {#testing-procedure}

アップグレードのテストに関しては、包括的なテスト計画を準備する必要があります。 アップグレードされたコードベースとアプリケーションのテストは、まず低レベルの環境でおこなう必要があります。 見つかったバグは、コードベースが安定するまで繰り返し修正する必要があります。その後、上位レベルの環境をアップグレードする必要があります。

### アップグレード手順のテスト {#testing-the-upgrade-procedure}

ここで説明するアップグレード手順は、カスタマイズした実行マニュアルに記載されているように、開発環境および QA 環境でテストする必要があります ( [アップグレードの計画](/help/sites-deploying/upgrade-planning.md)) をクリックします。 アップグレード手順は、すべての手順がアップグレード実行のマニュアルに記載され、アップグレードプロセスがスムーズになるまで繰り返す必要があります。

### 実装テスト領域  {#implementation-test-areas-}

環境をアップグレードし、アップグレードされたコードベースをデプロイした後に、テスト計画で対象とするAEM実装の重要な領域を次に示します。

<table>
 <tbody>
  <tr>
   <td><strong>機能テスト領域</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>公開済みサイト</td>
   <td>パブリッシュ層でのAEM実装および関連するコードのテスト<br /> Dispatcher を使用する。 ページ更新の条件と<br /> キャッシュの無効化。</td>
  </tr>
  <tr>
   <td>オーサリング</td>
   <td>AEMの実装と関連するコードをオーサー層でテストする。 ページ、コンポーネントオーサリング、ダイアログを含める必要があります。</td>
  </tr>
  <tr>
   <td>Experience Cloudソリューションとの統合</td>
   <td>Analytics、DTM、Target などの製品との統合の検証。</td>
  </tr>
  <tr>
   <td>サードパーティシステムとの統合</td>
   <td>オーサー層とパブリッシュ層の両方で、サードパーティ統合を検証します。</td>
  </tr>
  <tr>
   <td>認証、セキュリティ、権限</td>
   <td>LDAP/SAML などの認証メカニズムを検証する必要があります。<br /> 権限とグループは、オーサーとパブリッシュの両方でテストする必要があります<br /> 層。</td>
  </tr>
  <tr>
   <td>クエリ</td>
   <td>カスタムインデックスとクエリは、クエリパフォーマンスと共にテストする必要があります。</td>
  </tr>
  <tr>
   <td>UI のカスタマイズ</td>
   <td>オーサー環境でのAEM UI の拡張またはカスタマイズ。</td>
  </tr>
  <tr>
   <td>ワークフロー</td>
   <td>カスタムおよび/または標準搭載のワークフローと機能。</td>
  </tr>
  <tr>
   <td>パフォーマンステスト</td>
   <td>ロードテストは、実際のシナリオをシミュレートするオーサー層とパブリッシュ層の両方で実行する必要があります。</td>
  </tr>
 </tbody>
</table>

### テスト計画と結果の文書化 {#document-test-plan-and-results}

上記の実装テスト領域をカバーするテスト計画を作成する必要があります。 多くの場合、テスト計画を作成者タスクリストと発行タスクリストで区切ると効果的です。 このテスト計画は、実稼動環境をアップグレードする前に、開発環境、QA 環境、ステージ環境で実行する必要があります。 ステージ環境と実稼動環境をアップグレードする際に比較をおこなうために、低レベルの環境でテスト結果とパフォーマンス指標を取り込む必要があります。
