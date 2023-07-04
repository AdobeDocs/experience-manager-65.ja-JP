---
title: デザインモードでのコンポーネントの設定
description: AEM インスタンスを標準でインストールすると、サイドキックで直ちに様々なコンポーネントを使用できます。これらに加えて、他の様々なコンポーネントも使用できます。デザインモードを使用して、このようなコンポーネントを有効または無効にできます。
uuid: 2cd5dad0-2f9c-4f34-aae8-1638d1445eb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 10466b49-f8bd-4c2c-8106-b0c7ba054989
docset: aem65
exl-id: cb2d2d0d-feb4-4b89-8325-80f735816904
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: ht
source-wordcount: '500'
ht-degree: 100%

---

# デザインモードでのコンポーネントの設定{#configuring-components-in-design-mode}

AEM インスタンスを標準でインストールすると、サイドキックで直ちに様々なコンポーネントを使用できます。

これらに加えて、その他の様々なコンポーネントも使用できます。このような[コンポーネントを有効または無効にする](#enabledisablecomponentsusingdesignmode)には、デザインモードを使用します。コンポーネントを有効にしてページに配置したら、デザインモードを使用して属性パラメーターを編集することで[コンポーネントデザインの様々な要素を設定](#configuringcomponentsusingdesignmode)できます。

>[!NOTE]
>
>これらのコンポーネントを編集する際は慎重に行ってください。デザインの設定は、通常、web サイト全体のデザインで重要な部分なので、適切な権限（および十分な経験）のあるユーザー（通常は、管理者または開発者）のみが変更を行う必要があります。詳しくは、[コンポーネントの開発](/help/sites-developing/components.md)を参照してください。

具体的には、ページの段落システムで許可された構成要素を追加したり、削除したりすることです。段落システム（`parsys`）は、他のすべての段落コンポーネントを含む複合コンポーネントです。段落システムを使用すると、作成者は異なるタイプのコンポーネントを、他のすべての段落コンポーネントを含むページに追加できます。各段落タイプは、コンポーネントとして表されます。

例えば、製品ページのコンテンツには、次の情報を含む段落システムを含めることができます。

* 製品の画像（画像または textimage 段落の形式）
* 製品の説明（テキスト段落として）
* 技術データを含むテーブル（表の段落として）
* ユーザー入力フォーム（フォーム開始、フォーム要素、フォーム終了の段落として）

>[!NOTE]
>
>[ について詳しくは、](/help/sites-developing/components.md#paragraphsystem)コンポーネントの開発[および](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components)テンプレートとコンポーネントの使用に関するガイドライン`parsys`を参照してください。

## コンポーネントを有効／無効にする {#enable-disable-components}

デザインモードでは、サイドキックは最小化され、オーサリング用にアクセス可能なコンポーネントを設定できます。

1. デザインモードに入るには、編集するページを開き、サイドキックアイコンを使用します。

   ![](do-not-localize/chlimage_1.png)

1. 段落システムの「**編集**」（**段落のデザイン**）をクリックします。

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. ダイアログが開き、サイドキックに表示されるコンポーネントグループと、それらが含む個々のコンポーネントが一覧表示されます。

   必要に応じて、サイドキックで使用可能なコンポーネントを追加または削除します。

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. デザインモードでは、サイドキックは最小化されます。矢印をクリックすると、サイドキックを最大化して編集モードに戻ることができます。

   ![](do-not-localize/sidekick-collapsed.png)

## コンポーネントのデザインの設定 {#configuring-the-design-of-a-component}

デザインモードでは、個々のコンポーネントの属性を設定することもできます。各コンポーネントには独自のパラメーターがあり、次の例では&#x200B;**画像**&#x200B;コンポーネントが表示されます。

1. デザインモードに入るには、編集するページを開き、サイドキックアイコンを使用します。

   ![](do-not-localize/chlimage_1-1.png)

1. コンポーネントのデザインを設定できます。

   たとえば、画像コンポーネントの「**編集**」（**画像のデザイン**）をクリックすると、そのコンポーネント特有のパラメーターを設定できます。

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. 「**OK**」をクリックして、変更を保存します。

1. デザインモードでは、サイドキックは最小化されます。矢印をクリックすると、サイドキックを最大化して編集モードに戻ることができます。

   ![](do-not-localize/sidekick-collapsed-1.png)
