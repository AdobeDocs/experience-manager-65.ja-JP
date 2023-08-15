---
title: ポータル上のフォーム公開の概要
description: Adobe Experience Manager Formsは、Formsポータルの構築に使用できるコンポーネントを提供します。 この記事では、使用可能なForms Portal コンポーネントについて説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: 240ed4d8-b21b-46eb-80a9-9e8093b77235
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 43%

---

# ポータル上のフォーム公開の概要{#introduction-to-publishing-forms-on-a-portal}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html) |
| AEM 6.5 | この記事 |


## AEM Forms portal コンポーネントの概要 {#aem-forms-portal-components-overview}

一般的なフォーム中心のポータルデプロイメントシナリオでは、フォーム開発とポータル開発が 2 つの異なるアクティビティになります。 フォームデザイナーがフォームを設計してリポジトリに保存する一方、Web 開発者はフォームを一覧表示し、フォームの送信を処理する Web アプリケーションを作成します。 Formsは、フォームリポジトリと Web アプリケーションの間で通信がおこなわれないので、Web 層にコピーされます。

このようなシナリオは、多くの場合、管理上の問題と生産上の遅延を引き起こします。 例えば、リポジトリに新しいバージョンのフォームがある場合、Web 層でフォームを置き換え、Web アプリケーションを変更し、パブリックサイトでフォームを再デプロイする必要があります。 Web アプリケーションを再デプロイすると、サーバーのダウンタイムが発生する場合があります。 通常、サーバーのダウンタイムは計画的なアクティビティなので、変更を瞬時に公開サイトにプッシュすることはできません。

AEM Forms は管理のオーバーヘッドと実稼働の遅延を低減するポータルコンポーネントを提供します。コンポーネントにより、web 開発者は Adobe Experience Manager（AEM）を使用して作成された web サイト上にフォームポータルを作成してカスタマイズできます。

![AEM Forms ポータル](assets/aem-forms-portal.png)

フォームポータルコンポーネントを使用して、以下の機能を追加できます。

* カスタマイズしたレイアウトでフォームを一覧表示します。リスト表示、カード表示、パネル表示のレイアウトが標準で用意されています。 独自のカスタムレイアウトを作成できます。
* カスタムメタデータとカスタムアクションをリスト表示中に表示できます。
* フォームポータルコンポーネントを使用しているパブリッシュインスタンス上の AEM Forms UI が発行したフォームを一覧表示します。
* エンドユーザーが HTML 形式および PDF 形式でフォームをレンダリングできるようにします。
* カスタム HTML プロファイルを使用してフォームをレンダリングします。
* 様々な検索条件（フォームプロパティ、メタデータ、タグなど）に基づいたフォームの検索を有効にします。 
* フォームデータをサーブレットに送信します。
* カスタム CSS を使用してポータルのルックアンドフィールをカスタマイズします。 
* フォームへのリンクを作成します。
* エンドユーザーが作成したアダプティブフォームに関連するドラフトと送信を一覧表示します。

## 使用可能なAEM Forms Portal コンポーネント {#available-aem-forms-portal-components}

AEM Formsは、すぐに使用できる次のポータルコンポーネントを、の下にグループ化して提供します。 **ドキュメントサービス** および **Document Services の述語** コンポーネントグループ：

### 検索とリスター {#search-amp-lister}

Search &amp; Lister コンポーネントを使用すると、フォームリポジトリのフォームをポータルページに一覧表示でき、指定した条件に基づいてフォームを一覧表示するための設定オプションを提供します。 また、検索条件を指定して、ポータルユーザーがフォームのリスト全体を検索できるようにします。

### ドラフトと送信 {#drafts-amp-submissions}

Search &amp; Lister コンポーネントには、Formsの作成者が公開したフォームが表示され、Drafts &amp; Submissions コンポーネントには、後で完了するためにドラフトとして保存されたフォームと送信済みのフォームが表示されます。 このコンポーネントは、ログインしたユーザーに対してパーソナライズされたエクスペリエンスを提供します。

### リンク {#link}

リンクコンポーネントを使用すると、ページ上の任意の場所にフォームへのリンクを作成できます。 トレーニングプログラムを提供し、ユーザーがフォームを送信してトレーニングに登録したい場合を考えてみましょう。 Web サイトに、プログラムの詳細を投稿しました。 以下に、登録フォームへのリンクを示します。 リンクコンポーネントは、そのリンクの作成に役立ちます。

## フォームポータルのワークフロー {#forms-portal-workflow}

Forms Portal では、フォームリポジトリからポータルページにフォームをリストすることができます。 また、検索条件を指定して、ポータルユーザーがフォームのリスト全体を検索できるようにします。 また、ドラフトと送信コンポーネントを使用して、後で完成させるためにドラフトとして保存されたフォームや送信済みのフォームを表示することもできます。これらの機能を Sites ページで使用できるようになる前に、一連の操作を実行します。 リストに表示された順序で手順を実行して、コンポーネントと各機能をサイトページで使用できるようにします。

1. **Forms Portal コンポーネントの有効化**：デフォルトでは、Forms Portal コンポーネントは使用できません。 AEM Sites ページ用に [AEM サイドキックからコンポーネントを有効にします](/help/forms/using/enabling-forms-portal-components.md)。
1. **ページ上のフォームを一覧表示します (Forms Portal ページを作成 )。** AEM Sitesページと非AEM Site ページの両方でフォームを一覧表示できます。 リストには、パブリッシュインスタンスで使用できるフォームが含まれています。ユーザーはフォームを開き、入力を開始できます。ユーザーがフォームを開くたびに、フォームの新しいインスタンスが作成されます。

   1. **AEM Sites ページ上のフォームを一覧表示**：**[Search &amp; Lister](../../forms/using/creating-form-portal-page.md)** コンポーネントをページに追加してその中に&#x200B;**[リストペイン](../../forms/using/creating-form-portal-page.md#p-list-pane-p)**&#x200B;を設定し、 ページ上のフォームを一覧表示します。**検索ペイン**&#x200B;コンポーネントを **Search &amp; Lister** コンポーネントに追加して設定し、ページにも検索機能を追加します。Forms Portal コンポーネントを含むページは、 [Forms Portal ページ](../../forms/using/creating-form-portal-page.md).

   1. **非AEM Sitesページ上のフォームの一覧表示：** 以下を使用します。 [Forms Portal 検索 API](/help/forms/using/listing-forms-webpage-using-apis.md) を使用して、AEM Sites以外のページ上のフォームのクエリ、取得、リストを行います。

1. **Forms Portal ページにドラフトフォームと送信済みフォームを一覧表示する**：ドラフトと送信コンポーネントをForms Portal ページに追加し、設定します。 このコンポーネントは、ドラフト状態のすべてのフォームと、既に送信済みのフォームを一覧表示します。

   アダプティブフォームの送信を有効化して「送信」タブに表示するには、「**送信アクション**」を「**[フォームポータル送信アクション](configuring-submit-actions.md)」に設定します。**&#x200B;または、「フォームポータル送信」オプションを有効にします。ユーザーがフォームを送信するたびに、フォームが「送信」タブに追加されます。

1. **ドラフトおよび送信済みのフォームデータのストレージを設定：**&#x200B;デフォルトでは、ドラフトと送信データは AEM リポジトリに保存されます。実稼働環境では、ドラフトまたは送信済みのフォームデータを AEM リポジトリに格納しないことをお勧めします。[安全な場所にデータを保存するようにForms Portal コンポーネントを設定する](../../forms/using/draft-submission-component.md#customizing-the-storage).
1. **（オプション） Forms Portal コンポーネントのカスタマイズ：** [Forms Portal ページテンプレートのカスタマイズ](../../forms/using/customizing-templates-forms-portal-components.md) 部品に対して独特な外観を提供する。
1. **（オプション）フォームにカスタムメタデータを追加：** [フォームにカスタムメタデータを追加](../../forms/using/customizing-templates-forms-portal-components.md)して、リストと検索のエクスペリエンスを向上させます。
1. **Forms Portal ページを公開します。** これで、Forms Portal ページの準備が整いました。 ページを公開します。

## 関連記事 {#related-articles}

* [フォームポータルコンポーネントを有効にする](/help/forms/using/enabling-forms-portal-components.md)
* [Forms Portal の作成ページ](../../forms/using/creating-form-portal-page.md)
* [API を使用した Web ページ上のフォームの一覧表示](/help/forms/using/listing-forms-webpage-using-apis.md)
* [ドラフトと送信コンポーネントの使用](../../forms/using/draft-submission-component.md)
* [ドラフトと送信済みフォームのストレージのカスタマイズ](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [ドラフトと送信コンポーネントとデータベースの統合のサンプル](integrate-draft-submission-database.md)
* [Forms Portal コンポーネントのテンプレートのカスタマイズ](../../forms/using/customizing-templates-forms-portal-components.md)
* [ポータル上のフォーム公開の概要](../../forms/using/introduction-publishing-forms.md)
