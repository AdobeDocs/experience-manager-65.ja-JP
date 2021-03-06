---
cloud: Experience Cloud
product: adobe experience manager
solution: Experience Manager, Experience Manager Sites
audience: end-user
user-guide-title: AEM 6.5 開発ユーザーガイド
breadcrumb-title: 開発ガイド
user-guide-description: このガイドでは、AEM インスタンスの構築方法について説明します。
feature: Developing
role: Developer
source-git-commit: f29612ee633d2a62144b770f3c225fc82b9174f8
workflow-type: tm+mt
source-wordcount: '1299'
ht-degree: 100%

---


# AEM 6.5 開発ユーザーガイド {#developing}

+ [開発ユーザーガイドの概要](home.md)
+ デベロッパー向けの概要{#introduction}
   + [AEM Sites の開発の手引き - WKND チュートリアル](getting-started.md)
   + [AEM の中心概念](the-basics.md)
   + [AEM タッチ操作対応 UI の構造](touch-ui-structure.md)
   + [AEM タッチ操作対応 UI の概念](touch-ui-concepts.md)
   + [AEM の開発 - ガイドラインとベストプラクティス](dev-guidelines-bestpractices.md)
   + [クライアントサイドライブラリの使用](clientlibs.md)
   + [開発とページの差分](pagediff.md)
   + [編集者の制限事項](editor-limitations.md)
   + [CSRF 対策フレームワーク](csrf-protection.md)
   + [データモデリング - David Nuescheler のモデル](model-data.md)
   + [AEM への貢献](contributing-to-cq.md)
   + [セキュリティ](security.md)
   + [参照資料](reference-materials.md)
   + [完全に機能する Web サイトの作成（クラシック UI）](website.md)
   + [デザインとデザイナー（クラシック UI）](designer.md)
   + [タッチ UI への移行](/help/sites-developing/touch-ui-migration.md)
+ Platform{#platform}
   + [Sling チートシート](sling-cheatsheet.md)
   + [Sling アダプターの使用](sling-adapters.md)
   + [タグライブラリ](taglib.md)
   + テンプレート{#templates}
      + [テンプレート](templates.md)
      + [ページテンプレート - 編集可能 ](page-templates-editable.md)
      + [ページテンプレート - 静的](page-templates-static.md)
      + [コンテンツフラグメントテンプレート](content-fragment-templates.md)
      + [アダプティブテンプレートレンダリング](templates-adaptive-rendering.md)
   + [AEM での Sling Resource Merger の使用](sling-resource-merger.md)
   + [オーバーレイ](overlays.md)
   + [命名規則](naming-conventions.md)
   + [新しい Granite UI フィールドコンポーネントの作成](granite-ui-component.md)
   + Query Builder{#query-builder}
      + [Query Builder 用のカスタム述語エバリュエーターの実装](implementing-custom-predicate-evaluator.md)
      + [Query Builder の述語リファレンス](querybuilder-predicate-reference.md)
      + [Query Builder API](querybuilder-api.md)
   + タグ付け{#tagging}
      + [タグ付け](tags.md)
      + [AEM タグ付けフレームワーク](framework.md)
      + [AEM アプリケーションへのタグ付けの構築](building.md)
   + [エラーハンドラーによって表示されるページのカスタマイズ](customizing-errorhandler-pages.md)
   + [カスタムノードタイプ](custom-nodetypes.md)
   + [グラフィックレンダリング用のフォントの追加](adding-fonts.md)
   + [SQL データベースへの接続](jdbc.md)
   + [URL の外部化](externalizer.md)
   + [オフロードのためのジョブの作成と使用](dev-offloading.md)
   + [Cookie の使用法の設定](cookie-optout.md)
   + [AEM JCR へのプログラムからのアクセス方法](access-jcr.md)
   + [JMX コンソールを使用したサービスの統合](jmx-integration.md)
   + [Bulk Editor の開発](dev-bulk-editor.md)
   + [レポートの開発](dev-reports.md)
+ コンポーネント{#components}
   + [コアコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html)
   + [スタイルシステム](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/siteandpage/style-system.html?lang=ja)
   + [コンポーネントの概要](components.md)
   + [AEM コンポーネント - 基本](components-basics.md)
   + [AEM コンポーネントの開発](developing-components.md)
   + [AEM コンポーネントの開発 - コードサンプル](developing-components-samples.md)
   + [コンテンツサービス用の JSON エクスポーター](json-exporter.md)
   + [コンポーネントの JSON 書き出しの有効化](json-exporter-components.md)
   + [画像エディター](image-editor.md)
   + [装飾タグ](decoration-tag.md)
   + [非表示条件の使用](hide-conditions.md)
   + [複数のインプレースエディターの設定](multiple-inplace-editors.md)
   + [開発者モード](developer-mode.md)
   + [UI のテスト](hobbes.md)
   + [コンテンツフラグメント用コンポーネント](components-content-fragments.md)
   + [JSON 形式のページ情報の取得](pageinfo.md)
   + 国際化{#internationalization}
      + [コンポーネントの国際化](i18n.md)
      + [UI 文字列の国際化](i18n-dev.md)
      + [トランスレーターを使用した辞書の管理](i18n-translator.md)
      + [翻訳のための文字列の抽出](i18n-extract.md)
   + クラシック UI コンポーネント{#classic-ui-components}
      + [AEM コンポーネントの開発（クラシック UI）](developing-components-classic.md)
      + [ウィジェットの使用および拡張（クラシック UI）](widgets.md)
      + [xtype の使用（クラシック UI）](xtypes.md)
      + [Forms の開発（クラシック UI）](developing-forms.md)
+ [AEM におけるヘッドフルとヘッドレス](headful-headless.md)
+ ヘッドレスエクスペリエンス管理{#headless}
   + [ヘッドレスと AEM](headless/introduction.md)
   + ヘッドレスジャーニー {#journeys}
      + ヘッドレスデベロッパージャーニー {#developer}
         + [AEM のヘッドレスについて](https://experienceleague.adobe.com/docs/experience-manager-65/headless-journey/developer/overview.html?lang=ja)
         + [CMS ヘッドレス開発について](https://experienceleague.adobe.com/docs/experience-manager-65/headless-journey/developer/learn-about.html?lang=ja)
         + [AEM Headless as a Cloud Service の使用を開始する](https://experienceleague.adobe.com/docs/experience-manager-65/headless-journey/developer/getting-started.html?lang=ja)
         + [AEM ヘッドレス機能を初めて使用する際の手順](https://experienceleague.adobe.com/docs/experience-manager-65/headless-journey/developer/path-to-first-experience.html?lang=ja)
         + [コンテンツを AEM コンテンツモデルとしてモデル化する方法](https://experienceleague.adobe.com/docs/experience-manager-65/headless-journey/developer/model-your-content.html?lang=ja)
         + [AEM Delivery API を使用してコンテンツにアクセスする方法](https://experienceleague.adobe.com/docs/experience-manager-65/headless-journey/developer/access-your-content.html?lang=ja)
         + [AEM Assets API を使用してコンテンツを更新する方法](https://experienceleague.adobe.com/docs/experience-manager-65/headless-journey/developer/update-your-content.html?lang=ja)
         + [すべてをまとめる方法](https://experienceleague.adobe.com/docs/experience-manager-65/headless-journey/developer/put-it-all-together.html?lang=ja)
         + [ヘッドレスアプリケーションを運用する方法](https://experienceleague.adobe.com/docs/experience-manager-65/headless-journey/developer/go-live.html?lang=ja)
         + [オプション - AEM で単一ページアプリケーション（SPA）を作成する方法](https://experienceleague.adobe.com/docs/experience-manager-65/headless-journey/developer/create-spa.html?lang=ja)
      + ヘッドレスコンテンツアーキテクトジャーニー {#architect}
         + [AEM ヘッドレスコンテンツアーキテクトジャーニーの概要](https://experienceleague.adobe.com/docs/experience-manager-65/headless-journey/architect/overview.html?lang=ja)
         + [AEM を使用したヘッドレスのコンテンツモデリング - はじめに](https://experienceleague.adobe.com/docs/experience-manager-65/headless-journey/architect/introduction.html?lang=ja)
         + [AEM を使用したヘッドレス向けコンテンツモデリングの基本について](https://experienceleague.adobe.com/docs/experience-manager-65/headless-journey/architect/basics.html?lang=ja)
         + [AEM でのコンテンツフラグメントモデルの作成について学ぶ](https://experienceleague.adobe.com/docs/experience-manager-65/headless-journey/architect/model-structure.html?lang=ja)
   + 「はじめる前に」ガイド {#getting-started}
      + [はじめに](headless/getting-started/introduction.md)
      + [設定の作成](headless/getting-started/create-configuration.md)
      + [コンテンツフラグメントモデルの作成](headless/getting-started/create-content-model.md)
      + [アセットフォルダーの作成](headless/getting-started/create-assets-folder.md)
      + [コンテンツフラグメントの作成](headless/getting-started/create-content-fragment.md)
      + [コンテンツフラグメントへのアクセスと配信](headless/getting-started/create-api-request.md)
   + コンテンツフラグメント{#content-fragments}
      + [コンテンツフラグメントと GraphQL のヘッドレス配信](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-graphql.html?lang=ja)
      + [コンテンツフラグメントの操作](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments.html?lang=ja)
      + [インスタンスに対するコンテンツフラグメント機能の有効化](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-configuration-browser.html?lang=ja)
      + [コンテンツフラグメントモデル](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-models.html?lang=ja)
      + [コンテンツフラグメントの管理](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-managing.html?lang=ja)
      + [バリエーション - フラグメントコンテンツのオーサリング](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=ja)
      + [Markdown](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-markdown.html?lang=ja)
      + [関連コンテンツの使用](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-assoc-content.html?lang=ja)
      + [メタデータ - フラグメントのプロパティ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-metadata.html?lang=ja)
      + [構造ツリー](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-structure-tree.html?lang=ja)
      + [プレビュー - JSON 表現](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-json-preview.html?lang=ja)
   + 配信 API{#delivery-api}
      + [Assets HTTP API](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/mac-api-assets.html?lang=ja)
      + [コンテンツフラグメント REST API](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/assets-api-content-fragments.html?lang=ja)
      + [コンテンツフラグメント GraphQL API](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/graphql-api-content-fragments.html?lang=ja)
      + [AEM GraphQL API とコンテンツフラグメント - コンテンツとクエリの例](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/content-fragments-graphql-samples.html?lang=ja)
      + [コンテンツフラグメントに対するリモート AEM GraphQL クエリの認証](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/graphql-authentication-content-fragments.html?lang=ja)
+ ハイブリッドおよび SPA の AEM 開発{#spas}
   + [AEM でのハイブリッドと SPA](https://business.adobe.com/content/dam/dx/us/en/products/experience-manager/sites/headless-content-management-system/pdfs/aem-hybrid-architecture-wp-1-18-19.pdf)
   + [SPA の概要およびガイド](spa-walkthrough.md)
   + [SPA WKND チュートリアル](spa-wknd.md)
   + [React の使用を開始する](spa-getting-started-react.md)
   + [SPA への React コンポーネントの実装](spa-implementing-react-component.md)
   + [Angular の使用を開始する](spa-getting-started-angular.md)
   + [SPA の詳細](spa-deep-dives.md)
   + [AEM 向け SPA の開発](spa-architecture.md)
   + [SPA エディターの概要](spa-overview.md)
   + [SPA ブループリント](spa-blueprint.md)
   + [SPA ページコンポーネント](spa-page-component.md)
   + [コンポーネントマッピングの動的モデルSPA の場合](spa-dynamic-model-to-component-mapping.md)
   + [SPA モデルルーティング](spa-routing.md)
   + [RemotePage コンポーネント](spa-remote-page.md)
   + [AEM 内での外部 SPA の編集](spa-edit-external.md)
   + [SPA の複合コンポーネント](spa-composite-component.md)
   + [SPA およびサーバーサイドレンダリング](spa-ssr.md)
   + [コンポーネントの JSON 書き出しの有効化](https://experienceleague.adobe.com/docs/experience-manager-65/developing/components/json-exporter-components.html?lang=ja)
   + [ローンチの統合](spa-launch.md)
   + [SPA 参照資料](spa-reference-materials.md)
+ 開発ツール{#devtools}
   + [開発ツール](dev-tools.md)
   + [AEM モダナイゼーションツール](modernization-tools.md)
   + [ダイアログエディター](dialog-editor.md)
   + [ダイアログ変換ツール](dialog-conversion.md)
   + [CRXDE Lite による開発](developing-with-crxde-lite.md)
   + [Maven を使用したパッケージの管理](vlt-mavenplugin.md)
   + [Eclipse を使用して AEM プロジェクトを開発する方法](howto-projects-eclipse.md)
   + [Apache Maven を使用して AEM プロジェクトをビルドする方法](ht-projects-maven.md)
   + [IntelliJ IDEA を使用して AEM プロジェクトを開発する方法](ht-intellij.md)
   + [VLT ツールを使用する方法](ht-vlttool.md)
   + [プロキシサーバーツールを使用する方法](ht-proxy-server.md)
   + [AEM Brackets 拡張](aem-brackets.md)
   + [Eclipse 用 AEM 開発者ツール ](aem-eclipse.md)
   + [AEM Repo ツール](aem-repo-tool.md)
+ パーソナライズ機能{#personlization}
   + [ContextHub](contexthub.md)
   + [Context Hub の設定](ch-configuring.md)
   + [ページへの ContextHub の追加とストアへのアクセス](ch-adding.md)
   + [ContextHub の拡張](ch-extend.md)
   + [ContextHub ストア候補のサンプル](ch-samplestores.md)
   + [ContextHub UI モジュールタイプのサンプル](ch-samplemodules.md)
   + [ContextHub の診断](ch-diagnostics.md)
   + [ターゲットコンテンツの開発](target.md)
   + [ContextHub JavaScript API リファレンス](contexthub-api.md)
   + ClientContext{#client-context}
      + [ClientContext の詳細](client-context.md)
      + [ClientContext JavaScript API](ccjsapi.md)
+ AEM の拡張{#extending-aem}
   + [Adobe Developer App Builder を使用した AEM の拡張](app-builder.md)
   + [ページオーサリングのカスタマイズ](customizing-page-authoring-touch.md)
   + [コンソールのカスタマイズ](customizing-consoles-touch.md)
   + [ページプロパティのビューのカスタマイズ](page-properties-views.md)
   + [ページプロパティの一括編集のためのページの設定](bulk-editing.md)
   + [コンテンツフラグメントのカスタマイズと拡張](customizing-content-fragments.md)
   + [レンダリングコンポーネントのコンテンツフラグメントの設定](content-fragments-config-components-rendering.md)
   + [エクスペリエンスフラグメント](experience-fragments.md)
   + ワークフローの拡張{#extending-workflows}
      + [ワークフローの開発と拡張](workflows.md)
      + [ワークフローモデルの作成](workflows-models.md)
      + [ワークフロー機能の拡張](workflows-customizing-extending.md)
      + [プログラムによるワークフローとのやり取り](workflows-program-interaction.md)
      + [ワークフローステップのリファレンス](workflows-step-ref.md)
      + [ワークフローのベストプラクティス](workflows-best-practices.md)
      + [ワークフロープロセスのリファレンス](workflows-process-ref.md)
      + [AEM ワークフローの変数](/help/sites-developing/using-variables-in-aem-workflows.md)
   + [Multi Site Manager の拡張](extending-msm.md)
   + トラッキングと分析{#extending-analytics}
      + [イベント追跡の拡張](extending-analytics.md)
      + [コンポーネントへの Adobe Analyticsトラッキングの追加](extending-analytics-components.md)
      + [Adobe Analytics Framework のカスタマイズ](extending-analytics-framework.md)
      + [Analytics 用のサーバーサイドのページネーミングの実装](extending-analytics-pa-naming.md)
   + Cloud Services {#extending-cloud-services}
      + [クラウドサービスの設定](extending-cloud-config.md)
      + [カスタムクラウドサービスの作成](extending-cloud-config-custom-cloud.md)
   + [カスタムエクステンションの作成](extending-campaign-extensions.md)
   + Forms{#extending-forms}
      + [カスタムフォームマッピングの作成](extending-campaign-form-mapping.md)
      + [Adobe Campaign フォームコンポーネントを使用したカスタム AEM ページテンプレートの作成](extending-campaign-custom-template.md)
      + [リクエスト分析スクリプト](analyze-request.md)
   + [JMX コンソールを使用したサービスの統合](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/jmx-integration.html?lang=ja)
   + [Bulk Editor の開発](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/dev-bulk-editor.html?lang=ja)
   + クラシック UI の拡張{#extending-classic-ui}
      + [Web サイトコンソールのカスタマイズ（クラシック UI）](customizing-siteadmin.md)
      + [ようこそコンソールのカスタマイズ（クラシック UI）](customizing-the-welcome-console.md)
      + [レポートの開発](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/dev-reports.html?lang=ja)
+ テスト{#testing}
   + [計画](planning.md)
   + [必要になるテスト環境の種類](test-environments.md)
   + [テストケースの定義](test-cases.md)
   + [テスト - 実行のタイミングとテスター](when-who.md)
   + [テスト計画の策定](test-plan.md)
   + [結果の追跡とフィードバックの提供](results-and-feedback.md)
   + [テストツールおよび追跡ツール](tools.md)
   + [受け入れとサインオフ](acceptance-signoff.md)
   + [次期リリース](the-next-release.md)
   + [チェックリスト](checklists.md)
   + [Tough Day](tough-day.md)
   + [UI のテスト](https://experienceleague.adobe.com/docs/experience-manager-65/developing/components/hobbes.html?lang=ja)
+ ベストプラクティス{#bestpractices}
   + [ベストプラクティスの概要](best-practices.md)
   + [AEM の開発ガイドラインとベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/dev-guidelines-bestpractices.html?lang=ja)
   + [開発のベストプラクティス](development-practices.md)
   + [コンテンツのアーキテクチャ](content-architecture.md)
   + [ソフトウェアのアーキテクチャ](software-architecture.md)
   + We.Retail 参照実装{#we-retail}
      + [We.Retail 参照実装](we-retail.md)
      + [We.Retail のコンテンツフラグメントの使用](we-retail-content-fragments.md)
      + [We.Retail のコアコンポーネントの使用](we-retail-core-components.md)
      + [We.Retail の編集可能テンプレートの使用](we-retail-editable-templates.md)
      + [We.Retail のレスポンシブレイアウトの使用](we-retail-responsive-layout.md)
      + [We.Retail のグローバル化されたサイト構造の使用](we-retail-globalized-site-structure.md)
      + [We.Retail のコンテンツフラグメントの使用](we-retail-experience-fragments.md)
   + [コーディングのヒント](coding-tips.md)
   + [コードの落とし穴](code-pitfalls.md)
   + [OSGi バンドル](osgi-bundles.md)
   + [JCR 統合](jcr-integration.md)
   + [コードサンプル](code-samples.md)
   + [処理に時間のかかるクエリのトラブルシューティング](troubleshooting-slow-queries.md)
+ モバイル web{#mobileweb}
   + [モバイル web](mobile-web.md)
   + [デバイスグループフィルターの作成](groupfilters.md)
   + [Web ページのレスポンシブデザイン](responsive.md)
   + [モバイルデバイス用サイトの作成](mobile.md)
   + [エミュレーター](emulators.md)
