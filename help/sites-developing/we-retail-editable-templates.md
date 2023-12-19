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
ht-degree: 82%

---

# We.Retail の編集可能テンプレートの使用{#trying-out-editable-templates-in-we-retail}

編集可能なテンプレートでテンプレートを作成して管理することは、開発者のみのタスクではなくなりました。テンプレート作成者と呼ばれるパワーユーザーのタイプが、テンプレートを作成できるようになりました。環境の設定、クライアントライブラリの作成、使用されるコンポーネントの作成は今でも開発者が行う必要がありますが、これら基本となる部分が一度整ってしまえば、テンプレート作成者は開発プロジェクトなしにテンプレートを作成、設定できる柔軟性を持つようになります。

We.Retail のページはすべて編集可能テンプレートに基づいており、開発者以外のユーザーがテンプレートを変更したり、カスタマイズしたりできます。

## 試してみる {#trying-it-out}

1. 言語メインブランチの装備ページを編集します。

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. モードセレクターはデザインモードを提供しなくなりました。 We.Retail のページは、すべて編集可能テンプレートに基づいています。編集可能テンプレートのデザインを変更するには、テンプレートエディターで編集する必要があります。
1. **ページ情報**&#x200B;メニューから「**テンプレートを編集**」を選択します。
1. 現在編集しているのはヒーローページテンプレートです。

   ページの構造モードを使用して、テンプレートの構造を変更できます。これには、例えば、レイアウトコンテナで使用できるコンポーネントが含まれます。

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. レイアウトコンテナのポリシーを設定して、コンテナで使用できるコンポーネントを定義します。

   ポリシーはデザイン設定に相当します。

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. レイアウトコンテナのデザインダイアログで、次の操作を実行できます。

   * 既存のポリシーを選択するか、コンテナ用のポリシーを作成します
   * コンテナで使用できるコンポーネントを選択する
   * アセットをコンテナにドラッグしたときに配置されるデフォルトのコンポーネントを定義する

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. テンプレートエディターに戻り、レイアウトコンテナ内のテキストコンポーネントのポリシーを編集できます。

   次の操作が可能です。

   * 既存のポリシーを選択するか、コンテナ用のポリシーを作成します
   * ページ作成者がこのコンポーネントの使用時に利用できる、以下のような機能を定義する

      * 許可される貼り付け元
      * 書式設定オプション
      * 許可される段落スタイル
      * 許可される特殊文字

   コアコンポーネントに基づく多くのコンポーネントでは、編集可能テンプレートを使用してコンポーネントレベルでオプションを設定できるので、開発者がカスタマイズする必要がなくなります。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. テンプレートエディターに戻り、モードセレクターを使用して&#x200B;**初期コンテンツ**&#x200B;モードに変更し、ページに必要なコンテンツを定義できます。

   **レイアウト**&#x200B;モードを使用して、通常のページと同じように、テンプレートのレイアウトを定義できます。

## 詳細情報 {#more-information}

詳しくは、オーサリングドキュメントを参照してください [ページテンプレートの作成](/help/sites-authoring/templates.md) または開発者ドキュメントのページ [テンプレート — 編集可能](/help/sites-developing/page-templates-editable.md) を参照してください。

また、[コアコンポーネント](/help/sites-developing/we-retail-core-components.md)についても調べることをお勧めします。コアコンポーネントの機能の概要については、オーサリングドキュメントの[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)を参照してください。技術的な概要については、開発者用ドキュメントの[コアコンポーネントの開発](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=ja)を参照してください。
