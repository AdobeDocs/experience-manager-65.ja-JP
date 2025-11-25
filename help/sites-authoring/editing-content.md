---
title: ページのコンテンツの編集
description: ページが作成されたら、コンテンツを編集して、必要な更新を行うことができます。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: d5cf4478-51e4-4ca8-b3f8-6d7caed7d515
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '3015'
ht-degree: 100%

---

# ページのコンテンツの編集{#editing-page-content}

（新規で、またはローンチやライブコピーの一部として）ページが作成されたら、コンテンツを編集して、必要な更新を行うことができます。

コンテンツは、ページにドラッグ可能な[コンポーネント](/help/sites-authoring/default-components-console.md)（コンテンツのタイプに適したもの）を使用して追加できます。コンポーネントはその後、そのまま編集したり、移動や削除をおこなったりすることができます。

>[!NOTE]
>
>ページを編集するための[適切なアクセス権](/help/sites-administering/security.md)と[権限](/help/sites-administering/security.md#permissions)がアカウントにある必要があります。
>
>問題が発生した場合は、システム管理者にお問い合わせください。

>[!NOTE]
>
>ページ、テンプレート、またはその両方が適切に設定されている場合は、編集中に[レスポンシブレイアウト](/help/sites-authoring/responsive-layout.md)を使用できます。

>[!NOTE]
>
>**編集**&#x200B;モードでは、コンテンツのリンクは表示されますが、**アクセスできません**。コンテンツのリンクを使用して移動する場合は、[プレビューモード](#previewingpagestouchoptimizedui)を使用します。

## ページツールバー {#page-toolbar}

ページツールバーを使用すると、ページ設定に応じた適切な機能にアクセスできます。

![ページツールバー](assets/screen_shot_2018-03-22at111338.png)

ツールバーを使用すると、様々なオプションにアクセスできます。現在のコンテキストと設定によっては、一部のオプションを使用できないことがあります。

* **サイドパネルを切り替え**

  サイドパネルが開きます（または閉じます）。このパネルには、[アセットブラウザー](/help/sites-authoring/author-environment-tools.md#assets-browser)、[コンポーネントブラウザー](/help/sites-authoring/author-environment-tools.md#components-browser)および[コンテンツツリー](/help/sites-authoring/author-environment-tools.md#content-tree)が含まれています。

  ![サイドパネルを切り替え](do-not-localize/screen_shot_2018-03-22at111425.png)

* **ページ情報**

  ページの詳細およびページに対して実行できるアクション（ページ情報の表示と編集、ページのプロパティの表示、およびページの公開／非公開など）を含む[ページ情報](/help/sites-authoring/author-environment-tools.md#page-information)メニューにアクセスできます。

  ![ページ情報](do-not-localize/screen_shot_2018-03-22at111437.png)

* **エミュレーター**

  別のデバイスでのページのルックアンドフィールをエミュレートするために使用する[エミュレーターツールバー](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)を切り替えます。レイアウトモードでは自動的に切り替わります。

  ![エミュレーター](do-not-localize/screen_shot_2018-03-22at111442.png)

* **ContextHub**

  [ContextHub](/help/sites-authoring/ch-previewing.md) を開きます。プレビューモードでのみ使用できます。

  ![Context Hub](assets/screen_shot_2018-03-22at111543.png)

* **ページタイトル**

  情報のためにのみ表示されます。

  ![ページタイトル](assets/screen_shot_2018-03-22at111554.png)

* **モードセレクター**

  現在の[モード](/help/sites-authoring/author-environment-tools.md#page-modes)が表示され、別のモード（編集、レイアウト、タイムワープ、ターゲティングなど）を選択できます。

  ![モードセレクター](assets/chlimage_1-120.png)

* **プレビュー**

  [プレビューモード](/help/sites-authoring/editing-content.md#preview-mode)を有効にします。公開時に表示されるとおりにページを表示します。

  ![プレビューモード](assets/chlimage_1-121.png)

* **注釈**

  ページをレビューするときに、ページに[注釈](/help/sites-authoring/annotations.md)を追加できます。最初の注釈を追加後、アイコンは、ページ上の注釈の数を示す数字に切り替わります。

  ![注釈](do-not-localize/screen_shot_2018-03-22at111638.png)

### ステータスの通知 {#status-notification}

ページが 1 つまたは複数の[ワークフロー](/help/sites-authoring/workflows.md)の一部である場合、この情報はページの編集時に画面の上部にある通知バーに表示されます。

![ワークフローの通知](assets/screen_shot_2018-03-22at111739.png)

>[!NOTE]
>
>ステータスバーは、適切な特権を持つユーザーアカウントにのみ表示されます。

通知には、ページに対して実行されているワークフローが一覧表示されます。ユーザーが現在のワークフローステップに関係している場合は、[ワークフローのステータスに影響する](/help/sites-authoring/workflows-participating.md)オプションや、ワークフローの詳細を取得するオプションを使用できます。例えば、次のようなものがあります。

* **完了** - **作業項目を完了**&#x200B;ダイアログボックスが開きます

* **委任** - **作業項目を完了**&#x200B;ダイアログボックスが開きます

* **詳細を表示** - ワークフローの&#x200B;**詳細**&#x200B;ウィンドウが開きます

通知バーからのワークフローステップの完了および委任は、通知インボックスから[ワークフローに参加](/help/sites-authoring/workflows-participating.md)している場合に動作します。

ページが複数のワークフローの対象である場合は、ワークフローの数が、ワークフローをスクロールできる矢印ボタンと共に通知の右端に表示されます。

![ワークフロー数の通知](assets/chlimage_1-122.png)

## コンポーネントプレースホルダー {#component-placeholder}

コンポーネントプレースホルダーは、コンポーネントをドロップしたときのコンポーネントの配置場所（現在ポインタを置いているコンポーネントの上）を示すインジケーターです。

* コンポーネントをページに追加する（コンポーネントブラウザーからドラッグする）場合：

  ![新しいコンポーネントの追加](assets/screen_shot_2018-03-22at111928.png)

* 既存のコンポーネントを移動する場合：

  ![既存のコンポーネントの移動](assets/screen_shot_2018-03-22at112445.png)

## コンポーネントの挿入 {#inserting-a-component}

### コンポーネントブラウザーからのコンポーネントの挿入 {#inserting-a-component-from-the-components-browser}

[コンポーネントブラウザー](/help/sites-authoring/author-environment-tools.md#components-browser)を使用して、コンポーネントを追加できます。[コンポーネントプレースホルダー](#component-placeholder)にコンポーネントの配置先が表示されます。

1. ページが&#x200B;[**編集**&#x200B;モード](/help/sites-authoring/author-environment-tools.md#page-modes)であることを確認します。
1. [コンポーネントブラウザー](/help/sites-authoring/author-environment-tools.md#components-browser)を開きます。
1. 必要なコンポーネントを[必要な位置](#component-placeholder)までドラッグします。

1. コンポーネントを[編集](#editmovecopypastedelete)します。

>[!NOTE]
>
>モバイルデバイスでは、コンポーネントブラウザーが画面全体に表示されます。コンポーネントをドラッグすると、ブラウザーが閉じてページが再表示され、コンポーネントを配置できるようになります。

### 段落システムからのコンポーネントの挿入 {#inserting-a-component-from-the-paragraph-system}

段落システムの「**ここにコンポーネントをドラッグ**」ボックスを使用して、コンポーネントを追加できます。

1. ページが&#x200B;[**編集**&#x200B;モード](/help/sites-authoring/author-environment-tools.md#page-modes)であることを確認します。
1. 段落システムからコンポーネントを選択して追加するには、2 つの方法があります。

   * 既存のコンポーネントのツールバーまたは「**コンポーネントをここにドラッグ**」ボックスから「**コンポーネントを挿入**」オプション（+）を選択します。

   ![コンポーネントの選択を挿入](assets/screen_shot_2018-03-22at112536.png)

   * デスクトップデバイスを使用している場合は、「**ここにコンポーネントをドラッグ**」ボックスをダブルクリックします。

   **新規コンポーネントを挿入**&#x200B;ダイアログボックスが開き、必要なコンポーネントを選択できるようになります。

   ![新規コンポーネントを挿入](assets/screen_shot_2018-03-22at112650.png)

1. 選択したコンポーネントがページの下部に追加されます。必要に応じて、コンポーネントを[編集](#editmovecopypastedelete)します。

### アセットブラウザーを使用したコンポーネントの挿入 {#inserting-a-component-using-the-assets-browser}

[アセットブラウザー](/help/sites-authoring/author-environment-tools.md#assets-browser)からアセットをドラッグして、コンポーネントをページに追加することもできます。これにより、適切なタイプの新しいコンポーネント（アセットを含む）が自動的に作成されます。

これは次のアセットタイプに有効です（一部はページ／段落システムに依存します）。

<table>
 <tbody>
  <tr>
   <th><strong>アセットタイプ</strong></th>
   <th><strong>結果のコンポーネントのタイプ</strong></th>
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
>この動作は使用しているインストール環境で設定できます。詳しくは、[アセットをドラッグするとコンポーネントインスタンスが作成されるように段落システムを設定する](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance)を参照してください。

前述のいずれかのアセットタイプをドラッグしてコンポーネントを作成するには：

1. ページが&#x200B;[**編集**&#x200B;モード](/help/sites-authoring/author-environment-tools.md#page-modes)であることを確認します。
1. [アセットブラウザー](/help/sites-authoring/author-environment-tools.md#assets-browser)を開きます。
1. 必要なアセットを必要な位置にドラッグします。[コンポーネントプレースホルダー](#component-placeholder)にコンポーネントの配置先が表示されます。

   アセットタイプに適したコンポーネントが、必要な場所に作成されます。これには選択したアセットが含まれます。

1. 必要に応じて、コンポーネントを[編集](#editmovecopypastedelete)します。

>[!NOTE]
>
>モバイルデバイスでは、アセットブラウザーが画面全体に表示されます。アセットをドラッグすると、ブラウザーが閉じてページが再表示され、アセットを配置できるようになります。

アセットを参照したときに、アセットをすばやく変更する必要がある場合は、アセット名の横にある編集アイコンをクリックして、「[アセットエディター](/help/assets/manage-assets.md)」を起動します。

![編集アイコン](assets/screen_shot_2018-03-22at112735.png)

## 編集／設定／コピー／カット／削除／ペースト {#edit-configure-copy-cut-delete-paste}

コンポーネントを選択すると、ツールバーが開きます。これにより、コンポーネントで実行できる様々なアクションにアクセスできます。

ユーザーが使用できる実際のアクションは、必要に応じて表示されます。ここではすべてのアクションについては説明していません。

![コンポーネントツールバーオプション](assets/screen_shot_2018-03-22at112909.png)

* **編集**

  [コンポーネントの種類に応じて](/help/sites-authoring/default-components.md)[コンポーネントのコンテンツを編集](#edit-content)できます。多くの場合、ツールバーが用意されています。

  ![編集](do-not-localize/screen_shot_2018-03-22at112936.png)

* **設定**

  [コンポーネントの種類に応じて](/help/sites-authoring/default-components.md)、コンポーネントのプロパティを編集および設定できます。多くの場合、ダイアログボックスが開きます。

  ![設定](do-not-localize/screen_shot_2018-03-22at112955.png)

* **コピー**

  コンポーネントをクリップボードにコピーします。元のコンポーネントはペースト後も残ります。

  ![コピー](do-not-localize/screen_shot_2018-03-22at113000.png)

* **カット**

  コンポーネントをクリップボードにコピーします。ペースト後、元のコンポーネントは削除されます。

  ![カット](assets/screen_shot_2018-03-22at113007.png)

* **削除**

  確認後に、ページからコンポーネントを削除します。

  ![削除](do-not-localize/screen_shot_2018-03-22at113012.png)

* **コンポーネントを挿入**

  [新しいコンポーネントを追加](/help/sites-authoring/editing-content.md#inserting-a-component-from-the-paragraph-system)するためのダイアログが開きます。

  ![コンポーネントを挿入](do-not-localize/screen_shot_2018-03-22at113017.png)

* **ペースト**

  クリップボードのコンポーネントをページにペーストします。元のコンポーネントが残るかどうかは、コピーまたはカットのどちらを使用したかによって異なります。

   * 同じページまたは別のページにペーストできます。
   * ペースト操作を選択した項目の上に、対象の項目がペーストされます。
   * ペースト操作は、クリップボードにコンテンツがある場合にのみ表示されます。

  ![ペースト](assets/screen_shot_2018-03-22at113553.png)

  >[!NOTE]
  >
  >カット／コピー操作の前に開いていた別のページにペーストする場合は、ページを更新して、ペーストしたコンテンツを表示する必要があります。

* **グループ**

  複数のコンポーネントを一度に選択できます。デスクトップデバイスで同じ操作を行うには、**Control キーを押しながらクリック**&#x200B;するか、または **Command キーを押しながらクリック**&#x200B;します。

  ![グループ](do-not-localize/screen_shot_2018-03-22at113240.png)

* **親**

  選択したコンポーネントの親コンポーネントを選択できます。

  ![親](assets/screen_shot_2018-03-22at113028.png)

* **レイアウト**

  選択したコンポーネントの[レイアウト](/help/sites-authoring/editing-content.md#edit-component-layout)を変更できます。これは選択したコンポーネントにのみ適用され、ページ全体の[レイアウトモード](/help/sites-authoring/author-environment-tools.md#page-modes)はアクティベートされません。

  ![レイアウト](do-not-localize/screen_shot_2018-03-22at113044.png)

* **エクスペリエンスフラグメントバリエーションに変換**

  [エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)を、選択したコンポーネントから作成したり、既存のエクスペリエンスフラグメントに追加したりできます。

  ![エクスペリエンスフラグメントバリエーションに変換](do-not-localize/screen_shot_2018-03-22at113033.png)

## 編集（コンテンツ） {#edit-content}

コンポーネント内のコンテンツを追加または編集するには、次の 2 つの方法があります。

* [編集用のコンポーネントのダイアログ](#component-edit-dialog)を開きます。
* [アセットをドラッグ＆ドロップ](#draganddropintocomponent)して、アセットブラウザーからコンテンツを直接追加します。

### コンポーネント編集ダイアログ {#component-edit-dialog}

[コンポーネントツールバーの編集（鉛筆）アイコン](#edit-configure-copy-cut-delete-paste)を使用して、コンポーネントを開いてコンテンツを編集できます。

実際に使用できる編集オプションはコンポーネントによって異なります。一部のコンポーネントでは、[すべてのアクションが全画面モードでのみ使用できます](#edit-content-full-screen-mode)。例：

* [テキストコンポーネント](/help/sites-authoring/rich-text-editor.md#main-pars-title-24)

  ![テキストコンポーネント](assets/screen_shot_2018-03-22at120215.png)

* 画像コンポーネント

  ![画像コンポーネント](assets/screen_shot_2018-03-22at120252.png)

  >[!NOTE]
  >
  >編集は、空の画像コンポーネントでは動作しません。
  >
  >
  >画像を編集する前に、[（設定を使用して）画像をドラッグまたはアップロード](/help/sites-authoring/default-components-foundation.md#image)します。

* 画像コンポーネント - 全画面

  画像コンポーネントの[全画面モードに入ると](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode)、画像を編集する領域が広くなり、追加の編集オプション（「**マップを起動**」や「**ズームをリセット**」など）が表示されます。また、全画面表示では切り抜きプリセットを選択できます。

  ![画像コンポーネントの全画面表示](assets/screen_shot_2018-03-22at120529.png)

* [テキストと画像の基盤コンポーネント](/help/sites-authoring/default-components-foundation.md#text-image)など、複数の基本コンポーネントから構成されるコンポーネントでは、最初に編集オプションが確認されます。

  ![コンポーネントの編集オプション](assets/chlimage_1-123.png)

### アセットのコンポーネントへのドラッグ＆ドロップ {#drag-and-drop-assets-into-component}

次の特定のコンポーネントタイプでは、アセットブラウザーから直接コンポーネントにアセットをドラッグ＆ドロップして、コンテンツを更新できます。

| **アセットタイプ** | **コンポーネントの種類** |
|---|---|
| 画像 | 画像 |
| ドキュメント | ダウンロード |
| 製品 | 製品 |
| ビデオ | Flash |
| コンテンツフラグメント | コンテンツフラグメント |

## 全画面モードで（コンテンツを）編集 {#edit-content-full-screen-mode}

次のアイコンを使用して、すべてのコンポーネントで全画面表示モードにアクセス（または終了）できます。

![全画面モードで編集](do-not-localize/chlimage_1-20.png)

例えば、**テキスト**&#x200B;コンポーネントの場合は、次のように表示されます。

![テキストエディター](assets/screen_shot_2018-03-22at121616.png)

>[!NOTE]
>
>一部のコンポーネントでは、全画面モードにすると、基本のインプレースエディターより多くのオプションを使用できます。

## コンポーネントの移動 {#moving-a-component}

段落コンポーネントを移動するには：

1. 選択＆ホールドまたはクリック＆ホールドによって移動する段落を選択します。
1. 段落を新しい場所にドラッグします。段落を配置できる場所が示されます。目的の場所にドロップします。

   ![段落コンポーネントの移動](assets/screen_shot_2018-03-22at121821.png)

1. 段落が移動します。

>[!NOTE]
>
>[切り取りと貼り付け](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)を使用して、コンポーネントを移動することもできます。

## コンポーネントのレイアウトの編集 {#edit-component-layout}

コンポーネントを調整するために編集モードから[レイアウトモード](/help/sites-authoring/responsive-layout.md)に繰り返し切り替える代わりに、コンポーネントの&#x200B;**レイアウト**&#x200B;アクションを選択して、そのコンポーネントのレイアウトを変更することができます。これにより、編集モードを終了する必要がなくなり、時間が節約されます。

1. サイトコンソールの&#x200B;**編集**&#x200B;モードでコンポーネントを選択すると、コンポーネントのツールバーが表示されます。

   ![フォームの編集モード](assets/screen_shot_2018-03-22at133756.png)

   **レイアウト**&#x200B;アクションをクリックすると、コンポーネントのレイアウトを調整できます。

   ![コンポーネントツールバー](do-not-localize/chlimage_1-21.png)

1. レイアウトアクションを選択すると、次の処理が行われます。

   * コンポーネントのサイズ変更ハンドルが表示されます。
   * エミュレーターツールバーが画面の上部に表示されます。
   * 標準の編集アクションの代わりにレイアウトアクションが、コンポーネントツールバーに表示されます。

   ![複数のデバイスでのフォームプレビュー](assets/screen_shot_2018-03-22at133843.png)

   [レイアウトモード](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)と同様に、コンポーネントのレイアウトを変更できるようになりました。

1. 必要なレイアウトの変更を加えて、コンポーネントのアクションメニューの「**閉じる**」をクリックすると、コンポーネントのレイアウトの変更が停止します。コンポーネントのツールバーは通常の編集状態に戻ります。

   ![閉じる](do-not-localize/screen_shot_2018-03-22at133920.png)

>[!NOTE]
>
>レイアウトアクションは、選択したコンポーネントの範囲に限定されます。例えば、あるコンポーネントのレイアウトを編集中に別のコンポーネントを選択すると、新しく選択したコンポーネントに対して、レイアウトツールバーではなく標準の編集ツールバーが表示されます。サイズ変更ハンドルとエミュレーターツールバーが非表示になります。
>
>複数のコンポーネントに影響するページの全体のレイアウトを編集する必要がある場合は、[レイアウトモード](/help/sites-authoring/responsive-layout.md)に切り替えます。

## 継承されたコンポーネント {#inherited-components}

継承されたコンポーネントは、次のような様々なシナリオによって生成されます。

* [マルチサイト管理](/help/sites-administering/msm.md)
* [ローンチ](/help/sites-authoring/launches.md)（ライブコピーをベースとしている場合）
* 特定のコンポーネント（Geometrixx 内の継承された段落システムなど）

継承はキャンセル（その後再度有効化）できます。コンポーネントによって、次の場所から操作できます。

* **ライブコピー**

  ライブコピーまたは（ライブコピーに基づいた）ローンチの一部であるページにコンポーネントがある場合のコンポーネントツールバー。例：

  ![ライブコピー](assets/screen_shot_2018-03-22at134339.png)

  「継承をキャンセル」オプションを使用できます。

  ![継承をキャンセル](do-not-localize/screen_shot_2018-03-22at134406.png)

  キャンセル済みの場合は、継承を再度有効にできます。

  ![継承を再度有効にする](do-not-localize/screen_shot_2018-03-22at134417.png)

  ブループリントまたはライブコピーのソースでは、ロールアウトアクションも使用できます。

  ![ロールアウト](do-not-localize/screen_shot_2018-03-22at134516.png)

* **継承された段落システム**

  設定ダイアログボックス。例えば、次のような「継承された段落システム」と同様です。

  ![継承された段落システム](assets/chlimage_1-124.png)

## ページテンプレートの編集 {#editing-the-page-template}

ページが[編集可能なテンプレート](/help/sites-authoring/templates.md#editable-and-static-templates)に基づいている場合は、[ページ情報メニュー](/help/sites-authoring/author-environment-tools.md#page-information)の&#x200B;**編集テンプレート**&#x200B;を選択することによって、[テンプレートエディター](/help/sites-authoring/templates.md#editing-templates-template-authors)に簡単に切り替えることができます。

ページが[静的テンプレート](/help/sites-authoring/templates.md#editable-and-static-templates)に基づいている場合は、ツールバーの[ページモードセレクター](/help/sites-authoring/author-environment-tools.md#page-modes)を使用して[デザインモード](/help/sites-authoring/default-components-designmode.md)に切り替え、ページで使用するコンポーネントを有効／無効にすることができます。

[列表示](/help/sites-authoring/basic-handling.md#column-view)または[リスト表示](/help/sites-authoring/basic-handling.md#list-view)でページを選択するときに、ページが基にしているテンプレートを簡単に確認できます。

## ライブコピーステータス {#live-copy-status}

[ライブコピーステータスページモード](/help/sites-authoring/author-environment-tools.md#page-modes)では、ライブコピーのステータスの簡単な概要、および継承される（または継承されない）コンポーネントを示すことができます。

* 緑のボーダー：継承
* ピンクのボーダー：継承がキャンセルされている

例：

![ライブコピーの継承ステータス](assets/screen_shot_2018-03-22at134820.png)

## 注釈の追加 {#adding-annotations}

[注釈](/help/sites-authoring/annotations.md)を使用すると、レビュー担当者や他の作成者がコンテンツに関するフィードバックを提供できます。注釈は、レビューや検証の目的でよく使用されます。

## ページのプレビュー {#previewing-pages}

ページをプレビューするには、以下の 2 つの方法があります。

* [プレビューモード](#preview-mode) - その場ですばやく確認できるプレビュー

* [公開済みとして表示](#view-as-published) - ページを新しいタブに開くフルプレビュー

>[!NOTE]
>
>* コンテンツ内のリンクは表示されますが、編集モードでアクセスすることはできません。
>* リンクを使用して移動する場合には、いずれかのプレビューオプションを使用してください。
>* プレビューと最後に選択したモードを切り替えるには、[キーボードショートカット](/help/sites-authoring/keyboard-shortcuts.md) `Ctrl-Shift-M` を使用します。
>

>[!NOTE]
>
>両方のオプションで WCM Mode Cookie が設定されています。

### プレビューモード {#preview-mode}

コンテンツの編集時に、プレビュー[モード](/help/sites-authoring/author-environment-tools.md#page-modes)を使用してページをプレビューできます。このモードでは、次の操作を実行できます。

* 各種編集メカニズムを非表示にして、公開時にページがどのように表示されるかをすばやく確認できます。
* リンクを使用して移動できます。
* ページコンテンツは更新&#x200B;**されません**。

オーサリング時に、ページエディターの右上にある次のアイコンを使用して、プレビューモードに切り替えることができます。

![プレビュー](assets/chlimage_1-125.png)

### 公開済みとして表示 {#view-as-published}

「**公開済みとして表示**」オプションは、[ページ情報](/help/sites-authoring/author-environment-tools.md#page-information)メニューで使用できます。これによりページが新しいタブで開き、コンテンツが更新され、ページの公開時と同じ状態で表示されます。

## ページのロック {#locking-a-page}

AEM では、他のユーザーによるコンテンツの変更を防ぐためにページをロックできます。ページのロックは、1 つの特定のページで大量の編集作業を行う場合や、短期間ページを凍結する必要がある場合に便利です。

ページは次のいずれかの場所からロックできます。

* **サイト**&#x200B;コンソール

   1. [選択モード](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)でページを選択します。
   1. ロックアイコンを選択します。

  ![ロックアイコン](assets/screen_shot_2018-03-22at134928.png)

* **ページエディター**

   1. メニューを開くには、**ページ情報**&#x200B;アイコンを選択します。
   1. 「**ページをロック**」オプションを選択します。

ロックすると、コンソール表示の情報が更新され、編集時に鍵マークシンボルがツールバーに表示されます。

![鍵マークシンボル](assets/screen_shot_2018-03-22at135010.png)

>[!CAUTION]
>
>ページのロックは、[別のユーザーとして実行している](/help/sites-administering/security.md#impersonating-another-user)場合に実行できます。ただし、この方法でロックされたページをロック解除できるのは、別のユーザーとして実行したユーザーか、管理者ユーザーです。
>
>実際にページのロック作業を行ったユーザーに成り代わっても、ページをロック解除できません。

## ページのロック解除 {#unlocking-a-page}

ページのロック解除は、[ページのロック](#locking-a-page)と似ています。ページがロックされると、ロックオプションはロック解除アクションに置き換わります。

ページ情報メニューには「**ロック解除**」がオプションとして表示され、サイトコンソールのロックアイコンは&#x200B;**ロック解除**&#x200B;アイコンに置き換わります。

![ロック解除](assets/screen_shot_2018-03-22at134942.png)

>[!CAUTION]
>
>ページのロックは、[別のユーザーとして実行している](/help/sites-administering/security.md#impersonating-another-user)場合に実行できます。ただし、この方法でロックされたページをロック解除できるのは、別のユーザーとして実行したユーザーか、管理者ユーザーです。
>
>実際にページのロック作業を行ったユーザーに成り代わっても、ページをロック解除できません。

## ページ編集の取り消しとやり直し {#undoing-and-redoing-page-edits}

次のアイコンを使用して、アクションの取り消しまたはやり直しを行うことができます。これらのアイコンは、ツールバーに適宜表示されます。

![取り消しとやり直し](do-not-localize/screen_shot_2018-03-23at093614.png)

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
>システム管理者は、インスタンスの要件に応じて、[取り消しとやり直し機能の様々な側面を設定](/help/sites-administering/config-undo.md)できます。

AEM では、ユーザーが実行するアクションの履歴と、それらのアクションを実行した順序が保存されます。つまり、複数のアクションを実行した順に取り消したり、必要に応じて、やり直しを使用して 1 つまたは複数のアクションを再適用したりできます。

コンテンツページで要素（テキストコンポーネントなど）が選択されている場合、取り消しコマンドとやり直しコマンドは選択した項目に適用されます。

取り消しおよびやり直しコマンドの動作は、他のソフトウェアプログラムの動作と同様です。コンテンツに関する決定を行いながら、これらのコマンドを使用して web ページの直近の状態に戻すことができます。例えば、テキスト段落をページ上の別の場所に移動した場合に、取り消しコマンドを使用して、その段落を元の場所に戻すことができます。取り消し前の位置の方がいい場合は、やり直しコマンドを使用して「取り消しを取り消し」ます。

>[!NOTE]
>
>以下の操作を実行できます。
>
>* 取り消しを使用してからページの編集を行っていない限り、アクションをやり直すことができます。
>* 最大 20 回の編集アクションを取り消すことができます（デフォルト設定）。
>* 様々な[キーボードショートカット](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)を利用して取り消しとやり直しを行うこともできます。
>

取り消しおよびやり直しは、次のようなページの変更に対して使用できます。

* 段落の追加、編集、削除および移動
* 段落コンテンツのインプレース編集
* ページ内部での項目のコピー、カットおよび貼り付け

フォームコンポーネントがレンダリングするフォームフィールドは、ページのオーサリング中に指定された値を持つことにはなりません。そのため、取り消しおよびやり直しコマンドは、それらのタイプのコンポーネントの値に対して行った変更には影響を与えません。例えば、ドロップダウンリスト内の値の選択を取り消すことはできません。

>[!NOTE]
>
>ファイルと画像に対する変更の取り消しおよびやり直しには、特別な権限が必要になります。

>[!NOTE]
>
>ファイルや画像への変更の履歴は、少なくとも 10 時間維持されます。この時間を経過すると、変更の取り消しは保証されません。管理者はデフォルトの 10 時間を変更できます。
