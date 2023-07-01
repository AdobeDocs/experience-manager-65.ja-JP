---
title: ページのコンテンツの編集
description: コンテンツは、ページにドラッグできるコンポーネントを使用して追加されます。 コンポーネントはその後、そのまま編集したり、移動や削除をおこなったりすることができます。
uuid: e7b65ceb-263c-46f2-91e3-11dec3a016fa
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: de321869-ebf9-41a1-8203-e12bdb088678
docset: aem65
exl-id: e1b5aea0-983c-4e7b-9d35-d7beeee45dc7
source-git-commit: 4fd5e9a1bc603202ee52e85a1c09125b13cec315
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 33%

---

# ページのコンテンツの編集 {#editing-page-content}

ページが作成されたら（新規またはローンチまたはライブコピーの一部として）、コンテンツを編集して、必要な更新をおこなうことができます。

コンテンツを追加するには、 [コンポーネント](/help/sites-classic-ui-authoring/classic-page-author-default-components.md) （コンテンツタイプに適した）ページにドラッグできます。 コンポーネントはその後、そのまま編集したり、移動や削除をおこなったりすることができます。

>[!NOTE]
>
>アカウントに [適切なアクセス権](/help/sites-administering/security.md) および [権限](/help/sites-administering/security.md#permissions) ページを編集するには、例えば、コンポーネントの追加、編集または削除、注釈、ロック解除などです。
>
>問題が発生した場合は、システム管理者にお問い合わせください。

## Sidekick {#sidekick}

サイドキックは、ページをオーサリングする際の重要なツールです。 ページのオーサリング時にフローティングされるので、常に表示されます。

次のようないくつかのタブおよびアイコンを使用できます。

* コンポーネント
* ページ
* 情報
* バージョン管理
* ワークフロー
* モード
* 基礎モード
* ClientContext
* web サイト

![chlimage_1-71](assets/chlimage_1-71.png)

これらのタブやアイコンから、次のような幅広い機能にアクセスできます。

* [コンポーネントの選択](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick)
* [参照の表示](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#showing-references)
* [監査ログへのアクセス](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#audit-log)
* [モードの切り替え](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)
* バージョンの[作成](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#creating-a-new-version)、[復元](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick)および[比較](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#comparing-with-a-previous-version)

* ページの[公開](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#publishing-a-page)、[非公開](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#unpublishing-a-page)

* [ページプロパティの編集 ](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)

* [基礎モード](/help/sites-authoring/scaffolding.md)

* [クライアントコンテキスト](/help/sites-administering/client-context.md)

## コンポーネントの挿入 {#inserting-a-component}

### コンポーネントの挿入 {#inserting-a-component-1}

ページを開いた後、コンテンツの追加を開始できます。 これをおこなうには、コンポーネント（段落とも呼ばれます）を追加します。

新しいコンポーネントを挿入するには：

1. 挿入する段落の種類を選択する方法はいくつかあります。

   * ラベル付きの領域をダブルクリックします。 **コンポーネントまたはアセットをここにドラッグ…** - **新規コンポーネントを挿入** ツールバーが開きます。 コンポーネントを選択し、 **OK**.

   * 新しい段落を挿入するには、フローティングツールバー（サイドキックと呼ばれます）からコンポーネントをドラッグします。
   * 既存の段落を右クリックし、「 」を選択します。 **新規…** - 「新規コンポーネントを挿入」ツールバーが開きます。 コンポーネントを選択し、 **OK**.

   ![screen_shot_2012-02-15at115605am](assets/screen_shot_2012-02-15at115605am.png)

1. サイドキックと **新規コンポーネントを挿入** ツールバー使用可能なコンポーネント（段落タイプ）のリストが表示されます。 これらは、様々なセクション（「一般」、「列」など）に分割でき、必要に応じて展開できます。

   実稼動環境によっては、選択肢が異なる場合があります。 コンポーネントについて詳しくは、 [デフォルトのコンポーネント](/help/sites-classic-ui-authoring/classic-page-author-default-components.md).

1. 必要なコンポーネントをページに挿入します。 次に、段落をダブルクリックすると、段落を設定してコンテンツを追加できるウィンドウが開きます。

### コンテンツファインダーを使用したコンポーネントの挿入 {#inserting-a-component-using-the-content-finder}

また、ページに新しいコンポーネントを追加するには、 [コンテンツファインダー](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder). これにより、アセットを含む適切なタイプの新しいコンポーネントが自動的に作成されます。

これは次のアセットタイプに有効です（一部はページや段落システムに依存します）。

| アセットタイプ | 結果のコンポーネントタイプ |
|---|---|
| 画像 | 画像 |
| ドキュメント | ダウンロード |
| 製品 | 製品 |
| ビデオ | Flash |

>[!NOTE]
>
>この動作は使用しているインストール環境に応じて設定できます。詳しくは、 [アセットをドラッグするとコンポーネントインスタンスが作成されるように段落システムを設定する](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) 詳しくは、を参照してください。

前述のいずれかのアセットタイプをドラッグしてコンポーネントを作成するには：

1. ページが&#x200B;[**編集**&#x200B;モード](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)であることを確認します。
1. を開きます。 [コンテンツファインダー](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder).
1. 必要なアセットを必要な位置までドラッグします。 この [コンポーネントプレースホルダー](#componentplaceholder) コンポーネントを配置する場所を示します。

   アセットタイプに適したコンポーネントが必要な場所に作成され、選択したアセットが格納されます。

1. [編集](#editmovecopypastedelete) 必要に応じて、コンポーネントを選択します。

## コンポーネント（コンテンツとプロパティ）の編集 {#editing-a-component-content-and-properties}

既存の段落を編集するには、次のいずれかの操作を行います。

* **ダブルクリック** 段落を開きます。 既存のコンテンツを含む段落を作成したときと同じウィンドウが表示されます。 変更を加え、 **OK**.

* **右クリック** 段落をクリックし、 **編集**.

* **クリック** 段落を 2 回（ゆっくりダブルクリック）して、インプレース編集モードに入ります。 ダイアログウィンドウ内ではなく、ページ上のテキストを直接編集できます。 このモードでは、ページの上部にツールバーが表示されます。 変更を加えると、自動的に保存されます。

## コンポーネントの移動 {#moving-a-component}

段落を移動するには：

>[!NOTE]
>
>[切り取りと貼り付け](#cut-copy-paste-a-component)を使用して、コンポーネントを移動することもできます。

1. 移動する段落を選択します。

   ![screen_shot_2012-02-15at115855am](assets/screen_shot_2012-02-15at115855am.png)

1. 段落を新しい場所にドラッグします。段落の移動先に緑のチェックマークが付きます。AEM 目的の場所にドロップします。
1. 段落が移動されました：

   ![screen_shot_2012-02-15at120030pm](assets/screen_shot_2012-02-15at120030pm.png)

## コンポーネントの削除 {#deleting-a-component}

段落を削除するには：

1. 段落を選択し、 **右クリック**:

   ![screen_shot_2012-02-15at120220pm](assets/screen_shot_2012-02-15at120220pm.png)

1. 選択 **削除** を選択します。 AEM WCM は、段落を削除すると元に戻せないので、この確認を要求します。
1. 「**OK**」をクリックします。

>[!NOTE]
>
>[グローバル編集ツールバーを表示するためのユーザープロパティ](/help/sites-classic-ui-authoring/author-env-user-props.md)を設定している場合、表示される「**コピー**」、「**切り取り**」、「**貼り付け**」、「**削除**」の各ボタンを使用して、段落に対する特定の操作を実行できます。
>
>様々な[キーボードショートカット](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)も利用できます。

## コンポーネントの切り取り／コピー／貼り付け {#cut-copy-paste-a-component}

[コンポーネントを削除](#deleting-a-component)するときと同様に、コンテキストメニューを使用してコンポーネントのコピー、切り取り、貼り付けを行うことができます。

>[!NOTE]
>
>[グローバル編集ツールバーを表示するためのユーザープロパティ](/help/sites-classic-ui-authoring/author-env-user-props.md)を設定している場合、表示される「**コピー**」、「**切り取り**」、「**貼り付け**」、「**削除**」の各ボタンを使用して、段落に対する特定の操作を実行できます。
>
>様々な[キーボードショートカット](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)も利用できます。

>[!NOTE]
>
>コンテンツの切り取り、コピーおよび貼り付けは、同じページ内でのみサポートされています。

## 継承されたコンポーネント {#inherited-components}

継承されたコンポーネントは、次のような様々なシナリオによって生成されます。

* [マルチサイト管理](/help/sites-administering/msm.md);～と組み合わせて [基礎](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md#scaffolding-with-msm-inheritance).

* [ローンチ](/help/sites-classic-ui-authoring/classic-launches.md)（ライブコピーをベースとしている場合）
* 特定のコンポーネント（Geometrixx 内の継承された段落システムなど）

継承はキャンセル（その後再度有効化）できます。コンポーネントに応じて、次の場所から使用できます。

1. **ライブコピー**

   コンポーネントがライブコピーまたはローンチに含まれている場合は、南京錠アイコンによりそのことが示されます。この南京錠アイコンをクリックして継承をキャンセルできます。

   * 南京錠アイコンは、コンポーネントの選択時に、次のように表示されます。

   ![chlimage_1-72](assets/chlimage_1-72.png)

   * また、次に示すように、南京錠アイコンはコンポーネントのダイアログにも表示されます。

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. **継承された段落システム**

   設定ダイアログ。 例えば、Geometrixx内の継承された段落システムの場合は次のようになります。

   ![chlimage_1-74](assets/chlimage_1-74.png)

## 注釈の追加 {#adding-annotations}

[注釈](/help/sites-classic-ui-authoring/classic-page-author-annotations.md) 他の作成者がコンテンツに関するフィードバックを提供できるようにします。 これは、多くの場合、レビューおよび検証の目的で使用されます。

## ページのプレビュー {#previewing-pages}

ページのプレビューに重要な 2 つのアイコンがサイドキックの下の枠に表示されます。

![7 つのアイコンの横列を持つサイドキックの下の境界線。 行の先頭にある 2 つのアイコン（編集アイコンとプレビューモードアイコン）は、それぞれ鉛筆記号と虫眼鏡記号で示されます。](do-not-localize/chlimage_1-5.png)

* 鉛筆アイコンは、現在編集モードでコンテンツの追加、変更、移動または削除を行っていることを示します。

  ![鉛筆記号で示される編集アイコン。](do-not-localize/chlimage_1-6.png)

* 虫眼鏡アイコンを使用すると、プレビューモードを選択できます。このモードでは、パブリッシュ環境と同じようにページを表示できます（ページの更新も必要になる場合があります）。

  ![虫眼鏡の記号で示されるプレビューモードのアイコン。](do-not-localize/chlimage_1-7.png)

  プレビューモードでは、サイドキックが縮小されます。下向き矢印アイコンをクリックすると、編集モードに戻ります。

  ![タイトルがAEMのバーで、タイトルの右側に下向き矢印記号が付いた編集モードアイコンが表示されます。](do-not-localize/chlimage_1-8.png)

## 検索と置換 {#find-replace}

同じフレーズを大規模に編集する場合、 **[検索と置換](/help/sites-classic-ui-authoring/author-env-search.md#find-and-replace)** メニューオプションを使用すると、web サイトの特定のセクション内で、1 つの文字列を複数インスタンスで検索および置換できます。

## ページのロック {#locking-a-page}

AEMでは、他のユーザーがコンテンツを変更できないように、ページをロックできます。 これは、1 つの特定のページに多くの編集を加える場合や、短時間ページを凍結する必要がある場合に便利です。

>[!CAUTION]
>
>ページのロックは、ページのロックを解除できる唯一のユーザーがページをロックしたユーザー（または管理者権限を持つアカウント）なので、慎重に使用してください。

ページをロックするには：

1. 内 **Web サイト** 」タブで、ロックするページを選択します。
1. ページをダブルクリックして、編集用に開きます。
1. 内 **ページ** サイドキックのタブで、「 」を選択します。 **ページをロック**:

   ![screen_shot_2012-02-08at15750pm](assets/screen_shot_2012-02-08at15750pm.png)

   他のユーザーに対して、ページがロックされているというメッセージが表示されます。さらに、**web サイト**&#x200B;のコンソールの右側のパネルで、このページがロック済みとして表示され、ページをロックしたユーザーが示されます。

   ![screen_shot_2012-02-08at20657pm](assets/screen_shot_2012-02-08at20657pm.png)

## ページのロック解除 {#unlocking-a-page}

ページのロックを解除するには：

1. 内 **Web サイト** 」タブで、ロックを解除するページを選択します。
1. ページをダブルクリックして開きます。
1. 内 **ページ** サイドキックのタブで、「 」を選択します。 **ページのロックを解除**.

## ページ編集の取り消しとやり直し {#undoing-and-redoing-page-edits}

ページのコンテンツフレームにフォーカスがあるときは、次のキーボードショートカットを使用します。

* 取り消し：Ctrl + Z（Windows）または Cmd + Z（Mac）
* やり直し：Ctrl + Y（Windows）または Cmd + Y（Mac）

1 つまたは複数の段落の削除、追加、再配置の取り消しまたはやり直しを実行すると、影響を受ける段落が点滅します（デフォルトの動作）。

>[!NOTE]
>
>ページ編集の取り消しとやり直しで実行できることについて詳しくは、[ページ編集の取り消しとやり直し - 理論](#undoing-and-redoing-page-edits-the-theory)を参照してください。

## ページ編集の取り消しとやり直し - 理論 {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>システム管理者は、インスタンスの要件に応じて、[取り消しとやり直し機能の様々な側面を設定](/help/sites-administering/config-undo.md)できます。

AEMには、実行したアクションの履歴と、実行したアクションのシーケンスが保存されます。 したがって、実行した順序で、複数の操作を元に戻すことができます。 次に、やり直しを使用して、1 つ以上のアクションを再適用できます。

コンテンツページの要素を選択した場合、取り消しコマンドとやり直しコマンドは、選択した項目（テキストコンポーネントなど）に適用されます。

取り消しコマンドとやり直しコマンドの動作は、他のソフトウェアプログラムの動作と同じです。 コンテンツに関する決定を行う際に、Web ページの最新の状態を復元するには、コマンドを使用します。 例えば、テキスト段落をページ上の別の場所に移動した場合に、取り消しコマンドを使用して、その段落を元の場所に戻すことができます。その後、再び段落を移動する場合は、やり直しコマンドを使用します。

>[!NOTE]
>
>以下の操作を実行できます。
>
>* 取り消しを使用してからページの編集を行っていない限り、操作をやり直します。
>* 最大 20 個の編集アクションを取り消す（デフォルト設定）。
>* また、 [キーボードショートカット](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) 元に戻す/やり直しの場合。
>

取り消しとやり直しは、次のタイプのページの変更に対して使用できます。

* 段落の追加、編集、削除および移動
* 段落コンテンツのインプレース編集
* ページ内の項目のコピー、切り取り、貼り付け
* ページ間での項目のコピー、カットおよび貼り付け
* ファイルや画像の追加、削除、変更
* 注釈およびスケッチの追加、削除、変更
* 基礎モードの変更
* 参照の追加と削除
* コンポーネントダイアログボックスでプロパティ値を変更する。

フォームコンポーネントがレンダリングするフォームフィールドは、ページのオーサリング時に値を指定するものではありません。 したがって、取り消しコマンドとやり直しコマンドは、これらのタイプのコンポーネントの値に加えた変更には影響しません。 例えば、コンボボックス内の値の選択を取り消すことはできません。

>[!NOTE]
>
>ファイルと画像に対する変更の取り消しとやり直しには、特別な権限が必要になります。また、ファイルおよび画像に対する変更の取り消し履歴は、最低でも時間保持されます。 ただし、これ以降は、変更の取り消しは保証されません。 管理者は、権限を付与したり、デフォルトの 10 時間を変更したりすることができます。
