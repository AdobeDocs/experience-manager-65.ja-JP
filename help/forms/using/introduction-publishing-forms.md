---
title: ポータル上のフォーム発行の概要
seo-title: ポータル上のフォーム発行の概要
description: AEM Forms はフォームポータルを構築するために使用できるコンポーネントを提供します。この記事では、使用可能なフォームポータルコンポーネントを紹介します。
seo-description: AEM Forms はフォームポータルを構築するために使用できるコンポーネントを提供します。この記事では、使用可能なフォームポータルコンポーネントを紹介します。
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 60%

---


# ポータル上のフォーム発行の概要{#introduction-to-publishing-forms-on-a-portal}

## AEM Forms ポータルコンポーネントの概要 {#aem-forms-portal-components-overview}

一般的なフォーム中心のポータル展開シナリオでは、フォームの開発とポータルの開発が別々に行われます。フォーム開発者はフォームを設計してリポジトリに保存する一方、Web 開発者は Web アプリケーションを作成してフォームを一覧表示し、フォームの送信を処理します。フォームリポジトリと Web アプリケーション間では通信が行われないため、フォームは Web 層にコピーされます。

このようなシナリオでは、管理問題が発生したり生産が遅延したりすることがよくあります。例えば、リポジトリで新しいバージョンのフォームを利用できる場合、Web 層でフォームを置換し、Web アプリケーションを変更し、公共サイトでフォームを再展開する必要があります。Web アプリケーションの再展開によって、サーバーのダウンタイムが発生する可能性があります。通常、サーバーのダウンタイムは計画的に行われるため、変更を瞬時に公共サイトにプッシュすることはできません。

AEM Forms は管理のオーバーヘッドと実稼働の遅延を低減するポータルコンポーネントを提供します。コンポーネントにより、Web 開発者は Adobe Experience Manager（AEM）を使用して作成された Web サイト上にフォームポータルを作成してカスタマイズできます。

![AEM Forms ポータル](assets/aem-forms-portal.png)

フォームポータルコンポーネントにより、次の機能が追加されます。

* カスタマイズしたレイアウトによってフォームを一覧表示する。リスト表示、カード表示、パネル表示用のレイアウトをすぐに使用できる。独自のカスタムレイアウトを作成する。
* 一覧表示からカスタムメタデータおよびカスタムアクションを表示する。
* フォームポータルコンポーネントを使用しているパブリッシュインスタンス上の AEM Forms UI によって発行されたフォームを一覧表示する。
* HTML 形式および PDF 形式でフォームをレンダリングする。 
* カスタム HTML プロファイルを使用してフォームをレンダリングする。
* さまざまな検索条件（フォームプロパティ、メタデータ、タグなど）に基づいたフォームの検索を有効にする。 
* フォームデータをサーブレットに送信する。
* カスタム CSS を使用してポータルの外観をカスタマイズする。 
* フォームへのリンクを作成する。
* エンドユーザーが作成したアダプティブフォームに関連するドラフトおよび送信を一覧表示する。

## 使用可能な AEM Forms ポータルコンポーネント {#available-aem-forms-portal-components}

AEM Forms はすぐに使える次のポータルコンポーネントを、**Document Services** および **Document Services Predicates** コンポーネントグループの下にグループ化して提供します。

### 検索とリスター {#search-amp-lister}

Search &amp; Lister コンポーネントは、フォームリポジトリのフォームをポータルページに一覧表示するほか、指定した検索条件に基づいてフォームを一覧表示するオプションを提供します。また、検索条件を指定することにより、ポータルユーザーがフォームの一覧から検索できるようにします。

### ドラフトと送信 {#drafts-amp-submissions}

Search &amp; Lister コンポーネントはフォーム作成者によって発行されたフォームを表示する一方、Drafts &amp; Submissions コンポーネントはドラフトとして保存され、後で完了して送信されるフォームを表示します。このコンポーネントはログインユーザーに対してパーソナライズされたエクスペリエンスを提供します。

### リンク {#link}

Link コンポーネントでは、ページ上の任意の場所にあるフォームへのリンクを作成できます。トレーニングプログラムを提供し、ユーザーがフォームを送信してトレーニングに登録できるようにするシナリオを検討します。お客様は当社の Web サイトに、プログラムの詳細を投稿しました。次に示す詳細に、登録フォームへのリンクを記述しています。Link コンポーネントはリンクの作成に役立ちます。

## Formsポータルのワークフロー {#forms-portal-workflow}

Formsポータルでは、フォームリポジトリからポータルページにフォームをリストできます。 また、検索条件を指定することにより、ポータルユーザーがフォームの一覧から検索できるようにします。ドラフトと送信コンポーネントを使用して、後で完了し、送信されたフォームを完成させるためにドラフトとして保存されたフォームを表示することもできます。 これらの機能をサイトページで使用するには、あらかじめ特定の操作を行う必要があります。 リストに表示された順序で手順を実行し、コンポーネントとそれぞれの機能をサイトページで使用できるようにします。

1. **Formsポータルコンポーネントを有効にする**:デフォルトでは、フォームポータルコンポーネントは使用できません。 [AEM SitesページのAEMサイドキックのコンポーネントを有効にします](/help/forms/using/enabling-forms-portal-components.md) 。
1. **ページ上のリストフォーム（フォームポータルページの作成）:** AEM Sitesページと非AEMサイトページの両方でフォームをリストできます。 リストには、発行インスタンスで使用できるフォームが含まれます。 ユーザーは、フォームを開いて入力した開始を表示できます。 ユーザーがフォームを開くたびに、フォームの新しいインスタンスが作成されます。

   1. **AEM Sitesページのリストフォーム**:「 **[Search &amp; Lister](../../forms/using/creating-form-portal-page.md)** 追加」コンポーネントをページに追加し、その中で「 **[リストペイン](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** 」を設定して、ページ上のリストフォームを表示します。 「 **Search Pane** 」コンポーネントを「 **Search &amp; Lister** 」コンポーネントに設定し、ページに検索機能を追加します。 フォームポータルコンポーネントを含むページは、 [フォームポータルページと呼ばれ](../../forms/using/creating-form-portal-page.md)ます。

   1. **AEM Sites以外のページ上のリストフォーム：** フォー [ムポータル検索APIを使用して](/help/forms/using/listing-forms-webpage-using-apis.md) 、AEM Sites以外のページにあるフォームのクエリ、取得、リストを行います。

1. **フォームポータルページ上のリストドラフトおよび送信済みフォーム**:フォームポータルページ追加のドラフトと送信コンポーネントを設定します。 コンポーネントは、ドラフト状態のすべてのフォームと、既に送信済みのフォームをリストします。

   To enable a submitted adaptive form to appear in the submissions tab, set the **Submit action** to **[Forms Portal Submit Action](configuring-submit-actions.md).** または、「Formsポータル送信」オプションを有効にします。 ユーザーがフォームを送信するたびに、フォームが「送信」タブに追加されます。

1. **ドラフトおよび送信済みのフォームデータのストレージを設定：** デフォルトでは、ドラフトと送信データはAEMリポジトリに保存されます。 実稼働環境では、ドラフトまたは送信されたフォームデータを AEM リポジトリに保存しないことをお勧めします。[データを安全な場所に保存するようにフォームポータルコンポーネントを設定します](../../forms/using/draft-submission-component.md#customizing-the-storage)。
1. **（オプション）フォームポータルコンポーネントのカスタマイズ：**[フォームポータルページテンプレートをカスタマイズして](../../forms/using/customizing-templates-forms-portal-components.md) 、コンポーネントに独特の外観を与えます。
1. **（オプション）フ追加ォームのカスタムメタデータ：**[リスト表示と検索の追加操作性を向上させるため、フォームに対するカスタムメタデータ。](../../forms/using/customizing-templates-forms-portal-components.md)
1. **フォームポータルページを発行します。** これで、フォームポータルページの準備が整いました。 ページを公開します。

## 関連記事 {#related-articles}

* [フォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md)
* [フォームポータルページの作成](../../forms/using/creating-form-portal-page.md)
* [API を使用した Web ページ上のフォームの一覧表示](/help/forms/using/listing-forms-webpage-using-apis.md)
* [ドラフトと送信コンポーネントの使用](../../forms/using/draft-submission-component.md)
* [ドラフトと送信済みフォームのストレージのカスタマイズ](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [ドラフトと送信コンポーネントとデータベースの統合のサンプル](integrate-draft-submission-database.md)
* [フォームポータルコンポーネントのテンプレートをカスタマイズする](../../forms/using/customizing-templates-forms-portal-components.md)
* [ポータル上のフォーム発行の概要](../../forms/using/introduction-publishing-forms.md)

