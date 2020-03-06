---
title: Adobe Experience Manager 6.5 Service Pack 4の新機能
description: Adobe Experience Manager 6.5 Service Pack 4の新機能
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 14df85f7a815fe567ea87375727ebe1e54733464

---


# Adobe Experience Manager 6.5 Service Pack 4の新機能 {#aem-whats-new-service-pack-4}

2020年には、Adobe Experience Manager (AEM) 6.5で、四半期ごとのService Packの機能と継続的な改善が行われました。 お客様は、この新しいアプローチを利用して、より迅速に革新的な技術を導入できるようになります。

最新のAEM Service Pack 4(6.5.4.0)は、2020年3月6日にリリ **ースされます**。 この記事では、AEMの遍歴をより豊かにするために最新のService Packが提供する機能に焦点を当てています。

## AEM Sites {#aem-sites}

### 各領域のパフォーマンスの向上 {#performance-improvements}

* サイト内のContextHubの読み込みと初期化に要する時間を短縮しました(contexthub.kernel.js)。 その結果、サイト訪問中のページの読み込みが速くなります。

* ページエディターのキャンバスでエクスペリエンスフラグメントをドラッグ&amp;ドロップした後に、ページを更新する時間を短縮しました。

* ライブコピーの概要で、サイトに200を超えるライブコピーがある場合にエントリの読み込み時間を短縮。

* テンプレートエディターで、テンプレートエディターの動作が遅くなる可能性がある、不完全または無効なURLの処理を改善しました。

また、AEM 6.5 SP4にはスタイルシステムの機能強化が含まれています。 コンポーネントダイアログ内でスタイルを選択することもできるようになりました。


## AEM Assets {#aem-assets}

### Adobe I/Oコンソールを通じたBrand Portalとの統合 {#assets-integration-bp}

Adobe I/Oを通じてAEM AssetsがBrand Portalで設定され、Brand Portalテナントの認証用にIMSトークンが調達されるようになりました。 以前は、従来のOAuth Gatewayを介してClassic UIで設定されていました。

レガシーOAuthとの新しい統合は、2020年4月6日以降はサポートされなくなり、Adobe I/Oコンソールに移行します。 統合を変更しない場合、既存の設定は引き続き機能します。

新しい統合を作成するか、統合設定をAdobe I/Oコンソールにアップグレードできます。

### Accessibility enhancements {#accessibility-enhancements}

* 混合状態のチェックボックスの属性の値が「mixed」に設定され、混合状態がスクリーンリーダーに表示されるようになりました。

* キーボードベースのコントロールが、パスベースのジェスチャーとは別に、ズームされた画像内を移動できるようになりました。

* キーボードのみのユーザーが手動で日付を入力できるように、日付形式の制約がフィールドラベルに追加されました。

* Alt属性が装飾アイコンに追加され、role=img属性が削除され、そのようなアイコンや画像がスクリーンリーダーユーザーに表示されなくなりました。

* Alt属性が閉じるアイコンに追加され、Tabキーでスクリーンリーダーユーザーに通知できるようになりました。

## AEM Forms {#aem-forms}

### AEM Formsワークフローでの印刷可能出力の生成 {#generate-printable-output}

ソリューションでソーステンプレートファイルの複数のコピーを印刷し、多数のレコードを含むデータファイルと統合する場合、AEM Formsで新しい印刷可能出力の生成ワークフロー手順を使用できます。 例えば、印刷のたびに異なる名前でソースフォームを印刷する場合は、データファイルにそれらの名前を付け、標準のテンプレートファイルと統合できます。

この機能を利用するには、 **Create** / **[!UICONTROL Models]****[!UICONTROL /]** CreateCreate/ **[!UICONTROL Search]****** /Printable Output Workflow Stepを使用し、Printable Output Workflow Stepを使用します。

![印刷可能な出力を生成](assets/generate-print-output-demo.gif)

この機能について詳しくは、「 [Forms中心のOSGi上のワークフロー — 手順リファレンス」を参照してください](../forms/using/aem-forms-workflow-step-reference.md)。

### レイアウトモードでのアダプティブフォームとインタラクティブ通信の複数列のサポート {#multi-column-adaptive-forms}

アダプティブフォームとインタラクティブな通信で、パネルの列数を定義できるようになりました。

新しいオプションを見つけるには、レイアウトモードに切り替え、複数列形式に変換するパネルをタップし、親を選択し、次の図に示す複数列アイコンをタップして、パネルの列数を定義します。

![複数列レイアウト](assets/multi-column-layout.gif)

詳しくは、レイアウトモードを使用してコ [ンポーネントのサイズを変更するを参照してくださ](../forms/using/resize-using-layout-mode.md)い。

### AEM受信トレイのカスタマイズ {#aem-inbox}

AEMヘッダーで利用できるオプションをカスタマイズする必要があると感じることはありますか？ 新しいService Packリリースで、管理者コントロールオプションが導入されたので、この機能が **[!UICONTROL 利用できます]** 。

**ヘッダーテキストをカスタマイズ**

ワークフロー管理者グル **ープに属するユーザーは** 、上部に表示されるヘッダーテキストを独自の選択テキストでカスタマイズして、既存の **[!UICONTROL Adobe Experience Manager]** のテキストを置き換えることができます。

新しい「 **[!UICONTROL Customize header text]** 」オプションは、ビューセレクター（ツールバーの右上にあります）/管理コントロールにあ **[!UICONTROL ります]**。

**ロゴのカスタマイズ**

ヘッダーテキストのカスタマイズと同様に、ワークフ **ロー管理者グループに属するユーザーは** 、選択したロゴを使用して上部のロゴをカスタマイズできるようになりました。

新しい「ロゴのカスタマイズ」 **[!UICONTROL オプションは]** 、ビューセレクター/管理コントロールの下に **[!UICONTROL あります]**。

この機能の詳細については、「受信トレイ」を参 [照してください](../sites-authoring/inbox.md)。

### ユーザーナビゲーションコントロール {#user-navigation-control}

ワークフロー管理者グ **ループに属するユーザーは** 、その役割に基づいて、制限モードでAEM上でユーザーを操作するオプションを持ちます。 管理者は、ヘッダーで使用できるナビゲーションオプションの表示を制御し、ワークフローオーサリングモードに切り替えたり、ヘルプや他のソリューションリンクに移動したりするようにユーザーに制限できます。

ビューセレクター/管理コントロ **[!UICONTROL ールの下にある]** 、新しい「非表示」ナビゲーションオプションを **[!UICONTROL 確認しま]**&#x200B;す。

この機能の詳細については、「受信トレイ」を参 [照してください](../sites-authoring/inbox.md)。

### HTML5フォームでのリッチテキストのサポート {#rich-text-support}

レンダリングされたHTML5フォームで、テキストフィールドに形式設定オプションのリストを表示できるようになりました。 フィールドに適切な設定を適用するには、Forms Designerでテキストフィールドのフィールド形式を定義する必要があります。

この機能を使用するには、Forms Designerのデザインビューでテキ **[!UICONTROL ストフィールド]** をタップします。 「フィール **[!UICONTROL ド]** 」タブで、「フ **[!UICONTROL ィールドの形式]** 」ドロップダウンリストから **** 「リッチテキスト」を選択し、設定を適用します。 HTML5フォームでレンダリングする際に、テキストフィールドに形式設定オプションが表示されるようになりました。

詳しくは、「HTML5フォーム用のフ [ォームテンプレートのデザイン」を参照してください](../forms/using/designing-form-template.md)。

## 主なハイライト

AEM 6.5 Service Pack 4には、新機能に加え、次の主なハイライトが含まれています。

* 一部のコンテンツサブツリーのみを、すべてではなくScene7と同期できるようになりまし `content/dam`た。

* SOAP Webサービスを使用したフォームデータモデルの統合で、要素の選択グループまたは属性がサポートされるようになりました。

* SOAPの入力または出力と複雑なデータ構造で、動的グループの置換がサポートされるようになりました。

## 以前のAEM 6.5サービスパックの主な機能

### ダイナミックメディア向けスマートイメージング {#smart-imaging}

スマートイメージングでは、各ユーザーに固有の閲覧特性を利用して、ユーザーのエクスペリエンス用に最適化された適切な画像を自動的に提供することで、より良いパフォーマンスとエンゲージメントをもたらします。スマートイメージングは、既存の画像プリセットで機能し、配信の直前にインテリジェンスを使用して、ブラウザーまたはネットワークの接続速度に基づいて画像のファイルサイズをさらに低減します。スマートイメ [ージングを参照](../assets/imaging-faq.md)。

### AEM Assetsのビジュアル検索 {#visual-search}

Assets ユーザーは、視覚的に類似した画像を検索できます。AEM は、ユーザーが選択した画像に類似した、DAM リポジトリのスマートタグ付き画像を表示します。See [Visual search](../assets/search-assets.md).

### ユーザーの受信トレイ項目の共有とアクセスの要求 {#share-request-access}

受信トレイの項目を別のユーザーと共有できます。 別のユーザーが受信トレイのアイテムにアクセスできたら、共有アイテムに対して適切なアクションを実行できます。 同様に、他のユーザーから受信トレイ項目へのアクセスを要求できます。 詳しくは、 [ユーザーのインボックス項目の共有とアクセスの要求を参照してくださ](../forms/using/configure-shared-queues-osgi.md)い。

### 受信トレイ項目の不在設定の構成 {#configure-out-of-office}

不在にする予定がある場合は、その期間に割り当てられた品目に対して何が起こるかを指定できます。
不在設定が実施される開始日と時刻および終了日と時刻を指定するオプションがあります。すべてのアイテムを送信するデフォルトのユーザーを設定できます。 「不在 [時の設定」を参照してください](../forms/using/configure-out-of-office-settings.md)。

### Batch APIを使用して複数のインタラクティブな通信を生成する {#generate-multiple-ic}

Batch APIを使用すると、テンプレートから複数のインタラクティブな通信を作成できます。 テンプレートは、データのないインタラクティブな通信です。 Batch APIは、データをテンプレートと組み合わせて、インタラクティブな通信を生成します。 このAPIは、インタラクティブ通信の大量生産に役立ちます。 例えば、電話料金、複数の顧客のクレジットカード明細などです。 Batch APIを使用 [した複数のインタラクティブ通信の生成を参照してくださ](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)い。

### アダプティブフォームの標準検証エラーメッセージ {#standard-validation}

アダプティブフォームをカスタムサービスと統合して、データ検証を実行できるようになりました。 入力値が検証条件を満たさず、サーバーが返す検証エラーメッセージが標準のメッセージ形式の場合、エラーメッセージはフォームのフィールドレベルで表示されます。 入力値が検証条件を満たさず、サーバー検証エラーメッセージが標準メッセージ形式でない場合、アダプティブフォームは検証エラーメッセージを標準形式に変換し、フォームのフィールドレベルで表示するメカニズムを提供します。 「アダプテ [ィブフォームの標準検証エラーメッセージ](../forms/using/standard-validation-error-messages-adaptive-forms.md)」を参照。

## AEM 6.5 SP3以降の主なリリース

2019年12月12日から2020年3月5日までに、アドビはAEMの主要な成果物以外の次の機能をリリースしました。

* AEM Cloud Manager 2020.1.0および2020.2.0Cloud Managerの月別の機能強化、最近の2つのリリースでは、パイプラインのステータスの改善と様々な手順のログのダウンロード機能に重点を置いています。 以下のリリースノートを参照してください。
   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)

   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* AEM Cloud Manager CLIの更新コマンドラインツールを使用してCloud Managerのタスクを自動化します。 引き続きCLIの拡張 — [GitHubへの加入を行っています](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases)。

* AEMサイト：プロジェクトアーキタイプ23新しいAEMプロジェクトを開始する最良の方法。 アーキタイプ23では、SPA [と通常のサイトのプロジェクト・アーキタイプを1つに統合し](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23)、フロントエンド開発を開始するためのデフォルトのテーマを提供します。

* AEMサイト：WKNDリファレンスサイトAEMを使 [用してサイトを構築する方法に関する](https://www.wknd.site/) 、すべての新しいリファレンスプロジェクトにベストプラクティスが組み込まれています。 詳しくは、完全に更新された [WKNDチュートリアルを参照し](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html) 、GitHubからコードを入手して [ください](https://github.com/adobe/aem-guides-wknd/releases)。

* AEMサイト：コマースCIFコアコンポーネント0.7.0および0.9.0AEM SitesとMagento Commerceの統合を参照してください。 コアコンポーネントと [プロジェクトのアーキタイプを、コマースに重点を置いて引き続き拡張しています](https://github.com/adobe/aem-core-cif-components/releases)。

* AEM Assets:デスクトップアプリ2.0.1.1
   [アセットへのデスクトップアクセスを取得する](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)

* AEM Screens:機能パック202001デジタル署名はAEM内から直接実行できます。 最新の機能パックで最新の機能強化を入手し、今回は複数のメディアプ [レイヤーで同期再生を有効にします](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)。

## 役立つリソース

* [AEM 6.5ユーザーガイド](../user-guide/capabilities.md)

* [一般リリースノート（Adobe Experience Manager 6.5）](release-notes.md)

* [Adobe Experience Manager 6.5のService Packリリースノート](sp-release-notes.md)
