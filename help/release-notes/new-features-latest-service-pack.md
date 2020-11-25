---
title: Adobe Experience Manager6.5 Service Pack 7の新機能
description: Adobe Experience Manager6.5 Service Pack 7の新機能
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 34e41cf5984f5f69ae0ccead137fe4f180bd84ad
workflow-type: tm+mt
source-wordcount: '2705'
ht-degree: 5%

---


# Adobe Experience Manager6.5 Service Pack 7の新機能 {#aem-whats-new-service-pack}

![新機能](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5サービスパックは、新機能、お客様から要望を受けた機能強化、パフォーマンス、安定性、セキュリティの向上を四半期ごとに提供します。 四半期ごとの可用性により、新機能や革新性に容易にアクセスし、導入できます。

この記事では、最新の6.5 Service Packに含まれる機能、以前の6.5 Service Packに含まれる [主な機能](#key-features-previous-service-packs)、最後のService Pack [リリース以降の](#key-releases-since-last-sp) 主要なAEMリリースについて説明します。

## アドビ [!DNL Experience Manager Sites] {#aem-sites}

### 展開に使用できるライブコピーページを並べ替え {#sort-livecopy-pages}

[ [!UICONTROL 名前]]、[ [!UICONTROL 最終変更日]]、[ [!UICONTROL 最終ロールアウト日] ]の各プロパティを使用して、ロールアウト可能なライブコピーページを並べ替えることができるようになりました。 ページの [!UICONTROL 最終ロールアウト日] は、このリリースで導入された新しいプロパティです。

### ページの移動とMSMロールアウトを非同期操作として使用できる {#page-moves-msm-asynchronous}

これで、ページの移動およびMSMロールアウトを非同期操作として実行でき、実行時のパフォーマンスへの影響を軽減できます。 操作を即時に実行するか、後で実行するかをスケジュールできます。 関連するジョブとプロセスステップのステータスがコンソールに表示され、大規模なMSMロールアウトを監視する場合に便利です。

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* カードと列の表示ーでデジタルアセットを並べ替えることができます。

* [!DNL Assets] アクセシビリティを [!DNL Dynamic Media] 強化しました。 強化された機能は、キーボードナビゲーション、スクリーンリーダーの使用、支援テクノロジー(AT)の使用を可能にする機能強化と似ています。 詳しくは、 [アセットの機能強化](/help/release-notes/sp-release-notes.md#assets-6570) および [[!DNL Dynamic Media] 拡張を参照してください](/help/release-notes/sp-release-notes.md#dynamic-media-6570)。 <!-- TBD: Add link to a11y article after go-live. Adding RN link for now. -->

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>[!DNL Experience Manager Forms] アドオンパッケージは、予定されている [!DNL Experience Manager] Service Packのリリースの1週間後に公開されます。 [!DNL Experience Manager] 6.5 Service Pack 7(6.5.7.0)は、2020年11月27日にリリースされる予定です。

## 以前の [!DNL Experience Manager] 6.5サービスパックの主な機能 {#key-features-previous-service-packs}

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### 非同期モードでのPage Move操作の可用性(6.5.6.0) {#page-move-asynchronous}

「ページ移動」操作を非同期モードで使用できるようになりました。 即時実行に加えて、後で実行できるようにPage Move操作をスケジュールすることもできます。

#### アクセシビリティの向上(6.5.5.0) {#accessibility-sites}

* テキスト情報を追加してエラーレポートを改善。

* キーボードナビゲーション中のユーザーインターフェイスのフォーカスを改善。

* 様々なユーザーインターフェイス要素のコントラスト比が改善されました。

* ページ画像の代替属性の一貫性が向上しました。

* アクセシブルなリッチインターネットアプリケーション(ARIA)のラベルの一貫性が向上しました。

* Non-Visual Desktop Access(NVDA)機能を改善。

* スクリーンリーダーのサポートが強化されました。

#### その他の主な機能強化(6.5.5.0) {#other-enhancements-sites}

* CRXDE Liteへの匿名アクセスは、セキュリティを強化するために許可されていません。 代わりに、ユーザーはログイン画面に誘導されます。 See [Developing with CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* ページツリーをコピーまたは貼り付けるときに、ルートページを貼り付けるか、ルートページをツリーのサブページと共に貼り付けるかを選択できるようになりました。

* [!DNL Adobe Experience Manager Experience Fragments] ワークスペースに書き出したデータは、 [!DNL Adobe Target] で一意のオファータイプとオファーソースとして表示されるようにな [!DNL Target]りました。

* マルチサイトマネージャ — コンポーネントがソースページから削除されている場合、発行トリガーによって、発行済みページからコンポーネントが削除されるようになりました。

* マルチサイトマネージャ — [!UICONTROL ライブコピーのローカルコンポーネントの名前が設計図のコンポーネントの名前と同じで]`_msm_moved` 、コンポーネントが設計図からロールアウトされた場合、ローカルコンポーネントの名前にキーワードが追加されます。

#### スタイルシステムの拡張(6.5.4.0) {#style-system-enhancements}

拡張スタイルシステムを使用して、コンポーネントダイアログ内のスタイルを選択できるようになりました。

#### 様々な領域でのパフォーマンスの向上(6.5.4.0) {#performance-improvements}

* サイト内でContextHubを読み込んで初期化する時間を短縮しました(`contexthub.kernel.js`)。 サイト訪問中のページ読み込みが速くなります。

* ページエディターにドラッグした後にページを更新する時間 [!DNL Experience Fragments] を短縮し [!DNL Sites] ました。

* ライブコピーの概要で200を超えるライブコピーを含む [!DNL Sites] ページへのエントリの読み込み時間を短縮し **[!UICONTROL ました]**。

* 不完全または無効なURLの処理を改善。 このようなURLを使用すると、テンプレートエディターの動作が遅くなる場合があります。

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

#### Accessibility enhancements (6.5.6.0) {#accessibility-assets-6560}

* **キーボードナビゲーション中のユーザーインターフェイスフォーカスの強化(例**:

   * `x` アイコン( [!UICONTROL Versionプレビューダイアログ内)] 。 [!UICONTROL タイムライン内のアセット]。

   * 対応可能なユーザーインターフェイスオプション。

   * リンクを [!UICONTROL 共有] ダイアログの電子メールフィールド、およびフォルダー [!UICONTROL プロパティの「権限] 」タブで閉じたユーザーグループを追加するフィールド 。

* **キーボードキーを使用した機能の強化**

   スクリーンリーダーのブラウズモードでは、キーボードキーを使用して、メタデータスキーマフォームエディターのコントロールをドラッグできます。

* **次の点が理由で、スクリーンリーダーユーザーの使い勝手が向上しました**。

   * スクリーンリーダーは、ビデオプレーヤーとオーディオプレーヤーの目的を読み上げます。

   * スクリーンリーダーは、アセット [!UICONTROL プロパティのタグ選択ダイアログを使用して選択したタグを削除するための、ユーザーインターフェイスオプションの目的を読み上げます]。

   * スクリーンリーダーはテーブルの行ヘッダーと行項目を読み上げるので、ユーザーは同じ行に属するエントリを把握できます。

   * 検索ページのわかりやすいページタイトル。

   * スクリーンリーダーは、検索フィルターパネルのオプションを拡大可能なアコーディオンとして読み上げます。

#### (6.5.6. [!DNL Assets] 0)でのその他の機能強化 {#other-enhancements-assets-6560}

* フォルダーに関連付けられているユーザーグループ（プライベートおよび非プライベート）は、それらのフォルダーの [削除時にリポジトリから削除されるようになりました](/help/assets/private-folder.md#delete-private-folder)。 ただし、既存の冗長、親なし、未使用、自動生成のユーザーグループは、JMXを使用してリポジトリから削除できます。

#### アクセシビリティの強化( [!DNL Assets] 6.5.5.0) {#assets-accessibility}

[!DNL Experience Manager Assets] は、Webコンテンツアクセシビリティガイドライン(WCAG)に準拠してアクセシビリティを強化しました。 次の機能強化により、アクセシビリティが向上しました。

* 多くのユーザーインターフェイス要素、コントロール、ページ、ダイアログは、スクリーンリーダーに適しています。

* 多くのユーザーインターフェイス要素、コントロール、入力フォームフィールドには、キーボードを使用してアクセスできます。

* 一部のユーザインターフェイス要素の色とコントラストが更新され、視覚が限られたユーザや、色の知覚を持たないユーザが、これらのユーザインターフェイス要素を区別できるようになりました。For example, the color of star rating icons (such as in [!UICONTROL Rating] section of [!UICONTROL Advanced] tab in asset [!UICONTROL Properties] or in card view) is changed for appropriate contrast.

   ![コントラストが向上した評価アイコン](assets/star-rating-icons.png)

#### 拡張された例外処理(6.5.5.0) {#exception-handling}

[!DNL Assets] ユーザーインターフェイスフローの例外処理が改善されました。 アセットのディメンションにタイプが指定されていない場合、監視対象の例外がログファイルに記録されます。

#### 3Dアセットのサポート( [!DNL Dynamic Media] 6.5.5.0) {#support-for-3d}

での3D画像のサポートにより、ユーザーは3Dコンテンツを公開し、Webページやアプリケーションに追加で [!DNL Dynamic Media] きます。 次のサポートが含まれます。

* 共通の3Dアセット形式を公開し、Webページや他のアプリケーションで使用できるアセットURLを生成します。

* パブリッシュした3Dアセットをインタラクティブに表示す [!DNL Adobe Dimension]るための3D Web Viewer。

* WCMコンポーネントを使用して、 [!DNL Experience Manager Sites] ページ上の共通3Dアセットをパブリッシュおよび表示し [!DNL Sites] ます。

#### 次 [!DNL Experience Manager Assets] で設定 [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

との間の認証チャネル [!DNL Experience Manager Assets] が変更 [!DNL Brand Portal] されます。 Earlier, [!DNL Brand Portal] was configured in Classic UI via Legacy OAuth Gateway, which uses the JWT token exchange to obtain an IMS Access token for authorization. [!DNL Experience Manager Assets] は、テナントの認証のためにIMSトークンを取得する、 [!DNL Brand Portal] AdobeI/O経由で設定されるようにな [!DNL Brand Portal] りました。

The steps to configure [!DNL Experience Manager Assets] with [!DNL Brand Portal] are different depending on your [!DNL Experience Manager] version, and whether you are configuring for the first time, or upgrading the existing configurations. See [Configure Experience Manager Assets with Brand Portal](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) for details.

#### Accessibility enhancements (6.5.4.0) {#accessibility-enhancements}

[!DNL Experience Manager Assets] には、次のアクセシビリティの強化が含まれています。

* キーボードの矢印キーを使用して、ズームされた画像内の領域を移動およびパンできます。 詳しくは、キーボードキーのみを使用した [プレビューアセットを参照してください](../assets/manage-assets.md#previewing-assets)。

* フィルターパネル内の混在状態のチェックボックス（ネストされた述語のすべてを選択しない限り、最初のレベルのチェックボックスは選択されず、完全に読み取られます）は、スクリーンリーダーで読み取り可能です。

* 日付と時間の形式に関する制約が日付フィールドのフィールドラベルに設けられ、ユーザーがキーボードを使用して正しい形式で日付を入力できるようになっています。
例えば、`On Time (MM-DD-YYYY HH:mm)` のようになります。MMは2桁の形式の月、YYYYは年、DDは2桁の形式の日、HHは24時間の軍事形式の時、mmは分です。

* スクリーンリーダーは、選択したタグ(`X` 記号)と選択したタグの数を削除するオプションを読み上げます。

#### リスト表示の「作成日」の並べ替え可能な列(6.5.3.0) {#sortable-date-created-column}

作成したアセットの日付の並べ替えが可能な新しい列が、DAMリスト表示およびリスト表示のアセット検索結果に追加されます。

![作成日の並べ替え可能な列](assets/asset-created-date.png)

#### Visual Search for [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets] ユーザーは、視覚的に類似した画像を検索できます。Experience Managerは、ユーザーが選択した画像に類似した、DAMリポジトリのスマートタグ付け画像を表示します。 See [Visual search](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### CDNキャッシュコンテンツの無効化(6.5.6.0) {#invalidate-cdn-cached-content}

ユーザーインターフェイスを使用して、コンテンツ配信ネットワーク(CDN)のキャッシュされたコンテンツを無効にできるようになりました。 [!DNL Dynamic Media] その結果、キャッシュの期限が切れるのを待つ代わりに、更新されたアセットを即座に使用できます。 CDNは次の方法で無効にできます。

* CDN無効化テンプレートの作成：アセットとフォームに関連付けられたテンプレートベースのURLの選択

* アセット選択を使用したアセットと関連プリセットの選択

* 完全なアセットURLの追加

#### アセットの一部のみ [!DNL Experience Manager] および [!DNL Dynamic Media] (6.5.6.0) {#selective-publishing}

アセットを選択して発行または非公開にするか、クイック発行 [!DNL Experience Manager] ウィザード [!DNL Dynamic Media] またはパブリケーション  管理ウィザードを使用して選択的に発行または非公開にできるようになりました。 また、フォルダーレベルで `Publish` または `Unpublish` モードを設定することもできます。

#### ダイナミックメディア向けスマートイメージング {#smart-imaging}

スマートイメージングでは、各ユーザー固有の視聴特性を使用して、エクスペリエンスに最適化された適切な画像を自動的に提供し、パフォーマンスとエンゲージメントを向上させます。 スマートイメージングは、既存の画像プリセットで機能し、配信の直前にインテリジェンスを使用して、ブラウザーまたはネットワークの接続速度に基づいて画像のファイルサイズをさらに低減します。詳しくは、 [スマートイメージングを参照してください](../assets/imaging-faq.md)。

#### ダイナミックメディア用のビデオプロファイルでのスマート切り抜き(6.5.3.0) {#smart-crop-video}

ビデオのスマート切り抜き（ビデオプロファイルで使用できるオプション機能）は、Adobe Sensei の人工知能機能を使用して、サイズに関係なく、アップロードしたアダプティブビデオやプログレッシブビデオの重要な部分を自動的に検出して切り抜くツールです。See [About using smart crop in video profiles](../assets/video-profiles.md).

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### クライアントでのアダプティブフォームの事前入力(6.5.6.0) {#prefill-merge-data-at-client}

アダプティブフォームに事前入力すると、 [!DNL Experience Manager Forms] サーバーはデータをアダプティブフォームにマージし、入力済みのフォームをユーザーに配信します。 デフォルトでは、データの結合アクションはサーバーで実行されます。
これで、サーバーではなく、クライアントで [!DNL Experience Manager Forms] データの結合操作を [実行するように](../../help/forms/using/prepopulate-adaptive-form-fields.md) サーバーを設定できます。 これにより、アダプティブフォームの事前入力とレンダリングに要する時間が大幅に短縮されます。

#### 双方向SSL実装(6.5.6.0)を使用したサーバー上のRESTful APIとフォームデータモデルを統合 {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] フォームデータモデルは、双方向SSLが実装されたサーバー上のRESTful APIと [統合できるようになりました](../../help/forms/using/configure-data-sources.md)。

#### automated forms conversionサービス(6.5.6.0)の [!DNL Adobe Sign] テキストタグのサポートを追加しました。 {#sign-integration-acroform-afcs}

AcroFormに [!DNL Adobe Sign] テキストタグが含まれる場合、これらのフィールドが認識され、を使用して変換されたアダプティブフォームでフ [!DNL Adobe Sign] ィールドとして表されるようになり [!DNL Automated Forms Conversion service]ました。 署名者は、アダプティブフォームの署名時にこのようなフィールドに入力できます。

#### Support to convert colored PDF forms to adaptive forms (6.5.6.0) {#colored-PDF-forms}

を使用して、色付きPDF forms [!DNL Automated Forms Conversion service] をアダプティブフォームに変換できます。

#### SMB 2およびSMB 3プロトコル(6.5.6.0)のサポート {#smb-support}

[!DNL Experience Manager Forms] 現在は、SMB 2およびSMB 3プロトコルをサポートしています。

#### 翻訳済みアダプティブフォームページのキャッシュの強化(6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

アダプティブフォームURLの引数の代わりに、アダプティブフォームURLのセレクターとして [ロケールを指定できるようになりました](../../help/forms/using/supporting-new-language-localization.md)。 変換済みのアダプティブフォームをにキャッシュするのに役立ち [!DNL Experience Manager Dispatcher]ます。 変換済みのアダプティブフォームは、以前のバージョンではキャッシュできませんでした。 アダプティブフォームURLでロケールをセレクターとして使用するためのキャッシュの設定について詳しくは、「ディスパッチャーでのアダプティブフォームのキャッシュの [設定](../../help/forms/using/configure-adaptive-forms-cache.md)」を参照してください。

#### フォームデータモデルサービスの出力を変数に保存(6.5.6.0) {#save-fdm-service-to-variable}

フォームデータモデルを使用すると、フォームデータモデルサービスの出力を変数に保存できます。 [!DNL Experience Manager Forms] フォームデータモデルサービスの型を変数の型に自動的にマッピングするようになりました。

#### 添付ファイルコンポーネント用の複数のファイルの添付(6.5.6.0) {#attach-multiple-files}

アダプティブフォームの添付ファイルコンポー [ネントに](../../help/forms/using/introduction-forms-authoring.md) 、複数のファイルを添付できるようになりました。

#### 「Adobe Experience Managerインボックス」列のカスタマイズ(6.5.5.0) {#customize-aem-inbox-columns}

受信トレイをカスタマイズして、 [!DNL Experience Manager] 列の既定のタイトルを変更したり、列の位置を並べ替えたり、ワークフローのデータに基づいて追加の列を表示したりできます。 またはグループのメンバ `administrators``workflow-administrators` ーは、列をカスタマイズできます。 詳しくは、「 [管理コントロール](../sites-authoring/inbox.md#inbox-admin-control)」を参照してください。

![Experience Manager受信トレイ列のカスタマイズ](assets/customize-columns.gif)

#### Interactive Communicationsをドラフトとして保存(6.5.5.0) {#save-as-draft}

エージェントUIを使用して、各対話型通信用の1つ以上のドラフトを保存し、後でドラフトを取得して、そのドラフトの操作を続行できます。 ドラフトごとに異なる名前を指定して、ドラフトを識別できます。 詳しくは、「 [Save Interactive Communications as a draft](../forms/using/prepare-send-interactive-communication.md#save-as-draft)」を参照してください。

![ドラフトとして保存](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] アプリケーションサーバーのサポート(6.5.5.0) {#weblogic-support}

Adobe Experience Manager FormsはJEEでAdobe Experience Manager Forms [!DNL Oracle WebLogic 12] の支援を追加しました。 以前のバージョンからアップグレードするか、12.2.1.4以降のJEEサーバー上に新しいExperience Manager6.5Formsを設定す [!DNL Oracle WebLogic] ることができます。 後で、マイナーバージョンの変更に対応します。12.2.1.xのxはバージョン番号に置き換えられます。

#### アクセシビリティの向上(6.5.5.0) {#accessibility-improvements}

Adobe Experience Manager Formsでは、次のアクセシビリティの強化が行われました。

* アダプティブフォームをHTMLフォームとしてプレビューした場合、「 [!UICONTROL 手書き署名] 」フィールドはタブのフォーカスを保持します。

* アダプティブフォームの送信時に表示されるエラーメッセージに、属性が含まれるようにな `aria-describedBy` りました。 属性は、エラーメッセージで参照されるフィールドに添付されます。 属性は、オブジェクトを記述する要素のIDを示します。 `aria-describedby` ウィジェットまたはグループと、それらを説明するテキストとの間の関係を確立するのに役立ちます。

* アダプティブフォームに必須フィールドが含まれている場合、ARIAアクセシビリティスキーマでは、このようなフィールド `True` の必須属性はに設定されます。

#### フォームデータモデル(6.5.5.0)におけるSOAPベースのWebサービス用のX-509証明書ベースの認証 {#x509-based-authentication-soap}

フォームデータモデルで、SOAP Webサービスをデータソースとして使用している場合に、X-509証明書ベースの認証がサポートされるようになりました。 詳しくは、「SOAP Webサービスの [設定](../forms/using/configure-data-sources.md#configure-soap-web-services)」を参照してください。

#### その他の主な改善点(6.5.5.0) {#other-improvements}

* JEE上のExperience Manager6.5Formsドキュメントセキュリティがに基づくようになり [!DNL Apache Struts 2]ました。

* のサポートを追加し [!DNL Oracle Real Applications Cluster (RAC) 19c]ました。

#### Experience ManagerFormsワークフローでの印刷可能出力の生成(6.5.4.0) {#generate-printable-output}

印刷可能出力の生成ワークフローステップでは、ソーステンプレートファイルをデータファイルと統合できます。 この統合により、テンプレートファイルの別のコピーを印刷または保存できます。 このステップで、PCL、PostScript、ZPL、IPL、TPCLまたはDPL出力が生成されます。 この機能について詳しくは、『OSGiでの [Forms中心のワークフロー — 手順リファレンス](../forms/using/aem-forms-workflow-step-reference.md)』を参照してください。

![印刷可能な出力を生成](assets/generate-print-output-step.gif)

#### レイアウトモードでのアダプティブフォームとインタラクティブな通信の複数列のサポート(6.5.4.0) {#multi-column-adaptive-forms}

アダプティブフォームとインタラクティブな通信で、パネルの列数を定義できるようになりました。 レイアウトモードに切り替えて、新しい複数列オプションを使用します。 詳しくは、レイアウトモードを [使用してコンポーネントのサイズを変更するを参照してください](../forms/using/resize-using-layout-mode.md)。

![複数列のレイアウト](assets/multi-column-layout.gif)

#### Experience Managerインボックスのカスタマイズ(6.5.4.0) {#aem-inbox}

新しい「管理コントロール」オプションを使用すると、管理者は次のことができます。

* ヘッダーのテキストとロゴをカスタマイズします。

* ヘッダーで使用できるナビゲーションリンクの表示を制御します。

「管理者コントロール」オプションは、 `administrators` またはグループのメンバーにのみ表示され `workflow-administrators` ます。 この機能の詳細については、「受信トレイ [](../sites-authoring/inbox.md)」を参照してください。

#### HTML5フォームでのリッチテキストのサポート(6.5.4.0) {#rich-text-support}

XFAフォームのテキストフィールドをHTML5フォームのリッチテキストフィールドに変換します。 詳しくは、「HTML5フォーム用のフォームテンプレートの [デザイン](../forms/using/designing-form-template.md)」を参照してください。

#### Accessibility enhancements (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience ManagerFormsには、次のアクセシビリティの強化が含まれています。

* スクリーンリーダーは、アダプティブフォームで、チェックボックス、リンク、日付選択、日付入力の各フィールドについて正しく読み上げます。

* アダプティブフォームの各ページに、1つのタイトルと1つのメインのランドマークラベルが含まれるようになりました。

#### Experience ManagerFormsユーザーのインボックスアイテムの共有およびリクエスト(6.5.3.0) {#share-request-access}

受信トレイの項目を他のユーザーと共有できます。 別のユーザーが受信トレイのアイテムにアクセスできるようになると、そのユーザーは共有アイテムに対して適切なアクションを実行できます。 同様に、他のユーザーからインボックス項目へのアクセスを要求することもできます。 詳しくは、ユーザーのインボックスアイテムの [共有およびアクセスの要求を参照してください](../forms/using/configure-shared-queues-osgi.md)。

#### Experience ManagerのFormsユーザー(6.5.3.0)のインボックス項目の不在設定の構成 {#configure-out-of-office}

不在にする予定がある場合は、その期間に割り当てられたアイテムに対する処理を指定できます。
不在設定が実施される開始日と時刻および終了日と時刻を指定するオプションがあります。すべてのアイテムを送信するデフォルトのユーザーを設定できます。 「不在設定の [設定](../forms/using/configure-out-of-office-settings.md)」を参照してください。

#### Experience ManagerForms用のBatch APIを使用して複数の対話型通信を生成する(6.5.3.0) {#generate-multiple-ic}

Batch APIを使用すると、テンプレートから複数のインタラクティブな通信を作成できます。 テンプレートは、データを一切使用しないインタラクティブな通信です。 Batch APIは、データとテンプレートを組み合わせてインタラクティブな通信を行います。 このAPIは、インタラクティブ通信の大量生産に役立ちます。 例えば、電話料金、複数の顧客のクレジットカード明細などです。 Batch APIを使用した複数の対話型通信の [生成を参照してください](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

## Adobe Experience Manager6.5 SP6以降の主なリリース {#key-releases-since-last-sp}

2020年9月3日～ 2020年11月26日の間に、Adobeは、サービスパックおよび累積修正パックに加え、次の機能をリリースしました。

* [!DNL Adobe Experience Manager] をCloud Service2020.9.0 [と2020.10.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-2020-9-0.html?lang=en#release-notes)[として設定する必要があります](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-2020-10-0.html?lang=en#release-notes)。

* [[!DNL Experience Manager] デスクトップアプリ2.0 (2.0.3.2)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html)。

* [WKNDリファレンスサイト — 0.0.6](https://github.com/adobe/aem-guides-wknd/releases/tag/aem-guides-wknd-0.0.6)

* [Experience Manager Screens:機能パック202008](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202008.html)

* [Adobeアセットリンクv2.2](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html)

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] 6.5ドキュメント](../user-guide/home.md)
>* [6. [!DNL Adobe Experience Manager] 5の一般的なリリースノート](release-notes.md)
>* [Service Packリリースノート [!DNL Adobe Experience Manager] 6.5](sp-release-notes.md)

