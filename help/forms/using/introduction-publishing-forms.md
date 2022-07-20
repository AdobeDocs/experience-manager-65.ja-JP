---
title: ポータル上のフォーム発行の概要
seo-title: Introduction to publishing forms on a portal
description: AEM Forms はフォームポータルを構築するために使用できるコンポーネントを提供します。この記事では、使用可能なフォームポータルコンポーネントを紹介します。
seo-description: AEM Forms provides with components that you can use to build your forms portal. This articles introduces you to the available forms portal components.
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
exl-id: 240ed4d8-b21b-46eb-80a9-9e8093b77235
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 100%

---

# ポータル上のフォーム発行の概要{#introduction-to-publishing-forms-on-a-portal}

## AEM Forms ポータルコンポーネントの概要 {#aem-forms-portal-components-overview}

一般的なフォーム中心のポータル展開シナリオでは、フォームの開発とポータルの開発が別々に行われます。フォーム開発者はフォームを設計してリポジトリに保存する一方、Web 開発者は Web アプリケーションを作成してフォームを一覧表示し、フォームの送信を処理します。フォームリポジトリと Web アプリケーション間では通信が行われないため、フォームは Web 層にコピーされます。

このようなシナリオでは、管理問題が発生したり生産が遅延したりすることがよくあります。例えば、リポジトリで新しいバージョンのフォームを利用できる場合、Web 層でフォームを置換し、Web アプリケーションを変更し、公共サイトでフォームを再展開する必要があります。Web アプリケーションの再展開によって、サーバーのダウンタイムが発生する可能性があります。通常、サーバーのダウンタイムは計画的に行われるため、変更を瞬時に公共サイトにプッシュすることはできません。

AEM Forms は管理のオーバーヘッドと実稼働の遅延を低減するポータルコンポーネントを提供します。コンポーネントにより、Web 開発者は Adobe Experience Manager（AEM）を使用して作成された Web サイト上にフォームポータルを作成してカスタマイズできます。

![AEM Forms ポータル](assets/aem-forms-portal.png)

フォームポータルコンポーネントにより、次の機能が追加されます。

* カスタマイズしたレイアウトでフォームを一覧表示します。リスト表示、カード表示、パネル表示用のレイアウトをすぐに使用できる。独自のカスタムレイアウトを作成できます。
* 一覧表示からカスタムメタデータおよびカスタムアクションを表示する。
* フォームポータルコンポーネントを使用しているパブリッシュインスタンス上の AEM Forms UI が発行したフォームを一覧表示します。
* HTML 形式および PDF 形式でフォームをレンダリングできるようにします。 
* カスタム HTML プロファイルを使用してフォームをレンダリングします。
* 様々な検索条件（フォームプロパティ、メタデータ、タグなど）に基づいたフォームの検索を有効にします。 
* フォームデータをサーブレットに送信します。
* カスタム CSS を使用してポータルのルックアンドフィールをカスタマイズします。 
* フォームへのリンクを作成します。
* エンドユーザーが作成したアダプティブフォームに関連するドラフトおよび送信を一覧表示する。

## 使用可能な AEM Forms ポータルコンポーネント {#available-aem-forms-portal-components}

AEM Forms は次の標準ポータルコンポーネントを、**Document Services** および **Document Services Predicates** コンポーネントグループの下にグループ化して提供します。

### 検索とリスター {#search-amp-lister}

Search &amp; Lister コンポーネントは、フォームリポジトリのフォームをポータルページに一覧表示するほか、指定した検索条件に基づいてフォームを一覧表示するオプションを提供します。また、検索条件を指定することにより、ポータルユーザーがフォームのリストから検索できるようにします。

### ドラフトと送信 {#drafts-amp-submissions}

Search &amp; Lister コンポーネントはフォーム作成者によって発行されたフォームを表示する一方、Drafts &amp; Submissions コンポーネントはドラフトとして保存され、後で完了して送信されるフォームを表示します。このコンポーネントはログインユーザーに対してパーソナライズされたエクスペリエンスを提供します。

### リンク {#link}

Link コンポーネントでは、ページ上の任意の場所にあるフォームへのリンクを作成できます。トレーニングプログラムを提供し、ユーザーがフォームを送信してトレーニングに登録できるようにするシナリオを検討します。お客様は当社の Web サイトに、プログラムの詳細を投稿しました。次に示す詳細に、登録フォームへのリンクを記述しています。Link コンポーネントはリンクの作成に役立ちます。

## フォームポータルのワークフロー {#forms-portal-workflow}

フォームポータルを使用すると、フォームリポジトリからポータルページにフォームを一覧表示できます。また、検索条件を指定することにより、ポータルユーザーがフォームのリストから検索できるようにします。また、ドラフトと送信コンポーネントを使用して、後で完成させるためにドラフトとして保存されたフォームや送信済みのフォームを表示することもできます。これらの機能を Sites ページで使用するには、一連の操作を実行する必要があります。リストに表示された順序で手順を実行して、コンポーネントと各機能をサイトページで使用できるようにします。

1. **フォームポータルコンポーネントを有効にする**：標準提供のフォームポータルコンポーネントは使用できません。AEM Sites ページ用に [AEM サイドキックからコンポーネントを有効にします](/help/forms/using/enabling-forms-portal-components.md)。
1. **ページ上のフォームを一覧表示（フォームポータルページを作成）：** AEM Sites ページと非 AEM Site ページの両方でフォームを一覧表示できます。リストには、パブリッシュインスタンスで使用できるフォームが含まれています。ユーザーはフォームを開き、入力を開始できます。ユーザーがフォームを開くたびに、フォームの新しいインスタンスが作成されます。

   1. **AEM Sites ページ上のフォームを一覧表示**：**[Search &amp; Lister](../../forms/using/creating-form-portal-page.md)** コンポーネントをページに追加してその中に&#x200B;**[リストペイン](../../forms/using/creating-form-portal-page.md#p-list-pane-p)**&#x200B;を設定し、 ページ上のフォームを一覧表示します。**検索ペイン**&#x200B;コンポーネントを **Search &amp; Lister** コンポーネントに追加して設定し、ページにも検索機能を追加します。フォームポータルコンポーネントを含むページは、[フォームポータルページ](../../forms/using/creating-form-portal-page.md)と呼ばれます。

   1. **非 AEM Sites ページ上のフォームを一覧表示：** [フォームポータル検索 API](/help/forms/using/listing-forms-webpage-using-apis.md) を使用して、非 AEM Sites のページのフォームをクエリ、取得、一覧表示します。

1. **フォームポータルページ上のドラフトフォームと送信済みフォームを一覧表示**：Drafts &amp; Submissions コンポーネントをフォームポータルページに追加して設定します。このコンポーネントは、ドラフト状態のすべてのフォームと、既に送信済みのフォームを一覧表示します。

   アダプティブフォームの送信を有効化して「送信」タブに表示するには、「**送信アクション**」を「**[フォームポータル送信アクション](configuring-submit-actions.md)」に設定します。**&#x200B;または、「フォームポータル送信」オプションを有効にします。ユーザーがフォームを送信するたびに、フォームが「送信」タブに追加されます。

1. **ドラフトおよび送信済みのフォームデータのストレージを設定：**&#x200B;デフォルトでは、ドラフトと送信データは AEM リポジトリに保存されます。実稼働環境では、ドラフトまたは送信済みのフォームデータを AEM リポジトリに格納しないことをお勧めします。[安全な場所にデータを保存するためのフォームポータルコンポーネントを設定します](../../forms/using/draft-submission-component.md#customizing-the-storage)。
1. **（オプション）フォームポータルコンポーネントのカスタマイズ：** [フォームポータルのページテンプレートをカスタマイズ](../../forms/using/customizing-templates-forms-portal-components.md)して、コンポーネントに独特の外観を提供します。
1. **（オプション）フォームにカスタムメタデータを追加：** [フォームにカスタムメタデータを追加](../../forms/using/customizing-templates-forms-portal-components.md)して、リストと検索のエクスペリエンスを向上させます。
1. **フォームポータルページを公開：**&#x200B;これで、フォームポータルページの準備が整いました。ページを公開します。

## 関連記事 {#related-articles}

* [フォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md)
* [フォームポータルページの作成 ](../../forms/using/creating-form-portal-page.md)
* [API を使用した Web ページ上のフォームの一覧表示](/help/forms/using/listing-forms-webpage-using-apis.md)
* [ドラフトと送信コンポーネントの使用](../../forms/using/draft-submission-component.md)
* [ドラフトと送信済みフォームのストレージのカスタマイズ](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [ドラフトと送信コンポーネントとデータベースの統合のサンプル](integrate-draft-submission-database.md)
* [フォームポータルコンポーネントのテンプレートをカスタマイズする](../../forms/using/customizing-templates-forms-portal-components.md)
* [ポータル上のフォーム発行の概要](../../forms/using/introduction-publishing-forms.md)
