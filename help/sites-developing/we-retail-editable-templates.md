---
title: We.Retail の編集可能テンプレートの使用
description: We.Retail を使用して、Adobe Experience Managerで編集可能なテンプレートを試す方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: efebe66d-3d30-4033-9c4c-ae347e134f2f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 23%

---

# We.Retail の編集可能テンプレートの使用{#trying-out-editable-templates-in-we-retail}

編集可能なテンプレートを使用した場合、テンプレートの作成と管理は、開発者のみのタスクではなくなりました。 ある種のパワーユーザーは、テンプレート作成者と呼ばれ、テンプレートを作成できるようになりました。 環境の設定、クライアントライブラリの作成、使用されるコンポーネントの作成は今でも開発者が行う必要がありますが、これら基本となる部分が一度整ってしまえば、テンプレート作成者は開発プロジェクトなしにテンプレートを作成、設定できる柔軟性を持つようになります。

We.Retail のすべてのページは、編集可能なテンプレートに基づいており、開発者以外のユーザーがテンプレートを調整およびカスタマイズできます。

## 試す {#trying-it-out}

1. 言語マスターブランチの機器ページを編集します。

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. モードセレクターはデザインモードを提供しなくなりました。 We.Retail のすべてのページは、編集可能なテンプレートに基づいています。編集可能なテンプレートのデザインを変更するには、テンプレートエディターで編集する必要があります。
1. **ページ情報**&#x200B;メニューから「**テンプレートを編集**」を選択します。
1. ヒーローページテンプレートを編集中です。

   ページの構造モードを使用して、テンプレートの構造を変更できます。 これには、例えば、レイアウトコンテナで使用できるコンポーネントが含まれます。

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. レイアウトコンテナのポリシーを設定して、コンテナで許可されるコンポーネントを定義します。

   ポリシーは、デザイン設定と同じです。

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. レイアウトコンテナのデザインダイアログで、次の操作を実行できます。

   * 既存のポリシーを選択するか、コンテナ用のポリシーを作成します
   * コンテナで許可するコンポーネントを選択
   * アセットをコンテナにドラッグしたときに配置されるデフォルトのコンポーネントを定義する

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. テンプレートエディターに戻ると、レイアウトコンテナ内のテキストコンポーネントのポリシーを編集できます。

   次の操作が可能です。

   * 既存のポリシーを選択するか、コンテナ用のポリシーを作成します
   * ページ作成者がこのコンポーネントを使用する際に使用できる機能を定義します。例：

      * 許可されている貼り付けソース
      * 書式設定オプション
      * 許可される段落スタイル
      * 許可される特殊文字

   コアコンポーネントに基づく多くのコンポーネントでは、編集可能なテンプレートを使用してコンポーネントレベルでオプションを設定できるので、開発者がカスタマイズする必要がなくなります。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. テンプレートエディターに戻る場合は、モードセレクターを使用して、 **初期コンテンツ** モードを使用して、ページに必要なコンテンツを定義します。

   **レイアウト** モードは、通常のページと同様に使用して、テンプレートのレイアウトを定義できます。

## 詳細情報 {#more-information}

詳しくは、オーサリングドキュメントを参照してください [ページテンプレートの作成](/help/sites-authoring/templates.md) または開発者ドキュメントのページ [テンプレート — 編集可能](/help/sites-developing/page-templates-editable.md) を参照してください。

また、[コアコンポーネント](/help/sites-developing/we-retail-core-components.md)についても調べることをお勧めします。コアコンポーネントの機能の概要については、オーサリングドキュメントの[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)を参照してください。技術的な概要については、開発者用ドキュメントの[コアコンポーネントの開発](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=ja)を参照してください。
