---
title: We.Retail の編集可能テンプレートの使用
seo-title: We.Retail の編集可能テンプレートの使用
description: 'null'
seo-description: 'null'
uuid: 0d4b97cb-efcc-4312-a783-eae3ecd6f889
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3cc8ac23-98ff-449f-bd76-1203c7cbbed7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 86%

---


# We.Retail の編集可能テンプレートの使用{#trying-out-editable-templates-in-we-retail}

編集可能テンプレートでテンプレートを作成して管理することは、開発者のみのタスクではなくなりました。テンプレート作成者と呼ばれる一種の上級ユーザーは、テンプレートを作成できるようになりました。環境の設定、クライアントライブラリの作成、使用されるコンポーネントの作成は今でも開発者がおこなう必要がありますが、これら基本となる部分が一度配置されると、テンプレート作成者が開発プロジェクトなしにテンプレートを作成して構成できるようになります。

We.Retail のページはすべて編集可能テンプレートに基づいており、開発者以外のユーザーがテンプレートを変更したり、カスタマイズしたりできます。

## 試してみる  {#trying-it-out}

1. 言語マスターブランチの装備ページを編集します。

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. モードセレクターにデザインモードがなくなったことを確認します。We.Retail のページはすべて編集可能テンプレートに基づいています。編集可能テンプレートのデザインを変更するには、テンプレートエディターで編集する必要があります。
1. **ページ情報**&#x200B;メニューから、「**テンプレートを編集**」を選択します。
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

## 詳細情報  {#more-information}

編集可能なテンプレートの技術的な詳細については、オーサリングドキュメント[ページテンプレートの作成](/help/sites-authoring/templates.md)または開発者向けドキュメントページ[テンプレート — 編集可能](/help/sites-developing/page-templates-editable.md)を参照してください。

また、[コアコンポーネント](/help/sites-developing/we-retail-core-components.md)についても調べることをお勧めします。技術的な概要については、オーサリングドキュメント[コアコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html)および開発者向けドキュメント[コアコンポーネントの開発](https://helpx.adobe.com/experience-manager/core-components/using/developing.html)を参照してください。

