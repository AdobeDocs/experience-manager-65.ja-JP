---
title: AEM FAQ
description: これらの FAQ を使用して、AEMの一般的なワークフローや問題を理解、設定、トラブルシューティングします。
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
source-git-commit: f7bfbfab9fb9ec00304f2889735c70be924cc217
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 54%

---

# AEM FAQ {#aem-faqs}

AEMのトラブルシューティングと設定に関する問題の回答を理解します。

## Sites {#sites}

### バイナリレス配布を設定する方法を教えてください。 {#how-do-i-configure-binary-less-distribution}

バイナリレスディストリビューションは、共有データストアにわたる開発でサポートされ、Vault ベースのディストリビューションパッケージエクスポーター（ファクトリ PID：`org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`）パッケージビルダーを活用するエージェントが関係します。

バイナリレスモードを有効にした場合、配布されるコンテンツパッケージには、実際のバイナリではなくバイナリへの参照が含まれます。

#### バイナリレス配布を有効にする方法を教えてください。 {#how-do-i-enable-binary-less-distribution}

バイナリレスディストリビューションを有効にするには、共有 BLOB ストアと共にデプロイします。エージェントが使用しているファクトリ PID（`org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*）* を含む OSGI 設定の `useBinaryReferences` プロパティを確認します。

#### AEMサイトコンソールでページ階層を移動する際に、エラーメッセージをカスタマイズするにはどうすればよいですか？ {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

（Chrome ブラウザーの）ネットワークパネルで、個人用の設定（JS が縮小されていない）を確認します。

`Initiator` 列を表示して、リクエストのイニシエーターを判別します。AJAXの呼び出し元のファイルと行番号を提供します。 後で、エラー処理関数をトレースし、必要に応じてエラーメッセージを変更できます。

#### AEMで Content-Authors 用の言語コピーを作成する際に権限を有効にするにはどうすればよいですか？ {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

言語コピー機能を作成するには、content-authors が `/content/projects` の場所に対する権限を持つ必要があります。

プロジェクトの作成者が管理もおこなう場合は、回避策として、その作成者を `projects-administrators` グループに追加します。

#### プロジェクトの言語コピーを作成する際に形式を変更するにはどうすればよいですか？ {#how-to-change-the-format-while-creating-language-copy-for-a-project}

翻訳プロジェクトを作成する前に、ルート内に言語ルートと言語コピーを作成します。

例えば、`/content/geometrixx` に `fr_LU` という名前（タイトルは French (Luxembourg) とする）で言語ルートを作成します。次に、参照パネルからページの言語コピーを作成し、`Create & Translate` 内の `Create structure only` オプションに移動します。最後に、翻訳プロジェクトを作成し、言語コピーを翻訳ジョブに追加します。

詳しくは、以下のその他のリソースを参照してください。

* [翻訳するコンテンツの準備](/help/sites-administering/tc-prep.md)
* [翻訳プロジェクトの管理](/help/sites-administering/tc-manage.md)

#### ログイン試行や ACL／権限の変更といった AEM の機能を監査する方法を教えてください。 {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

トラブルシューティングと監査の質を高めるために、管理に関係する変更を記録する機能が追加されました。デフォルトでは、`error.log` ファイルに情報が記録されます。監視を容易にするために、この情報を別のログファイルにリダイレクトすることをお勧めします。出力を別のログファイルにリダイレクトする方法については、[AEM でのユーザー管理操作を監査する方法](/help/sites-administering/audit-user-management-operations.md)を参照してください。

#### デフォルトで SSL を有効にする方法は？ {#how-to-enable-ssl-by-default}

Adobe Experience Manager(AEM)6.4 には SSL ウィザードが付属し、Jetty および Granite Jetty SSL サポートを設定するためのユーザーインターフェイスが用意されています。

デフォルトで SSL を有効にするには、 [デフォルトでは SSL](/help/sites-administering/ssl-by-default.md).

#### モバイルアプリ（理想的には React Native）からAEM Content Services を使用する場合、どのようなアーキテクチャが推奨されますか？ {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

AEM のコンテンツサービスは Sling Model に基づきます。AEM デベロッパーは、書き出される各コンポーネントに Sling Model pojo を提供する必要があります。

AEM コンテンツサービスを React アプリケーションから使用する方法については、[AEM コンテンツサービスの使用準備](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)のチュートリアルを参照してください。

また、デベロッパーがコンポーネントのツリーを書き出す場合は、`ComponentExporter` および `ContainerExporter` インターフェイスを実装し、`ModelFactory` を使用して子コンポーネントに対して反復処理を行ってモデル表現を返すこともできます。以下のリソースを参照してください。

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling :: Sling Models](https://sling.apache.org/documentation/bundles/models.html)

#### AEM 6.4 の調査ポップアップを無効にする方法を教えてください。 {#how-to-disable-aem-survey-pop-up}

タッチ UI または Web コンソールを使用して、使用状況の統計の収集をオプトインできます。 詳しい手順については、 [集計された使用状況の統計の収集のオプトイン](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

#### AEM 6.4 へのアップグレードに関する主な機能を強調したリソースはありますか。 {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

[AEM をアップグレードする理由について](https://helpx.adobe.com/jp/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html)を参考にしてください。これは、Adobe Experience Manager の最新バージョンへのアップグレードを検討しているお客様向けの主要機能の概要を説明しています。

## Assets {#assets}

### MP4 ファイルのアップロード時に Assets ワークフローが繰り返されるのはなぜですか（例えば、ドラッグ&amp;ドロップの方法を使用して）? {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

ユーザーがムービーファイルのアップロードに asset ノードの削除権限を持っていない場合、削除チャンクノードは失敗し、アップロードが再開します。

#### 言語コピーを作成する際の OOTB 設定のデフォルト設定を教えてください。 {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

一方で、タッチ UI を利用して言語コピーを作成するときは（**参照**／**言語コピーを更新**）、新しい DAM フォルダーが新しい言語下に作成され、アセットはそのフォルダーから参照されます。

これは OOTB 設定のデフォルト設定です。翻訳設定で「**ページのアセットを翻訳**」を「**翻訳しない**」に設定できます。AEM 6.4 の場合は、**ツール**／**クラウドサービス**／**翻訳クラウドサービス**&#x200B;を選択して設定します。

#### AEM SegmentStore（AEM 6.3.1.1）の急増を引き起こす AEM コンポーネントを無効にする方法を教えてください。 {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

OSGi Component Disabler を無効にすることができます。 このサービスを使用するには、 [OSGi Component Disabler](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

回避策として、AEM が再開するたびに、UI または `curl` コマンド（以下の例を参照）を使用して、このコンポーネントを手動で無効にすることもできます。

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### アドミンコンソールをカスタマイズする方法を教えてください。 {#how-to-customize-admin-consoles}

AEM には、オーサーインスタンスのコンソールおよびページオーサリング機能をカスタマイズできる様々な仕組みが用意されています。カスタムコンソールを作成し、コンソールのデフォルト表示をカスタマイズする方法については、 [コンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md).

#### CoralUI 2 と CoralUI 3 ベースのコンポーネントの違いは何ですか。 {#what-is-the-difference-between-coralui-and-coralui-based-components}

Granite UI Foundation の Sling コンポーネントの新しいセットが Coral3 用に作成され、[/libs/granite/ui/components/coral/foundation にあります。](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) CoralUI 2 ベースのコンポーネント用のセットと、CoralUI 3 ベースのコンポーネント用のセットが 1 つあります。 新しいセットは、古いセットのコピー&amp;ペーストではなく、クリーンアップされます（例えば、廃止された機能の整理、削除）。 そのため、ページでは、CoralUI 3 ベースまたは CoralUI 2 ベースのセットのみを使用することをお勧めします。

詳細については、[CoralUI 3 ベースの移行ガイド](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html)を参照してください。

#### AEM Assetsで検索コンポーネントをカスタマイズする方法は？ {#how-to-customize-the-search-component-in-aem-assets}

検索ブースト/ランキングおよびその他の実装情報について詳しくは、 [シンプルな検索実装ガイド](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html).

簡易検索の実装は、2017 Summit lab AEM Search Demystified の資料です。

#### 顧客がAdobeのアセットピッカーにアクセスして画像を選択できる WordPress 用のプラグインを構築することは可能ですか？ {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

はい。WordPress を使用しているお客様は、Adobeのアセットピッカーを使用して、AEM Assetsサーバーから画像を選択し、WordPress サイト上の投稿に追加できます。

参照： [アセットセレクター](../assets/search-assets.md#assetpicker) を参照してください。
