---
title: AEM FAQ
seo-title: AEM 6.4 に関する一般的な質問
description: AEM の一般的なワークフローの理解と設定、または AEM で発生する一般的な問題のトラブルシューティングに役立つ FAQ です。
seo-description: AEM の一般的なワークフローの理解と設定、または AEM で発生する一般的な問題のトラブルシューティングに役立つ FAQ です。
uuid: 17d34923-f1ce-463b-8e9d-a713edcce51b
contentOwner: jsyal
discoiquuid: a3bb5695-6593-413d-9c2f-4c164e663b15
docset: aem65
translation-type: tm+mt
source-git-commit: 117208c634613559bb13556e12f094add70006e2
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 71%

---


# AEM FAQ {#aem-faqs}

AEM でのトラブルシューティングと設定に関するいくつかの問題の解決方法を説明します。

## Sites {#sites}

### バイナリレス配布の設定方法を教えてください。{#how-do-i-configure-binary-less-distribution}

バイナリレスディストリビューションは、共有データストアにわたる開発でサポートされ、Vault ベースのディストリビューションパッケージエクスポーター（ファクトリ PID：`org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`）パッケージビルダーを活用するエージェントが関係します。

バイナリレスモードを有効にすると、ディストリビュートされたコンテンツパッケージに、実際のバイナリではなく、バイナリへの参照が含まれます。

#### バイナリレスディストリビューションを有効にする方法を教えてください。  {#how-do-i-enable-binary-less-distribution}

バイナリレスディストリビューションを有効にするには、共有 BLOB ストアと共にデプロイします。OSGI設定の`useBinaryReferences`プロパティを、エージェントが使用しているファクトリのPID ( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)*&#x200B;で確認します。

#### AEMサイトコンソールでページ階層を移動中にエラーメッセージをカスタマイズする方法を教えてください。{#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

（Chrome ブラウザーの）Network パネルの個人設定を確認します（JS は縮小されていません）。

`Initiator` 列を表示して、リクエストのイニシエーターを判別します。AJAX 呼び出しがおこなわれたファイルおよび行番号がわかります。次に、エラー処理関数をトレースし、要件に応じてエラーメッセージを変更できます。

#### 言語コピーを作成する際に AEM で Content-Authors の権限を有効にする方法を教えてください。  {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

言語コピー機能を作成するには、コンテンツ作成者は`/content/projects`の場所に権限が必要です。

プロジェクトの管理も作成者に依頼する場合は、回避策として`project-administrators`グループに作成者を追加します。

#### プロジェクトの言語コピーを作成する際に形式を変更する方法{#how-to-change-the-format-while-creating-language-copy-for-a-project}

翻訳プロジェクトを作成する前に、ルート内部に言語ルートおよび言語コピーを作成します。

例えば、
`/content/geometrixx`に言語ルートを作成し、名前を`fr_LU`(タイトルはフランス語（ルクセンブルク）)にします。 次に、参照パネルからページの言語コピーを作成し、`Create & Translate`の`Create structure only`オプションに移動します。 最後に、翻訳プロジェクトを作成し、言語コピーを翻訳ジョブに追加します。

詳しくは、次の追加リソースを参照してください。

* [翻訳するコンテンツの準備](/help/sites-administering/tc-prep.md)
* [翻訳プロジェクトの管理](/help/sites-administering/tc-manage.md)

#### ログイン試行や ACL／権限の変更といった AEM の機能を監査する方法を教えてください。  {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

トラブルシューティングと監査の質を高めるために、管理に関係する変更を記録する機能が追加されました。デフォルトでは、情報は`error.log`ファイルに記録されます。 監視を容易にするために、この情報を別のログファイルにリダイレクトすることをお勧めします。出力を別のログファイルにリダイレクトする方法については、[AEM でのユーザー管理操作を監査する方法](/help/sites-administering/audit-user-management-operations.md)を参照してください。

#### デフォルトでSSLを有効にする方法を教えてください。{#how-to-enable-ssl-by-default}

Adobe Experience Manager（AEM）6.4 には SSL ウィザードが付属し、Jetty および Granite Jetty SSL のサポートを設定するユーザーインターフェイスが備わっています。

デフォルトの SSL を有効にする方法については、[デフォルトの SSL](/help/sites-administering/ssl-by-default.md) を参照してください。

#### AEM のコンテンツサービスをモバイルアプリから使用する場合に推奨されるアーキテクチャは何ですか。理想的には React Native ですか。  {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

Content ServicesはSlingモデルに基づいており、AEMの開発者は、エクスポートされる各コンポーネントに対してSlingモデルのポジションを提供する必要があります。

AEM コンテンツサービスを React アプリケーションから使用する方法については、[AEM コンテンツサービスの使用準備](https://helpx.adobe.com/jp/experience-manager/kt/sites/using/content-services-tutorial-use.html)のチュートリアルを参照してください。

また、開発者がコンポーネントのツリーを書き出したい場合は、`ComponentExporter`と`ContainerExporter`インターフェイスを実装し、`ModelFactory`を使用して子コンポーネントを反復し、モデル表現を返すこともできます。 以下のリソースを参照してください。

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2 ] [Apache Sling ::Slingモデル](https://sling.apache.org/documentation/bundles/models.html)

#### AEM 6.4調査のポップアップを無効にする方法{#how-to-disable-aem-survey-pop-up}

使用状況に関する統計情報の収集をオプトインするには、タッチ UI または Web コンソールを使用します。詳しくは、[集計した使用状況の統計の収集をオプトインする方法](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)を参照してください。

#### AEM 6.4 にアップグレードするための主な機能を説明しているリソースを教えてください。  {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

最新バージョンのAdobe Experience Managerへのアップグレードを検討しているお客様の主な機能の概要を説明した『AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html)アップグレードの理由について』を参照してください。[

## Assets {#assets}

### MP4ファイルのアップロード中にアセットワークフローが繰り返し表示されるのはなぜですか（例えば、ドラッグ&amp;ドロップを使用した場合）。{#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

ムービーファイルをアップロードするユーザーが asset ノード以下の削除権限を持っていない場合、削除チャンクノードは失敗し、アップロードが再開します。

#### AEM 6.4 で一度に操作できるデジタルアセットの最大数を教えてください。  {#what-is-the-maximum-number-of-digital-assets-that-can-be-operated-with-aem-at-a-time}

Adobe Experience Manager（AEM）6.5 では現在、一度に 2 GB のアセットをアップロードできます。

AEM 6.5 で操作できるアセットの最大数について詳しくは、[Assets サイジングガイド](/help/assets/assets-sizing-guide.md)を参照してください。

#### 言語コピーの作成時のOOTB設定のデフォルト設定は何ですか。{#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

クラシック UI を利用して言語コピーを作成するときは、Assets は新しい言語階層下に移動されるのではなく、言語マスターから使用されます。

一方で、タッチ UI を利用して言語コピーを作成するときは（**参照**／**言語コピーを更新**）、新しい DAM フォルダーが新しい言語下に作成され、アセットはそのフォルダーから参照されます。

これは OOTB 設定のデフォルト設定です。翻訳設定で「**ページのアセットを翻訳**」を「**翻訳しない**」に設定できます。AEM 6.4 の場合は、**ツール**／**クラウドサービス**／**翻訳クラウドサービス**&#x200B;を選択して設定します。

#### AEM SegmentStore(AEM 6.3.1.1)で指数的な増加を引き起こすAEMコンポーネントを無効にする方法を教えてください。{#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

OSGi Component Disabler を無効にできます。このサービスの使用方法については、[OSGi Component Disabler](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html) を参照してください。

回避策として、AEM が再開するたびに、UI または `curl` コマンド（以下の例を参照）を使用して、このコンポーネントを手動で無効にすることもできます。

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### AEM 6.5インスタンスでアセットインサイトを設定する方法{#how-to-configure-asset-insights-with-aem-instance}

Adobeアクティベーション(DTM)を介してデプロイされたExperience Managerに対してアセットインサイトを設定および設定するには、[AEM Assets](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html)でアセットインサイトを設定する方法を参照してください。

#### 管理コンソールのカスタマイズ方法{#how-to-customize-admin-consoles}

AEMには様々なメカニズムが用意されており、オーサリングインスタンスのコンソールとページオーサリング機能をカスタマイズできます。 カスタムコンソールの作成する方法、およびコンソールのデフォルトビューのカスタマイズ方法については、[コンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md)を参照してください。

#### CoralUI 2 と CoralUI 3 ベースのコンポーネントの違いを教えてください。  {#what-is-the-difference-between-coralui-and-coralui-based-components}

Granite UI FoundationのSlingコンポーネントの新しいセットがCoral3用に作成され、[/libs/granite/ui/components/coral/foundationに配置されます。](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html)CoralUI 2 ベースのコンポーネント用と CoralUI 3 ベースのコンポーネント用のセットが1 つずつあります。新しいセットは、古いセットをただコピーして貼り付けたものではなく、（合理化、廃止予定の機能を削除するなど）クリーンアップしたものです。そのため、ページは CoralUI 3 ベースまたは CoralUI 2 ベースのいずれかのセットのみを使用することをお勧めします。

詳細については、[CoralUI 3 ベースの移行ガイド](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html)を参照してください。

#### AEM Assetsの検索コンポーネントのカスタマイズ方法{#how-to-customize-the-search-component-in-aem-assets}

検索ブースト／ランキングおよびその他の実装情報については、[簡易検索実装ガイド](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html)を参照してください。

簡易検索の実装は、2017 Summit lab AEM Search Demystified の資料です。

#### AEM AssetsとAEM MediaLibraryの違いは何ですか。{#what-is-the-difference-between-aem-assets-and-aem-medialibrary}

AEM Assets は、AEM プラットフォーム上のアプリケーションです。お客様はこのアプリケーションを使用して、Web ベースのリポジトリ内でデジタルアセット（画像、ビデオ、ドキュメントおよびオーディオクリップ）を管理できますが、AEM Media Library は、画像やその他の共有リソースの保存専用に設けられた、AEM WCM コンテンツリポジトリ内の構成要素です。

詳細については、[AEM Assets と AEM Media Library との比較](/help/assets/medialibrary.md)を参照してください。

#### 顧客が Adobe アセットピッカーにアクセスして画像を選択できるように、WordPress 用のプラグインを作成することは可能ですか。  {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

はい、WordPress を使用しているお客様は、Adobe アセットピッカーを使用して AEM Assets サーバーから画像を選択し、WordPress サイトの投稿に追加できます。

詳細については、[アセットセレクター](../assets/search-assets.md#assetpicker)を参照してください。

#### 述語を追加するために AEM Assets の検索ファセットを拡張することは可能ですか。  {#is-it-possible-to-extend-the-search-facets-in-aem-assets-to-add-additional-predicates}

Adobe Experience Manager (AEM) Assets の企業全体のデプロイメントには、多くのアセットが格納されています。述語をデフォルトフォームに追加する、または選択したファセットを含むカスタムフォームを使用することができます。

詳しくは、[検索ファセット](/help/assets/search-facets.md)を参照してください。
