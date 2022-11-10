---
title: We.Retail の編集可能テンプレートの使用
seo-title: Trying out Editable Templates in We.Retail
description: We.Retail の編集可能テンプレートの使用
seo-description: null
uuid: 0d4b97cb-efcc-4312-a783-eae3ecd6f889
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3cc8ac23-98ff-449f-bd76-1203c7cbbed7
exl-id: efebe66d-3d30-4033-9c4c-ae347e134f2f
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 100%

---

# We.Retail の編集可能テンプレートの使用{#trying-out-editable-templates-in-we-retail}

編集可能テンプレートでテンプレートを作成して管理することは、開発者のみのタスクではなくなりました。テンプレート作成者と呼ばれる一種の上級ユーザーは、テンプレートを作成できるようになりました。環境の設定、クライアントライブラリの作成、使用されるコンポーネントの作成は今でも開発者が行う必要がありますが、これら基本となる部分が一度整ってしまえば、テンプレート作成者は開発プロジェクトなしにテンプレートを作成、設定できる柔軟性を持つようになります。

We.Retail のページはすべて編集可能テンプレートに基づいており、開発者以外のユーザーがテンプレートを変更したり、カスタマイズしたりできます。

## 試してみる {#trying-it-out}

1. 言語マスターブランチの装備ページを編集します。

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. モードセレクターにデザインモードがなくなったことを確認します。We.Retail のページはすべて編集可能テンプレートに基づいています。編集可能テンプレートのデザインを変更するには、テンプレートエディターで編集する必要があります。
1. **ページ情報**&#x200B;メニューから「**テンプレートを編集**」を選択します。
1. 現在編集しているのはヒーローページテンプレートです。

   ページの構造モードにより、テンプレートの構造を変更できます。これには、例えば、レイアウトコンテナで使用可能なコンポーネントが含まれます。

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. レイアウトコンテナのポリシーを設定して、コンテナで使用可能なコンポーネントを定義します。

   ポリシーはデザイン設定に相当します。

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. レイアウトコンテナのデザインダイアログでは、以下を実行できます。

   * コンテナに既存のポリシーを選択するか、新しいポリシーを作成します。
   * コンテナで使用できるコンポーネントを選択します。
   * アセットがコンテナにドラッグされたときに配置されるデフォルトのコンポーネントを定義します。

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. テンプレートエディターに戻り、レイアウトコンテナ内のテキストコンポーネントのポリシーを編集できます。

   以下を実行できます。

   * コンテナに既存のポリシーを選択するか、新しいポリシーを作成します。
   * ページ作成者がこのコンポーネントの使用時に利用できる機能を定義します。これには以下のような機能があります。

      * 許可される貼り付け元
      * 書式設定オプション
      * 許可される段落スタイル
      * 許可される特殊文字

   コアコンポーネントに基づく多くのコンポーネントでは、編集可能テンプレートを通じて、コンポーネントレベルでオプションを設定できます。開発者がカスタマイズする必要はありません。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. テンプレートエディターに戻り、モードセレクターを使用して&#x200B;**初期コンテンツ**&#x200B;モードに変更し、ページに必要なコンテンツを定義します。

   テンプレートのレイアウトを定義するには、通常のページと同様に、**レイアウト**&#x200B;モードを使用できます。

## 詳細情報 {#more-information}

詳しくは、オーサリングドキュメントの[ページテンプレートの作成](/help/sites-authoring/templates.md)を参照してください。また、編集可能テンプレートの技術的な詳細については、開発者用ドキュメントページの[テンプレート - 編集可能](/help/sites-developing/page-templates-editable.md)を参照してください。

また、[コアコンポーネント](/help/sites-developing/we-retail-core-components.md)についても調べることをお勧めします。コアコンポーネントの機能の概要については、オーサリングドキュメントの[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)を参照してください。技術的な概要については、開発者用ドキュメントの[コアコンポーネントの開発](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=ja)を参照してください。
