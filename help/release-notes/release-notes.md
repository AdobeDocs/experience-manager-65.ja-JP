---
title: ' [!DNL Adobe Experience Manager]  6.5 のリリースノート'
description: ' [!DNL Adobe Experience Manager] 6.5 のリリース情報、新機能、インストール方法、詳細な変更リストを確認します。'
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 14b52e7763c4d83a4dcce593f155cb1bb8f56b97
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 54%

---

# [!DNL Adobe Experience Manager] 6.5 の最新のサービスパックのリリースノート {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.21.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| タイプ | サービスパックのリリース |
| 日付 | 2024年5月23日木曜日（PT）<!-- UPDATE FOR EACH NEW RELEASE --> |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=ja#package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.21.0 の内容 {#what-is-included-in-aem-6521}

[!DNL Experience Manager] 6.5.21.0 には、2019 年 4 月の 6.5 リリースの公開当初にリリースされた新機能、お客様からリクエストされた主な機能強化、バグ修正およびパフォーマンス、安定性、セキュリティの向上が含まれています。 [このサービスパックをインストール](#install) 日付： [!DNL Experience Manager] 6.5

<!-- UPDATE FOR EACH NEW RELEASE -->

## 主な機能および機能強化

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

このリリースの主な機能と機能強化は次のとおりです。

* 既存のサービスアカウント（JWT）資格情報に代わる、サーバー間認証用の新しい使いやすい資格情報。 （NPR-41994）重要

### [!DNL Forms]

* A

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## サービスパック 21 で修正された問題 {#fixed-issues}

### [!DNL Sites]{#sites-6521}

#### アクセシビリティ {#sites-accessibility-6521}

* この **[!UICONTROL 保存済みの検索]** ラベルは永続的ではありません。 このプレースホルダーは、テキストフィールドの唯一の表示ラベルとして使用されています。 （SITES-3050）

#### 管理ユーザーインターフェイス{#sites-adminui-6521}

* クリックした場合 **[!UICONTROL Sites]** > **[!UICONTROL コアコアコンポーネント]** > **[!UICONTROL プロパティ]** > **[!UICONTROL 権限]** タブ > **[!UICONTROL 有効な許可]**, **有効な権限** ダイアログボックスがで開かない。 （SITES-17378）

#### クラシック UI{#sites-classicui-6521}

* T

#### [!DNL Content Fragments]{#sites-contentfragments-6521}

* フォーム要素のダブルインクルージョンを修正しました。 （SITES-21109）ブロッカー
* コンテンツフラグメントの作成時に「閉じる」ボタンが応答しなくなり、ページ全体がフリーズし、コンテンツフラグメントを閉じるにはページを更新する必要が生じることがあります。 バージョン作成の問題については、コンテンツフラグメントの新しいバージョンが作成されます。 この問題は、ユーザーが変更を行っていない場合でも、RTE やテキストフィールドを操作するだけで発生します。 （SITES-21187）重要


#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6521}

* Adobe Experience Managerを 6.5.19.0 から 6.5.20.0 にアップグレードする際のパス `/libs/cq/graphql/sites/graphiql` が削除されました。 （SITES-20098）重大




#### [!DNL Content Fragments] - GraphQL クエリエディター{#sites-graphql-query-editor-6521}

* 水

#### [!DNL Content Fragments] - REST API{#sites-restapi-6521}

* 水

#### コアバックエンド{#sites-core-backend-6521}

* 水

#### コアコンポーネント{#sites-core-components-6521}

* I

#### Campaign 統合{#sites-campaign-integration-6521}

* A

#### エクスペリエンスフラグメント{#sites-experiencefragments-6521}

* からのエクスペリエンスフラグメントのロールアウト `masters/language` 対象： `country/language` 相互参照は更新されません。 （SITES-20559）ブロッカー
* で指定されたテンプレートだけではありません `cq:allowedTemplates`ただし、次の条件を満たすテンプレートは `allowedPaths` テンプレートレベルで設定され、新しいエクスペリエンスフラグメントの作成時にオプションとして表示されます。 （SITES-20855）重要

#### 基盤コンポーネント（レガシー）{#sites-foundation-components-legacy-6521}

* T

#### ローンチ{#sites-launches-6521}

* この `sourceRootResource` CRXDE Lite内のローンチ設定で指定されている、存在しなくなったコンテンツを指している場合、ローンチを削除しようとすると誤動作が発生します。 ローンチの削除（ページが削除されている場合やパスが異なる場合でも） （SITES-20750）

#### MSM - ライブコピー{#sites-msm-live-copies-6521}

* ページプロパティでタブを追加するために、ページコンポーネントをオーバーレイしました。 その 1 つはページ設定で、エクスペリエンスフラグメント URL を追加するプロパティを持っています。 エクスペリエンスフラグメントのページプロパティで設定されたリンクが、そのページ用に作成された言語コピーで変更されることはありません。 設定されたリンクは、言語コピーの URL と共に変更されます。 （SITES-19580）重要

#### ページエディター{#sites-pageeditor-6521}

* 編集モードでは、WCAG （Web Content Accessibility Guidelines）のカラーコントラスト標準に準拠していないグレーの背景が一貫して適用されません。 （SITES-20060）

### [!DNL Assets]{#assets-6521}

* U

#### [!DNL Dynamic Media]{#assets-dm-6521}

* 2024年5月1日（PT）以降、Adobe Dynamic Media は次のサポートを終了します。
   * SSL（Secure Socket Layer）2.0
   * SSL 3.0
   * TLS（Transport Layer Security）1.0 および 1.1
   * TLS 1.2 での以下の脆弱な暗号：
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

### [!DNL Forms]{#forms-6521}

<!--Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.21.0 Forms add-on package release is scheduled for Thursday, May 30, 2024. A list of Forms fixes and enhancements is added to this section post the release.-->

#### [!DNL Adaptive Forms]

* 
  <!-- THIS BUG WAS ALREADY REPORTED IN 6.5.20.0 RELEASE NOTES. IS IT NEEDED AGAIN IN THE 6.5.21.0 RELEASE NOTES? (AEM Forms on JEE Only) The PDF Generator service fails to enumerate the fonts available on the server. Consequently, the font selection panel on the Adobe PDF Settings page in the PDFG Admin UI remains empty, effectively preventing (un)embedding of chosen fonts. (FORMS-12095) -->


#### [!DNL Forms Designer] {#forms-designer-6521}

* 水


### 基盤 {#foundation-6521}

#### Apache Felix {#felix-6521}

* AEM 6.5 サービスパック 19 （SP19）のアップグレード問題で、SP19 のインストール後、Apache Felix への未認証のリクエストに対してアプリケーションサーバーの context-root パスが欠落します。 Apache Felix Web Management Console 4.9.8 を更新します。 （NPR-41933）

* U

#### Campaign{#campaign-6521}

* AEM 6.5 サービスパック 15 では、重要なエントリを含んだ継続的なエラーログが生成されています。 次の問題が報告されました。

   * パスにリソースがありません。404 INFO エラー `/libs/granite/ui/content/shell/start.html`
   * が原因でキャッチされなかった SlingException のエラーログエントリ `NullPointerException` 時刻 `CampaignsDataSourceServlet.java:147`

  エラーログは、頻繁で大量のエラーエントリで埋められないようにして、リソースの不足や例外に関連する問題が発生することなく、AEM インスタンスが機能するようにします。 （CQ-4357064）

#### Communities {#communities-6521}

* U

#### コンテンツの配布{#foundation-content-distribution-6521}

* T

#### Granite{#granite-6521}

* **削除** または **変更** 権限を選択するには次の条件を満たす必要があります **参照** 設定ブラウザーでの権限。 （GRANITE-51002）

#### 統合{#integrations-6521}

* について `cq-target-integration`:Google Guava のテスト以外の使用を削除する必要があります。 （CQ-4357101）
* サービスアカウント（JSON web トークンまたは JWT）資格情報を OAuth2 サーバー間資格情報（サービスプリンシパルとも呼ばれます）に置き換えます。（NPR-41994）重要
* IMS （Identity Management System）設定でオーディエンスリクエストの作成が失敗します。 （NPR-41888）重要
* 顧客がペイロードページを表示しようとすると、URL の形式が正しくないため、コンテンツが正しく表示されず、404 エラーが表示されます。 このエラーは、URL のクエリパラメーターの前に疑問符の記号がないことが原因です。 この問題を解決するには、ペイロードページを正しく表示するために、疑問符の記号を手動で挿入する必要があります。 （NPR-41957）
* に到達したAEM 6.5 からAdobeSearch&amp;Promoteのコードと依存関係を削除します。 [通知に従って 2022 年 9 月の提供終了を発表](https://experienceleague.adobe.com/en/docs/discontinued/using/search-promote). （NPR-41855）


#### ローカライゼーション{#localization-6521}

* テンプレートエディターで、テキスト文字列 *`No video available.`* はローカライズされていません。 （SITES-13190）
* ユーザーをアクティブ化または非アクティブ化した後の文字列が、でローカライズされていない **ツール** > **セキュリティ** > **ユーザー** > *any_user_name* > **Activate** > **OK**&#x200B;を選択し、 *any_user_name* > **非アクティブ化** > **OK**. （NPR-41737）

#### プラットフォーム{#foundation-platform-6521}

* この `Unclosed resource resolver` に対してエラーが発生しています `com.day.cq.mailer.impl.DefaultMailService`. この `MessageGatewayService` クラスは標準で、リソースリゾルバーなしで使用されていました。 このクラスを使用して E メールを送信するフォーム送信ボタンのあるページで問題が発生しました。 （NPR-41853）

#### Sling{#foundation-sling-6521}

* T

#### 翻訳{#foundation-translation-6521}

* AEM 6.5.19 の標準の翻訳ステータスがローンチの期待どおりに更新されない問題。 翻訳済みファイルをAEM ローンチに関連付けられた翻訳ジョブに読み込むと、ステータスが「」に変わることが予想されていました。 `Approved`. 代わりに、ステータスがに変更されます。 `Ready for Review`（想定されている動作ではありません）。 （NPR-41756）重要
* 複数の設定を作成して翻訳Cloud Serviceの設定に移動すると、すべての要素が UI に表示されるわけではありません。 最初の 40 個の要素/フォルダーのみが表示され、遅延読み込みがトリガーされますが、コンテンツはそれ以上追加されません。 （NPR-41829）
* 日本語の場合、タッチユーザーインターフェイスの権限ページに文字化けが発生します。 （NPR-41794）

#### ユーザーインターフェイス{#foundation-ui-6521}

* ツール / セキュリティ / ユーザーで &lt;user_name> > プロファイル、内 **ユーザー設定の編集** ダイアログ ボックスで [ キャンセル ] をクリックしても、ダイアログ ボックスは終了しません。 （NPR-41793）重要
* Granite `pathfield` コンポーネント `/libs/granite/ui/components/coral/foundation/form/pathfield` を有効にできない **[!UICONTROL を選択]** ボタンをクリックしてアセットを選択します。 パスフィールドがポップアップ表示され、ユーザーがアセットのチェックボックス **[!UICONTROL を選択]** ボタンが有効になっていません。グレーから青に変わりません。 （NPR-41970）
* AEM内のコンテンツフラグメントモデル（CFM）参照フィールドに問題がある。 CFM 参照フィールドは必須として設定されていますが、ユーザーは「保存」をクリックして、特定のシナリオで CFM 以外の値を含むコンテンツを保存できます。 「保存」ボタンはグレー表示（使用不可）になっているはずです。 （NPR-41894）
* を使用する標準の Coral ユーザーインターフェイスダイアログボックス `successresponse` アクションは、アクションの後に成功応答をトリガーにする必要があります。 ただし、AEM 6.5 サービスパック 19 では、再読み込みアクションは呼び出されず、メッセージは表示されません。 （NPR-41797）
* AEM 6.5 サービスパック 18 でAEM通知のリンクが機能しない。 Service Pack 18 にアップグレードすると、「通知」ボタンでメッセージを選択する際にAEM通知リンクが機能しません。 （NPR-41792）

#### WCM{#wcm-6521}

* T

#### ワークフロー{#foundation-workflow-6521}

* AEM 6.5.18 では、パージ中にユーザーメタデータキャッシュから削除する際にエラーが繰り返し発生していました。 （NPR-41762）

## [!DNL Experience Manager] 6.5.21.0 のインストール{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.21.0 には [!DNL Experience Manager] 6.5 が必要です。手順について詳しくは、[アップグレードに関するドキュメント](/help/sites-deploying/upgrade.md)を参照してください。<!-- UPDATE FOR EACH NEW RELEASE -->
* サービスパックは、Adobeからダウンロードできます。 [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=ja#package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip).
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用して、オーサーインスタンスの 1 つに [!DNL Experience Manager] 6.5.21.0 をインストールしてください。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> アドビでは、[!DNL Experience Manager] 6.5.21.0 パッケージを削除またはアンインストールすることを推奨しません。したがって、パッケージをインストールする前に、ロールバックする必要がある場合に備えて `crx-repository` のバックアップを作成する必要があります。<!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### サービスパックのインストール [!DNL Experience Manager] 6.5{#install-service-pack}

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。

1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。

1. Service Sack のダウンロード元 [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=ja#package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. パッケージマネージャーを開き、「**[!UICONTROL パッケージをアップロード]**」を選択して、パッケージをアップロードします。詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択して、「**[!UICONTROL インストール]**」を選択します。

1. S3 コネクタを更新するには、サービスパックのインストール後にインスタンスを停止し、既存のコネクタをインストールフォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。[Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログが終了することがあります。 Adobeでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。この問題は、通常 [!DNL Safari] ブラウザーで発生しますが、どのブラウザーでも断続的に発生する場合があります。

**自動インストール**

[!DNL Experience Manager] 6.5.21.0 の自動インストールに使用できる方法は 2 つあります。<!-- UPDATE FOR EACH NEW RELEASE -->

* サーバーがオンラインで使用可能な場合、パッケージを `../crx-quickstart/install` フォルダーに配置します。パッケージが自動的にインストールされます。
* [パッケージマネージャーの HTTP API](/help/sites-administering/package-manager.md#package-share) を使用します。ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

>[!NOTE]
>
>Experience Manager 6.5.21.0 では、Bootstrap のインストールをサポートしていません。<!-- UPDATE FOR EACH NEW RELEASE -->

**インストールの検証**

このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

1. 製品情報ページ（`/system/console/productinfo`）の[!UICONTROL インストール済み製品]に、更新されたバージョン文字列 `Adobe Experience Manager (6.5.21.0)` が表示されます。<!-- UPDATE FOR EACH NEW RELEASE -->

1. すべての OSGi バンドルは、OSGi コンソールで **[!UICONTROL アクティブ]** または **[!UICONTROL フラグメント]** です（web コンソールを使用：`/system/console/bundles`）。

1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン 1.22.18 以降です（Web コンソールを使用：`/system/console/bundles`）。<!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### [!DNL Experience Manager] Forms へのサービスパックのインストール{#install-aem-forms-add-on-package}

Experience Manager Formsへのサービスパックのインストール手順については、を参照してください。 [Experience Manager Forms サービスパックのインストール手順](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>[AEM 6.5 クイックスタート](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/deploying/deploy.html?lang=ja)で使用できるアダプティブフォーム機能は、探索と評価のみを目的として設計されています。 アダプティブフォームの機能には適切なライセンスが必要なので、実稼動環境で使用する場合は、AEM Forms の有効なライセンスを取得することが不可欠です。

### Experience Manager コンテンツフラグメント用の GraphQL インデックスパッケージのインストール{#install-aem-graphql-index-add-on-package}

GraphQL を使用しているお客様は、[Experience Manager コンテンツフラグメントと GraphQL インデックスパッケージ 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=ja#package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip) をインストールする必要があります。

これにより、実際に使用する機能に基づいて、必要なインデックス定義を追加できます。

このパッケージをインストールしないと、GraphQL クエリが遅くなったり失敗したりする場合があります。

>[!NOTE]
>
>このパッケージは、インスタンスごとに 1 度だけインストールします。サービスパックごとに再インストールする必要はありません。

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.21.0 の UberJar は、[Maven Central リポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.20/)で入手できます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Maven プロジェクトで UberJar を使用するには、[UberJar の使用方法](/help/sites-developing/ht-projects-maven.md)を参照し、プロジェクト POM に次の依存関係を含めます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.21</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar およびその他の関連アーティファクトは、Adobe のパブリック Maven リポジトリー （`repo.adobe.com`） ではなく、Maven Central リポジトリーで入手できます。メインの UberJar ファイルの名前は、「`uber-jar-<version>.jar`」に変更されます。そのため `classifier` が存在せず、`apis` が値として `dependency` タグに使用されます。


## 廃止される機能および削除された機能{#removed-deprecated-features}

[廃止される機能および削除された機能](/help/release-notes/deprecated-removed-features.md/)を参照してください。

## 既知の問題{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->


* **Oak 関連**
サービスパック 13 以降で、永続性キャッシュに影響する次のエラーログが表示されるようになりました。

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  または

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  この例外を解決するには、次の手順を実行します。

   1. 次の 2 つのフォルダーを `crx-quickstart/repository/` から削除する

      * `cache`
      * `diff-cache`

   1. サービスパックをインストールするか、Experience Manager as a Cloud Serviceを再起動します。
`cache` および `diff-cache` の新しいフォルダーが自動的に作成され、`error.log` 内で `mvstore` に関連する例外は発生しなくなりました。

* コンテンツモデルのカスタム API 名を使用していた可能性のある GraphQL クエリを、代わりにコンテンツモデルのデフォルト名を使用するように更新してください。

* GraphQL クエリでは、`fragments` インデックスの代わりに `damAssetLucene` インデックスを使用する場合があります。このアクションは結果的に、GraphQL クエリが失敗するか、実行に非常に長い時間がかかる可能性があります。

  問題を修正するには、`damAssetLucene` では、`/indexRules/dam:Asset/properties` に次の 2 つのプロパティを含むように設定する必要があります。

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  インデックス定義を変更した後、インデックス再作成が必要です（`reindex` = `true`）。

  これらの手順を行うと、GraphQL クエリの実行が高速化されます。

* コンテンツフラグメント、サイト、ページのいずれかを移動、削除または公開しようとすると、バックグラウンドクエリが失敗したため、コンテンツフラグメント参照が取得される際に問題が発生します。つまり、この機能が動作しなくなります。
正しく動作させるには、インデックス定義ノード `/oak:index/damAssetLucene` に次のプロパティを追加する必要があります（インデックスの再作成は不要です）。

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* をアップグレードする場合 [!DNL Experience Manager] インスタンスが 6.5.0～6.5.4 から Java™ 11 の最新のサービスパックに変換された場合は、次のようになります `RRD4JReporter` の例外 `error.log` ファイル。 例外を停止するには、[!DNL Experience Manager] のインスタンスを再起動します。<!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* ユーザーは、[!DNL Assets] の階層内のフォルダーの名前を変更し、ネストされたフォルダーを [!DNL Brand Portal] に公開できます。ただし、ルートフォルダーが再公開されるまで、[!DNL Brand Portal] でフォルダーのタイトルは更新されません。

* [!DNL Experience Manager] 6.5.x.x のインストール中に、次のエラーや警告メッセージが表示される場合があります。
   * 「Target Standard API（IMS 認証）を使用して [!DNL Experience Manager] に Adobe Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。Target では、「エクスペリエンスフラグメント」／ソース「Adobe Experience Manager」タイプではなく、「HTML」／ソース「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MIN などの集計関数が使用される場合、アダプティブフォームのサーバー側検証が失敗します （CQ-4274424）。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューしている間、Dynamic Media インタラクティブ画像のホットスポットは表示されません。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]`：登録状況を未登録に変更する処理が完了するのを待機中にタイムアウトになりました。

* AEM 6.5.15 以降、```org.apache.servicemix.bundles.rhino``` バンドルで提供される Rhino JavaScript Engine には、新しい巻上げ動作が追加されました。strict モード（```use strict;```）を使用するスクリプトでは、変数を正しく宣言する必要があります。宣言しない場合、スクリプトは実行されず、代わりにランタイムエラーが発生します。

* 公式の更新パッケージ（サービスパック、セキュリティサービスパック、拡張機能パック、累積機能パック、パッチなどを含む）を通じてタグ付け関連の標準コンテンツをインストールすると、`/content/cq:tags` ノードの言語プロパティがデフォルトにリセットされます。 したがって、インストール前にプロパティから追加しておく必要があります。

### AEM Sitesの既知の問題 {#known-issues-aem-sites-6521}

* SITES-17934 - コンテンツフラグメント - 大きなフラグメントツリーに対する DoS 保護が原因でプレビューに失敗する。を参照してください。 [GraphQL Query Executor のデフォルトの設定オプションに関するナレッジベース記事](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-23945)

### AEM Forms の既知の問題 {#known-issues-aem-forms-6521}

* T

## 含まれている OSGi バンドルとコンテンツパッケージ{#osgi-bundles-and-content-packages-included}

次のテキストドキュメントには、この [!DNL Experience Manager] 6.5 サービスパックリリースに含まれている OSGi バンドルとコンテンツパッケージのリストが記載されています。

* [Experience Manager 6.5.21.0 に含まれている OSGi バンドルのリスト](/help/release-notes/assets/65200-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.21.0 に含まれているコンテンツパッケージのリスト](/help/release-notes/assets/65200-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 制限付き Web サイト{#restricted-sites}

以下の web サイトはお客様のみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=ja)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/jp/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
>* [アドビ製品アップデートの優先通知に登録する](https://www.adobe.com/subscription/priority-product-update.html)
