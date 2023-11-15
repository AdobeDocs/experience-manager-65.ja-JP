---
title: オーサリング - AEM の環境とツール
description: AEM のオーサリング環境は、コンテンツを構造化および編集するための様々なメカニズムを提供しています。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: 3b3c118b-ca35-484b-a62e-7bec98953123
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '2227'
ht-degree: 58%

---

# オーサリング - 環境とツール{#authoring-the-environment-and-tools}

AEM のオーサリング環境は、コンテンツを編成および編集するための様々なメカニズムを提供しています. 提供されるツールには、様々なコンソールおよびページエディターからアクセスします。

## サイトの管理 {#managing-your-site}

The **Sites** コンソールを使用すると、ヘッダーバー、ツールバー、アクションアイコン（選択したリソースに適用）、パンくずリストおよび選択時にセカンダリレール（タイムラインや参照など）を使用して、Web サイトの移動と管理をおこなえます。

例えば、列表示では次のようになります。

![ateat-01](assets/ateat-01.png)

## ページコンテンツの編集 {#editing-page-content}

ページの編集は、ページエディターで行えます。次に例を示します。

`https://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

![ateat-02](assets/ateat-02.png)

>[!NOTE]
>
>初めてページを開いて編集する際に、一連のスライドを使用して機能に関するツアーを表示できます。
>
>必要がない場合は、このツアーをスキップすることができます。このツアーは、**ページ情報**&#x200B;メニューからいつでも表示できます。

## ヘルプへのアクセス {#accessing-help}

ページの編集中、**ヘルプ**&#x200B;には次の場所からアクセスできます。

* の [**ページ情報**](/help/sites-authoring/editing-page-properties.md#page-properties) セレクター。これには、（エディターに初めてアクセスしたときに表示される）紹介用のスライドが表示されます。
* の [設定](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) 特定のコンポーネント用のダイアログ ( 疑問符 (?) アイコンを使用 )。これは、状況依存のヘルプを表示します。

それ以外の[ヘルプ関連リソースは、コンソールから表示できます](/help/sites-authoring/basic-handling.md#accessing-help)。

## コンポーネントブラウザー {#components-browser}

コンポーネントブラウザーには、現在のページで使用可能なすべてのコンポーネントが表示されます。これらのコンポーネントを適切な場所にドラッグして編集することで、コンテンツを追加できます。

コンポーネントブラウザーはサイドパネル内のタブです（[アセットブラウザー](/help/sites-authoring/author-environment-tools.md#assets-browser)と[コンテンツツリー](/help/sites-authoring/author-environment-tools.md#content-tree)も同じ場所にあります）。サイドパネルを開く（または閉じる）には、ツールバーの左上にある次のアイコンを使用します。

![ateat-03](assets/ateat-03.png)

サイドパネルを開くと、パネルが左側からスライドして開きます ( **コンポーネント** タブ（必要に応じて）をクリックします。 開いたら、ページで使用可能なすべてのコンポーネントを参照できます。

実際の外観と処理は、使用しているデバイスの種類によって異なります。

>[!NOTE]
>
>モバイルデバイスは、幅が 1,024 px 未満の場合に検出されます。このことは、デスクトップの小さいウィンドウの場合にも当てはまります。

* **モバイルデバイス（例：iPad）**

  コンポーネントブラウザーには、編集中のページ全体が表示されます。

  ページにコンポーネントを追加するには、必要なコンポーネントをタッチ&amp;ホールドし、右側に移動します。コンポーネントブラウザーが閉じてページが再度表示され、コンポーネントの配置先になります。

  ![ateat-04](assets/ateat-04.png)

* **デスクトップデバイス**

  ウィンドウの左側にコンポーネントブラウザーが開きます。

  ページにコンポーネントを追加するには、必要なコンポーネントをクリックし、目的の場所にドラッグします。

  ![ateat-05](assets/ateat-05.png)

  コンポーネントは次のもので表されます。

   * コンポーネント名
   * コンポーネントグループ（グレー）
   * アイコンまたは略語

      * 標準コンポーネントのアイコンはモノクロです。
      * 略語は常にコンポーネント名の最初の 2 文字です。

  上部のツールバー ( **コンポーネント** ブラウザーでは、次の操作を実行できます。

   * コンポーネントを名前でフィルターします。
   * ドロップダウンから選択して特定のグループのみを表示します。

  コンポーネントについて詳しくは、**コンポーネント**&#x200B;ブラウザー内のコンポーネントの横にある情報アイコンをクリックまたはタップしてください（使用可能な場合）。例えば、**レイアウトコンテナ**&#x200B;の場合は、次のようになります。

  ![ateat-06](assets/ateat-06.png)

  使用可能なコンポーネントについて詳しくは、 [コンポーネントコンソール](/help/sites-authoring/default-components-console.md).

## アセットブラウザー {#assets-browser}

アセットブラウザーには、現在のページ上で直接使用できるすべての[アセット](/help/assets/home.md)が表示されます。

アセットブラウザーはサイドパネル内のタブであり、[コンポーネントブラウザー](/help/sites-authoring/author-environment-tools.md#components-browser)と[コンテンツツリー](/help/sites-authoring/author-environment-tools.md#content-tree)も同じ場所にあります。サイドパネルを開く（または閉じる）には、ツールバーの左上にある次のアイコンを使用します。

![ateat-03-1](assets/ateat-03-1.png)

サイドパネルを開くと、パネルが左側からスライドして開きます。 を選択します。 **Assets** タブに移動します（必要な場合）。

![ateat-07](assets/ateat-07.png)

アセットブラウザーを開いたら、ページで使用可能なすべてのアセットを参照できます。 必要に応じて、無限スクロールを使用してリストを展開できます。

![ateat-08](assets/ateat-08.png)

ページにアセットを追加するには、アセットを選択して必要な場所までドラッグします。次のことが考えられます。

* 適切なタイプの既存のコンポーネント。

   * 例えば、画像タイプのアセットを画像コンポーネントにドラッグできます。

* A [プレースホルダー](/help/sites-authoring/editing-content.md#component-placeholder) を使用して、適切なタイプのコンポーネントを作成します。

   * 例えば、画像タイプのアセットを段落システムにドラッグして画像コンポーネントを作成できます。

>[!NOTE]
>
>特定のタイプのアセットとコンポーネントで使用できます。詳しくは、[アセットブラウザーを使用したコンポーネントの挿入](/help/sites-authoring/editing-content.md#inserting-a-component-using-the-assets-browser)を参照してください。

アセットブラウザーの上部のツールバーでは、アセットを次の項目でフィルタリングできます。

* 名前
* パス
* アセットのタイプ（画像、原稿、ドキュメント、ビデオ、ページ、段落、製品など）
* 向き（縦、横、正方形）やスタイル（カラー、モノクロ、グレースケール）などのアセットの特性

   * 特定のアセットタイプに対してのみ使用可能

実際の外観と処理は、使用しているデバイスの種類によって異なります。

>[!NOTE]
>
>モバイルデバイスは、幅が 1,024 px 未満の場合に検出されます。つまり、画面の小さいデスクトップも検出されます。

* **iPadなどのモバイルデバイス**

  アセットブラウザーには、編集中のページ全体が表示されます。

  ページにアセットを追加するには、必要なアセットをタッチ&amp;ホールドし、右側に移動します。アセットブラウザーが閉じてページが再度表示され、必要なコンポーネントにアセットを追加できます。

  ![ateat-09](assets/ateat-09.png)

* **デスクトップデバイス**

  アセットブラウザーがウィンドウの左側に開きます。

  ページにアセットを追加するには、アセットをクリックし、必要なコンポーネントまたは場所にドラッグします。

  ![ateat-10](assets/ateat-10.png)

アセットをすばやく変更する必要がある場合は、 [アセットエディター](/help/assets/manage-assets.md) アセット名の横にある編集アイコンをクリックして、アセットブラウザーから直接移動します。

![Assets ブラウザーデスクトップデバイス](do-not-localize/screen_shot_2018-03-22at142448.png)

## コンテンツツリー {#content-tree}

The **コンテンツツリー** では、ページ上のすべてのコンポーネントの概要を階層で表示し、ページの構成方法を一目で確認できます。

コンテンツツリーは、サイドパネル内のタブです（コンポーネントブラウザーとアセットブラウザーも同じ場所にあります）。サイドパネルを開く（または閉じる）には、ツールバーの左上にある次のアイコンを使用します。

![コンテンツツリー](do-not-localize/screen_shot_2018-03-22at142042.png)

サイドパネルを開くと、パネルが（左側から）スライドして開きます。 必要に応じて「**コンテンツツリー**」タブを選択します。開くと、ページやテンプレートのツリービュー表示が表示され、コンテンツが階層的にどのように構造化されているかを理解しやすくなります。 また、複雑なページでは、ページのコンポーネント間をジャンプしやすくなります。

![ateat-11](assets/ateat-11.png)

ページは同じタイプの多数のコンポーネントで簡単に構成できます。コンテンツ（コンポーネント）ツリーには、コンポーネントタイプの名前（黒色）の後に説明テキスト（グレー）が表示されます。説明テキストは、コンポーネントの一般的なプロパティ（タイトルやテキストなど）から得られます。

コンポーネントタイプがユーザーの言語で表示されるのに対して、コンポーネントの説明テキストはページの言語で表示されます。

コンポーネントの横にある山形記号をクリックすると、そのレベルが折りたたまれたり展開されたりします。

![screen_shot_2018-03-22at142559](assets/screen_shot_2018-03-22at142559.png)

>[!NOTE]
>
>モバイルデバイス（ブラウザーの幅が 1,024 px より小さい場合）でページを編集している場合、コンテンツツリーは表示されません。

コンポーネントをクリックすると、ページエディターでそのコンポーネントがハイライトされます。 使用できるアクションは、ページの状態によって異なります。

* 基本ページの例を次に示します。

  `https://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html`

  ![ateat-12](assets/ateat-12.png)

  ツリー内でクリックしたコンポーネントが編集可能な場合は、名前の右側にレンチアイコンが表示されます。 このアイコンをクリックすると、コンポーネントの編集ダイアログボックスが開きます。

  ![レンチアイコン - 編集](do-not-localize/screen_shot_2018-03-22at142725.png)

* または、[ライブコピー](/help/sites-administering/msm.md)の一部を構成するページが開かれます。ここでは例として、コンポーネントが別のページから継承されます。

  `https://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

  ![ateat-13](assets/ateat-13.png)

## フラグメント - 関連コンテンツのブラウザー {#fragments-associated-content-browser}

ページにコンテンツフラグメントが含まれている場合は、 [関連コンテンツのブラウザー](/help/sites-authoring/content-fragments.md#using-associated-content).

## 参照 {#references}

**参照** 選択したページへの接続を表示：

* ブループリント
* ローンチ
* ライブコピー
* 言語コピー
* 被リンク
* 参照コンポーネントの使用：借りたコンテンツと貸したコンテンツ
* 製品ページへの参照（コマース／製品コンソールから）

必要なコンソールを開いたら、必要なリソースに移動し、次を使用して「**参照**」を開きます。

![screen_shot_2018-03-22at153653](assets/screen_shot_2018-03-22at153653.png)

[必要なリソースを選択](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) は、そのリソースに関連する参照タイプのリストを表示します。

![ateat-22](assets/ateat-22.png)

適切な参照タイプを選択すると、詳細情報が表示されます。特定の状況では、特定の参照を選択する際に、次のような追加のアクションを使用できます。

* **被リンク** は、ページを参照するページのリストと、 **編集** いずれかのページを選択します。

   * これにより、静的リンクのみが表示され、動的に生成されたリンク（例えば、リストコンポーネントから）は表示されません。

* **参照**&#x200B;コンポーネントを使用した借りたコンテンツおよび貸したコンテンツのインスタンス（ここから参照元／参照先ページに移動可能）

* [製品ページへの参照](/help/commerce/cif-classic/administering/generic.md#showing-product-references)（コマース／製品コンソールから使用可能）
* [起動回数](/help/sites-authoring/launches.md) は、関連するローンチへのアクセスを提供します。
* [ライブコピー](/help/sites-administering/msm.md)（選択したリソースに基づくすべてのライブコピーのパスを表示）
* [ブループリント](/help/sites-administering/msm-best-practices.md) に、詳細と様々なアクションを示します。
* [言語コピー](/help/sites-administering/tc-manage.md#creating-translation-projects-using-the-references-panel) に、詳細と様々なアクションを示します。

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

* [ローンチを昇格](/help/sites-authoring/launches-promoting.md) （ページがローンチの場合）
* [クラシック UI で開く](/help/sites-authoring/select-ui.md#switching-to-classic-ui-when-editing-a-page) このオプションが [管理者によって有効にされています](/help/sites-administering/enable-classic-ui-editor.md)

該当する場合、**ページ情報**&#x200B;から分析やレコメンデーションを確認することもできます。

## ページモード {#page-modes}

ページの編集時には様々なモードがあり、異なるアクションを行うことができます。

* [編集](/help/sites-authoring/editing-content.md)  — ページコンテンツの編集時には、このモードを使用します。
* [レイアウト](/help/sites-authoring/responsive-layout.md)  — デバイスに応じたレスポンシブレイアウトを作成および編集できます（ページがレイアウトコンテナに基づいている場合）

* [基礎モード](/help/sites-authoring/scaffolding.md)  — 構造は共有するがコンテンツは異なる大量のページを作成するのに役立ちます。
* [開発者](/help/sites-developing/developer-mode.md) ：様々なアクションを実行できます（権限が必要です）。 これには、ページとそのコンポーネントの技術的な詳細の検査が含まれます。

* [デザイン](/help/sites-authoring/default-components-designmode.md)  — ページで使用するコンポーネントを有効または無効にしたり、コンポーネントのデザインを設定したりできます ( ページが [静的テンプレート](/help/sites-authoring/templates.md#editable-and-static-templates)) をクリックします。

* [ターゲット設定](/help/sites-authoring/content-targeting-touch.md) - すべてのチャネルにわたるターゲティングと測定で、コンテンツの関連性を高めます。
* [Activity Map](/help/sites-authoring/page-analytics-using.md#analyticsvisiblefromthepageeditor) - ページの分析データを表示します。

* [タイムワープ](/help/sites-authoring/working-with-page-versions.md#timewarp) ：特定の時点のページの状態を表示できます。
* [ライブコピーステータス](/help/sites-authoring/editing-content.md#live-copy-status) - ライブコピーのステータスと継承される（または継承されない）コンポーネントの概要を素早く確認できます。
* [プレビュー](/help/sites-authoring/editing-content.md#previewing-pages) - パブリッシュ環境で表示されるページの表示、またはコンテンツ内のリンクを使用して移動するために使用します。

* [注釈](/help/sites-authoring/annotations.md) - ページで注釈の追加または表示を行う場合に使用するモード。

これらには、右上隅のアイコンを使用してアクセスできます。 実際のアイコンは、現在使用しているモードに応じて変化します。

![ateat-18](assets/ateat-18.png)

>[!NOTE]
>
>* ページの特性によっては、一部のモードを使用できない場合があります。
>* 一部のモードにアクセスするには、適切な権限または権限が必要です。
>* モバイルデバイスでは、スペースの制約により、開発者モードを使用できません。
>* ここに [キーボードショートカット](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) ( `Ctrl-Shift-M`) を切り替えます。 **プレビュー** 現在選択されているモード ( 例： **編集**、および **レイアウト**) をクリックします。
>

## パスの選択 {#path-selection}

オーサリング時に、別のリソースを選択する必要が生じる場合がよくあります（別のページまたはリソースへのリンクを定義する場合、画像を選択する場合など）。パスの選択を簡単にするために、[パスフィールド](/help/sites-authoring/author-environment-tools.md#path-fields)にはオートコンプリート機能があり、[パスブラウザー](/help/sites-authoring/author-environment-tools.md#path-browser)ではより堅牢な選択が可能になっています。

### パスフィールド {#path-fields}

説明のためにここで使用する例は、画像コンポーネントです。コンポーネントの使用と編集について詳しくは、 [ページオーサリング用コンポーネント](/help/sites-authoring/default-components.md).

パスフィールドには、オートコンプリート機能とルックアヘッド機能があり、リソースを見つけやすくなりました。

パスフィールドで「**選択ダイアログを開く**」ボタンをクリックすると、[パスブラウザー](/help/sites-authoring/author-environment-tools.md#path-browser)ダイアログが開き、より詳細な選択オプションが表示されます。

![選択ダイアログを開く](do-not-localize/screen_shot_2018-03-22at154427.png)

または、入力時にパスフィールドに入力し、AEMオファーで一致するパスを指定することもできます。

![ateat-19](assets/ateat-19.png)

### パスブラウザー {#path-browser}

パスブラウザーは、サイトコンソールの[列表示](/help/sites-authoring/basic-handling.md#column-view)のように整理されており、リソースをより詳細に選択できます。

![screen_shot_2018-03-22at154521](assets/screen_shot_2018-03-22at154521.png)

* リソースを選択すると、ダイアログの右上にある「**選択**」ボタンがアクティブになります。クリックまたはタップして選択を確定するか、「**キャンセル**」をクリックまたはタップして中止します。
* コンテキストで複数のリソースを選択できる場合、リソースを選択すると「**選択**」ボタンがアクティブ化され、選択したリソースの数がウィンドウの右上に表示されます。クリック **X** すべての選択を解除するには、数字の横に表示されます。
* ツリー内を移動すると、ダイアログ上部のパンくずリストに現在の位置が反映されます。これらのパンくずリストを使用すると、リソース階層内で素早くジャンプすることもできます。
* ダイアログの上部にある検索フィールドは、いつでも使用できます。 検索フィールドの「**X**」をクリックして、検索をクリアします。
* 検索を絞り込むには、フィルターオプションを表示して、特定のパスに基づいて結果をフィルターできます。

  ![ateat-21](assets/ateat-21.png)

## キーボードショートカット {#keyboard-shortcuts}

様々な[キーボードショートカット](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)を利用できます。
