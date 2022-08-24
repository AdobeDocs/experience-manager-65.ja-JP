---
title: 'デザインモードでのコンポーネントの設定 '
seo-title: Configuring Components in Design Mode
description: AEM インスタンスが標準インストールされている場合、コンポーネントの選択はサイドキックですぐに使用できます。これらに加えて、その他の様々なコンポーネントも使用できます。このようなコンポーネントを有効または無効にするには、デザインモードを使用します。
seo-description: When AEM instance is installed out-of-the-box, a selection of components are immediately available in the sidekick. In addition to these, various other components are also available. You can use Design mode to Enable/disable such components.
uuid: 2cd5dad0-2f9c-4f34-aae8-1638d1445eb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 10466b49-f8bd-4c2c-8106-b0c7ba054989
docset: aem65
exl-id: cb2d2d0d-feb4-4b89-8325-80f735816904
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 100%

---

# デザインモードでのコンポーネントの設定 {#configuring-components-in-design-mode}

AEM インスタンスが標準インストールされている場合、コンポーネントの選択はサイドキックですぐに使用できます。

これらに加えて、その他の様々なコンポーネントも使用できます。このような[コンポーネントを有効または無効にする](#enabledisablecomponentsusingdesignmode)には、デザインモードを使用します。コンポーネントを有効にしてページに配置したら、デザインモードを使用して属性パラメーターを編集することで[コンポーネントデザインの様々な要素を設定](#configuringcomponentsusingdesignmode)できます。

>[!NOTE]
>
>これらのコンポーネントを編集する際は慎重に行ってください。デザインの設定は、通常、web サイト全体のデザインで重要な部分なので、適切な権限（および十分な経験）のあるユーザー（通常は、管理者または開発者）のみが変更を行う必要があります。詳しくは、[コンポーネントの開発](/help/sites-developing/components.md)を参照してください。

具体的には、ページの段落システムで許可された構成要素を追加したり、削除したりすることです。段落システム（`parsys`）は、他のすべての段落コンポーネントを含む複合コンポーネントです。段落システムを使用すると、他のすべての段落コンポーネントを含んでいるので、作成者は、様々なタイプのコンポーネントをページに追加できます。それぞれの段落タイプはコンポーネントとして表されます。

例えば、商品ページのコンテンツに次の項目を保持する段落システムを含めることができます。

* 商品の画像（画像またはテキスト画像の段落として）
* 商品の説明（テキスト段落として）
* 技術データを含むテーブル（テーブル段落として）
* ユーザー入力フォーム（フォーム開始、フォーム要素、フォーム終了の段落として）

>[!NOTE]
>
>[ について詳しくは、](/help/sites-developing/components.md#paragraphsystem)コンポーネントの開発[および](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components)テンプレートとコンポーネントの使用に関するガイドライン`parsys`を参照してください。

## コンポーネントの有効化/無効化 {#enable-disable-components}

デザインモードではサイドキックは最小化され、オーサリング用にアクセス可能なコンポーネントを設定できます。

1. デザインモードに切り替えるには、編集用のページを開き、サイドキックアイコンを使用します。

   ![](do-not-localize/chlimage_1.png)

1. 段落システムの「**編集**」（**段落のデザイン**）をクリックします。

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. ダイアログが開き、コンポーネントグループが、格納されている個々のコンポーネントと共にサイドキックに表示されます。

   サイドキックで使用するコンポーネントを必要に応じて追加または削除します。

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. デザインモードでは、サイドキックは最小化されます。矢印をクリックすると、サイドキックを最大化して編集モードに戻ることができます。

   ![](do-not-localize/sidekick-collapsed.png)

## コンポーネントのデザインの設定 {#configuring-the-design-of-a-component}

デザインモードでは、個々のコンポーネントの属性も設定できます。コンポーネントにはそれぞれ独自のパラメーターがあります。次に、**画像**&#x200B;コンポーネントの例を示します。

1. デザインモードに切り替えるには、編集用のページを開き、サイドキックアイコンを使用します。

   ![](do-not-localize/chlimage_1-1.png)

1. コンポーネントのデザインを設定できます。

   たとえば、画像コンポーネントの「**編集**」（**画像のデザイン**）をクリックすると、そのコンポーネント特有のパラメーターを設定できます。

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. 「**OK**」をクリックして、変更を保存します。

1. デザインモードでは、サイドキックは最小化されます。矢印をクリックすると、サイドキックを最大化して編集モードに戻ることができます。

   ![](do-not-localize/sidekick-collapsed-1.png)
