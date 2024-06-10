---
title: ' [!DNL Adobe Experience Manager]  6.5 のリリースノート'
description: ' [!DNL Adobe Experience Manager] 6.5 のリリース情報、新機能、インストール方法、詳細な変更リストを確認します。'
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: a52311b9-ed7a-432e-8f35-d045c0d8ea4c
source-git-commit: 4035bfae6a525292ca71b182ebed2ac9839426b8
workflow-type: tm+mt
source-wordcount: '3050'
ht-degree: 99%

---

# [!DNL Adobe Experience Manager] 6.5 の最新のサービスパックのリリースノート {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.21.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| タイプ | サービスパックのリリース |
| 日付 | 2024年6月6日木曜日（PT）<!-- UPDATE FOR EACH NEW RELEASE --> |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.21.0 の内容 {#what-is-included-in-aem-6521}

[!DNL Experience Manager] 6.5.21.0 には、新機能、お客様からリクエストされた主な機能強化、バグ修正が含まれています。また、2019年4月の 6.5 の公開当初以降にリリースされたパフォーマンス、安定性、セキュリティの改善も含まれています。[このサービスパックを [!DNL Experience Manager] 6.5 にインストールします](#install)。

<!-- UPDATE FOR EACH NEW RELEASE -->

## 主な機能および機能強化

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

このリリースの主な機能と機能強化は次のとおりです。

* 既存のサービスアカウント（JWT）資格情報に代わる、サーバー間認証用の新しく使いやすい資格情報。（NPR-41994）

### [!DNL Assets]

#### 機能強化

このリリースで提供される機能強化は、次のリストのとおりです。

* IPTC タブは、[!UICONTROL 代替テキスト]と[!UICONTROL 詳細な説明]テキストフィールドをサポートするようになりました。（ASSETS-34918）

#### アクセシビリティの修正

このリリースに含まれるアクセシビリティの修正は、次のリストのとおりです。

* アセットの処理ステータスが「失敗」または「メタデータ失敗」の場合、キャプションとオーディオトラックの UI は適切に機能しません。（ASSETS-37281）
* アセットメタデータを保存して編集しようとすると、言語名が表示されません。（ASSETS-37281）

<!-- ### [!DNL Forms]
* A -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## サービスパック 21 で修正された問題 {#fixed-issues}

### [!DNL Sites]{#sites-6521}

#### アクセシビリティ {#sites-accessibility-6521}

* **[!UICONTROL 保存検索]**&#x200B;ラベルは永続的ではありません。プレースホルダーは、テキストフィールドの唯一の表示ラベルとして使用されています。（SITES-3050）

#### 管理者ユーザーインターフェイス{#sites-adminui-6521}

* **[!UICONTROL Sites]**／**[!UICONTROL コアコンポーネント]**／**[!UICONTROL プロパティ]**／**[!UICONTROL 権限]**&#x200B;タブ／**[!UICONTROL 有効な権限]**&#x200B;をクリックしても、**有効な権限**&#x200B;ダイアログボックスが開きません。（SITES-17378）

<!-- #### Classic UI{#sites-classicui-6521} 

* A -->

#### [!DNL Content Fragments]{#sites-contentfragments-6521}

* フォーム要素が重複して含まれていたのを修正しました。（SITES-21109）
* コンテンツフラグメントの作成時に「閉じる」ボタンが応答しなくなり、ページ全体がフリーズし、コンテンツフラグメントを閉じるにはページを更新しなければならなくなることがあります。バージョン作成の問題については、システムでコンテンツフラグメントの新しいバージョンを作成しています。この問題は、ユーザーが変更を行っていない場合でも、RTE やテキストフィールドを操作するだけで発生します。（SITES-21187）

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6521}

* Adobe Experience Manager を 6.5.19.0 から 6.5.20.0 にアップグレードする際のパス `/libs/cq/graphql/sites/graphiql` が削除されました。（SITES-20098）

<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6521}

* W -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6521}

* W -->

<!-- #### Core Backend{#sites-core-backend-6521}

* W -->

<!-- #### Core Components{#sites-core-components-6521}

* I -->

<!-- #### Campaign integration{#sites-campaign-integration-6521}

* A -->

#### エクスペリエンスフラグメント{#sites-experiencefragments-6521}

* `masters/language` から `country/language` へのエクスペリエンスフラグメントのロールアウトでは、相互参照は更新されません。（SITES-21172）
* 新しいエクスペリエンスフラグメントの作成時には、`cq:allowedTemplates` で指定されたテンプレートだけではなく、テンプレートレベルで `allowedPaths` が設定されたテンプレートもオプションとして表示されます。（SITES-20855）

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6521}

* T -->

<!-- #### Launches{#sites-launches-6521} -->

<!-- DELETED MAY 22, 2024 FROM TOTAL RELEASE CANDIDATE ISSUES * The `sourceRootResource` configured in the Launch configuration within CRXDE Lite points to content that no longer exists, leading to a malfunction when attempts are made to delete launches. Delete launches even if the page is deleted or if the path is not the same. (SITES-20750) -->

#### MSM - ライブコピー{#sites-msm-live-copies-6521}

* ページコンポーネントをオーバーレイして、ページプロパティでタブを追加します。そのうち 1 つはページ設定で、エクスペリエンスフラグメント URL を追加するプロパティを備えています。エクスペリエンスフラグメントのページプロパティで設定されたリンクが、そのページ用に作成された言語コピーに対して変更されることはありません。設定されたリンクは、言語コピーの URL と共に変更されます。（SITES-19580）

#### ページエディター{#sites-pageeditor-6521}

* 編集モードでは、WCAG（Web Content Accessibility Guidelines）のカラーコントラスト標準に準拠していない、グレーの背景を例外的に適用しています。（SITES-20060）

### [!DNL Assets]{#assets-6521}

* アセットが Brand Portal に公開される場合、公開ステータスの一貫性は失われたままになります。（ASSETS-36807）
* API 呼び出しを使用してインスタンスからアセットを削除しても、アセットは削除されません。（ASSETS-35131）
* メタデータを読み込もうとすると、英語以外の言語の文字の挿入が `question mark (?)` に置き換えられます。（ASSETS-35091）
* データタイプ文字列で `dc:title` プロパティを使用すると、サービスパック 6.5.19 のインストール後にアセットコンテンツツリーが適切に機能しません。（ASSETS-34684）
* アセット名に特殊文字がある場合、エラーが表示されます。（ASSETS-33248）

#### [!DNL Dynamic Media]{#assets-dm-6521}

* AEM 6.5.18 で、ホットスポットを編集する際に、アセットに追加したすべてのホットスポットが表示されません。ただし、公開済みアセットでは、すべてのホットスポットが機能しますが、必要になっても後で編集できません。（ASSETS-33609）
* アップロードされた最新の EPS ファイルは、再処理後にサムネールを生成しません。（ASSETS-32617）
* ツール／アセット／Dynamic Media 公開設定／リクエスト属性タブで、`Width(px)` と `Height(px)` の入力がスペイン語、イタリア語、ポルトガル語で異なって表示されます。これらの場所では、相互に連携していません。（ASSETS-31896）
* 2024年5月1日（PT）以降、Adobe Dynamic Media は次のサポートを終了しました。
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

[!DNL Experience Manager] Forms の修正は、[!DNL Experience Manager] サービスパックリリース予定日の 1 週間後に、別のアドオンパッケージとして提供されます。この場合、AEM 6.5.21.0 Forms アドオンパッケージリリースは、2024年6月13日木曜日（PT）に予定されています。Forms の修正および機能強化のリストは、リリース後にこの節に追加されます。

<!-- #### [!DNL Adaptive Forms]

* THIS BUG WAS ALREADY REPORTED IN THE 6.5.20.0 RELEASE NOTES. IS IT NEEDED AGAIN IN THE 6.5.21.0 RELEASE NOTES? (AEM Forms on JEE Only) The PDF Generator service fails to enumerate the fonts available on the server. Consequently, the font selection panel on the Adobe PDF Settings page in the PDFG Admin UI remains empty, effectively preventing (un)embedding of chosen fonts. (FORMS-12095) -->


<!-- #### [!DNL Forms Designer] {#forms-designer-6521}

* W -->

### 基盤 {#foundation-6521}

#### Apache Felix {#foundation-apachefelix-6521}

* AEM 6.5 サービスパック 19（SP19）のアップグレード問題では、SP19 のインストール後、Apache Felix への未認証のリクエストに対してアプリケーションサーバーの context-root パスが消えます。Apache Felix Web Management Console 4.9.8 に更新します。（NPR-41933）

#### Campaign{#foundation-campaign-6521}

* AEM 6.5 サービスパック 15 では、重要なエントリを含んだ継続的なエラーログが生成されています。次の問題が報告されました。

   * パス `/libs/granite/ui/content/shell/start.html` にリソースがないことによる 404 INFO エラー
   * `CampaignsDataSourceServlet.java:147` での `NullPointerException` が原因でキャッチされなかった SlingException のエラーログエントリ

  エラーログは、頻繁かつ大量のエラーエントリでいっぱいにならないようにし、リソース不足や例外に関連する問題を発生させずに、AEM インスタンスが機能するようにします。（CQ-4357064）

#### クラウドサービス{#foundation-cloudservices-6521}

* AEM Cloud Service から Google Guava を削除します。（CQ-4356436）

<!-- #### Communities {#foundation-communities-6521}

* U -->

<!-- #### Content distribution{#foundation-content-distribution-6521}

* T -->

#### Granite{#foundation-granite-6521}

* 設定ブラウザーで&#x200B;**参照**&#x200B;権限がなければ、「**削除**」または「**変更**」を選択することはできません。（GRANITE-51002）

#### 統合{#foundation-integrations-6521}

* `cq-target-integration` については、Google Guava のテスト以外の使用を削除する必要があります。（CQ-4357101）
* サービスアカウント（JSON web トークン、または JWT）資格情報を OAuth2 サーバー間資格情報（サービスプリンシパルとも呼ばれる）に置き換えます。（NPR-41994）
* IMS（Identity Management System）設定でオーディエンスリクエストの作成に失敗します。（NPR-41888）
* 顧客がペイロードページを表示しようとすると、URL の形式が正しくないことが原因でコンテンツが正しく表示されず、404 エラーが表示されます。URL 内のクエリパラメーターの前に疑問符記号が欠落している場合、エラーが発生していました。この問題でペイロードページを正しく表示するには、顧客が疑問符記号を挿入する必要があります。（NPR-41957）
* [通知の通り、2022年9月](https://experienceleague.adobe.com/ja/docs/discontinued/using/search-promote)に提供を終了した、AEM 6.5 から Adobe Search&amp;Promote のコードと依存関係を削除します。（NPR-41855）

#### ローカライゼーション{#foundation-localization-6521}

* テンプレートエディターでは、テキスト文字列 *`No video available.`* はローカライズされていません。（SITES-13190）
* ユーザーをアクティベートまたはディアクティベートした後の文字列は、**ツール**／**セキュリティ**／**ユーザー**／*any_user_name*／**アクティベート**／**OK** ではローカライズされておらず、*any_user_name*／**ディアクティベート**／**OK** を選択します。（NPR-41737）

#### Oak {#foundation-oak-6521}

* パフォーマンス回帰修正：類似条件に対する範囲クエリを避けます。 （OAK-9481）

* 新しい Oak バージョンは 1.22.20 です。

#### プラットフォーム{#foundation-platform-6521}

* `com.day.cq.mailer.impl.DefaultMailService` に対して `Unclosed resource resolver` エラーが発生しています。`MessageGatewayService` クラスは標準で、リソースリゾルバーなしで使用されていました。このクラスを使用してメールを送信するフォーム送信ボタンのあるページで問題が発生しました。（NPR-41853）
* **Adobe Experience Manager** ダイアログボックスでは、著作権の年度は 2023 のままになります。（CQ-4356349）


<!-- #### Sling{#foundation-sling-6521}

* T -->

#### 翻訳{#foundation-translation-6521}

* AEM 6.5.19 の標準の翻訳ステータスがローンチ用に想定通りに更新されない問題。翻訳されたファイルを AEM ローンチに関連付けられた翻訳ジョブに読み込むと、ステータスが `Approved` に変わることが想定されていました。代わりに、ステータスが `Ready for Review` に変更されます（想定されている動作ではありません）。（NPR-41756）
* 複数の設定を作成して翻訳クラウドサービス設定に移動すると、一部の要素が UI に表示されません。最初の 40 個の要素／フォルダーのみが表示され、遅延読み込みがトリガーされますが、コンテンツはそれ以上追加されません。（NPR-41829）
* 日本語の場合、タッチユーザーインターフェイスの権限ページで文字化けが発生します。（NPR-41794）
* AEM 6.5.14 および 6.5.9 では、変換の絵文字を送信しません。（CQ-4357000）

#### ユーザーインターフェイス{#foundation-ui-6521}

* **ユーザー設定を編集**&#x200B;ダイアログボックス内のツール／セキュリティ／ユーザー／&lt;user_name>／プロファイルで、ダイアログボックス内で「キャンセル」をクリックできません。（NPR-41793）
* アセットが選択されている場合、`/libs/granite/ui/components/coral/foundation/form/pathfield` での Granite `pathfield` コンポーネントで「**[!UICONTROL 選択]**」ボタンを有効にできません。パスフィールドがポップアップ表示され、ユーザーがアセットのチェックボックスを選択しても、「**[!UICONTROL 選択]**」ボタンが有効になりません（グレーからブルーに変化しません）。（NPR-41970）
* AEM 内のコンテンツフラグメントモデル（CFM）参照フィールドに問題があります。CFM 参照フィールドは必須として設定されていますが、システムによってユーザーは「保存」をクリックし、特定のシナリオで CFM 以外の値を含むコンテンツを保存できます。「保存」ボタンはグレー表示（使用不可）になります。（NPR-41894）
* `successresponse` アクションを使用する標準の Coral ユーザーインターフェイスダイアログボックスは、アクションの後に成功応答をトリガーにする必要があります。ただし、AEM 6.5 サービスパック 19 では、リロードアクションは呼び出されず、メッセージが表示されません。（NPR-41797）
* AEM 6.5 サービスパック 18 で AEM 通知のリンクが機能しません。サービスパック 18 にアップグレードすると、「通知」ボタンでメッセージを選択する際に AEM 通知リンクが機能しません。（NPR-41792）

<!-- #### WCM{#foundation-wcm-6521}

* T -->

#### ワークフロー{#foundation-workflow-6521}

* AEM 6.5.18 では、パージ中にユーザーメタデータキャッシュから削除する際にエラーが繰り返し発生していました。（NPR-41762）

## [!DNL Experience Manager] 6.5.21.0 のインストール{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.21.0 には [!DNL Experience Manager] 6.5 が必要です。手順について詳しくは、[アップグレードに関するドキュメント](/help/sites-deploying/upgrade.md)を参照してください。<!-- UPDATE FOR EACH NEW RELEASE -->
* サービスパックは、アドビの[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip)からダウンロードできます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用して、オーサーインスタンスの 1 つに [!DNL Experience Manager] 6.5.21.0 をインストールします。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> アドビでは、[!DNL Experience Manager] 6.5.21.0 パッケージを削除またはアンインストールすることを推奨しません。したがって、パッケージをインストールする前に、ロールバックする必要がある場合に備えて `crx-repository` のバックアップを作成する必要があります。<!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### [!DNL Experience Manager] 6.5 へのサービスパックのインストール{#install-service-pack}

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。

1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip)からサービスパックをダウンロードします。<!-- UPDATE FOR EACH NEW RELEASE -->

1. パッケージマネージャーを開き、「**[!UICONTROL パッケージをアップロード]**」を選択して、パッケージをアップロードします。詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択して、「**[!UICONTROL インストール]**」を選択します。

1. S3 コネクタを更新するには、サービスパックのインストール後にインスタンスを停止し、既存のコネクタをインストールフォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。[Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログが終了することがあります。アドビでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。この問題は、通常 [!DNL Safari] ブラウザーで発生しますが、どのブラウザーでも断続的に発生する場合があります。

**自動インストール**

[!DNL Experience Manager] 6.5.21.0 のインストール方法は 2 つあります。<!-- UPDATE FOR EACH NEW RELEASE -->

* サーバーがオンラインで使用可能な場合、パッケージを `../crx-quickstart/install` フォルダーに配置します。パッケージが自動的にインストールされます。
* [パッケージマネージャーの HTTP API](/help/sites-administering/package-manager.md#package-share) を使用します。ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

>[!NOTE]
>
>Experience Manager 6.5.21.0 では、Bootstrap のインストールをサポートしていません。<!-- UPDATE FOR EACH NEW RELEASE -->

**インストールの検証**

このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

1. 製品情報ページ（`/system/console/productinfo`）の[!UICONTROL インストール済み製品]に、更新されたバージョン文字列 `Adobe Experience Manager (6.5.21.0)` が表示されます。<!-- UPDATE FOR EACH NEW RELEASE -->

1. すべての OSGi バンドルは、OSGi コンソールで **[!UICONTROL アクティブ]** または **[!UICONTROL フラグメント]** です（web コンソールを使用：`/system/console/bundles`）。

1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン 1.22.20 以降です（web コンソールを使用：`/system/console/bundles`）。<!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### [!DNL Experience Manager] Forms へのサービスパックのインストール{#install-aem-forms-add-on-package}

Experience Manager Forms にサービスパックをインストールする手順について詳しくは、[Experience Manager Forms サービスパックのインストール手順](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)を参照してください。

>[!NOTE]
>
>[AEM 6.5 クイックスタート](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)で使用できるアダプティブフォーム機能は、探索と評価のみを目的として設計されています。 アダプティブフォームの機能には適切なライセンスが必要なので、実稼動環境で使用する場合は、AEM Forms の有効なライセンスを取得することが不可欠です。

### Experience Manager コンテンツフラグメント用の GraphQL インデックスパッケージのインストール{#install-aem-graphql-index-add-on-package}

GraphQL を使用しているお客様は、[Experience Manager コンテンツフラグメントと GraphQL インデックスパッケージ 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=ja#package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip) をインストールする必要があります。

これにより、実際に使用する機能に基づいて、必要なインデックス定義を追加できます。

このパッケージをインストールしないと、GraphQL クエリが遅くなったり失敗したりする場合があります。

>[!NOTE]
>
>このパッケージは、インスタンスごとに 1 度だけインストールします。サービスパックごとに再インストールする必要はありません。

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.21.0 の UberJar は、[Maven Central リポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.21/)で入手できます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

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

* コンテンツフラグメント、サイト、ページのいずれかを移動、削除または公開しようとすると、コンテンツフラグメント参照が取得される際に問題が発生します。バックグラウンドクエリが失敗します。つまり、この機能が動作しなくなります。
正しく動作させるには、インデックス定義ノード `/oak:index/damAssetLucene` に次のプロパティを追加する必要があります（インデックスの再作成は不要です）。

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* [!DNL Experience Manager] インスタンスを 6.5.0 ～ 6.5.4 から Java™ 11 の最新サービスパックにアップグレードすると、`error.log` ファイルに `RRD4JReporter` 例外が表示されます。例外を停止するには、[!DNL Experience Manager] のインスタンスを再起動します。<!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* ユーザーは、[!DNL Assets] の階層内のフォルダーの名前を変更し、ネストされたフォルダーを [!DNL Brand Portal] に公開できます。ただし、ルートフォルダーが再公開されるまで、[!DNL Brand Portal] でフォルダーのタイトルは更新されません。

* [!DNL Experience Manager] 6.5.x.x のインストール中に、次のエラーや警告メッセージが表示される場合があります。
   * 「Target Standard API（IMS 認証）を使用して [!DNL Experience Manager] に Adobe Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。Target では、「エクスペリエンスフラグメント」／ソース「Adobe Experience Manager」タイプではなく、「HTML」／ソース「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MIN などの集計関数が使用される場合、アダプティブフォームのサーバー側検証が失敗します （CQ-4274424）。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューしている間、Dynamic Media インタラクティブ画像のホットスポットは表示されません。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]`：登録状況を未登録に変更する処理が完了するのを待機中にタイムアウトになりました。

* AEM 6.5.15 以降、```org.apache.servicemix.bundles.rhino``` バンドルで提供される Rhino JavaScript Engine には、新しい巻上げ動作が追加されました。strict モード（```use strict;```）を使用するスクリプトでは、正しい変数を宣言する必要があります。そうしないと、実行されず、ランタイムエラーがスローされます。

* 公式アップデートパッケージを通じてタグ付け関連の標準コンテンツをインストールすると、`/content/cq:tags` ノードの言語プロパティがデフォルトにリセットされます。このアクションは、サービスパック、セキュリティサービスパック、拡張機能パック、累積機能パック、パッチなどに当てはまります。したがって、インストール前にプロパティから追加しておく必要があります。

### AEM Sites の既知の問題 {#known-issues-aem-sites-6521}

* SITES-17934 - コンテンツフラグメント - 大きなフラグメントツリーに対する DoS 保護が原因でプレビューに失敗する。詳しくは、[GraphQL Query Executor のデフォルト設定オプションに関するナレッジベース記事](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-23945)を参照してください。

### AEM Forms の既知の問題 {#known-issues-aem-forms-6521}

* チェックボックスにスクリプトが埋め込まれた XDP に基づくアダプティブフォームでは、このようなチェックボックスの後の要素に対してスクリプトは実行されません。（FORMS-14244）
* Correspondence Management レターを作成できません。ユーザーがレターを作成すると、「`Object Object`」という説明のエラーが表示され、レターが作成されません。レイアウトのサムネールもレター作成画面に読み込めません。[最新の AEM 6.5 Form サービスパック 20（6.5.20.0）](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)をインストールすると、問題を解決できます。（FORMS-13496）
* インタラクティブ通信サービスでは PDF ドキュメントが作成されますが、フォームフィールドにはユーザーのデータが自動的に入力されません。事前入力サービスが期待どおりに動作しません。[最新の AEM 6.5 Form サービスパック 20（6.5.20.0）](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)をインストールすると、問題を解決できます。（FORMS-13413、FORMS-13493）
* 自動フォーム変換サービスのレビューと修正（RnC）エディターの読み込みに失敗します。[最新の AEM 6.5 Form サービスパック 20（6.5.20.0）](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)をインストールすると、問題を解決できます。（FORMS-13491）
* AEM 6.5 Forms サービスパック 18（6.5.18.0）または AEM 6.5 Forms サービスパック 19（6.5.19.0）から AEM 6.5 Forms サービスパック 20（6.5.20.0）に更新すると、JSP コンパイルエラーが発生します。アダプティブフォームを開いたり作成したりすることができず、ページエディター、AEM Forms UI、AEM ワークフローエディターなどの他の AEM インターフェイスでエラーが発生します。[最新の AEM 6.5 Form サービスパック 20（6.5.20.0）](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)をインストールすると、問題を解決できます。（FORMS-13492）
* 編集／表示パターンを持つフィールドのポップアップウィジェットで月をトラバースすると、日付選択ウィジェットの行が切り捨てられます。（FORMS-13620）
* バックエンドで DOR（レコードのドキュメント）サービスを使用しようとすると、フォームの送信が失敗します。「フォームリソースが正しく割り当てられていないので、送信アクションを完了できませんでした」というエラーメッセージが表示されます。（FORMS-13798）
* アダプティブフォームを Adobe Experience Manager パブリッシュインスタンスから Adobe Experience Manager ワークフローに送信すると、ワークフローでは添付ファイルの保存に失敗します。（FORMS-14209）
* AEM 6.5 Forms サービスパック 20 パッケージ（SP20 用の AEM Forms アドオンパッケージ）をインストールすると、AEM Sites ユーザーインターフェイス（UI）のパフォーマンスが大幅に低下します。（FORMS-13791）
* インタラクティブ通信で null ポインターの例外が発生して、事前入力サービスが失敗します。（CQDOC-21355）
* アダプティブフォームでは、ECMAScript バージョン 5 以前でカスタム関数を使用できます。カスタム関数で ECMAScript バージョン 6 以降（`let`、`const`、アロー関数など）が使用されている場合、ルールエディターが正しく開かない可能性があります。

## 含まれている OSGi バンドルとコンテンツパッケージ{#osgi-bundles-and-content-packages-included}

次のテキストドキュメントには、この [!DNL Experience Manager] 6.5 サービスパックリリースに含まれている OSGi バンドルとコンテンツパッケージのリストが記載されています。

* [Experience Manager 6.5.21.0 に含まれている OSGi バンドルのリスト](/help/release-notes/assets/65210-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.21.0 に含まれているコンテンツパッケージのリスト](/help/release-notes/assets/65210-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 制限付き Web サイト{#restricted-sites}

以下の web サイトはお客様のみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/ja/docs/customer-one/using/home)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/jp/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-65)
>* [アドビ製品アップデートの優先通知を購読](https://www.adobe.com/subscription/priority-product-update.html)
