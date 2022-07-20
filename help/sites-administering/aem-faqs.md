---
title: AEM FAQ
seo-title: AEM 6.4 frequently asked questions
description: AEM の一般的なワークフローの理解と設定、または AEM で発生する一般的な問題のトラブルシューティングに役立つ FAQ です。
seo-description: Use these FAQs to understand, configure, and troubleshoot common workflows or issues in AEM.
uuid: 17d34923-f1ce-463b-8e9d-a713edcce51b
contentOwner: jsyal
discoiquuid: a3bb5695-6593-413d-9c2f-4c164e663b15
docset: aem65
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
source-git-commit: 68c36d4e3a14567a4d115ee64a4474bcaf9aa386
workflow-type: ht
source-wordcount: '1096'
ht-degree: 100%

---

# AEM FAQ {#aem-faqs}

AEM でのトラブルシューティングと設定に関するいくつかの問題の解決方法を説明します。

## Sites {#sites}

### バイナリレスディストリビューションの設定方法を教えてください。 {#how-do-i-configure-binary-less-distribution}

バイナリレスディストリビューションは、共有データストアにわたる開発でサポートされ、Vault ベースのディストリビューションパッケージエクスポーター（ファクトリ PID：`org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`）パッケージビルダーを活用するエージェントが関係します。

バイナリレスモードを有効にすると、ディストリビュートされたコンテンツパッケージに、実際のバイナリではなく、バイナリへの参照が含まれます。

#### バイナリレスディストリビューションを有効にする方法を教えてください。 {#how-do-i-enable-binary-less-distribution}

バイナリレスディストリビューションを有効にするには、共有 BLOB ストアと共にデプロイします。エージェントが使用しているファクトリ PID（`org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*）* を含む OSGI 設定の `useBinaryReferences` プロパティを確認します。

#### AEM Sites コンソールでページ階層を移動する際のエラーメッセージのカスタマイズ方法を教えてください。 {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

（Chrome ブラウザーの）Network パネルの個人設定を確認します（JS は縮小されていません）。

`Initiator` 列を表示して、リクエストのイニシエーターを判別します。AJAX 呼び出しがおこなわれたファイルおよび行番号がわかります。次に、エラー処理関数をトレースし、要件に応じてエラーメッセージを変更できます。

#### 言語コピーを作成する際に AEM で Content-Authors の権限を有効にする方法を教えてください。 {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

言語コピー機能を作成するには、content-authors が `/content/projects` の場所に対する権限を持つ必要があります。

プロジェクトの作成者が管理もおこなう場合は、回避策として、その作成者を `project-administrators` グループに追加します。

#### プロジェクトの言語コピーを作成する際に形式を変更する方法を教えてください。 {#how-to-change-the-format-while-creating-language-copy-for-a-project}

翻訳プロジェクトを作成する前に、ルート内部に言語ルートおよび言語コピーを作成します。

例えば、`/content/geometrixx` に `fr_LU` という名前（タイトルは French (Luxembourg) とする）で言語ルートを作成します。次に、参照パネルからページの言語コピーを作成し、`Create & Translate` 内の `Create structure only` オプションに移動します。最後に、翻訳プロジェクトを作成し、言語コピーを翻訳ジョブに追加します。

詳しくは、次の追加リソースを参照してください。

* [翻訳するコンテンツの準備](/help/sites-administering/tc-prep.md)
* [翻訳プロジェクトの管理](/help/sites-administering/tc-manage.md)

#### ログイン試行や ACL／権限の変更といった AEM の機能を監査する方法を教えてください。 {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

トラブルシューティングと監査の質を高めるために、管理に関係する変更を記録する機能が追加されました。デフォルトでは、`error.log` ファイルに情報が記録されます。監視を容易にするために、この情報を別のログファイルにリダイレクトすることをお勧めします。出力を別のログファイルにリダイレクトする方法については、[AEM でのユーザー管理操作を監査する方法](/help/sites-administering/audit-user-management-operations.md)を参照してください。

#### デフォルトの SSL を有効にする方法を教えてください。 {#how-to-enable-ssl-by-default}

Adobe Experience Manager（AEM）6.4 には SSL ウィザードが付属し、Jetty および Granite Jetty SSL のサポートを設定するユーザーインターフェイスが備わっています。

デフォルトの SSL を有効にする方法については、[デフォルトの SSL](/help/sites-administering/ssl-by-default.md) を参照してください。

#### AEM のコンテンツサービスをモバイルアプリから使用する場合に推奨されるアーキテクチャは何ですか。理想的には React Native ですか。 {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

AEM のコンテンツサービスは Sling Model に基づきます。AEM デベロッパーは、書き出される各コンポーネントに Sling Model pojo を提供する必要があります。

AEM コンテンツサービスを React アプリケーションから使用する方法については、[AEM コンテンツサービスの使用準備](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)のチュートリアルを参照してください。

また、デベロッパーがコンポーネントのツリーを書き出す場合は、`ComponentExporter` および `ContainerExporter` インターフェイスを実装し、`ModelFactory` を使用して子コンポーネントに対して反復処理を行ってモデル表現を返すこともできます。以下のリソースを参照してください。

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling :: Sling Models](https://sling.apache.org/documentation/bundles/models.html)

#### AEM 6.4 のサーベイポップアップを無効にする方法を教えてください。 {#how-to-disable-aem-survey-pop-up}

使用状況に関する統計情報の収集をオプトインするには、タッチ UI または Web コンソールを使用します。詳しくは、[集計した使用状況の統計の収集をオプトインする方法](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)を参照してください。

#### AEM 6.4 にアップグレードするための主な機能を説明しているリソースを教えてください。 {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

[AEM をアップグレードする理由について](https://helpx.adobe.com/jp/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html)を参考にしてください。これは、Adobe Experience Manager の最新バージョンへのアップグレードを検討しているお客様向けの主要機能の概要を説明しています。

## Assets {#assets}

### MP4 ファイルのアップロード時に、Assets ワークフローが繰り返されるのはなぜですか（例えば、ドラッグ＆ドロップの使用）。 {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

ムービーファイルをアップロードするユーザーが asset ノード以下の削除権限を持っていない場合、削除チャンクノードは失敗し、アップロードが再開します。

#### 言語コピーを作成する際の OOTB 設定のデフォルト設定を教えてください。 {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

一方で、タッチ UI を利用して言語コピーを作成するときは（**参照**／**言語コピーを更新**）、新しい DAM フォルダーが新しい言語下に作成され、アセットはそのフォルダーから参照されます。

これは OOTB 設定のデフォルト設定です。翻訳設定で「**ページのアセットを翻訳**」を「**翻訳しない**」に設定できます。AEM 6.4 の場合は、**ツール**／**クラウドサービス**／**翻訳クラウドサービス**&#x200B;を選択して設定します。

#### AEM SegmentStore（AEM 6.3.1.1）の急増を引き起こす AEM コンポーネントを無効にする方法を教えてください。 {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

OSGi Component Disabler を無効にできます。このサービスの使用方法については、[OSGi Component Disabler](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html) を参照してください。

回避策として、AEM が再開するたびに、UI または `curl` コマンド（以下の例を参照）を使用して、このコンポーネントを手動で無効にすることもできます。

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### アドミンコンソールをカスタマイズする方法を教えてください。 {#how-to-customize-admin-consoles}

AEM には、オーサーインスタンスのコンソールおよびページオーサリング機能をカスタマイズできる様々な仕組みが用意されています。カスタムコンソールの作成する方法、およびコンソールのデフォルトビューのカスタマイズ方法については、[コンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md)を参照してください。

#### CoralUI 2 と CoralUI 3 ベースのコンポーネントの違いを教えてください。 {#what-is-the-difference-between-coralui-and-coralui-based-components}

Granite UI Foundation の Sling コンポーネントの新しいセットが Coral3 用に作成され、[/libs/granite/ui/components/coral/foundation にあります。](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html)CoralUI 2 ベースのコンポーネント用と CoralUI 3 ベースのコンポーネント用のセットが1 つずつあります。新しいセットは、古いセットをただコピーして貼り付けたものではなく、（合理化、廃止予定の機能を削除するなど）クリーンアップしたものです。そのため、ページは CoralUI 3 ベースまたは CoralUI 2 ベースのいずれかのセットのみを使用することをお勧めします。

詳細については、[CoralUI 3 ベースの移行ガイド](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html)を参照してください。

#### AEM Assets の検索コンポーネントをカスタマイズする方法を教えてください。 {#how-to-customize-the-search-component-in-aem-assets}

検索ブースト／ランキングおよびその他の実装情報については、[簡易検索実装ガイド](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html)を参照してください。

簡易検索の実装は、2017 Summit lab AEM Search Demystified の資料です。

#### 顧客が Adobe アセットピッカーにアクセスして画像を選択できるように、WordPress 用のプラグインを作成することは可能ですか。 {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

はい、WordPress を使用しているお客様は、Adobe アセットピッカーを使用して AEM Assets サーバーから画像を選択し、WordPress サイトの投稿に追加できます。

詳細については、[アセットセレクター](../assets/search-assets.md#assetpicker)を参照してください。
