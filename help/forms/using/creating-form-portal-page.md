---
title: フォームポータルページの作成
seo-title: Creating a forms portal page
description: フォームポータルでは、Web開発者にAdobe Experience Manager (AEM)を使用して作成されたWebサイトでフォームポータルを作成してカスタマイズするためのコンポーネントが支給されます。
seo-description: Forms Portal equips Web Developers with components to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM).
uuid: a5017de5-616c-4ce4-81aa-f28c741f8e8f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 8fff78cb-9ef9-426e-8b30-d70b4f26887f
docset: aem65
feature: Forms Portal
exl-id: 22d7c24e-7a77-4324-afdf-74c1fbf15773
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 100%

---

# フォームポータルページの作成{#creating-a-forms-portal-page}

フォームポータルのコンポーネントでは、Web開発者にAdobe Experience Manager (AEM)を使用してフォームポータル用Webサイトを作成し、カスタマイズするためのコンポーネントが用意されています。フォームポータルの概要については、「[ポータル上でフォームを発行する](../../forms/using/introduction-publishing-forms.md)」を参照してください。

## 前提条件 {#prerequisites}

デフォルトでは、フォームポータルコンポーネントは使用できません。「[フォームポータルのコンポーネントを有効にする](/help/forms/using/enabling-forms-portal-components.md)」の説明に従い、フォームポータルコンポーネントにおける次のカテゴリが有効になっていることを確認してください。

**Document Services**：検索とリスター、リンクおよびドラフトと送信のコンポーネントが含まれています。

**Document Services Predicates**：「Date Predicate」、「Full Text Predicate」、「Properties Predicate」、および「Tags Predicate」のコンポーネントが含まれています。これらのコンポーネントは、「Search &amp; Lister」コンポーネントで検索を設定する際に使用します。

これらをAEMサイトのページで有効にすると、コンポーネントの各カテゴリはコンポーネントブラウザで使用でるようになります。

![コンポーネントブラウザにおけるAEM Formsポータルコンポーネント](assets/component-categories.png)

Formsポータルコンポーネントのカテゴリ

## Search &amp; Listerコンポーネント {#search-amp-lister-component}

「Document Services」のコンポーネントカテゴリにある「Search &amp; Lister」コンポーネントは、ページ上にフォームを一覧表示し、その中から検索を実行するのに使用されます。コンポーネントには、次の2つのペインが含まれます。

* フォームが一覧表示される「リスト」ペイン。
* 検索機能を追加する「検索」ペイン。

検索とリスターコンポーネントは、コンポーネントブラウザの Document Services コンポーネントカテゴリからページまでドラッグ＆ドロップすることができます。コンポーネントを追加すると、下記の画像のようになります。

![ページ中のSearch &amp; Lister コンポーネント](assets/fp-grid-viw.png)

ページ中のグリッドレイアウトのSearch &amp; Lister コンポーネント

### 「リスト」ペイン {#list-pane}

リストペインはフォームが一覧表示される領域です。検索とリスターコンポーネントでは各種の設定オプションが提供されており、リストウィンドウでフォームの表示を制御するのに使用します。

リストウィンドウを設定するには、検索とリスターコンポーネントをタップし、![settings_icon](assets/settings_icon.png) をタップします。**[!UICONTROL 編集コンポーネント]**&#x200B;ダイアログが開きます。

![編集モードのリストペイン](assets/edit-list.png)

編集モードのリストペイン

「**編集**」ダイアログには複数のタブが含まれており、以下の表で説明される設定オプションを提供します。終わったら「**OK**」をタップして、設定を保存します。

<table>
 <tbody>
  <tr>
   <th>タブ</th>
   <th>設定</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>アセットフォルダー</strong></code></td>
   <td>項目を追加</td>
   <td>アセットのアップロード先フォルダーを、AEM FormsのUIから設定します。デフォルトでは、アップロードされたすべてのアセットが一覧表示されます。AEM Forms の UI に関する詳細は、「<a href="../../forms/using/introduction-managing-forms.md" target="_blank">フォーム管理の概要</a>」を参照してください。</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>ディスプレイ</strong></code></p> </td>
   <td>タイトルテキスト</td>
   <td>Search &amp; Listerコンポーネントのタイトルデフォルトのタイトルは<strong>フォームポータルです。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>テンプレートのレイアウト</td>
   <td>アセットのレイアウト </td>
  </tr>
  <tr>
   <td> </td>
   <td>詳細検索の無効化</td>
   <td>このオプションを有効にすると、詳細検索アイコンが非表示になります。</td>
  </tr>
  <tr>
   <td> </td>
   <td>テキスト検索の無効化</td>
   <td>このオプションを有効にすると、全文検索バーが非表示になります。</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>結果</strong></code></td>
   <td>ページごとの結果の数</td>
   <td>ページに表示するフォームの最大数を設定します。</td>
  </tr>
  <tr>
   <td> </td>
   <td>結果のテキスト</td>
   <td><p>結果のテキストを設定します（例えば、1-12/601の</strong>「結果」<strong>）。デフォルト値は<strong>「Results」</strong>です。</strong></p> <p>例えば、このフィールドで<strong>フォーム</strong>を指定し、合計 601 のフォームがある場合、結果のテキストは 1-12/601 の「<strong>Forms</strong>」に変わります。</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>ページテキスト</td>
   <td><p>ページテキストを設定します（例：1/51 <strong>ページ</strong>）。デフォルト値は<strong>「ページ」</strong>です。</p> <p>例えば、このフィールドに<strong>アプリケーションフォーム</strong>を指定し、ページが 51 ページある場合、ページテキストは 1/51 <strong>アプリケーションフォーム</strong>に変わります。</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>/ テキスト</td>
   <td><p>指定されたテキストの <strong>of</strong> という文字を指定したテキストに置き換えます（Page 1 <strong>of </strong>51）。デフォルト値は <strong>/</strong> です。</p> <p>例えば、このフィールドに <strong>out of </strong> を指定した場合、テキストは Page 1 <strong>out of </strong>51 に変わります。</p> </td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>フォームリンク</strong></code></td>
   <td>レンダリングタイプ</td>
   <td>指定したレンダリングタイプに基づいて、フォームのリストをコントロールします。使用可能なオプションは「PDF」と「HTML」です。例えば、レンダリングタイプとして HTML のみを指定した場合は、PDF フォームが除外されます。</td>
  </tr>
  <tr>
   <td> </td>
   <td>HTML プロファイル</td>
   <td>レンダリングに使用されるHTMLプロファイルを設定します。使用可能なすべてのプロファイルがドロップダウンリストに一覧表示されます。</td>
  </tr>
  <tr>
   <td> </td>
   <td>送信 URL</td>
   <td><p>フォームデータが送信されるサーブレットを設定します。</p> <p><strong>注意：</strong><em>フォームの送信 URL は、複数の場所で指定できます。また、その優先順位は以下の通りです。</em></p>
    <ol>
     <li><em>優先順位が最も高いのは、フォームに埋め込まれている送信URL（送信ボタン）です。</em></li>
     <li><em>2番目に優先順位が高いのは、AEMフォームUIで説明している送信URLです。</em></li>
     <li><em>一番優先順位が引くのが、フォームポータルで説明している送信URLです。</em></li>
    </ol> </td>
  </tr>
  <tr>
   <td> </td>
   <td>HTMLレンダリングアクションのツールチップ</td>
   <td>（HTML5のアイコン）<img height="16" src="assets/aem6forms_panel-html.png" width="13" />の上にマウスを置くと表示されるツールチップのテキストを設定します。</td>
  </tr>
  <tr>
   <td> </td>
   <td>PDFレンダリングアクションのツールチップ</td>
   <td><img height="16" src="assets/aem6forms_panel-pdf.png" width="14" /> （PDF のアイコン）の上にマウスのポインターを置くと表示されるツールチップのテキストを設定します。</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>スタイル</strong></code></td>
   <td>スタイルタイプ</td>
   <td>フォームのリスト表示には、<strong>書式なし、デフォルトスタイル</strong>または<strong>カスタムスタイル</strong>を指定できます。</td>
  </tr>
  <tr>
   <td> </td>
   <td>カスタムスタイルパス</td>
   <td>スタイルタイプとして「カスタム」を選択した場合、カスタム CSS へのパスを参照して指定します。そうでない場合、「デフォルト」を選択します。</td>
  </tr>
 </tbody>
</table>

### 検索ペイン {#search-pane}

検索ペインでは、サイドキックの「Document Services Predicates」カテゴリから、「Date Predicate」、「Full Text Predicate」、「Properties Predicate」、および「Tags Predicate」コンポーネントを追加することができます。これらのコンポーネントにより、一覧表示されるフォームに対してユーザーが検索を実行するための検索機能が実装されます。

**チップ：** *フォームポータルに表示されるフォームのリストを既定の条件に基づいて制御し、エンドユーザーに対して検索機能を非表示にできます。フォームのリストを制御するには、検索フィルターを適用するためにPredicateコンポーネントを使用します。デフォルトフィルター値を指定して、コンポーネントの編集ダイアログの「表示」タブで検索を無効にすることもできます。*

![日付、フルテキスト、プロパティ、およびTags Predicate付きの検索パネル](assets/search-with-predicates.png)

日付、フルテキスト、プロパティ、およびTags Predicate付きの検索パネル

#### 日付の述語 {#date-predicate}

「Date Predicate」コンポーネントが追加されている場合は、指定された期間に変更されたフォームについて、一覧表示されたフォームの中から検索できます。

「Date Predicate」コンポーネントを構成するには、次の手順を実行します。

1. コンポーネントをタップし、![settings_icon](assets/settings_icon.png) をタップします。編集ダイアログが開きます。
1. 以下のプロパティを指定します。

   * **タイプ：**&#x200B;選択できるオプションは「**最終変更日**」のみです。

   * **テキスト：** Date Predicateコンポーネントのラベルまたはキャプションです。デフォルト値は「**最終変更日**」です。

   * **開始日のラベル：**&#x200B;開始日フィールドのラベルまたはキャプションです。
   * **終了日のラベル：**&#x200B;終了日フィールドのラベルまたはキャプションです。
   * **非表示：**&#x200B;デフォルトの日付フィルターを適用してフォームを一覧表示します。

1. 「**OK**」をタップします。

#### フルテキストの述語 {#full-text-predicate}

「Full Text Predicate」コンポーネントは、フォームデータに対して名前や説明などを検索する、フルテキスト検索を実装します。名前や説明にテキストを含む戻りフォームで、テキスト文字列を検索できます。

Full Text Predicate コンポーネントを構成するには、次の手順を実行します。

1. コンポーネントをタップし、![ettings_icon](assets/settings_icon.png) をタップします。編集ダイアログが開きます。
1. 「**メインタイトル**」フィールドにタイトルを指定します。
1. 「**OK**」をタップします。

#### プロパティの述語 {#properties-predicate}

Properties Predicateコンポーネントは、フォームプロパティ（タイトル、作成者および説明など）に基づいたフォームの検索機能を実装します。

Properties Predicate コンポーネントを構成するには、次の手順を実行します。

1. コンポーネントをタップし、![settings_icon](assets/settings_icon.png) をタップします。編集ダイアログが開きます。
1. 「全般」タブで、検索ラベルを指定します。デフォルト値は、**プロパティ**&#x200B;です。

1. 「オプション」タブで、「**アイテムの追加**」をタップします。
1. ドロップダウンリストからプロパティを選択し、ドロップダウンリストの下のフィールドでプロパティの検索ラベルを指定します。
1. 手順 4 を繰り返してさらにプロパティを追加します。デフォルトのフィルター値を指定して、指定の条件に基づいてフォームをリスト表示したり、エンドユーザーごとに検索のプロパティを非表示にしたりできます。プロパティの「非表示」チェックボックスを選択し、デフォルトフィルター値を指定します。例えば、タイトルに「Travel」という文字を含むフォームを表示するには、「タイトル」プロパティ横の「非表示」を選択します。さらに、デフォルトフィルター値のテキストボックスで Travel と指定します。

1. 「**OK**」をタップします。

#### タグの述語 {#tags-predicate}

Tags Predicate コンポーネントは、Forms Manager で定義されているタグに基づいて、フォームの検索機能を実装します。

Tags Predicate コンポーネントを構成するには、次の手順を実行します。

1. コンポーネントをタップし、![settings_icon](assets/settings_icon.png) をタップします。編集ダイアログが開きます。
1. 「タグ」フィールド横の下向き矢印ボタンをタップします。
1. 適切なタグを選択します。
1. 「**OK**」をタップします。

選択したタグが、選択のためのチェックボックスと一緒に検索ペインに表示されます。ユーザーはこのタグに基づいて検索を絞り込めるようになります。

## ページ上でフォームを一覧表示 {#list-forms-on-a-page-br}

ページ上でフォームを一覧表示するには、そのページに **[!UICONTROL Search &amp; Lister]** コンポーネントを追加し、**[!UICONTROL リストペイン]**&#x200B;を設定します。エンドユーザーが、日付、テキスト、およびタグでフォームを検索できるようにするには、**[!UICONTROL 検索ペイン]**&#x200B;コンポーネントを追加します。

ページ上の任意の場所からフォームにリンクするには、リンクコンポーネントを使用します。リンクコンポーネントについての詳細は、「[ページ内のリンクコンポーネントの埋め込み](../../forms/using/embedding-link-component-page.md)」を参照してください。

ドラフト状態で、既に送信済みのフォームをリストするには、「**[!UICONTROL ドラフト&amp;送信]**」コンポーネントを使用します。詳しくは、「[ドラフト・送信コンポーネントのカスタマイズ](../../forms/using/draft-submission-component.md)」を参照してください。

## モバイルデバイスへの適合性 {#mobile-device-friendliness}

フォームポータルのSearch &amp; Listerコンポーネントは、モバイルデバイスフレンドリーで、デバイスに応じて表示幅を調整します。3 つすべてのデフォルトビュー：グリッド、カード、パネルは、web ページにも適応するという事実を踏まえて、デバイスに応じて再レイアウトされます。簡単に言えば、Search &amp; Listerは単なるコンポーネントであり、ページレベルのスタイリングは管理しません。

次の画像は、モバイルデバイス上で開いた場合の Search &amp; Lister コンポーネントを示します。

![Search &amp; Listerコンポーネントのスクリーンショット](assets/search_lister.png)

Search &amp; Listerコンポーネント

## フォームポータルページのカスタマイズ {#customizing-a-forms-portal-page-br}

フォームポータルページをカスタマイズすることで、特徴のある外観にすることができます。また、メタデータを追加することで、検索機能の改善、ページのレイアウト変更、およびカスタムCCSスタイルの追加を行うこともできます。詳しくは、「[フォームポータルコンポーネント用テンプレートのカスタマイズ](../../forms/using/customizing-templates-forms-portal-components.md)」を参照してください。

AEMフォームUIでは、カスタムメタデータをフォームに追加することができます。カスタムメタデータは、エンドユーザーに対してフォームの展開・検索機能を提供するのに役に立ちます。カスタムメタデータについて詳しくは、「[フォームポータルコンポーネント用テンプレートのカスタマイズ](../../forms/using/customizing-templates-forms-portal-components.md)」を参照してください。

フォームポータルは、デフォルトでレンダリングアクションを提供します。フォームポータルをカスタマイズして、他のオプションを追加することもできます。詳しくは、「[フォームリスター項目にカスタムアクションボタンを追加する](../../forms/using/add-custom-action-form-lister.md)」を参照してください。

## 関連記事

* [フォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md)
* [フォームポータルページの作成](/help/forms/using/creating-form-portal-page.md)
* [API を使用した Web ページ上のフォームの一覧表示](/help/forms/using/listing-forms-webpage-using-apis.md)
* [ドラフトと送信コンポーネントの使用](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信済みフォームのストレージのカスタマイズ](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信コンポーネントとデータベースの統合のサンプル](/help/forms/using/integrate-draft-submission-database.md)
* [フォームポータルコンポーネントのテンプレートをカスタマイズする](/help/forms/using/customizing-templates-forms-portal-components.md)
* [ポータル上のフォーム発行の概要](/help/forms/using/introduction-publishing-forms.md)
