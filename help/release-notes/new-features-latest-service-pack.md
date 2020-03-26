---
title: Adobe Experience Manager 6.5 Service Pack 4の新機能
description: Adobe Experience Manager 6.5 Service Pack 4の新機能
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 7c937b425d909a1f3a9af0a1c3357c44220af0f2

---


# Adobe Experience Manager 6.5 Service Pack 4の新機能 {#aem-whats-new-service-pack-4}

Adobe Experience Manager (AEM) 6.5では、四半期ごとのService Packを通じて、機能と継続的な改善を提供しています。 このアプローチは、イノベーションを導入しやすくなるため、お客様にとってメリットがあります。

AEM Service Pack 4(6.5.4.0)は2020年3月6日にリ **リースされます**。 この記事では、AEMの遍歴をより豊かにするために6.5 Service Packが提供する主な機能に焦点を当てます。

## AEM Sites {#aem-sites}

### スタイルシステムの強化

拡張されたスタイルシステムを使用して、コンポーネントダイアログ内のスタイルを選択できるようになりました。

### 各領域のパフォーマンスの向上 {#performance-improvements}

* サイト内のContextHubの読み込みと初期化に要する時間を短縮しま`contexthub.kernel.js`した()。 サイト訪問中のページ読み込みが速くなります。

* エクスペリエンスフラグメントをサイトのページエディターにドラッグした後に、ページを更新する時間を短縮しました。

* ライブコピーの概要で200を超えるライブコピーが含まれるサイトページのエントリの読み込み時 **[!UICONTROL 間を短縮しました]**。

* 不完全または無効なURLの処理を改善。 このようなURLを使用すると、テンプレートエディターの動作が遅くなる可能性があります。

## AEM Assets {#aem-assets}

### AEM Assets と Brand Portal の連携の設定 {#configure-assets-bp}

AEM AssetsとBrand Portalの間の認証チャネルが変更されました。 これまで、Brand Portal は、旧来の OAuth ゲートウェイを通じてクラシック UI で設定されていました。このゲートウェイは、JWT トークン交換を使用して認証用の IMS アクセストークンを取得します。AEM Assets と Brand Portal の連携が、Adobe I/O を通じて設定されるようになりました。Adobe I/O が Brand Portal テナントの認証用の IMS トークンを取得します。

Brand PortalでAEM Assetsを設定する手順は、AEMのバージョン、および初めて設定するか、既存の設定をアップグレードするかによって異なります。 See [Configure AEM Assets with Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) for details.


### Accessibility enhancements {#accessibility-enhancements}

Experience Manager Assetsには、次のアクセシビリティ機能の強化が含まれています。

* キーボードの矢印キーを使用して、ズームされた画像内の領域を移動およびパンできます。 詳しくは、キーボードキーを使用したア [セットのプレビューのみを参照してくださ](../assets/managing-assets-touch-ui.md#previewing-assets)い。

* フィルターパネルの混合状態のチェックボックス（ネストされた述語をすべて選択しない限り、最初のレベルのチェックボックスは選択されず、読み取られます）は、スクリーンリーダーで読み取り可能です。

* 日付と時間の形式の制約は、ユーザーがキーボードを使用して正しい形式で日付を入力できるように、日付フィールドのフィールドラベルに設定されています。

   例： `On Time (MM-DD-YYYY HH:mm)`ここで、MMは2桁の形式の月、YYYYは年、DDは2桁の形式の日、HHは24時間の軍用形式の時、mmは分です。

* 現在選 `X` 択されているタグを削除するボタン上のシンボルが、選択されているタグの数と共にスクリーンリーダーによって通知されるようになりました。

## AEM Forms {#aem-forms}

### AEM Formsワークフローでの印刷可能出力の生成 {#generate-printable-output}

印刷可能出力の生成ワークフローの手順を使用すると、ソーステンプレートファイルをデータファイルと統合できます。 この統合により、テンプレートファイルの異なるコピーを印刷または保存できます。 この手順で、PCL、PostScript、ZPL、IPL、TPCLまたはDPL出力が生成されます。 この機能について詳しくは、「 [Forms中心のOSGi上のワークフロー — 手順リファレンス」を参照してください](../forms/using/aem-forms-workflow-step-reference.md)。

![印刷可能な出力を生成](assets/generate-print-output-demo.gif)

### レイアウトモードでのアダプティブフォームとインタラクティブ通信の複数列のサポート {#multi-column-adaptive-forms}

アダプティブフォームとインタラクティブな通信で、パネルの列数を定義できるようになりました。 レイアウトモードに切り替えて、新しい複数列オプションを使用します。 詳しくは、レイアウトモードを使用してコ [ンポーネントのサイズを変更するを参照してくださ](../forms/using/resize-using-layout-mode.md)い。

![複数列レイアウト](assets/multi-column-layout.gif)

### AEM受信トレイのカスタマイズ {#aem-inbox}

新しい「管理者制御」オプションを使用すると、管理者は次のことができます。

* ヘッダーテキストとロゴのカスタマイズ

* ヘッダーで使用できるナビゲーションリンクの表示を制御する

「管理者コントロール」オプションは、管理者またはワークフロー管理者グループのメンバーにのみ表示されます。 この機能の詳細については、「受信トレイ」を参 [照してください](../sites-authoring/inbox.md)。

### HTML5フォームでのリッチテキストのサポート {#rich-text-support}

XFAフォームのテキストフィールドをHTML5フォームのリッチテキストフィールドに変換します。 詳しくは、「HTML5フォーム用のフ [ォームテンプレートのデザイン」を参照してください](../forms/using/designing-form-template.md)。

### Accessibility enhancements {#forms-accessibility-enhancements-6540}

Experience Manager Formsには、次のアクセシビリティの強化が含まれています。

* スクリーンリーダーは、アダプティブフォームでチェックボックス、リンク、日付選択、日付入力の各フィールドを正しく読み上げます。

* アダプティブフォームの各ページに、1つのタイトルと1つのメインのランドマークラベルが含まれるようになりました。

## 以前のAEM 6.5サービスパックの主な機能

### ダイナミックメディア向けスマートイメージング(6.5.3.0) {#smart-imaging}

スマートイメージングでは、各ユーザーの独自の表示特性を使用して、エクスペリエンスに最適化された適切な画像を自動的に提供し、パフォーマンスとエンゲージメントを向上させます。 スマートイメージングは、既存の画像プリセットで機能し、配信の直前にインテリジェンスを使用して、ブラウザーまたはネットワークの接続速度に基づいて画像のファイルサイズをさらに低減します。スマートイメ [ージングを参照](../assets/imaging-faq.md)。

### AEM Assetsのビジュアル検索(6.5.2.0) {#visual-search}

Assets ユーザーは、視覚的に類似した画像を検索できます。AEM は、ユーザーが選択した画像に類似した、DAM リポジトリのスマートタグ付き画像を表示します。See [Visual search](../assets/search-assets.md).

### AEM Formsユーザー(6.5.3.0)のインボックス項目の共有とアクセスの要求 {#share-request-access}

受信トレイの項目を別のユーザーと共有できます。 別のユーザーが受信トレイの項目にアクセスしたら、そのユーザーは共有項目を要求し、適切なアクションを実行できます。 同様に、他のユーザーから受信トレイ項目へのアクセスを要求できます。 詳しくは、 [ユーザーのインボックス項目の共有とアクセスの要求を参照してくださ](../forms/using/configure-shared-queues-osgi.md)い。

### AEM Formsユーザー(6.5.3.0)の「Inbox」項目の不在設定の指定 {#configure-out-of-office}

不在にする予定がある場合は、その期間に割り当てられた品目に対して何が起こるかを指定できます。
不在設定が実施される開始日と時刻および終了日と時刻を指定するオプションがあります。すべてのアイテムを送信するデフォルトのユーザーを設定できます。 「不在 [時の設定」を参照してください](../forms/using/configure-out-of-office-settings.md)。

### AEM Forms用のBatch API(6.5.3.0)を使用して複数のインタラクティブな通信を生成する {#generate-multiple-ic}

Batch APIを使用すると、テンプレートから複数のインタラクティブな通信を作成できます。 テンプレートは、データのないインタラクティブな通信です。 Batch APIは、データをテンプレートと組み合わせて、インタラクティブな通信を生成します。 このAPIは、インタラクティブ通信の大量生産に役立ちます。 例えば、電話料金、複数の顧客のクレジットカード明細などです。 Batch APIを使用 [した複数のインタラクティブ通信の生成を参照してくださ](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)い。

## AEM 6.5 SP3以降の主なリリース

2019年12月12日から2020年3月5日まで、アドビは、AEMの主要な成果物以外の次の機能をリリースしました。

* AEM Cloud Manager 2020.1.0および2020.2.0

   パイプラインのステータスを改善し、様々な手順でログをダウンロードする機能を改善。 参照先：

   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)


   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)


* AEM Cloud Manager CLIの更新

   コマンドラインツールを使用して、Cloud Managerのタスクを自動化します。 GitHubを参照 [してください](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases)。

* AEMサイト：プロジェクトのアーキタイプ23

   新しいAEMプロジェクトを開始する最良の方法です。 アーキタイプ23は、SPAと通 [常のサイトのプロジェクトアーキタイプを1つに結合し](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23) 、フロントエンド開発を開始するためのデフォルトのテーマを提供します。

* AEMサイト：WKNDリファレンスサイト

   [AEMを使用してサイトを構築する方法に関する](https://www.wknd.site/) 、ベストプラクティスが詰め込まれた新しいリファレンスプロジェクトです。 詳しくは、最新の [WKNDチュートリアルを参照してください](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)。 GitHubから最新のコードを取得で [きます](https://github.com/adobe/aem-guides-wknd/releases)。

* AEMサイト：コマースCIFコアコンポーネント0.7.0および0.9.0

   AEMサイトとMagento Commerceの統合を参照してください。 コマースに重 [点を置いた専用のコアコンポーネントおよびプロジェクトアーキタイプの拡張を参照してくださ](https://github.com/adobe/aem-core-cif-components/releases)い。

* AEM Assets:デスクトップアプリ2.0.1.1

   詳しくは、ア [セットへのデスクトップアクセスの取得を参照してくださ](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)い。

* AEM Screens:機能パック202001

   AEM内から直接デジタル署名を使用できます。 最新の機能パックを使用して改良点をインストールし、複数のメ [ディアプレーヤー間で同期再生を有効にしま](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)す。

## 役立つリソース

* [AEM 6.5ユーザーガイド](../user-guide/home.md)

* [一般リリースノート（Adobe Experience Manager 6.5）](release-notes.md)

* [Adobe Experience Manager 6.5のService Packリリースノート](sp-release-notes.md)
