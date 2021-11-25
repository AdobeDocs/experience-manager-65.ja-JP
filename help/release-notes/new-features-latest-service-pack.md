---
title: の新機能 [!DNL Experience Manager] 6.5 サービスパック 11
description: の新機能 [!DNL Experience Manager] 6.5 サービスパック 11
contentOwner: AK
mini-toc-levels: 1
exl-id: 32470e6e-8a66-4670-82da-2259f6e001c3
source-git-commit: 35260325b583bd047f22ffa88afb9469b2023e60
workflow-type: tm+mt
source-wordcount: '4391'
ht-degree: 6%

---

# の新機能 [!DNL Adobe Experience Manager] 6.5 サービスパック 11 {#aem-whats-new-service-pack}

<!-- TBD: Downsample this image. We do not need as big an image since customers don't use as big a screen to view. Also, having a 700+ KB decorative image is bad for page load time.
-->

![新着情報](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5 サービスパックは、新機能、お客様からリクエストされた機能強化、パフォーマンス、安定性、およびセキュリティの改善を四半期ごとに提供します。 四半期ごとの可用性により、新しい機能やイノベーションに簡単にアクセスし、導入できます。

この記事では、最新の Service Pack に含まれる機能について説明します [以前の 6.5 サービスパックに含まれていた主な機能](#key-features-previous-service-packs)、および [前回の Service Pack 以降の主要リリース](#key-releases-since-last-sp) リリース。

## [!DNL Adobe Experience Manager Sites] {#aem-sites}

* SEO 用のサイトマップの自動生成は、 [SEO インデックスパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip). サイトマップ、代替 URL、ロボットメタタグなどを [!DNL Core Components].

* 複数行テキストデータタイプのマルチフィールドサポートを追加しました。

* ユーザーがバックグラウンドで現在実行中の非同期ジョブを認識し、同じパスで複数の非同期操作をトリガーしないようにする機能強化。

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* ユーザーエクスペリエンスが改善され、フォルダー内に存在するアセットの数が表示されます。1 つのフォルダー内のアセットが 1000 個を超える場合、[!DNL Assets] には「1000+」と表示されます。

   ![フォルダー内のアセット数](/help/assets/assets/browse-folder-number-of-assets.png)

* 次のアクセシビリティの強化が利用できます。

   * カード表示の [!DNL Assets] リポジトリ、使用時 `Tab` フォーカスをフォーカス時にクイックアクションを開く最初の項目に移動するためのキー。スクリーンリーダーは、フォーカスされた項目の名前を読み上げます。
   * In [!DNL Dynamic Media] [!UICONTROL ビューアプリセットエディター]「シャドウの色」と「境界線の色」が存在しない場合、「無効」プロパティを使用して入力が無効になります。 キーボードユーザーが入力にフォーカスできず、スクリーンリーダーがコントロールの状態を無効と発表しない。
   * In [!DNL Dynamic Media]新しいビデオエンコーディングプロファイルを作成するためのインターフェイスで、 [!UICONTROL スマート切り抜き率] オプションにはアクセシビリティのラベルが付いているので、スクリーンリーダーが適切に読み上げます。

### [!DNL Dynamic Media] {#dynamic-media}

* これで、 [!DNL Dynamic Media] を設定することで、 [!DNL Dynamic Media Classic] デスクトップアプリケーション。 詳しくは、 [Dynamic Mediaの一般設定](/help/assets/dm-general-settings.md).

   ![DM の一般設定](/help/assets/assets-dm/dm-general-settings.png)

* これで、 [!DNL Dynamic Media] を設定して、 [!DNL Dynamic Media Classic] デスクトップアプリケーション。 詳しくは、 [Dynamic Media Publish Setup の設定](/help/assets/dm-publish-settings.md).

   ![DM 公開設定](/help/assets/assets-dm/dm-publish-setup.png)

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] サービスパックリリース日の 1 週間後にアドオンパッケージをリリースします。


## 以前の主な機能 [!DNL Experience Manager] 6.5 サービスパック {#key-features-previous-service-packs}

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### AEM 6.5.10.0リリースに含まれる機能 {#features-sites-65100}

* **強化機能 [!DNL Content Fragment] モデルとエディター**:ネストされたを使用して、構造化コンテンツ用の複雑なモデルやカスタムモデルを作成できるようになりました。 [!DNL Content Fragment] モデル。 コンテンツ構造は、サブフラグメントとしてモデル化された基本要素にモジュール化されます。 上位レベルのフラグメントは、これらのサブフラグメントを参照します。 高度な検証ルールなどのデータタイプの強化により、 [!DNL Content Fragments]. この [!DNL Experience Manager] [!DNL Content Fragment] エディターは、一般的なエディターセッションでネストされたフラグメント構造をサポートします。たとえば、構造ツリー表示や、フラグメント階層を介したタブ付きパンくずナビゲーションなどの機能強化がおこなわれます。

* **の GraphQL API[!DNL Content Fragments]**:新しい GraphQL API は、構造化コンテンツを JSON 形式で配信する標準の方法です。 GraphQL クエリを使用すると、クライアントはエクスペリエンスをレンダリングする関連コンテンツ項目のみを要求できます。 このような選択により、クライアント側でのコンテンツ解析を必要とするコンテンツの過剰配信（HTTP REST API での可能性）が排除されます。 GraphQL スキーマは次から派生します。 [!DNL Content Fragment] モデルと API の応答は JSON 形式でおこなわれます。 In [!DNL Experience Manager] as a [!DNL Cloud Service], [GraphQL クエリが保持されます](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) キャッシュに適したGETリクエストを処理 ～ではまだ不可能だ [!DNL Experience Manager] 6.5.

* **階層の管理と今後のプレビュー**:ユーザーは、 [!DNL Experience Manager] ローンチに含まれるページの追加と削除の機能を含むローンチ。 この機能により、 [!DNL Experience Manager] 今後の公開をターゲットとするコンテンツバージョンを作成するためのローンチ。 [タイムワープ機能](/help/sites-authoring/working-with-page-versions.md#timewarp) ユーザーは、ローンチを将来のコンテンツステートとしてプレビューできます。

* [!DNL Experience Manager] フォルダーの下にすべてのコンテンツモデルのリストを直接表示します。コンテンツ作成者はファイル構造内を移動する必要はありません。 この機能により、クリック数が少なくなり、オーサリングの効率が向上しました。

* のパスフィールド [!DNL Sites] エディターを使用すると、作成者は次の場所からアセットをドラッグできます： [!DNL Content Finder].

* Platform では、アクセシビリティがいくつか強化されています。 詳しくは、 [Platform の更新](/help/release-notes/sp-release-notes.md#platform-65100).

#### 削除されたページおよびツリーを復元する機能 (6.5.9.0) {#ability-to-restore-pages-tree}

これで、 [!DNL Experience Manager Sites] ページ。

#### ロールアウトで使用可能なライブコピーページの並べ替え (6.5.8.0) {#sort-livecopy-pages}

これで、 [!UICONTROL 名前], [!UICONTROL 最終変更日]、および [!UICONTROL 前回のロールアウト日] プロパティ。 この [!UICONTROL 前回のロールアウト日] （ページ用）は、このリリースで導入された新しいプロパティです。

#### ページ移動および MSM ロールアウトが非同期操作として使用できる (6.5.7.0) {#page-moves-msm-asynchronous}

これで、ページの移動や MSM のロールアウトを非同期操作として実行できるようになり、実行時のパフォーマンスに対する影響を減らすことができます。 操作を即時または後で実行するようにスケジュールできます。 関連するジョブとプロセスステップのステータスはコンソールに表示され、大規模な MSM ロールアウトの監視に役立ちます。

#### 非同期モードでのページ移動操作の可用性 (6.5.6.0) {#page-move-asynchronous}

非同期モードでページ移動操作を使用できるようになりました。 即時実行に加えて、後で実行するように「ページ移動」操作をスケジュールすることもできます。

#### アクセシビリティの改善 (6.5.5.0) {#accessibility-sites}

* テキスト情報を追加することでエラーレポートを改善しました。

* キーボードナビゲーション中のユーザーインターフェイスのフォーカスを改善した。

* 様々なユーザーインターフェイス要素のコントラスト比が改善されました。

* ページ画像の代替属性の一貫性を改善しました。

* アクセス可能なリッチインターネットアプリケーション (ARIA) ラベルの一貫性が向上しました。

* 非ビジュアルデスクトップアクセス (NVDA) 機能が改善されました。

* スクリーンリーダーのサポートを改善しました。

#### その他の主要な機能強化 (6.5.5.0) {#other-enhancements-sites}

* 匿名でCRXDE Liteにアクセスすると、セキュリティが強化されます。 代わりに、ユーザーはログイン画面に移動します。 詳しくは、 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* ページツリーをコピーまたは貼り付ける際に、ルートページを貼り付けるか、ルートページをツリーのサブページと共に貼り付けるかのいずれかのオプションが追加されました。

* [!DNL Adobe Experience Manager Experience Fragments] 書き出し先 [!DNL Adobe Target] ワークスペースが [!DNL Target].

* マルチサイトマネージャー — コンポーネントがソースページから削除された場合、公開トリガーは、公開されたページからコンポーネントを削除するようになりました。

* マルチサイトマネージャ — 内のローカルコンポーネントの名前 [!UICONTROL ライブコピー] は、ブループリント内のコンポーネントの名前と同じで、コンポーネントはブループリントからロールアウトされた後、「 `_msm_moved` がローカルコンポーネントの名前に追加されます。

#### スタイルシステムの強化 (6.5.4.0) {#style-system-enhancements}

拡張スタイルシステムを使用して、コンポーネントダイアログ内でスタイルを選択できるようになりました。

#### 様々な領域でのパフォーマンスの向上 (6.5.4.0) {#performance-improvements}

* サイト内での ContextHub の読み込みと初期化に要する時間を短縮しました (`contexthub.kernel.js`) をクリックします。 その結果、サイト訪問中のページ読み込みがより高速になります。

* ドラッグ後のページの更新時間を短縮 [!DNL Experience Fragments] から [!DNL Sites] ページエディター。

* エントリの読み込み時間を短縮 [!DNL Sites] 200 個を超えるライブコピーが含まれるページ **[!UICONTROL ライブコピーの概要]**.

* 不完全な URL または無効な URL の処理を改善しました。 このような URL を使用すると、テンプレートエディターの速度が遅くなる可能性があります。

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

#### AEM 6.5.10.0リリースに含まれる機能 {#features-assets-65100}

* [!DNL Experience Manager] は、Connected Assets の機能を [!DNL Dynamic Media] 該当するコアコンポーネント内の画像。 「[Connected Assets の使用](/help/assets/use-assets-across-connected-assets-instances.md)」を参照してください。

* 個々のアセットとコレクションをリンクとして共有する場合 ( [!UICONTROL リンク共有] ダイアログ ) を使用して、受信者に元のアセット、レンディションまたはその両方をダウンロードさせるかどうかを選択できます。 詳しくは、 [リンクを使用したアセットの共有](/help/assets/link-sharing.md).

   ![オリジナルのアセットのみ、レンディションのみ、またはその両方をダウンロードすることを許可するオプション](/help/release-notes/assets/share-assets-as-link.png)

* ユーザーがリンクとして共有されているアセットをダウンロードする場合、元のアセット、レンディションまたはその両方をダウンロードするよう選択できます。

* **生成されるサブアセットを制限**:管理者は、 [!DNL Experience Manager] は、PDF、PowerPoint、InDesign、キーノートファイルなどの複合アセットに対してを生成します。

   ![サブアセットの生成を制限](/help/assets/assets/sub-asset-limit.png)

* 新しい [!DNL Camera Raw] をサポートするパッケージが利用可能です [!DNL Adobe Camera Raw] v10.4。詳しくは、 [を使用して画像を処理 [!DNL Camera Raw]](/help/assets/camera-raw.md).

#### 以前のリリース {#previous-releases-assets}

* 中国の社会的・政治的見解 (6.5.9.0) と一致するよう、香港、マカオ、台湾に関する中国のロケールおよび地域の命名を更新しました。

* ACP API 応答の電子メール ID の大文字と小文字を変更するためのオプション設定が、 [!DNL Adobe Experience Manager] (6.5.9.0)。

   ![ACP 応答で電子メール ID を小文字に変更するための設定 [!DNL Experience Manager]](assets/email-lowcase-config.png)

* 様々な機能で、テキストとアイコンの背景とのコントラストが強化されます。 この Web コンテンツアクセシビリティガイドライン (WCAG) ガイドラインの実装により、 [!DNL Assets] 視覚や色の知覚が限られているユーザーがアクセスしやすくなりました。 詳しくは、 [のアクセシビリティの強化 [!DNL Assets]](sp-release-notes.md#assets-accessibility-6590) (6.5.9.0)。
* を使用する場合 [Connected Assets の機能](/help/assets/use-assets-across-connected-assets-instances.md)に設定すると、 [!DNL Sites] アセットを使用するページ。 アセットへのこれらの参照は、アセットの [!UICONTROL プロパティ] ページ。 これにより、管理者、マーケターおよびライブラリ担当者は、アセットの使用状況を完全に把握でき、トラッキング、管理およびブランドの一貫性 (6.5.8.0) を向上できます。

* Web ページで参照されているアセットを削除する場合、 [!DNL Experience Manager] 警告を表示します。 参照元のアセットを強制的に削除することも、 [!DNL Properties] ページに表示されます。 参照をクリックすると、ローカルおよびリモートの [!DNL Sites] ページ (6.5.8.0) のみです。

* [!DNL Assets] および [!DNL Dynamic Media] では、複数のアクセシビリティを強化しています。 この機能強化は、キーボードナビゲーション、スクリーンリーダーの使用、支援テクノロジー (AT) を使用するための同様の機能強化に関連しています。 詳しくは、 [[!DNL Assets] 機能強化](/help/release-notes/sp-release-notes.md#assets-6570) および [[!DNL Dynamic Media] 機能強化](/help/release-notes/sp-release-notes.md#dynamic-media-6570) (6.5.7.0)

* ユーザーは、カード表示および列表示 (6.5.7.0) でデジタルアセットを並べ替えることができます。

#### アクセシビリティの強化 (6.5.6.0) {#accessibility-assets-6560}

* **キーボードナビゲーション中のユーザーインターフェイスフォーカスの強化**&#x200B;例えば、次に焦点を当てます。

   * `x` アイコン [!UICONTROL バージョンのプレビュー] でのアセットのダイアログ [!UICONTROL タイムライン].

   * 実用的なユーザーインターフェイスオプション。

   * E メールフィールド [!UICONTROL リンクを共有] ダイアログ、閉じられたユーザーグループを追加するフィールド [!UICONTROL 権限] フォルダーのタブ [!UICONTROL プロパティ].

* **キーボードキーを使用した機能強化**

   キーボードのキーを使用して、スクリーンリーダーの参照モードでメタデータスキーマフォームエディターのコントロールをドラッグできます。

* **スクリーンリーダーユーザーの使いやすさの向上**、次の理由によります。

   * スクリーンリーダーは、ビデオプレーヤーとオーディオプレーヤーの目的を読み上げます。

   * スクリーンリーダーは、を使用して選択したタグを削除するユーザーインターフェイスオプションの目的を読み上げます。 [!UICONTROL タグ選択ダイアログ] アセット上 [!UICONTROL プロパティ].

   * スクリーンリーダーは、テーブルの行ヘッダーと行項目を読み上げるので、ユーザーは、同じ行に属するエントリを把握できます。

   * 検索ページのわかりやすいページタイトル。

   * スクリーンリーダーは、検索フィルターパネルのオプションを拡大可能なアコーディオンとして読み上げます。

#### のその他の機能強化 [!DNL Assets] (6.5.6.0) {#other-enhancements-assets-6560}

* フォルダーに関連付けられているユーザーグループ（プライベートおよび非プライベート）が、 [これらのフォルダーの削除](/help/assets/private-folder.md#delete-private-folder). ただし、既存の冗長、親なし、未使用および自動生成されたユーザーグループは、JMX を使用してリポジトリから削除できます。

#### のアクセシビリティの強化 [!DNL Assets] (6.5.5.0) {#assets-accessibility}

[!DNL Experience Manager Assets] は、Web コンテンツアクセシビリティガイドライン (WCAG) に準拠してアクセシビリティを強化しました。 次の機能強化により、アクセシビリティが向上しました。

* 多くのユーザーインターフェイス要素、コントロール、ページ、ダイアログは、スクリーンリーダーに適しています。

* 多くのユーザーインターフェイス要素、コントロールおよび入力フォームフィールドは、キーボードを使用してアクセスできます。

* 一部のユーザインターフェイス要素の色とコントラストが更新され、視覚が限られたユーザや、色の知覚を持たないユーザが、これらのユーザインターフェイス要素を区別できるようになりました。例えば、星評価アイコンの色 ( [!UICONTROL 評価] セクション [!UICONTROL 詳細] アセットのタブ [!UICONTROL プロパティ] またはカード表示で ) は、適切なコントラストに合わせて変更されます。

   ![コントラストが改善された評価アイコン](assets/star-rating-icons.png)

#### 拡張例外処理 (6.5.5.0) {#exception-handling}

[!DNL Assets] ユーザーインターフェイスのフローにより、より優れた例外処理が提供されます。 アセットのディメンションにタイプがない場合、観察された例外はログファイルに記録されます。

#### 設定 [!DNL Experience Manager Assets] と [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

次の間の認証チャネル： [!DNL Experience Manager Assets] および [!DNL Brand Portal] が変更されました。 以前は [!DNL Brand Portal] は、旧来の OAuth ゲートウェイを通じてクラシック UI で設定されていました。このゲートウェイは、JWT トークン交換を使用して認証用の IMS アクセストークンを取得します。 [!DNL Experience Manager Assets] は次のように設定されています： [!DNL Brand Portal] 経由 [!DNL Adobe I/O]: [!DNL Brand Portal] テナント。

設定の手順 [!DNL Experience Manager Assets] と [!DNL Brand Portal] は、 [!DNL Experience Manager] のバージョン、および初めて設定するか、既存の設定をアップグレードするか。 詳しくは、[Experience Manager Assets と Brand Portal の連携の設定](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html?lang=ja)を参照してください。

#### アクセシビリティの強化 (6.5.4.0) {#accessibility-enhancements-6540}

[!DNL Experience Manager Assets] には、次のアクセシビリティの強化が含まれています。

* キーボードの矢印キーを使用して、ズームされた画像内の領域を移動およびパンできます。 詳しくは、 [キーボードのキーを使用したみでアセットをプレビュー](../assets/manage-assets.md#previewing-assets).

* フィルターパネルの混合状態チェックボックス（ネストされた述語をすべて選択した場合を除き、第 1 レベルのチェックボックスは選択されず、侵入される）は、スクリーンリーダーで読み取り可能です。

* 日付と時刻の形式の制約が日付フィールドのフィールドラベルに提供され、ユーザーがキーボードを使用して正しい形式で日付を入力できるようになります。
例えば、`On Time (MM-DD-YYYY HH:mm)` のようになります。ここで、MM は 2 桁の形式、YYYY は年、DD は 2 桁の形式で表された日、HH は 24 時間の形式で表された時、mm は分です。

* スクリーンリーダーは、選択したタグ (`X` 記号 ) および選択したタグの数。

#### リスト表示でのアセットの作成日の並べ替え可能な列 (6.5.3.0) {#sortable-date-created-column}

アセットの作成日の新しい並べ替え可能な列が DAM リスト表示およびリスト表示のアセット検索結果に追加されます。

![作成日の並べ替え可能な列](assets/asset-created-date.png)

#### 次を視覚的に検索 [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets] ユーザーは、視覚的に類似した画像を検索できます。Experience Managerは、ユーザーが選択した画像に類似した、DAM リポジトリのスマートタグ付き画像を表示します。 詳しくは、 [ビジュアル検索](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

* では多くのアクセシビリティが強化されています [!DNL Dynamic Media] スクリーンリーダーが、アクションやユーザーインターフェイスに関するより適切で有用な説明を提示できるように、クライアントを使用します。 詳しくは、 [[!DNL Dynamic Media] 更新](/help/release-notes/sp-release-notes.md#dynamic-media-65100) (6.5.10.0)。

* [[!DNL Dynamic Media] アクセスしやすくなりました](sp-release-notes.md#assets-accessibility-6590) 次の条件で：

   * キーボードキーを使いやすくする。
   * 様々なエディターでのテキスト、プレースホルダーテキスト、コントロールのコントラスト（背景）。
   * スクリーンリーダーによるアクセシビリティとナレーション。

* スマートイメージング DPR（デバイスのピクセル比）とネットワーク帯域幅の最適化により、高解像度のディスプレイとネットワーク帯域幅の制限があるデバイスで、最高品質の画像を効率的に配信します。 詳しくは、 [スマートイメージングに関する FAQ](/help/assets/imaging-faq.md) (6.5.9.0)。

* [!DNL Dynamic Media] 配信 (`fmt` URL 修飾子 ) で、次世代の画像形式 AVIF（AV1 画像形式）がサポートされるようになりました。 詳しくは、 [画像サービングおよびレンダリング API fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html) (6.5.9.0)。

#### での 3D アセットのサポート [!DNL Dynamic Media] (6.5.5.0) {#support-for-3d}

での 3D 画像のサポート [!DNL Dynamic Media] を使用すると、3D コンテンツを公開して Web ページやアプリケーションに追加できます。 サポートには以下が含まれます。

* 共通の 3D アセット形式を公開し、Web ページや他のアプリケーションで使用できるアセット URL を生成します。

* 3D Web Viewer（を活用） [!DNL Adobe Dimension]を使用して、公開した 3D アセットをインタラクティブに表示できます。

* 上の一般的な 3D アセットの公開と表示 [!DNL Experience Manager Sites] ページ [!DNL Sites] WCM コンポーネント。

#### CDN にキャッシュされたコンテンツ (6.5.6.0) を無効にする {#invalidate-cdn-cached-content}

これで、 [!DNL Dynamic Media] コンテンツ配信ネットワーク (CDN) にキャッシュされたコンテンツを無効にするユーザーインターフェイス。 その結果、更新されたアセットは、キャッシュの有効期限が切れるのを待つ代わりに、即座に使用できるようになります。 CDN を無効にするには、次の手順を実行します。

* CDN 無効化テンプレートの作成：アセットとフォーム関連のテンプレートベースの URL の選択

* アセットピッカーを使用したアセットと関連プリセットの選択

* 完全なアセット URL の追加

#### へのアセットの選択的公開 [!DNL Experience Manager] および [!DNL Dynamic Media] (6.5.6.0) {#selective-publishing}

次のいずれかに対して、アセットを選択的に公開または非公開にすることができるようになりました。 [!DNL Experience Manager] または [!DNL Dynamic Media] using [!UICONTROL クイック公開] または [!UICONTROL 公開を管理] ウィザード。 また、 `Publish` または `Unpublish` フォルダーレベルでのモード。

#### Dynamic Media用スマートイメージング {#smart-imaging}

スマートイメージングは、各ユーザーに固有の閲覧特性を使用して、ユーザーのエクスペリエンスに最適化された適切な画像を自動的に提供するので、パフォーマンスとエンゲージメントが向上します。 スマートイメージングは、既存の画像プリセットで機能し、配信の直前にインテリジェンスを使用して、ブラウザーまたはネットワークの接続速度に基づいて画像のファイルサイズをさらに低減します。詳しくは、[スマートイメージング](../assets/imaging-faq.md)を参照してください。

#### Dynamic Mediaのビデオプロファイルでのスマート切り抜き (6.5.3.0) {#smart-crop-video}

ビデオのスマート切り抜き（ビデオプロファイルで使用できるオプション機能） Adobe Senseiを使用すると、サイズに関係なく、アダプティブビデオまたはプログレッシブビデオ内の焦点を自動的に検出して切り抜くことができます。 詳しくは、 [ビデオプロファイルでのスマート切り抜きの使用について](../assets/video-profiles.md).

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### AEM 6.5.10.0リリースに含まれる機能 {#features-forms-65100}

>[!NOTE]
>
>のアドオンパッケージ [!DNL Experience Manager Forms] が予定より 1 週間後に使用可能になる [!DNL Experience Manager] Service Pack リリース。

* これで、Automated forms conversionサービスを [PDF formsをフランス語、ドイツ語、スペイン語、イタリア語、ポルトガル語の各言語で変換する](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html#language-specific-meta-model) アダプティブフォームに変換する

* **プロパティブラウザーのエラーメッセージ**：アダプティブフォームのプロパティブラウザーに、各プロパティに関するエラーメッセージを追加しました。これらのメッセージは、フィールドの許可値を理解するのに役立ちます。

* **リテラルオプションを使用して JSON タイプの変数の値を設定する機能をサポート**:リテラルオプションを使用して、AEM Workflow の変数設定手順で JSON 型変数の値を設定できます。 リテラルオプションを使用すると、文字列の形式で JSON を指定できます。

* [プラットフォームの更新](../forms/using/aem-forms-jee-supported-platforms.md): [!DNL Adobe Experience Manager Forms] JEE 上では、次のプラットフォームのサポートが追加されました。
   * [!DNL Adobe Acrobat 2020]
   * [!DNL Ubuntu 20.04]
   * [!DNL Open Office 4.1.10]
   * [!DNL Microsoft Office 2019]
   * [!DNL Microsoft Windows Server 2019]
   * [!DNL RHEL8]

* のサポートを追加しました。 `GuideBridge#getGuidePath` の API [!DNL AEM Forms].

#### のサポート [!DNL Azul Zulu OpenJDK] (6.5.9.0) {#support-azul-zulu}

を使用してアプリケーションを開発および操作できるようになりました。 [!DNL Azul Zulu] 組み立て [!DNL OpenJDK] 対象 [!DNL Experience Manager Forms] （OSGi デプロイメント） 詳しくは、 [Experience Manager6.5 Service Pack 9 リリースノート](sp-release-notes.md) および [技術要件](../sites-deploying/technical-requirements.md).

#### 次を使用してグループに通知 E メールを送信する機能 [!UICONTROL タスクを割り当て] (6.5.9.0) {#group-notification-email}

タスクの割り当てワークフローステップを使用して、グループ電子メールアドレスに通知電子メールを送信できるようになりました。

#### ソースのインタラクティブ通信 (6.5.9.0) を変更した後にインタラクティブ通信下書きを取得する機能 {#retrieve-draft-after-source-modifications}

インタラクティブ通信のソースを変更した後、下書きとして保存されたインタラクティブ通信を取得できるようになりました。

#### reCAPTCHA サービス (6.5.9.0) の読み込み、レンダリングおよび検証のためのカスタムドメイン名を設定します。 {#set-custom-domain-name-recaptcha}

reCAPTCHA サービスは、`https://www.recaptcha.net/` をデフォルトドメインとして使用します。設定を変更して、 `https://www.google.com/` または reCAPTCHA サービスの読み込み、レンダリング、検証をおこなうカスタムドメイン名。

#### の入力データの強化 [!UICONTROL フォームデータモデルサービスを起動] ワークフローステップ (6.5.9.0) {#input-data-enhancements-fdm}

フォームデータモデルとサービスを [!UICONTROL フォームデータモデルサービスを起動] ワークフローステップでは、入力データのサービス引数を指定します。

次を選択した場合、 [!UICONTROL ペイロードを基準とする] ファイルをサービス引数として添付するオプションで、実際のファイル名の代わりにファイルを含むフォルダーパスを指定できるようになりました。 添付ファイル名の代わりにフォルダー名を定義すると、ワークフローモデルを再利用できます。 ワークフローモデルを 1 つのファイル添付ファイル名に制限することはありません。

#### レコードのドキュメントテンプレートで複数のマスターページを使用する機能 (6.5.9.0) {#use-multiple-master-pages-dor-template}

レコードのドキュメントテンプレートで複数のマスターページを使用できるようになりました。 その結果、タイトルページやテンプレートの他のページに、異なるヘッダー、フッター、フォント、ロゴ情報を表示できるようになりました。

#### レコードのドキュメントでの改ページのサポート (6.5.9.0) {#support-page-breaks-dor}

レコードのドキュメントに改ページを追加できるようになりました。 その結果、ページ内でパネルが分割された場合、改ページを追加して、レコードのドキュメント内の新しいページにパネルを移動できます。

#### ルールに基づくアダプティブフォーム内の CAPTCHA コンポーネントの表示/非表示を切り替えます (6.5.8.0)。 {#show-hide-captcha}

アダプティブフォーム送信時またはユーザーアクション時に、CAPTCHA を検証できるようになりました。 また、ルールに基づいてアダプティブフォーム内の CAPTCHA コンポーネントの表示と非表示を切り替えるための条件を追加して、ユーザーアクションで CAPTCHA を検証することもできます。

#### カスタム CAPTCHA サービスの追加 (6.5.8.0) {#add-custom-captcha-services}

[!DNL Experience Manager Forms] は、Google reCAPTCHA(Google reCAPTCHA API の別のライセンスが必要 ) を CAPTCHA 検証サービスとして使用するためのサポートを標準で提供しています。 また、カスタム CAPTCHA サービスを使用して CAPTCHA を検証することもできます。

#### その他の機能強化 (6.5.8.0) {#other-enhancements-forms-6580}

* アクセシビリティの向上 [!DNL Experience Manager Forms] 日付選択コンポーネント。

* PrintChannel API を使用して PCL 形式のインタラクティブ通信を生成するサポートが追加されました。

* PDFG 変換を実行する際に、 [!DNL Experience Manager Forms] カスタムブックマークの生成に関するレジストリの変更。

#### パフォーマンスの向上 (6.5.7.0) {#performance-improvements-forms}

[!DNL Experience Manager] 6.5 Service Pack 7 Formsにより、次のパフォーマンスが向上しました。

* アダプティブフォームを送信する際に、サーバー上のフィールド値を検証する。

* を使用してPDFフォームをアダプティブフォームに変換する [!DNL Automated Forms Conversion service].

#### Microsoft SQL Server 2016 のサポート高可用性のための常時稼動グループ (6.5.7.0) {#always-on-availability-groups}

[!DNL Experience Manager Forms] がサポートされるようになりました [!DNL Microsoft] SQL Server 2016 OSGi デプロイメントの高可用性のための可用性グループが常に稼動します。

#### パフォーマンスを最適化するためのフォームデータモデル HTTP クライアント設定 (6.5.7.0) {#fdm-http-client-config}

[!DNL Experience Manager Forms] フォームデータモデルを使用して、データソースとして RESTful Web サービスとの統合時に、パフォーマンスを最適化するための HTTP クライアント設定が含まれるようになりました。 詳しくは、 [データソースの設定](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration).

#### レイアウトモードでの各コンポーネントのリセットオプションの使用可否 (6.5.7.0) {#reset-option-layout-mode}

アダプティブフォームのレイアウトモードで、各コンポーネントのリセットオプションを使用できるようになりました。 パネルに複数列のレイアウトを定義する場合、この機能を使用して、パネル内の個々のコンポーネントをリセットできます。 詳しくは、 [レイアウトモードを使用してコンポーネントのサイズを変更する](../../help/forms/using/resize-using-layout-mode.md#resize-components).

#### クライアントでのアダプティブフォームの事前入力 (6.5.6.0) {#prefill-merge-data-at-client}

アダプティブフォームに事前入力すると、 [!DNL Experience Manager Forms] サーバーはデータをアダプティブフォームと結合し、入力済みのフォームをユーザーに配信します。 デフォルトでは、データの結合アクションはサーバーで実行されます。これで、 [!DNL Experience Manager Forms] サーバーから [クライアントでのデータ結合アクションの実行](../../help/forms/using/prepopulate-adaptive-form-fields.md) サーバーの代わりにを使用します。 これにより、アダプティブフォームの事前入力とレンダリングに要する時間が大幅に短縮されます。

#### 双方向 SSL 実装 (6.5.6.0) を使用したサーバー上の RESTful API とのフォームデータモデル統合 {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] フォームデータモデルが次のフォームにフォームデータモデル [双方向 SSL が実装されているサーバー上の RESTful API との統合](../../help/forms/using/configure-data-sources.md).

#### のサポートを追加しました。 [!DNL Adobe Sign] automated forms conversionサービスのテキストタグ (6.5.6.0) {#sign-integration-acroform-afcs}

AcroForms に [!DNL Adobe Sign] テキストタグを使用する場合、これらのフィールドが認識され、 [!DNL Adobe Sign] を使用して変換されたアダプティブフォームのフィールド [!DNL Automated Forms Conversion service]. 署名者は、アダプティブフォームの署名時に、このようなフィールドに入力できます。

#### カラーPDF formsのアダプティブフォームへの変換のサポート (6.5.6.0) {#colored-PDF-forms}

以下を使用できます。 [!DNL Automated Forms Conversion service] カラーのPDF formsをアダプティブフォームに変換するには

#### SMB 2 および SMB 3 プロトコル (6.5.6.0) のサポート {#smb-support}

[!DNL Experience Manager Forms] は、SMB 2 および SMB 3 プロトコルをサポートするようになりました。

#### 翻訳済みアダプティブフォームページのキャッシュ機能が強化されました (6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

これで、 [アダプティブフォーム URL の引数の代わりに、アダプティブフォーム URL のセレクターとしてのロケール](../../help/forms/using/supporting-new-language-localization.md). これは、 [!DNL Experience Manager Dispatcher]. 以前のバージョンでは、翻訳済みのアダプティブフォームのキャッシュは使用できませんでした。 アダプティブフォームの URL でロケールをセレクターとして使用するためのキャッシュの設定について詳しくは、 [Dispatcher でのアダプティブフォームのキャッシュの設定](../../help/forms/using/configure-adaptive-forms-cache.md).

#### フォームデータモデルサービスの出力を変数 (6.5.6.0) に保存する {#save-fdm-service-to-variable}

フォームデータモデルを使用すると、フォームデータモデルサービスの出力を変数に保存できます。 [!DNL Experience Manager Forms] フォームデータモデルサービスのタイプを変数のタイプに自動的にマッピングするようになりました。

#### ファイル添付コンポーネントに複数のファイルを添付 (6.5.6.0) {#attach-multiple-files}

次の操作を実行できます。 [複数のファイルを添付](../../help/forms/using/introduction-forms-authoring.md) から [!UICONTROL 添付ファイル] アダプティブフォームのコンポーネント

#### Adobe Experience Manager受信トレイ列のカスタマイズ (6.5.5.0) {#customize-aem-inbox-columns}

次の項目をカスタマイズできます： [!DNL Experience Manager] インボックス：列のデフォルトのタイトルの変更、列の位置の並べ替え、ワークフローのデータに基づく追加の列の表示をおこないます。 のメンバー `administrators` または `workflow-administrators` グループは、列をカスタマイズできます。 詳しくは、 [管理コントロール](../sites-authoring/inbox.md#inbox-admin-control).

![Experience Manager受信トレイの列をカスタマイズ](assets/customize-columns.gif)

#### Interactive Communications を下書きとして保存 (6.5.5.0) {#save-as-draft}

エージェント UI を使用して、各インタラクティブ通信の 1 つ以上のドラフトを保存し、後でドラフトを取得して、作業を続行できます。 それぞれのドラフトに異なる名前を指定して、それを識別できます。 詳しくは、 [Interactive Communications を下書きとして保存](../forms/using/prepare-send-interactive-communication.md#save-as-draft).

![ドラフトとして保存](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] アプリケーションサーバーのサポート (6.5.5.0) {#weblogic-support}

Adobe Experience Manager Formsが [!DNL Oracle WebLogic 12] (JEE 上のAdobe Experience Manager Forms) 以前のバージョンからアップグレードするか、JEE 上の新しいExperience Manager6.5 Formsサーバーを [!DNL Oracle WebLogic] 12.2.1.4 以降。 後で、マイナーバージョンの変更に対応します。ここで、x は 12.2.1.x のバージョン番号に置き換えられます。

#### アクセシビリティの改善 (6.5.5.0) {#accessibility-improvements}

Adobe Experience Manager Formsのアクセシビリティが次のように強化されています。

* ユーザーがアダプティブフォームをHTMLフォームとしてプレビューする場合、 [!UICONTROL 手書き署名] フィールドはタブフォーカスを保持します。

* アダプティブフォームの送信時に表示されるエラーメッセージに、 `aria-describedBy` 属性。 属性は、エラーメッセージで参照されるフィールドに添付されます。 この `aria-describedby` attribute は、オブジェクトを記述する要素の ID を示します。 ウィジェットやグループと、それらを記述したテキストとの間の関係を確立するのに役立ちます。

* アダプティブフォームにいくつかの必須フィールドがある場合、mandatory 属性は `True` ARIA アクセシビリティスキーマのそのようなフィールド用です。

#### フォームデータモデル (6.5.5.0) の SOAP ベース Web サービス用の X-509 証明書ベースの認証 {#x509-based-authentication-soap}

フォームデータモデルで、SOAP Web サービスをデータソースとして使用している間、X-509 証明書ベースの認証がサポートされるようになりました。 詳しくは、 [SOAP Web サービスの設定](../forms/using/configure-data-sources.md#configure-soap-web-services).

#### その他の主な改善 (6.5.5.0) {#other-improvements}

* JEE 上のForms 6.5 Document Security は、 [!DNL Apache Struts 2].

* のサポートを追加しました。 [!DNL Oracle Real Applications Cluster (RAC) 19c].

#### Experience Manager Formsワークフローでの印刷可能な出力の生成 (6.5.4.0) {#generate-printable-output}

印刷可能な出力を生成ワークフローのステップでは、ソーステンプレートファイルをデータファイルと統合できます。 この統合により、テンプレートファイルの別のコピーを印刷または保存できます。 このステップでは、PCL、PostScript、ZPL、IPL、TPCL、または DPL 出力が生成されます。 この機能について詳しくは、 [OSGi 上のForms中心のワークフロー — ステップリファレンス](../forms/using/aem-forms-workflow-step-reference.md).

![印刷可能な出力を生成](assets/generate-print-output-step.gif)

#### レイアウトモード (6.5.4.0) でのアダプティブフォームおよびインタラクティブ通信の複数列のサポート {#multi-column-adaptive-forms}

アダプティブフォームおよびインタラクティブ通信で、パネルの列数を定義できるようになりました。 新しい複数列オプションを使用するには、レイアウトモードに切り替えます。 詳しくは、[レイアウトモードを使用したコンポーネントのサイズ変更](../forms/using/resize-using-layout-mode.md)を参照してください。

![複数列のレイアウト](assets/multi-column-layout.gif)

#### Experience Manager受信ボックスのカスタマイズ (6.5.4.0) {#aem-inbox}

新しい「管理コントロール」オプションでは、管理者は次の操作を実行できます。

* ヘッダーのテキストとロゴをカスタマイズします。

* ヘッダーで使用できるナビゲーションリンクの表示を制御します。

「管理コントロール」オプションは、 `administrators` または `workflow-administrators` グループ化します。 この機能について詳しくは、 [インボックス](../sites-authoring/inbox.md).

#### HTML5 フォーム (6.5.4.0) でのリッチテキストのサポート {#rich-text-support}

XFA フォームのテキストフィールドを Convert5 フォームのリッチテキストフィールドにHTMLします。 詳しくは、 [フォーム 5 フォーム用のフォームHTMLのデザイン](../forms/using/designing-form-template.md).

#### アクセシビリティの強化 (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Formsのアクセシビリティが次のように強化されています。

* スクリーンリーダーは、アダプティブフォーム内で、チェックボックス、リンク、日付選択、日付入力の各フィールドを正しく読み上げます。

* アダプティブフォームの各ページに、1 つのタイトルと 1 つのメインランドマークラベルが含まれるようになりました。

#### Experience Manager Formsユーザーのインボックス項目へのアクセスを共有してリクエストする (6.5.3.0) {#share-request-access}

インボックスの項目を別のユーザーと共有できます。 別のユーザーがインボックス項目にアクセスしたら、ユーザーは共有項目に対して適切なアクションを要求し、実行できます。 同様に、他のユーザーからインボックス項目へのアクセスをリクエストすることもできます。詳しくは、 [ユーザーのインボックス項目へのアクセスを共有およびリクエスト](../forms/using/configure-shared-queues-osgi.md).

#### Experience Manager Formsユーザーのインボックス項目に対する不在設定 (6.5.3.0) の設定 {#configure-out-of-office}

不在にする予定がある場合は、その期間に割り当てられる項目に対して実行する操作を指定できます。不在設定が有効になる開始日時および終了日時を指定するオプションがあります。すべてのアイテムを送信するデフォルトの担当者を設定できます。 詳しくは、 [不在設定の構成](../forms/using/configure-out-of-office-settings.md).

#### Experience Manager Forms用 Batch API を使用して複数のインタラクティブ通信を生成する (6.5.3.0) {#generate-multiple-ic}

Batch API を使用すると、テンプレートから複数のインタラクティブ通信を作成できます。 テンプレートは、データのないインタラクティブ通信です。 Batch API は、データとテンプレートを組み合わせて、インタラクティブな通信を作成します。 この API は、インタラクティブ通信を大量に生産する際に役立ちます。 例えば、電話料金、複数の顧客のクレジットカード明細などです。 詳しくは、 [Batch API を使用して複数のインタラクティブ通信を生成する](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

<!-- TBD: Check if the wider team released anything in FY21.
-->

## 主なリリース日 [!DNL Adobe Experience Manager] 6.5 SP10{#key-releases-since-last-sp}

2021 年 8 月 26 日 (PT)～2021 年 11 月 25 日 (PT) の間に、Adobeはサービスパックに加えて、次の機能をリリースしました。

* [!DNL Adobe Experience Manager] as a Cloud Service [2021.9.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-9-0.html) および [2021.10.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja).

* [[!DNL Experience Manager] デスクトップアプリケーション 2.1 (2.1.3.4)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

* [Experience Manager Screens:機能パック202109](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202109.html?lang=ja)

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
>* [の一般リリースノート [!DNL Experience Manager] 6.5](release-notes.md)
>* [サービスパックリリースノート： [!DNL Experience Manager] 6.5](sp-release-notes.md)

