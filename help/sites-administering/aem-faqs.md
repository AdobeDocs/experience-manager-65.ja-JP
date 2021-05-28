---
title: AEM FAQ
seo-title: AEM 6.4 に関する一般的な質問
description: AEM の一般的なワークフローの理解と設定、または AEM で発生する一般的な問題のトラブルシューティングに役立つ FAQ です。
seo-description: AEM の一般的なワークフローの理解と設定、または AEM で発生する一般的な問題のトラブルシューティングに役立つ FAQ です。
uuid: 17d34923-f1ce-463b-8e9d-a713edcce51b
contentOwner: jsyal
discoiquuid: a3bb5695-6593-413d-9c2f-4c164e663b15
docset: aem65
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
source-git-commit: 68c36d4e3a14567a4d115ee64a4474bcaf9aa386
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 66%

---

# AEM FAQ {#aem-faqs}

AEM でのトラブルシューティングと設定に関するいくつかの問題の解決方法を説明します。

## サイト {#sites}

### バイナリレスディストリビューションの設定方法を教えてください。  {#how-do-i-configure-binary-less-distribution}

バイナリレスディストリビューションは、共有データストアにわたる開発でサポートされ、Vault ベースのディストリビューションパッケージエクスポーター（ファクトリ PID：`org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`）パッケージビルダーを活用するエージェントが関係します。

バイナリレスモードを有効にすると、ディストリビュートされたコンテンツパッケージに、実際のバイナリではなく、バイナリへの参照が含まれます。

#### バイナリレスディストリビューションを有効にする方法を教えてください。  {#how-do-i-enable-binary-less-distribution}

バイナリレスディストリビューションを有効にするには、共有 BLOB ストアと共にデプロイします。OSGI設定の`useBinaryReferences`プロパティを、エージェントが使用しているファクトリPID(`org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)*&#x200B;で確認します。

#### AEMサイトコンソールでページ階層を移動する際に、エラーメッセージをカスタマイズするにはどうすればよいですか？{#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

（Chrome ブラウザーの）Network パネルの個人設定を確認します（JS は縮小されていません）。

`Initiator` 列を表示して、リクエストのイニシエーターを判別します。AJAX 呼び出しがおこなわれたファイルおよび行番号がわかります。次に、エラー処理関数をトレースし、要件に応じてエラーメッセージを変更できます。

#### 言語コピーを作成する際に AEM で Content-Authors の権限を有効にする方法を教えてください。  {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

言語コピー機能を作成するには、content-authorsに`/content/projects`の場所に権限が必要です。

作成者がプロジェクトの管理も必要な場合は、回避策として`project-administrators`グループに作成者を追加します。

#### プロジェクトの言語コピーを作成する際に形式を変更する方法{#how-to-change-the-format-while-creating-language-copy-for-a-project}

翻訳プロジェクトを作成する前に、ルート内部に言語ルートおよび言語コピーを作成します。

例：
`/content/geometrixx`に、名前が`fr_LU`(タイトルはフランス語（ルクセンブルグ）)の言語ルートを作成します。 次に、参照パネルからページの言語コピーを作成し、`Create & Translate`の`Create structure only`オプションに移動します。 最後に、翻訳プロジェクトを作成し、言語コピーを翻訳ジョブに追加します。

詳しくは、次の追加リソースを参照してください。

* [翻訳するコンテンツの準備](/help/sites-administering/tc-prep.md)
* [翻訳プロジェクトの管理](/help/sites-administering/tc-manage.md)

#### ログイン試行、ACLまたは権限の変更などのAEM機能を監査する方法を教えてください。{#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

トラブルシューティングと監査の質を高めるために、管理に関係する変更を記録する機能が追加されました。デフォルトでは、情報は`error.log`ファイルに記録されます。 監視を容易にするために、この情報を別のログファイルにリダイレクトすることをお勧めします。出力を別のログファイルにリダイレクトする方法については、[AEM でのユーザー管理操作を監査する方法](/help/sites-administering/audit-user-management-operations.md)を参照してください。

#### デフォルトでSSLを有効にする方法を教えてください。{#how-to-enable-ssl-by-default}

Adobe Experience Manager（AEM）6.4 には SSL ウィザードが付属し、Jetty および Granite Jetty SSL のサポートを設定するユーザーインターフェイスが備わっています。

デフォルトの SSL を有効にする方法については、[デフォルトの SSL](/help/sites-administering/ssl-by-default.md) を参照してください。

#### AEM のコンテンツサービスをモバイルアプリから使用する場合に推奨されるアーキテクチャは何ですか。理想的には React Native ですか。  {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

コンテンツサービスはSlingモデルに基づいており、AEM開発者は、書き出される各コンポーネントに対してSlingモデルのポジションを提供する必要があります。

AEM コンテンツサービスを React アプリケーションから使用する方法については、[AEM コンテンツサービスの使用準備](https://helpx.adobe.com/jp/experience-manager/kt/sites/using/content-services-tutorial-use.html)のチュートリアルを参照してください。

また、コンポーネントのツリーを書き出す場合は、`ComponentExporter`と`ContainerExporter`インターフェイスを実装し、`ModelFactory`を使用して子コンポーネントを反復し、そのモデル表現を返すこともできます。 以下のリソースを参照してください。

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2 ] [Apache Sling ::Slingモデル](https://sling.apache.org/documentation/bundles/models.html)

#### AEM 6.4の調査のポップアップを無効にする方法を教えてください。{#how-to-disable-aem-survey-pop-up}

使用状況に関する統計情報の収集をオプトインするには、タッチ UI または Web コンソールを使用します。詳しくは、[集計した使用状況の統計の収集をオプトインする方法](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)を参照してください。

#### AEM 6.4 にアップグレードするための主な機能を説明しているリソースを教えてください。  {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

Adobe Experience Managerの最新バージョンへのアップグレードを検討しているお客様の主な機能の大まかな分類については、[AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html)をアップグレードする理由についてを参照してください。

## Assets {#assets}

### MP4 ファイルのアップロード時に、Assets ワークフローが繰り返されるのはなぜですか（例えば、ドラッグ＆ドロップの使用）。  {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

ムービーファイルをアップロードするユーザーが asset ノード以下の削除権限を持っていない場合、削除チャンクノードは失敗し、アップロードが再開します。

#### 言語コピーの作成時のOOTB設定のデフォルト設定は何ですか？{#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

タッチUI（**参照** -> **言語コピーを更新**）を使用して言語コピーを作成すると、新しい言語の下に新しいDAMフォルダーが作成され、アセットが参照されます。

これは OOTB 設定のデフォルト設定です。翻訳設定で「**ページのアセットを翻訳**」を「**翻訳しない**」に設定できます。AEM 6.4 の場合は、**ツール**／**クラウドサービス**／**翻訳クラウドサービス**&#x200B;を選択して設定します。

#### AEM SegmentStore(AEM 6.3.1.1)の指数的な増加を引き起こすAEMコンポーネントを無効にするには、どうすればよいですか？{#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

OSGi Component Disabler を無効にできます。このサービスの使用方法については、[OSGi Component Disabler](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html) を参照してください。

回避策として、AEM が再開するたびに、UI または `curl` コマンド（以下の例を参照）を使用して、このコンポーネントを手動で無効にすることもできます。

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### 管理コンソールのカスタマイズ方法は？{#how-to-customize-admin-consoles}

AEMは、オーサリングインスタンスのコンソールとページオーサリング機能をカスタマイズできる様々なメカニズムを提供します。 カスタムコンソールの作成する方法、およびコンソールのデフォルトビューのカスタマイズ方法については、[コンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md)を参照してください。

#### CoralUI 2 と CoralUI 3 ベースのコンポーネントの違いを教えてください。  {#what-is-the-difference-between-coralui-and-coralui-based-components}

Granite UI Foundationの新しいSlingコンポーネントのセットがCoral3用に作成され、[/libs/granite/ui/components/coral/foundationに配置されます。](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html)CoralUI 2 ベースのコンポーネント用と CoralUI 3 ベースのコンポーネント用のセットが1 つずつあります。新しいセットは、古いセットをただコピーして貼り付けたものではなく、（合理化、廃止予定の機能を削除するなど）クリーンアップしたものです。そのため、ページは CoralUI 3 ベースまたは CoralUI 2 ベースのいずれかのセットのみを使用することをお勧めします。

詳細については、[CoralUI 3 ベースの移行ガイド](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html)を参照してください。

#### AEM Assetsで検索コンポーネントをカスタマイズする方法{#how-to-customize-the-search-component-in-aem-assets}

検索ブースト／ランキングおよびその他の実装情報については、[簡易検索実装ガイド](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html)を参照してください。

簡易検索の実装は、2017 Summit lab AEM Search Demystified の資料です。

#### 顧客がアセットピッカーにアクセスして画像を選択できるWordPress用のAdobeを構築することは可能ですか？{#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

はい、WordPress を使用しているお客様は、Adobe アセットピッカーを使用して AEM Assets サーバーから画像を選択し、WordPress サイトの投稿に追加できます。

詳細については、[アセットセレクター](../assets/search-assets.md#assetpicker)を参照してください。
