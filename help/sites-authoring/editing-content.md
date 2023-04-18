---
title: ページのコンテンツの編集
description: ページが作成されたら、コンテンツを編集して必要な更新を行うことができます。
uuid: 5b4f0a8f-5196-42ea-8413-203783a0b77b
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: f92ed674-5865-4a53-8c3a-369536861f14
docset: aem65
exl-id: d5cf4478-51e4-4ca8-b3f8-6d7caed7d515
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '3047'
ht-degree: 52%

---

# ページのコンテンツの編集 {#editing-page-content}

ページが作成されたら（新規またはローンチまたはライブコピーの一部として）、コンテンツを編集して、必要な更新をおこなうことができます。

コンテンツを追加するには、 [コンポーネント](/help/sites-authoring/default-components-console.md) （コンテンツタイプに適した）ページにドラッグできます。 コンポーネントはその後、そのまま編集したり、移動や削除をおこなったりすることができます。

>[!NOTE]
>
>アカウントに [適切なアクセス権](/help/sites-administering/security.md) および [権限](/help/sites-administering/security.md#permissions) ページを編集する場合。
>
>問題が発生した場合は、システム管理者にお問い合わせください。

>[!NOTE]
>
>ページやテンプレートが適切に設定されていると、編集中に[レスポンシブレイアウト](/help/sites-authoring/responsive-layout.md)を使用できます。

>[!NOTE]
>
>**編集**&#x200B;モードでは、コンテンツのリンクは表示されますが、**アクセスできません**。コンテンツのリンクを使用して移動する場合は、[プレビューモード](#previewingpagestouchoptimizedui)を使用します。

## ページツールバー {#page-toolbar}

ページツールバーを使用すると、ページ設定に応じた適切な機能にアクセスできます。

![screen_shot_2018-03-22at111338](assets/screen_shot_2018-03-22at111338.png)

ツールバーを使用すると、多数のオプションにアクセスできます。 現在のコンテキストと設定によっては、一部のオプションを使用できない場合があります。

* **サイドパネルを切り替え**

   これにより、サイドパネルが開く（または閉じる）ので、 [アセットブラウザー](/help/sites-authoring/author-environment-tools.md#assets-browser), [コンポーネントブラウザー](/help/sites-authoring/author-environment-tools.md#components-browser)、および [コンテンツツリー](/help/sites-authoring/author-environment-tools.md#content-tree).

   ![](do-not-localize/screen_shot_2018-03-22at111425.png)

* **ページ情報**

   次にアクセスできる [ページ情報](/help/sites-authoring/author-environment-tools.md#page-information) ページ上で実行できるページの詳細やアクションを含むメニュー（ページ情報の表示と編集、ページプロパティの表示、ページの公開/非公開を含む）。

   ![](do-not-localize/screen_shot_2018-03-22at111437.png)

* **エミュレーター**

   を切り替えます。 [エミュレーターツールバー](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)：別のデバイスでのページのルックアンドフィールをエミュレートするために使用されます。 これは、レイアウトモードで自動的に切り替えられます。

   ![](do-not-localize/screen_shot_2018-03-22at111442.png)

* **ContextHub**

   を開きます。 [コンテキストハブ](/help/sites-authoring/ch-previewing.md). プレビューモードでのみ使用できます。

   ![screen_shot_2018-03-22at111543](assets/screen_shot_2018-03-22at111543.png)

* **ページタイトル**

   これは単なる情報です。

   ![screen_shot_2018-03-22at111554](assets/screen_shot_2018-03-22at111554.png)

* **モードセレクター**

   現在の [mode](/help/sites-authoring/author-environment-tools.md#page-modes) また、編集、レイアウト、タイムワープ、ターゲット設定など、別のモードを選択することもできます。

   ![chlimage_1-120](assets/chlimage_1-120.png)

* **プレビュー**

   有効 [プレビューモード](/help/sites-authoring/editing-content.md#preview-mode). 公開時に表示されるページが表示されます。

   ![chlimage_1-121](assets/chlimage_1-121.png)

* **注釈**

   次を追加できます： [注釈](/help/sites-authoring/annotations.md) をページに追加します。 最初の注釈の後、アイコンはページ上の注釈の数を示す番号に切り替わります。

   ![](do-not-localize/screen_shot_2018-03-22at111638.png)

### ステータスの通知 {#status-notification}

ページが 1 つまたは複数の[ワークフロー](/help/sites-authoring/workflows.md)の一部である場合、この情報はページの編集時に画面の上部にある通知バーに表示されます。

![screen_shot_2018-03-22at111739](assets/screen_shot_2018-03-22at111739.png)

>[!NOTE]
>
>ステータスバーは、適切な特権を持つユーザーアカウントにのみ表示されます。

通知には、ページに対して実行されているワークフローが一覧表示されます。 ユーザーが現在のワークフローステップに関与している場合は、次のオプションを選択します。 [ワークフローのステータスに影響を与える](/help/sites-authoring/workflows-participating.md) また、ワークフローに関する詳細情報も次のように表示されます。

* **完了** - 「**作業項目を完了**」ダイアログが開きます

* **委任** - 「**作業項目を完了**」ダイアログが開きます

* **詳細を表示** - ワークフローの&#x200B;**詳細**&#x200B;ウィンドウを開きます

通知バーからのワークフローステップの完了および委任は、通知インボックスから[ワークフローに参加](/help/sites-authoring/workflows-participating.md)している場合に動作します。

ページが複数のワークフローの対象である場合は、ワークフローの数がワークフローをスクロールできる矢印ボタンと共に通知の右端に表示されます。

![chlimage_1-122](assets/chlimage_1-122.png)

## コンポーネントプレースホルダー {#component-placeholder}

コンポーネントプレースホルダーは、コンポーネントをドロップしたときの位置を示すインジケーターで、現在カーソルを合わせているコンポーネントの上に表示されます。

* 新しいコンポーネントをページに追加する場合（コンポーネントブラウザーからドラッグ）:

   ![screen_shot_2018-03-22at111928](assets/screen_shot_2018-03-22at111928.png)

* 既存のコンポーネントを移動する場合：

   ![screen_shot_2018-03-22at112445](assets/screen_shot_2018-03-22at112445.png)

## コンポーネントの挿入 {#inserting-a-component}

### コンポーネントブラウザーからのコンポーネントの挿入 {#inserting-a-component-from-the-components-browser}

[コンポーネントブラウザー](/help/sites-authoring/author-environment-tools.md#components-browser)を使用して、新しいコンポーネントを追加できます。[コンポーネントプレースホルダー](#component-placeholder)にコンポーネントの配置先が表示されます。

1. ページが&#x200B;[**編集**&#x200B;モード](/help/sites-authoring/author-environment-tools.md#page-modes)であることを確認します。
1. [コンポーネントブラウザー](/help/sites-authoring/author-environment-tools.md#components-browser)を開きます。
1. 必要なコンポーネントを[必要な位置](#component-placeholder)までドラッグします。

1. コンポーネントを[編集](#editmovecopypastedelete)します。

>[!NOTE]
>
>モバイルデバイスでは、コンポーネントブラウザーが画面全体に表示されます。 コンポーネントのドラッグを開始すると、ブラウザーが閉じてページが再度表示され、コンポーネントを配置できます。

### 段落システムからのコンポーネントの挿入 {#inserting-a-component-from-the-paragraph-system}

段落システムの「**コンポーネントをここにドラッグ**」ボックスを使用して、新しいコンポーネントを追加できます。

1. ページが&#x200B;[**編集**&#x200B;モード](/help/sites-authoring/author-environment-tools.md#page-modes)であることを確認します。
1. 段落システムから新しいコンポーネントを選択して追加する方法は 2 つあります。

   * を選択します。 **コンポーネントを挿入** オプション (+) を既存のコンポーネントのツールバーまたは **ここにコンポーネントをドラッグ** ボックス

   ![screen_shot_2018-03-22at112536](assets/screen_shot_2018-03-22at112536.png)

   * デスクトップデバイスを使用している場合は、「**コンポーネントをここにドラッグ**」ボックスをダブルクリックします。

   **新規コンポーネントを挿入**&#x200B;ダイアログが表示され、必要なコンポーネントを選択できるようになります。

   ![screen_shot_2018-03-22at112650](assets/screen_shot_2018-03-22at112650.png)

1. 選択したコンポーネントがページの下部に追加されます。必要に応じてコンポーネントを[編集](#editmovecopypastedelete)します。

### アセットブラウザーを使用したコンポーネントの挿入 {#inserting-a-component-using-the-assets-browser}

また、ページに新しいコンポーネントを追加するには、 [アセットブラウザー](/help/sites-authoring/author-environment-tools.md#assets-browser). これにより、適切なタイプ（およびアセットを含む）の新しいコンポーネントが自動的に作成されます。

これは次のアセットタイプに有効です（一部はページや段落システムに依存します）。

<table>
 <tbody>
  <tr>
   <th><strong>アセットタイプ</strong></th>
   <th><strong>結果のコンポーネントタイプ</strong></th>
  </tr>
  <tr>
   <td>画像</td>
   <td>画像</td>
  </tr>
  <tr>
   <td>ドキュメント</td>
   <td>ダウンロード</td>
  </tr>
  <tr>
   <td>製品</td>
   <td>製品</td>
  </tr>
  <tr>
   <td>ビデオ</td>
   <td>Flash</td>
  </tr>
  <tr>
   <td>コンテンツフラグメント</td>
   <td>コンテンツフラグメント<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>この動作は使用しているインストール環境で設定できます。詳しくは、 [アセットをドラッグするとコンポーネントインスタンスが作成されるように段落システムを設定する](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) 詳しくは、を参照してください。

前述のいずれかのアセットタイプをドラッグしてコンポーネントを作成するには：

1. ページが&#x200B;[**編集**&#x200B;モード](/help/sites-authoring/author-environment-tools.md#page-modes)であることを確認します。
1. を開きます。 [アセットブラウザー](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. 必要なアセットを必要な位置までドラッグします。 この [コンポーネントプレースホルダー](#component-placeholder) コンポーネントを配置する場所を示します。

   アセットタイプに適したコンポーネントが必要な場所に作成され、選択したアセットが格納されます。

1. [編集](#editmovecopypastedelete) 必要に応じて、コンポーネントを選択します。

>[!NOTE]
>
>モバイルデバイスでは、アセットブラウザーが画面全体に表示されます。 アセットのドラッグを開始すると、ブラウザーが閉じてページが再度表示され、アセットを配置できます。

アセットを参照したときに、アセットをすばやく変更する必要があることに気づいた場合は、 [アセットエディター](/help/assets/manage-assets.md) ブラウザーから直接アセット名の横にある編集アイコンをクリックします。

![screen_shot_2018-03-22at112735](assets/screen_shot_2018-03-22at112735.png)

## 編集/設定/コピー/切り取り/削除/貼り付け {#edit-configure-copy-cut-delete-paste}

コンポーネントを選択すると、ツールバーが開きます。このツールバーからコンポーネントに対して様々なアクションを実行できます。

ユーザーが使用できる実際のアクションは、必要に応じて表示されます。ここではすべてのアクションについては説明していません。

![screen_shot_2018-03-22at112909](assets/screen_shot_2018-03-22at112909.png)

* **編集**

   [コンポーネントの種類に応じて](/help/sites-authoring/default-components.md)[コンポーネントのコンテンツを編集](#edit-content)できます。多くの場合、ツールバーが提供されます。

   ![](do-not-localize/screen_shot_2018-03-22at112936.png)

* **設定**

   [コンポーネントの種類に応じて](/help/sites-authoring/default-components.md)、コンポーネントのプロパティを編集および設定できます。多くの場合、ダイアログが開きます。

   ![](do-not-localize/screen_shot_2018-03-22at112955.png)

* **コピー**

   これにより、コンポーネントがクリップボードにコピーされます。 貼り付け操作の後も、元のコンポーネントは保持されます。

   ![](do-not-localize/screen_shot_2018-03-22at113000.png)

* **切り取り**

   これにより、コンポーネントがクリップボードにコピーされます。 貼り付け操作の後、元のコンポーネントは削除されます。

   ![screen_shot_2018-03-22at113007](assets/screen_shot_2018-03-22at113007.png)

* **削除**

   これにより、確認を含むページからコンポーネントが削除されます。

   ![](do-not-localize/screen_shot_2018-03-22at113012.png)

* **コンポーネントの挿入**

   これにより、次のダイアログが開きます。 [新しいコンポーネントを追加](/help/sites-authoring/editing-content.md#inserting-a-component-from-the-paragraph-system).

   ![](do-not-localize/screen_shot_2018-03-22at113017.png)

* **貼り付け**

   これにより、コンポーネントがクリップボードからページに貼り付けられます。 オリジナルが残るかどうかは、コピーを使用したか切り取ったかによって異なります。

   * 同じページまたは別のページに貼り付けることができます。
   * 貼り付けられた項目は、貼り付けアクションを選択した項目の上に貼り付けられます。
   * 貼り付けアクションは、クリップボードにコンテンツがある場合にのみ表示されます。

   ![screen_shot_2018-03-22at113553](assets/screen_shot_2018-03-22at113553.png)

   >[!NOTE]
   >
   >切り取り/コピー操作の前に開いていた別のページに貼り付ける場合は、ページを更新して、貼り付けたコンテンツを表示する必要があります。

* **グループ**

   これにより、複数のコンポーネントを一度に選択できます。 デスクトップデバイスで同じ操作をおこなうには、**Ctrl キーを押しながらクリック**&#x200B;するか、または **Command キーを押しながらクリック**&#x200B;します。

   ![](do-not-localize/screen_shot_2018-03-22at113240.png)

* **親**

   選択したコンポーネントの親コンポーネントを選択できます。

   ![screen_shot_2018-03-22at113028](assets/screen_shot_2018-03-22at113028.png)

* **レイアウト**

   これにより、 [レイアウト](/help/sites-authoring/editing-content.md#edit-component-layout) 選択したコンポーネントの。 これは、選択したコンポーネントにのみ適用され、 [レイアウトモード](/help/sites-authoring/author-environment-tools.md#page-modes) ページ全体に対して

   ![](do-not-localize/screen_shot_2018-03-22at113044.png)

* **エクスペリエンスフラグメントバリエーションに変換**

   これを使用すると、選択したコンポーネントから新しい[エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)を作成したり、既存のエクスペリエンスフラグメントに追加したりできます。

   ![](do-not-localize/screen_shot_2018-03-22at113033.png)

## 編集（コンテンツ） {#edit-content}

コンポーネント内のコンテンツを追加または編集するには、次の 2 つの方法があります。

* を開きます。 [編集用のコンポーネントダイアログ](#component-edit-dialog).
* [アセットをドラッグ&amp;ドロップ](#draganddropintocomponent) アセットブラウザーからコンテンツを直接追加します。

### コンポーネント編集ダイアログ {#component-edit-dialog}

[コンポーネントツールバーの編集（鉛筆）アイコン](#edit-configure-copy-cut-delete-paste)を使用して、コンポーネントを開いてコンテンツを編集できます。

正確な編集オプションは、コンポーネントによって異なります。一部のコンポーネントでは[全画面表示モードでのみすべてのアクションを使用できます](#edit-content-full-screen-mode)。次に例を示します。

* [テキストコンポーネント](/help/sites-authoring/rich-text-editor.md#main-pars-title-24)

   ![screen_shot_2018-03-22at120215](assets/screen_shot_2018-03-22at120215.png)

* 画像コンポーネント

   ![screen_shot_2018-03-22at120252](assets/screen_shot_2018-03-22at120252.png)

   >[!NOTE]
   >
   >編集は、空の画像コンポーネントでは動作しません。
   >
   >
   >必ず [画像のドラッグまたはアップロード（設定を使用）](/help/sites-authoring/default-components-foundation.md#image) 編集を開始する前に

* 画像コンポーネント — 全画面表示

   画像コンポーネント[の全画面表示モードに入ると](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode)、画像を編集する領域が広くなり、追加の編集オプション（「**マップを起動**」や「**ズームをリセット**」など）が表示されます。また、全画面表示では切り抜きプリセットを選択できます。

   ![screen_shot_2018-03-22at120529](assets/screen_shot_2018-03-22at120529.png)

* [テキストと画像の基盤コンポーネント](/help/sites-authoring/default-components-foundation.md#text-image)など、複数の基本コンポーネントから構成されるコンポーネントでは、最初に編集オプションが確認されます。

   ![chlimage_1-123](assets/chlimage_1-123.png)

### アセットのコンポーネントへのドラッグ＆ドロップ {#drag-and-drop-assets-into-component}

特定のコンポーネントタイプでは、アセットブラウザーから直接コンポーネントにアセットをドラッグ&amp;ドロップして、コンテンツを更新できます。

| **アセットタイプ** | **コンポーネントの種類** |
|---|---|
| 画像 | 画像 |
| ドキュメント | ダウンロード |
| 製品 | 製品 |
| ビデオ | Flash |
| コンテンツフラグメント | コンテンツフラグメント |

## （コンテンツ）全画面表示モードの編集 {#edit-content-full-screen-mode}

次のアイコンを使用して、すべてのコンポーネントで全画面表示モードにアクセス（または終了）できます。

![](do-not-localize/chlimage_1-20.png)

例えば、**テキスト**&#x200B;コンポーネントの場合は、次のように表示されます。

![screen_shot_2018-03-22at121616](assets/screen_shot_2018-03-22at121616.png)

>[!NOTE]
>
>一部のコンポーネントでは、全画面表示モードには、基本のインプレースエディターよりも多くのオプションが用意されています。

## コンポーネントの移動 {#moving-a-component}

段落コンポーネントを移動するには：

1. タップ&amp;ホールドまたはクリック&amp;ホールドで移動する段落を選択します。
1. 段落を新しい場所にドラッグします。 AEMは、段落を預ける場所を示します。 目的の場所にドロップします。

   ![screen_shot_2018-03-22at121821](assets/screen_shot_2018-03-22at121821.png)

1. 段落が移動します。

>[!NOTE]
>
>[切り取りと貼り付け](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)を使用して、コンポーネントを移動することもできます。

## コンポーネントのレイアウトの編集 {#edit-component-layout}

コンポーネントを調整するために編集モードから[レイアウトモード](/help/sites-authoring/responsive-layout.md)に繰り返し切り替える代わりに、コンポーネントの&#x200B;**レイアウト**&#x200B;アクションを選択してそのコンポーネントのレイアウトを変更すると、編集モードから切り替える必要がなくなり、時間を節約できます。

1. サイトコンソールの&#x200B;**編集**&#x200B;モードでコンポーネントを選択すると、コンポーネントのツールバーが表示されます。

   ![screen_shot_2018-03-22at133756](assets/screen_shot_2018-03-22at133756.png)

   コンポーネントのレイアウトを調整するには、**レイアウト**&#x200B;アクションをクリックまたはタップします。

   ![](do-not-localize/chlimage_1-21.png)

1. 「Layout」アクションを選択したら、次の操作を実行します。

   * コンポーネントのサイズ変更ハンドルが表示されます。
   * 画面の上部にエミュレーターツールバーが表示されます。
   * 標準の編集アクションの代わりにレイアウトアクションがコンポーネントツールバーに表示されます。

   ![screen_shot_2018-03-22at133843](assets/screen_shot_2018-03-22at133843.png)

   [レイアウトモード](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)と同様に、コンポーネントのレイアウトを変更できるようになりました。

1. 必要なレイアウトの変更を加えて、コンポーネントのアクションメニューの「**閉じる**」ボタンをクリックすると、コンポーネントのレイアウトの変更が終わります。コンポーネントのツールバーは通常の編集状態に戻ります。

   ![](do-not-localize/screen_shot_2018-03-22at133920.png)

>[!NOTE]
>
>レイアウトアクションは、選択したコンポーネントの範囲に限定されます。例えば、あるコンポーネントのレイアウトを編集してから別のコンポーネントをクリックすると、新しく選択したコンポーネントに（レイアウトツールバーではなく）標準の編集ツールバーが表示され、サイズ変更ハンドルとエミュレーターツールバーが表示されなくなります。
>
>複数のコンポーネントに影響するページの全体のレイアウトを編集する必要がある場合は、[レイアウトモード](/help/sites-authoring/responsive-layout.md)に切り替えます。

## 継承されたコンポーネント {#inherited-components}

継承されたコンポーネントは、次のような様々なシナリオによって生成されます。

* [マルチサイト管理](/help/sites-administering/msm.md)
* [ローンチ](/help/sites-authoring/launches.md)（ライブコピーをベースとしている場合）
* 特定のコンポーネント（Geometrixx 内の継承された段落システムなど）

継承はキャンセル（その後再度有効化）できます。コンポーネントに応じて、次の場所から使用できます。

* **ライブコピー**

   ライブコピーまたは（ライブコピーに基づく）ローンチの一部であるページ上にコンポーネントがある場合、コンポーネントツールバー。 次に例を示します。

   ![screen_shot_2018-03-22at134339](assets/screen_shot_2018-03-22at134339.png)

   「継承をキャンセル」オプションを使用できます。

   ![](do-not-localize/screen_shot_2018-03-22at134406.png)

   または、既にキャンセルされている場合は継承を再度有効にします。

   ![](do-not-localize/screen_shot_2018-03-22at134417.png)

   ブループリントまたはライブコピーのソースでは、ロールアウトアクションも使用できます。

   ![](do-not-localize/screen_shot_2018-03-22at134516.png)

* **継承された段落システム**

   設定ダイアログ。 例えば、継承された段落システムの場合は次のようになります。

   ![chlimage_1-124](assets/chlimage_1-124.png)

## ページテンプレートの編集 {#editing-the-page-template}

ページが [編集可能なテンプレート](/help/sites-authoring/templates.md#editable-and-static-templates)を使用すると、 [テンプレートエディター](/help/sites-authoring/templates.md#editing-templates-template-authors) 選択する **テンプレートを編集** 内 [ページ情報メニュー](/help/sites-authoring/author-environment-tools.md#page-information).

ページが[静的テンプレート](/help/sites-authoring/templates.md#editable-and-static-templates)に基づいている場合は、ツールバーの[ページモードセレクター](/help/sites-authoring/author-environment-tools.md#page-modes)を使用して[デザインモード](/help/sites-authoring/default-components-designmode.md)に切り替え、ページで使用するコンポーネントを有効／無効にすることができます。

[列表示](/help/sites-authoring/basic-handling.md#column-view)または[リスト表示](/help/sites-authoring/basic-handling.md#list-view)でページを選択するときに、ページが基にしているテンプレートを簡単に確認できます。

## ライブコピーステータス {#live-copy-status}

この [ライブコピーステータスページモード](/help/sites-authoring/author-environment-tools.md#page-modes) ライブコピーのステータスと継承される（または継承されない）コンポーネントの概要を簡単に確認できます。

* 緑の境界線：継承
* ピンクの境界線：継承がキャンセルされました

次に例を示します。

![screen_shot_2018-03-22at134820](assets/screen_shot_2018-03-22at134820.png)

## 注釈の追加 {#adding-annotations}

[注釈](/help/sites-authoring/annotations.md) レビュー担当者や他の作成者がコンテンツに関するフィードバックを提供することを許可します。 多くの場合、レビューや検証の目的で使用されます。

## ページのプレビュー {#previewing-pages}

ページをプレビューするには、以下の 2 つの方法があります。

* [プレビューモード](#preview-mode) - その場ですばやく確認できるプレビュー

* [公開済みとして表示](#view-as-published)  — ページを新しいタブで開く完全なプレビュー

>[!NOTE]
>
>* コンテンツ内のリンクは表示されますが、編集モードではアクセスできません。
>* リンクを使用して移動する場合には、いずれかのプレビューオプションを使用してください。
>* プレビューと最後に選択したモードを切り替えるには、[キーボードショートカット](/help/sites-authoring/keyboard-shortcuts.md) `Ctrl-Shift-M` を使用します。
>


>[!NOTE]
>
>両方のオプションに WCM Mode Cookie が設定されている。

### プレビューモード {#preview-mode}

コンテンツの編集時に、プレビューを使用してページをプレビューできます [mode](/help/sites-authoring/author-environment-tools.md#page-modes). このモード：

* 各種編集メカニズムを非表示にして公開時にページがどのように表示されるかをすばやく確認できます。
* リンクを使用して移動できます。
* 実行 **not** ページコンテンツを更新します。

オーサリング時には、ページエディターの右上にある次のアイコンを使用してプレビューモードを使用できます。

![chlimage_1-125](assets/chlimage_1-125.png)

### 公開済みとして表示 {#view-as-published}

この **公開済みとして表示** オプションは、 [ページ情報](/help/sites-authoring/author-environment-tools.md#page-information) メニュー これにより、新しいタブでページが開き、コンテンツが更新され、ページがパブリッシュ環境で表示されるとおりに表示されます。

## ページのロック {#locking-a-page}

AEM では、他のユーザーによるコンテンツの変更を防ぐためにページをロックすることができます。ページのロックは、1 つの特定のページで大量の編集作業をおこなう場合や、短期間ページを凍結する必要がある場合に便利です。

ページは次のいずれかからロックできます。

* **サイト** コンソール

   1. を含むページを選択します。 [選択モード](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
   1. ロックアイコンを選択します。

   ![screen_shot_2018-03-22at134928](assets/screen_shot_2018-03-22at134928.png)

* **ページエディター**

   1. を選択します。 **ページ情報** アイコンをクリックしてメニューを開きます。
   1. を選択します。 **ページをロック** オプション。

ロックすると、コンソール表示の情報が更新され、編集時にロック記号がツールバーに表示されます。

![screen_shot_2018-03-22at135010](assets/screen_shot_2018-03-22at135010.png)

>[!CAUTION]
>
>ページのロックは、[別のユーザーとして実行している](/help/sites-administering/security.md#impersonating-another-user)場合に実行できます。ただし、この方法でロックされたページのロックを解除できるのは、別のユーザーとして実行されたか、管理者ユーザーによってのみです。
>
>実際にページのロック作業を行ったユーザーに成り代わっても、ページをロック解除できません。

## ページのロック解除 {#unlocking-a-page}

ページのロック解除は、[ページのロック](#locking-a-page)とよく似ています。ページがロックされると、ロックオプションはロック解除アクションに置き換えられます。

ページ情報メニューには「**ロック解除**」がオプションとして表示され、サイトコンソールのロックアイコンは「**ロック解除**」アイコンに置き換えられます。

![screen_shot_2018-03-22at134942](assets/screen_shot_2018-03-22at134942.png)

>[!CAUTION]
>
>ページのロックは、[別のユーザーとして実行している](/help/sites-administering/security.md#impersonating-another-user)場合に実行できます。ただし、この方法でロックされたページのロックを解除できるのは、別のユーザーとして実行されたか、管理者ユーザーによってのみです。
>
>実際にページのロック作業を行ったユーザーに成り代わっても、ページをロック解除できません。

## ページ編集の取り消しとやり直し {#undoing-and-redoing-page-edits}

次のアイコンを使用して、アクションの取り消しまたはやり直しを行うことができます。これらのアイコンは、ツールバーに適宜表示されます。

![](do-not-localize/screen_shot_2018-03-23at093614.png)

>[!NOTE]
>
>[キーボードショートカット](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) `Ctrl-Z` を使用して、ページの編集アクションを取り消すこともできます。
>
>キーボードショートカット `Ctrl-Y` を使用して、ページの編集アクションをやり直すこともできます。

>[!NOTE]
>
>ページ編集の取り消しとやり直しによって実行可能なことについて詳しくは、[ページ編集の取り消しとやり直し - 理論](#undoing-and-redoing-page-edits-the-theory)を参照してください。

## ページ編集の取り消しとやり直し - 理論 {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>システム管理者は、インスタンスの要件に従って[取り消しおよびやり直し機能の様々な面を設定](/help/sites-administering/config-undo.md)できます。

AEM では、ユーザーが実行するアクションの履歴と、それらのアクションを実行した順序が保存されます。そのため、複数のアクションの取り消しは、ユーザーが実行した順序でおこなうことができます。その後、必要に応じて、やり直しを使用して 1 つ以上のアクションを再適用することもできます。

コンテンツページで要素（テキストコンポーネントなど）が選択されている場合、取り消しコマンドとやり直しコマンドは選択した項目に適用されます。

取り消しコマンドとやり直しコマンドの動作は、他のソフトウェアプログラムの動作と同じです。 コンテンツに関する決定を行う際に、Web ページの最新の状態を復元するには、コマンドを使用します。 例えば、テキスト段落をページ上の別の場所に移動した場合に、取り消しコマンドを使用して、その段落を元の場所に戻すことができます。その後、前の位置の方が良いと判断した場合は、やり直しコマンドを使用して「元に戻す」操作を元に戻します。

>[!NOTE]
>
>以下の操作を実行できます。
>
>* 取り消しを使用してからページの編集を行っていない限り、操作をやり直します。
>* 最大 20 個の編集アクションを取り消します（デフォルト設定）。
>* また、 [キーボードショートカット](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) 元に戻す/やり直しの場合。
>


取り消しとやり直しは、次のタイプのページの変更に対して使用できます。

* 段落の追加、編集、削除および移動
* 段落コンテンツのインプレース編集
* ページ内の項目のコピー、切り取り、貼り付け

フォームコンポーネントがレンダリングするフォームフィールドは、ページのオーサリング時に値を指定するものではありません。 したがって、取り消しコマンドとやり直しコマンドは、これらのタイプのコンポーネントの値に加えた変更には影響しません。 例えば、コンボボックス内の値の選択を取り消すことはできません。

>[!NOTE]
>
>ファイルと画像に対する変更の取り消しおよびやり直しには、特別な権限が必要になります。

>[!NOTE]
>
>ファイルおよび画像に対する変更の履歴は、少なくとも 10 時間保持されます。 ただし、これ以降は、変更の取り消しは保証されません。 管理者は、デフォルトの 10 時間を変更できます。
