---
title: Adobe Experience Manager 6.5 Service Pack 5の新機能
description: Adobe Experience Manager 6.5 Service Pack 5の新機能
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: cc423a199e860429e85895690f6c1a81c20d1a19
workflow-type: tm+mt
source-wordcount: '1853'
ht-degree: 12%

---


# What&#39;s new in AEM 6.5 Service Pack 5 {#aem-whats-new-service-pack-5}

Adobe Experience Manager 6.5のサービスパックは、新機能、お客様から要請された機能強化、パフォーマンス、安定性に関する改善を四半期ごとに提供します。 四半期別配信モデルを使用すると、新機能や革新的な機能に簡単にアクセスし、導入できます。

この記事では、最新の6.5 Service Packに含まれる機能、以前の6.5 Service Packに含まれる [主な機能](#key-features-previous-service-packs)、Experience Manager 6.5.4.0 [リリース以降の](#key-features-sice-sp3) 主なリリースの一部について説明します。

## AEM Sites {#aem-sites}

### アクセシビリティの強化 {#accessibility-sites}

* テキスト情報を追加してエラーレポートを改善

* キーボードナビゲーション中のUIフォーカスの改善

* テキストのコントラストの改善（輝度比）

* ページ画像の代替属性の一貫性の向上

* アクセシブルなリッチインターネットアプリケーション(ARIA)ラベルの一貫性の向上

* Non-Visual Desktop Access(NVDA)機能の改善

* スクリーンリーダーのサポートの強化

### その他の主な機能強化 {#other-enhancements-sites}

* ページツリーをコピーまたは貼り付けるときに、ルートページを貼り付けるか、ルートページをツリーのサブページと共に貼り付けるかを選択できるようになりました。

* Adobeターゲットワークスペースに書き出されたAEMエクスペリエンスフラグメントは、で一意のオファータイプおよびオファーソースとして表示されるようになり [!DNL Target]ました。

* マルチサイトマネージャ — 発行トリガーは、コンポーネントがソースページから削除された場合に、発行済みページからコンポーネントを正常に削除するようになりました。

* マルチサイトマネージャー — LiveCopyのローカルコンポーネントの名前がブループリントのコンポーネントの名前と同じで、コンポーネントがブループリントからロールアウトされた場合、ローカルコンポーネントの名前に_msm_movedという用語が正常に追加されました。

## AEM Assets {#aem-assets}

### アセットのアクセシビリティの強化 {#assets-accessibility}

[!DNL Adobe Experience Manager] Webコンテンツアクセシビリティガイドライン(WCAG)に準拠して、アセット機能にアクセスしやすくなりました。 アクセシビリティは、次の領域で改善されました。

* ユーザーインターフェイスの要素、コントロール、ページ、ダイアログは、スクリーンリーダーに適しています。

* ユーザーインターフェイスの要素、コントロールおよび入力フォームのフィールドには、キーボードを使用してアクセスできます。

* 一部のグラフィックの色とコントラストの変更。視覚や色の知覚が限られているユーザーによって、区別できるようになります。 例えば、星レーティングアイコンの色(アセットのプ [!UICONTROL ロパティの「] 詳細」タブの「レーティング [!UICONTROL 」セクションやカードの] 表示など  )は、適切なコントラストに合わせて変更されます。

![コントラストを改善するために変更された星評価アイコンの色](assets/star-rating-icons.png)

### 例外処理の強化 {#exception-handling}

アセットユーザーインターフェイスのフローの例外処理が改善されました。 以前は、アセットのディメンションに適切なタイプがなかった場合、ログ内のトレースなしでサイレントにキャッチされた例外が観察されていました。 この動作は変更され、すべての例外がログに記録されます。

## [!DNL Dynamic Media] {#dynamic-media}

### 3Dサポート [!DNL Dynamic Media] {#support-for-3d}

の3Dサポートにより、3Dコンテンツを投稿してWebページやアプリケーションに追加できるようにな [!DNL Dynamic Media] りました。 以下が含まれます。

* 共通の3Dアセット形式を公開して、アセットURLを生成する。

* Adobe Dimensionを利用した、Viewerライブラリで使用可能な新しい3D Web Viewerを使用した、パブリッシュ済みの3Dアセットのインタラクティブな表示。 [!DNL Dynamic Media]

* WCMコンポーネントを使用した3Dパブリッシングと [!DNL Experience Manager Sites][!DNL Sites] ページでの表示。

## AEM Forms {#aem-forms}

### AEMインボックスの列のカスタマイズ {#customize-aem-inbox-columns}

AEMインボックスをカスタマイズして、列のデフォルトタイトルの変更、列の位置の並べ替え、ワークフローのデータに基づいた追加の列の表示を行うことができます。 お客様は、列をカスタマイズする `administrators` または `workflow-administrators` グループのメンバーである必要があります。

![AEMインボックスの列のカスタマイズ](assets/customize-columns.gif)

### 対話型通信をドラフトとして保存 {#save-as-draft}

エージェントUIを使用して、各対話型通信用の1つ以上のドラフトを保存し、後でドラフトを取得して、そのドラフトの操作を続行できます。 ドラフトごとに異なる名前を指定して、簡単に識別できます。

![ドラフトとして保存](assets/save-as-draft.gif)

### [!DNL Oracle WebLogic] アプリケーションサーバーサポート {#weblogic-support}

AEM Formsでは、JEE上のAEM Formsのサポート [!DNL Oracle WebLogic 12] が追加されました。 以前のバージョンからアップグレードすることも、12.2.1.4以降で新しいJEE上のAEM 6.5 Formsサーバーを設定するこ [!DNL Oracle WebLogic] ともできます。 後で、マイナーバージョンの変更に対応します。12.2.1.xのxはバージョン番号に置き換えられます。

### アクセシビリティの強化 {#accessibility-improvements}

AEM Formsのアクセシビリティの強化は次のとおりです。

* アダプティブフォームをHTMLフォームとしてプレビューした場合、「 [!UICONTROL 手書き署名] 」フィールドはタブのフォーカスを保持します。

* アダプティブフォームの送信時に表示されるエラーメッセージに、属性が含まれるようにな `aria-describedBy` りました。 属性は、エラーメッセージで参照されるフィールドに添付されます。 属性は、オブジェクトを記述する要素のIDを示します。 `aria-describedby` ウィジェットまたはグループと、それらを説明するテキストとの間の関係を確立するのに役立ちます。

* アダプティブフォームに必須フィールドが含まれている場合、ARIAアクセシビリティスキーマでは、このようなフィールド `True` の必須属性はに設定されます。

### フォームデータモデルのSOAPベースWebサービス用のX-509証明書ベースの認証 {#x509-based-authentication-soap}

フォームデータモデルで、SOAP Webサービスをデータソースとして使用している場合に、X-509証明書ベースの認証がサポートされるようになりました。

### その他の主な改善点 {#other-improvements}

* JEE上のAEM 6.5 Formsドキュメントセキュリティがに基づくようになり [!DNL Apache Struts 2]ました。

* のサポートを追加し [!DNL Oracle Real Applications Cluster (RAC) 19c]ました。

## 以前のAEM 6.5サービスパックの主な機能 {#key-features-previous-service-packs}

### AEM Sites {#aem-sites-previous-service-packs}

#### スタイルシステムの拡張(6.5.4.0) {#style-system-enhancements}

拡張スタイルシステムを使用して、コンポーネントダイアログ内のスタイルを選択できるようになりました。

#### 様々な領域でのパフォーマンスの向上(6.5.4.0) {#performance-improvements}

* サイト内でのContextHubの読み込みと初期化に要する時間が短縮されました(`contexthub.kernel.js`)。 サイト訪問中のページ読み込みが速くなります。

* エクスペリエンスフラグメントをサイトページエディターにドラッグした後にページを更新する時間を短縮しました。

* ライブコピーの概要で200を超えるライブコピーがあるサイトページのエントリの読み込み時間を短縮 **[!UICONTROL しました]**。

* 不完全または無効なURLの処理を改善。 このようなURLを使用すると、テンプレートエディターの動作が遅くなる場合があります。

### AEM Assets {#aem-assets-previous-service-packs}

#### Configure AEM Assets with Brand Portal (6.5.4.0) {#configure-assets-bp}

AEM AssetsとBrand Portal間の認証チャネルが変更されました。 これまで、Brand Portal は、旧来の OAuth ゲートウェイを通じてクラシック UI で設定されていました。このゲートウェイは、JWT トークン交換を使用して認証用の IMS アクセストークンを取得します。AEM Assets と Brand Portal の連携が、Adobe I/O を通じて設定されるようになりました。Adobe I/O が Brand Portal テナントの認証用の IMS トークンを取得します。

Brand PortalでAEM Assetsを設定する手順は、AEMのバージョン、および初回の設定か既存の設定のアップグレードかによって異なります。 詳しくは、[AEM Assets と Brand Portal の連携の設定](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)を参照してください。

#### Accessibility enhancements (6.5.4.0) {#accessibility-enhancements}

Experience Manager Assetsには、次のアクセシビリティの強化が含まれています。

* キーボードの矢印キーを使用して、ズームされた画像内の領域を移動およびパンできます。 詳しくは、キーボードキーのみを使用した [プレビューアセットを参照してください](../assets/managing-assets-touch-ui.md#previewing-assets)。

* フィルターパネル内の混在状態のチェックボックス（ネストされた述語のすべてを選択しない限り、最初のレベルのチェックボックスは選択されず、完全に読み取られます）は、スクリーンリーダーで読み取り可能です。

* 日付と時間の形式に関する制約が日付フィールドのフィールドラベルに設けられ、ユーザーがキーボードを使用して正しい形式で日付を入力できるようになっています。

   例えば、`On Time (MM-DD-YYYY HH:mm)` のようになります。MMは2桁の形式の月、YYYYは年、DDは2桁の形式の日、HHは24時間の軍事形式の時、mmは分です。

* 現在選択されているタグを削除するボタンの `X` 記号が、選択されているタグの数と共に、スクリーンリーダーによって通知されるようになりました。

#### AEM Assetsのビジュアル検索(6.5.2.0) {#visual-search}

Assets ユーザーは、視覚的に類似した画像を検索できます。AEM は、ユーザーが選択した画像に類似した、DAM リポジトリのスマートタグ付き画像を表示します。See [Visual search](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### ダイナミックメディア向けスマートイメージング {#smart-imaging}

スマートイメージングでは、各ユーザー固有の視聴特性を使用して、エクスペリエンスに最適化された適切な画像を自動的に提供し、パフォーマンスとエンゲージメントを向上させます。 スマートイメージングは、既存の画像プリセットで機能し、配信の直前にインテリジェンスを使用して、ブラウザーまたはネットワークの接続速度に基づいて画像のファイルサイズをさらに低減します。詳しくは、 [スマートイメージングを参照してください](../assets/imaging-faq.md)。

#### ダイナミックメディア用のビデオプロファイルでのスマート切り抜き(6.5.3.0) {#smart-crop-video}

ビデオのスマート切り抜き（ビデオプロファイルで使用できるオプション機能）は、Adobe Sensei の人工知能機能を使用して、サイズに関係なく、アップロードしたアダプティブビデオやプログレッシブビデオの重要な部分を自動的に検出して切り抜くツールです。See [About using smart crop in video profiles](../assets/video-profiles.md).

### AEM Forms {#aem-forms-previous-service-packs}

#### AEM Formsワークフロー(6.5.4.0)で印刷可能出力を生成する {#generate-printable-output}

印刷可能出力の生成ワークフローステップでは、ソーステンプレートファイルをデータファイルと統合できます。 この統合により、テンプレートファイルの別のコピーを印刷または保存できます。 このステップで、PCL、PostScript、ZPL、IPL、TPCLまたはDPL出力が生成されます。 この機能について詳しくは、「OSGiでの [フォーム中心のワークフロー — ステップリファレンス](../forms/using/aem-forms-workflow-step-reference.md)」を参照してください。

![印刷可能な出力を生成](assets/generate-print-output-step.gif)

#### レイアウトモードでのアダプティブフォームとインタラクティブ通信の複数列のサポート(6.5.4.0) {#multi-column-adaptive-forms}

アダプティブフォームとインタラクティブな通信で、パネルの列数を定義できるようになりました。 レイアウトモードに切り替えて、新しい複数列オプションを使用します。 詳しくは、レイアウトモードを [使用してコンポーネントのサイズを変更するを参照してください](../forms/using/resize-using-layout-mode.md)。

![複数列のレイアウト](assets/multi-column-layout.gif)

#### AEMインボックスのカスタマイズ(6.5.4.0) {#aem-inbox}

新しい「管理コントロール」オプションを使用すると、管理者は次のことができます。

* ヘッダーテキストとロゴのカスタマイズ

* ヘッダーで使用可能なナビゲーションリンクの表示を制御する

「管理者コントロール」オプションは、管理者またはワークフロー管理者グループのメンバーにのみ表示されます。 この機能の詳細については、「受信トレイ [](../sites-authoring/inbox.md)」を参照してください。

#### HTML5フォームでのリッチテキストのサポート(6.5.4.0) {#rich-text-support}

XFAフォームのテキストフィールドをHTML5フォームのリッチテキストフィールドに変換します。 詳しくは、「HTML5フォーム用のフォームテンプレートの [デザイン](../forms/using/designing-form-template.md)」を参照してください。

#### Accessibility enhancements (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Formsでは、次のアクセシビリティの強化が行われました。

* スクリーンリーダーは、アダプティブフォームで、チェックボックス、リンク、日付選択、日付入力の各フィールドについて正しく読み上げます。

* アダプティブフォームの各ページに、1つのタイトルと1つのメインのランドマークラベルが含まれるようになりました。

#### AEM Formsユーザーのインボックスアイテムの共有とアクセス要求(6.5.3.0) {#share-request-access}

受信トレイの項目を他のユーザーと共有できます。 別のユーザーが受信トレイのアイテムにアクセスできるようになると、そのユーザーは共有アイテムに対して適切なアクションを実行できます。 同様に、他のユーザーからインボックス項目へのアクセスを要求することもできます。 詳しくは、ユーザーのインボックスアイテムの [共有およびアクセスの要求を参照してください](../forms/using/configure-shared-queues-osgi.md)。

#### AEM Formsユーザーのインボックスアイテムに対する不在設定の設定(6.5.3.0) {#configure-out-of-office}

不在にする予定がある場合は、その期間に割り当てられたアイテムに対する処理を指定できます。
不在設定が実施される開始日と時刻および終了日と時刻を指定するオプションがあります。すべてのアイテムを送信するデフォルトのユーザーを設定できます。 「不在設定の [設定](../forms/using/configure-out-of-office-settings.md)」を参照してください。

#### Batch API for AEM Forms(6.5.3.0)を使用して複数のインタラクティブな通信を生成する {#generate-multiple-ic}

Batch APIを使用すると、テンプレートから複数のインタラクティブな通信を作成できます。 テンプレートは、データを一切使用しないインタラクティブな通信です。 Batch APIは、データとテンプレートを組み合わせてインタラクティブな通信を行います。 このAPIは、インタラクティブ通信の大量生産に役立ちます。 例えば、電話料金、複数の顧客のクレジットカード明細などです。 Batch APIを使用した複数の対話型通信の [生成を参照してください](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

## AEM 6.5 SP4以降の主なリリース {#key-releases-since-last-sp}

2020年3月5日～2020年6月4日の間に、Adobeは、主要なAEM成果物以外の次の機能をリリースしました。

* AEM Cloud Manager [2020.3.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-3-0.html)、 [2020.4.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-4-0.html)[、2020.5.0](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-manager/using/release-notes/release-notes-current.translate.html)

* [AEM Assets: デスクトップアプリ2.0.2.0](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)

* [AEM Screens: 機能パック202004](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202004.html)

## 役立つリソース

* [AEM 6.5ユーザーガイド](../user-guide/home.md)

* [一般リリースノート（Adobe Experience Manager 6.5）](release-notes.md)

* [Adobe Experience Manager 6.5用Service Packリリースノート](sp-release-notes.md)
