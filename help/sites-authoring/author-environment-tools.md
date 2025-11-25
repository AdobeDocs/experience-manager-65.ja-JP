---
title: オーサリング - AEM の環境とツール
description: AEM のオーサリング環境は、コンテンツを構造化および編集するための様々なメカニズムを提供しています。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: 3b3c118b-ca35-484b-a62e-7bec98953123
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '2246'
ht-degree: 100%

---

# オーサリング - 環境とツール{#authoring-the-environment-and-tools}

AEM のオーサリング環境は、コンテンツを編成および編集するための様々なメカニズムを提供しています. 提供されるツールには、様々なコンソールおよびページエディターからアクセスします。

## サイトの管理 {#managing-your-site}

**Sites** コンソールでは、ヘッダーバー、ツールバー、アクションアイコン（選択したリソースに適用）、パンくずリスト、選択時のセカンダリレール（タイムラインや参照など）を使用して web サイトを移動および管理できます。

例えば、列表示では次のようになります。

![ateat-01](assets/ateat-01.png)

## ページコンテンツの編集 {#editing-page-content}

ページの編集は、ページエディターで行えます。例：

`https://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

![ateat-02](assets/ateat-02.png)

>[!NOTE]
>
>編集対象のページを初めて開くと、機能を紹介する一連のスライドが表示されます。
>
>このツアーは必要に応じてスキップし、**ページ情報**&#x200B;メニューから選択していつでも表示することができます。

## ヘルプへのアクセス {#accessing-help}

ページの編集中、**ヘルプ**&#x200B;には次の場所からアクセスできます。

* [**ページ情報**](/help/sites-authoring/editing-page-properties.md#page-properties)&#x200B;セレクター。これには、紹介用のスライドが表示されます（エディターへの初回アクセス時に表示）。
* 特定のコンポーネントの[設定](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)ダイアログ（ダイアログボックスのツールバーにある疑問符「？」アイコンを使用）。これにより、コンテキスト依存のヘルプが表示されます。

それ以外の[ヘルプ関連リソースは、コンソールから表示できます](/help/sites-authoring/basic-handling.md#accessing-help)。

## コンポーネントブラウザー {#components-browser}

コンポーネントブラウザーには、現在のページで使用可能なすべてのコンポーネントが表示されます。これらのコンポーネントを適切な場所にドラッグして編集することで、コンテンツを追加できます。

コンポーネントブラウザーはサイドパネル内のタブです（[アセットブラウザー](/help/sites-authoring/author-environment-tools.md#assets-browser)と[コンテンツツリー](/help/sites-authoring/author-environment-tools.md#content-tree)も同じ場所にあります）。サイドパネルを開く（または閉じる）には、ツールバーの左上にある次のアイコンを使用します。

![ateat-03](assets/ateat-03.png)

サイドパネルを開くと、パネルが左側からスライドして開きます（必要に応じて「**コンポーネント**」タブを選択します）。開いたら、ページで使用可能なすべてのコンポーネントを参照できます。

実際のアピアランスや処理は、使用しているデバイスの種類によって異なります。

>[!NOTE]
>
>モバイルデバイスは、幅が 1,024 px 未満の場合に検出されます。このことは、デスクトップの小さいウィンドウの場合にも当てはまります。

* **モバイルデバイス（例：iPad）**

  コンポーネントブラウザーには、編集中のページ全体が表示されます。

  ページにコンポーネントを追加するには、目的のコンポーネントをタッチ＆ホールドし、右側に移動します。コンポーネントブラウザーが閉じてページが再表示され、このページ上にコンポーネントを配置できます。

  ![ateat-04](assets/ateat-04.png)

* **デスクトップデバイス**

  ウィンドウの左側にコンポーネントブラウザーが開きます。

  ページにコンポーネントを追加するには、目的のコンポーネントをクリックして、目的の場所までドラッグします。

  ![ateat-05](assets/ateat-05.png)

  コンポーネントは次のもので表されます。

   * コンポーネント名
   * コンポーネントグループ（グレー）
   * アイコンまたは略語

      * 標準コンポーネントのアイコンはモノクロです。
      * 略語は常にコンポーネント名の最初の 2 文字です。

  **コンポーネント**&#x200B;ブラウザーの上部のツールバーでは、次の操作を実行できます。

   * コンポーネントを名前でフィルターします。
   * ドロップダウンから選択して、特定のグループのみを表示します。

  コンポーネントについて詳しくは、**コンポーネント**&#x200B;ブラウザー内のコンポーネントの横にある情報アイコンを（使用可能な場合）クリックしてください。例えば、**レイアウトコンテナ**&#x200B;の場合は、次のようになります。

  ![ateat-06](assets/ateat-06.png)

  使用可能なコンポーネントについて詳しくは、[コンポーネントコンソール](/help/sites-authoring/default-components-console.md)を参照してください。

## アセットブラウザー {#assets-browser}

アセットブラウザーには、現在のページ上で直接使用できるすべての[アセット](/help/assets/assets.md)が表示されます。

アセットブラウザーはサイドパネル内のタブであり、[コンポーネントブラウザー](/help/sites-authoring/author-environment-tools.md#components-browser)と[コンテンツツリー](/help/sites-authoring/author-environment-tools.md#content-tree)も同じ場所にあります。サイドパネルを開く（または閉じる）には、ツールバーの左上にある次のアイコンを使用します。

![ateat-03-1](assets/ateat-03-1.png)

サイドパネルを開くと、パネルが左側からスライドして開きます。必要に応じて「**アセット**」タブを選択します。

![ateat-07](assets/ateat-07.png)

アセットブラウザーが開くと、ページで使用可能なすべてのアセットを参照できます。必要に応じて、無限スクロールを使用してリストを展開できます。

![ateat-08](assets/ateat-08.png)

ページにアセットを追加するには、アセットを選択して必要な場所までドラッグします。次のことが考えられます。

* 適切なタイプの既存のコンポーネント。

   * 例えば、画像タイプのアセットを画像コンポーネントにドラッグできます。

* 適切なタイプの新しいコンポーネントを作成するために使用する、段落システム内の[プレースホルダー](/help/sites-authoring/editing-content.md#component-placeholder)。

   * 例えば、画像タイプのアセットを段落システムにドラッグして画像コンポーネントを作成できます。

>[!NOTE]
>
>特定のタイプのアセットとコンポーネントで使用できます。詳しくは、[アセットブラウザーを使用したコンポーネントの挿入](/help/sites-authoring/editing-content.md#inserting-a-component-using-the-assets-browser)を参照してください。

アセットブラウザーの上部のツールバーでは、アセットを次の項目でフィルタリングできます。

* 名前
* パス
* アセットタイプ（画像、原稿、ドキュメント、ビデオ、ページ、段落、商品など）
* 向き（縦、横、正方形）やスタイル（カラー、モノクロ、グレースケール）などのアセットの特性

   * 特定のアセットタイプに対してのみ使用可能

実際のアピアランスや処理は、使用しているデバイスの種類によって異なります。

>[!NOTE]
>
>モバイルデバイスは、幅が 1,024 px 未満の場合に検出されます。つまり、画面の小さいデスクトップも検出されます。

* **iPadなどのモバイルデバイス**

  アセットブラウザーには、編集中のページ全体が表示されます。

  ページにアセットを追加するには、目的のアセットをタッチ＆ホールドし、右側に移動します。アセットブラウザーが閉じてページが再表示され、このページ上で目的のコンポーネントにアセットを追加できます。

  ![ateat-09](assets/ateat-09.png)

* **デスクトップデバイス**

  アセットブラウザーがウィンドウの左側に開きます。

  ページにアセットを追加するには、目的のアセットをクリックし、目的のコンポーネントまたは場所までドラッグします。

  ![ateat-10](assets/ateat-10.png)

アセットをすぐに変更する必要がある場合は、アセット名の横にある編集アイコンをクリックして、アセットブラウザーから直接[アセットエディター](/help/assets/manage-assets.md)を開始できます。

![Assets ブラウザーデスクトップデバイス](do-not-localize/screen_shot_2018-03-22at142448.png)

## コンテンツツリー {#content-tree}

**コンテンツツリー**&#x200B;では、ページ上のすべてのコンポーネントの概要が階層形式で表示されるので、ページの構成を一目で確認できます。

コンテンツツリーは、サイドパネル内のタブです（コンポーネントブラウザーとアセットブラウザーも同じ場所にあります）。サイドパネルを開く（または閉じる）には、ツールバーの左上にある次のアイコンを使用します。

![コンテンツツリー](do-not-localize/screen_shot_2018-03-22at142042.png)

サイドパネルを開くと、パネルが（左側から）スライドして開きます。必要に応じて「**コンテンツツリー**」タブを選択します。このタブを開くと、ページやテンプレートがツリー形式で表示されるので、コンテンツの階層構造を理解しやすくなります。さらに、複雑なページでは、ページのコンポーネント間を簡単にジャンプできるようになります。

![ateat-11](assets/ateat-11.png)

ページは同じタイプの多数のコンポーネントで簡単に構成できます。コンテンツ（コンポーネント）ツリーには、コンポーネントタイプの名前（黒色）の後に説明テキスト（グレー）が表示されます。説明テキストは、コンポーネントの一般的なプロパティ（タイトルやテキストなど）から得られます。

コンポーネントのタイプはユーザー言語で表示されますが、コンポーネントの説明テキストはページ言語で表示されます。

コンポーネントの横にある山形アイコンをクリックすると、レベルを折りたたんだり、展開したりできます。

![screen_shot_2018-03-22at142559](assets/screen_shot_2018-03-22at142559.png)

>[!NOTE]
>
>モバイルデバイス（ブラウザーの幅が 1,024 px より小さい場合）でページを編集している場合、コンテンツツリーは表示されません。

コンポーネントをクリックすると、ページエディターでそのコンポーネントがハイライト表示されます。使用可能なアクションは、ページの状態によって異なります。

* 基本ページの例を次に示します。

  `https://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html`

  ![ateat-12](assets/ateat-12.png)

  ツリー内でクリックしたコンポーネントが編集可能な場合は、レンチアイコンが名前の右側に表示されます。このアイコンをクリックすると、コンポーネントの編集ダイアログボックスが開きます。

  ![レンチアイコン - 編集](do-not-localize/screen_shot_2018-03-22at142725.png)

* または、[ライブコピー](/help/sites-administering/msm.md)の一部を構成するページが開かれます。ここでは例として、コンポーネントが別のページから継承されます。

  `https://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

  ![ateat-13](assets/ateat-13.png)

## フラグメント - 関連コンテンツのブラウザー {#fragments-associated-content-browser}

ページにコンテンツフラグメントが含まれている場合、[関連コンテンツのブラウザー](/help/sites-authoring/content-fragments.md#using-associated-content)にアクセスできます。

## 参照 {#references}

**参照**&#x200B;には、選択したページへの接続が表示されます。

* ブループリント
* ローンチ
* ライブコピー
* 言語コピー
* 被リンク
* 参照コンポーネントの使用：借りたコンテンツと貸したコンテンツ
* 製品ページへの参照（コマース／製品コンソールから）

必要なコンソールを開いたら、必要なリソースに移動し、次を使用して「**参照**」を開きます。

![screen_shot_2018-03-22at153653](assets/screen_shot_2018-03-22at153653.png)

[必要なリソースを選択](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)には、そのリソースに関連する参照タイプのリストが表示されます。

![ateat-22](assets/ateat-22.png)

適切な参照タイプを選択すると、詳細情報が表示されます。状況によっては、特定の参照を選択すると、次のような追加のアクションが使用可能です。

* **被リンク**&#x200B;は、当該ページを参照するページのリストと、特定のリンクを選択したときにそれらのページのいずれかを&#x200B;**編集**&#x200B;できる直接アクセスを提供します。

   * これにより、静的リンクのみが表示され、動的に生成されるリンク（リストコンポーネントからのリンクなど）は表示されません。

* **参照**&#x200B;コンポーネントを使用した借りたコンテンツおよび貸したコンテンツのインスタンス（ここから参照元／参照先ページに移動可能）

* [製品ページへの参照](/help/commerce/cif-classic/administering/generic.md#showing-product-references)（コマース／製品コンソールから使用可能）
* [ローンチ](/help/sites-authoring/launches.md)（関連するローンチへのアクセスを提供）
* [ライブコピー](/help/sites-administering/msm.md)（選択したリソースに基づくすべてのライブコピーのパスを表示）
* [ブループリント](/help/sites-administering/msm-best-practices.md)（詳細と各種アクションを提供）
* [言語コピー](/help/sites-administering/tc-manage.md#creating-translation-projects-using-the-references-panel)（詳細と各種アクションを提供）

例えば、壊れている参照は、参照コンポーネントで修正できます。

![ateat-14](assets/ateat-14.png)

## イベント - タイムライン {#events-timeline}

適切なリソース（例：**Sites** コンソールからのページ、**アセット**&#x200B;コンソールからのアセット）では、[タイムラインを使用して、選択した項目に対する最近のアクティビティを表示できます](/help/sites-authoring/basic-handling.md#timeline)。

必要なコンソールを開いたら、必要なリソースに移動し、次を使用して「**タイムライン**」を開きます。

![ateat-15](assets/ateat-15.png)

[必要なリソースを選択](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)し、「**すべて表示**」または「**アクティビティ**」を選択すると、選択したリソースに対する最近のアクションが一覧表示されます。

![ateat-16](assets/ateat-16.png)

## ページ情報 {#page-information}

ページ情報ボタン（イコライザーアイコン）をクリックするとメニューが開き、最後の編集および最後の公開に関する詳細も表示されます。ページ、そのページのサイト、使用しているインスタンスの特性に応じて、使用できるオプションの数は異なります。

![ateat-17](assets/ateat-17.png)

* [プロパティを開く](/help/sites-authoring/editing-page-properties.md)
* [ページをロールアウト](/help/sites-administering/msm.md#msm-from-the-ui)
* [ワークフローを開始](/help/sites-authoring/workflows-applying.md#starting-a-workflow-from-the-page-editor)
* [ページをロック](/help/sites-authoring/editing-content.md#locking-a-page)
* [ページを公開](/help/sites-authoring/publishing-pages.md#main-pars-title-10)
* [ページを非公開](/help/sites-authoring/publishing-pages.md#main-pars-title-5)
* [テンプレートを編集](/help/sites-authoring/templates.md)（ページが[編集可能なテンプレート](/help/sites-authoring/templates.md#editable-and-static-templates)に基づいている場合）

* [公開済みとして表示](/help/sites-authoring/editing-content.md#view-as-published)
* 管理画面で表示。ページを [Sites コンソール](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)で開きます。
* [ヘルプ](/help/sites-authoring/basic-handling.md#accessing-help)

例えば、該当する場合、**ページ情報**&#x200B;には次のオプションもあります。

* [ローンチを昇格](/help/sites-authoring/launches-promoting.md)（ページがローンチの場合）
* [クラシック UI で開く](/help/sites-authoring/select-ui.md#switching-to-classic-ui-when-editing-a-page)（このオプションが[管理者によって有効にされている](/help/sites-administering/enable-classic-ui-editor.md)場合）

該当する場合、**ページ情報**&#x200B;から分析やレコメンデーションを確認することもできます。

## ページモード {#page-modes}

ページの編集時には様々なモードがあり、異なるアクションを行うことができます。

* [編集](/help/sites-authoring/editing-content.md) - ページコンテンツの編集時には、このモードを使用します。
* [レイアウト](/help/sites-authoring/responsive-layout.md) - デバイスに応じたレスポンシブレイアウトを作成および編集できます（ページがレイアウトコンテナに基づいている場合）。

* [基礎モード](/help/sites-authoring/scaffolding.md) - 同じ構造を共有しながらコンテンツが異なるページを大量に作成する場合に役立ちます。
* [開発者](/help/sites-developing/developer-mode.md) - 様々なアクションを実行できます（権限が必要）。これには、ページとそのコンポーネントの技術的な詳細の検査が含まれます。

* [デザイン](/help/sites-authoring/default-components-designmode.md) - ページで使用するコンポーネントを有効または無効にしたり、コンポーネントのデザインを設定したりできます（ページが[静的テンプレート](/help/sites-authoring/templates.md#editable-and-static-templates)に基づいている場合）。

* [ターゲット設定](/help/sites-authoring/content-targeting-touch.md) - すべてのチャネルにわたるターゲティングと測定で、コンテンツの関連性を高めます。
* [Activity Map](/help/sites-authoring/page-analytics-using.md#analyticsvisiblefromthepageeditor) - ページの分析データを表示します。

* [タイムワープ](/help/sites-authoring/working-with-page-versions.md#timewarp) - 特定の時点のページの状態を表示できます。
* [ライブコピーステータス](/help/sites-authoring/editing-content.md#live-copy-status) - ライブコピーのステータスと継承される（または継承されない）コンポーネントの概要をすばやく確認できます。
* [プレビュー](/help/sites-authoring/editing-content.md#previewing-pages) - パブリッシュ環境とまったく同じ形式でページを表示する、またはコンテンツ内のリンクを使って移動するために使用します。

* [注釈](/help/sites-authoring/annotations.md) - ページに注釈を追加または表示するために使用します。

これらには、右上のアイコンを使用してアクセスできます。実際のアイコンは、現在使用しているモードに応じて異なります。

![ateat-18](assets/ateat-18.png)

>[!NOTE]
>
>* ページの特性によっては、一部のモードを使用できない場合があります。
>* 一部のモードにアクセスするには、適切な権限または特権が必要です。
>* モバイルデバイスでは、スペースの制約により、開発者モードを使用できません。
>* [キーボードショートカット](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)（`Ctrl-Shift-M`）で、**プレビュー**&#x200B;と、現在選択されているモード（**編集**&#x200B;や&#x200B;**レイアウト**&#x200B;など）を切り替えることができます。
>

## パスの選択 {#path-selection}

オーサリング時に、別のリソースを選択する必要が生じる場合がよくあります（別のページまたはリソースへのリンクを定義する場合、画像を選択する場合など）。パスの選択を簡単にするために、[パスフィールド](/help/sites-authoring/author-environment-tools.md#path-fields)にはオートコンプリート機能があり、[パスブラウザー](/help/sites-authoring/author-environment-tools.md#path-browser)ではより堅牢な選択が可能になっています。

### パスフィールド {#path-fields}

説明のためにここで使用する例は、画像コンポーネントです。コンポーネントの使用および編集について詳しくは、[ページオーサリング用コンポーネント](/help/sites-authoring/default-components.md)を参照してください。

パスフィールドには、オートコンプリート機能とルックアヘッド機能があり、リソースを見つけやすくなりました。

パスフィールドで「**選択ダイアログを開く**」ボタンをクリックすると、[パスブラウザー](/help/sites-authoring/author-environment-tools.md#path-browser)ダイアログが開き、より詳細な選択オプションが表示されます。

![選択ダイアログを開く](do-not-localize/screen_shot_2018-03-22at154427.png)

または、パスフィールドで入力を開始すると、入力した内容と一致するパスが表示されます。

![ateat-19](assets/ateat-19.png)

### パスブラウザー {#path-browser}

パスブラウザーは、サイトコンソールの[列表示](/help/sites-authoring/basic-handling.md#column-view)のように整理されており、リソースをより詳細に選択できます。

![screen_shot_2018-03-22at154521](assets/screen_shot_2018-03-22at154521.png)

* リソースを選択すると、ダイアログの右上にある「**選択**」ボタンがアクティブになります。クリックして選択内容を確定するか、「**キャンセル**」をクリックして中止します。
* コンテキストで複数のリソースを選択できる場合、リソースを選択すると「**選択**」ボタンがアクティブ化され、選択したリソースの数がウィンドウの右上に表示されます。すべての選択を解除するには、数字の横にある **X** をクリックします。
* ツリー内を移動すると、ダイアログ上部のパンくずリストに現在の位置が反映されます。これらのパンくずリストを使用すると、リソース階層内で素早くジャンプすることもできます。
* ダイアログの上部にある検索フィールドは、いつでも使用できます。検索フィールドの「**X**」をクリックして、検索をクリアします。
* 検索を絞り込むには、フィルターオプションを表示して、特定のパスに基づいて結果をフィルターできます。

  ![ateat-21](assets/ateat-21.png)

## キーボードショートカット {#keyboard-shortcuts}

様々な[キーボードショートカット](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)を利用できます。
