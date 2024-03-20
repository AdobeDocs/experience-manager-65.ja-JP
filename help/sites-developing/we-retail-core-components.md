---
title: We.Retail のコアコンポーネントの使用
description: We.Retail での Adobe Experience Manager のコアコンポーネントの使用方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: b5f2be67-c93c-4dbc-acc0-3edd8f1a282f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 100%

---

# We.Retail のコアコンポーネントの使用{#trying-out-core-components-in-we-retail}

コアコンポーネントは、柔軟性の高い最新のコンポーネントです。拡張が容易で、プロジェクトに簡単に統合できます。コアコンポーネントは、HTL、設定不要の使いやすさ、設定可能、バージョン管理、拡張性など、いくつかの重要な設計の原理に基づいて構築されています。We.Retail はコアコンポーネントを基盤に構築されています。

## 試してみる {#trying-it-out}

1. We.Retail サンプルコンテンツを使用して Adobe Experience Manager（AEM）を起動し、[コンポーネントコンソール](/help/sites-authoring/default-components-console.md)を開きます。

   **グローバルナビゲーション／ツール／コンポーネント**

1. コンポーネントコンソールでパネルを開くと、特定のコンポーネントグループをフィルタリングできます。コアコンポーネントは次の場所にあります。

   * `.core-wcm`：標準コアコンポーネント
   * `.core-wcm-form`：フォーム送信コアコンポーネント

   `.core-wcm` を選択します。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. すべてのコアコンポーネントの名前が **v1** になっています。これは、このコアコンポーネントの最初のバージョンであることを示します。今後、定期的にバージョンがリリースされる予定です。これは、AEM とバージョンの互換性があり、簡単にアップグレードできるので、最新機能を利用できます。
1. 「**Text (v1)**」をクリックします。

   コンポーネントの&#x200B;**リソースタイプ**&#x200B;が `/apps/core/wcm/components/text/v1/text` であることを確認します。コアコンポーネントは `/apps/core/wcm/components` の下にあり、コンポーネントごとにバージョン管理されます。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 「**ドキュメント**」タブをクリックして、コンポーネントの開発者用ドキュメントを表示します。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. コンポーネントコンソールに戻ります。**We.Retail** グループをフィルタリングし、**テキスト**&#x200B;コンポーネントを選択します。
1. **リソースタイプ**&#x200B;が `/apps/weretail` 下の想定したコンポーネントを指していることを確認します。ただし、**リソースのスーパータイプ**&#x200B;は元のコアコンポーネント `/apps/core/wcm/components/text/v1/text` を指しています。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 「**ライブ使用状況**」タブをクリックして、このコンポーネントが使用されているページを表示します。最初の&#x200B;**ありがとう**&#x200B;ページをクリックしてページを編集します。

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. ありがとうページで、テキストコンポーネントを選択し、コンポーネントの編集メニューで、継承をキャンセルアイコンをクリックします。

   [We.Retail にはグローバル化されたサイト構造が用意されており](/help/sites-developing/we-retail-globalized-site-structure.md)、この構造では、コンテンツが言語マスターから[継承と呼ばれるメカニズムを通じてライブコピーにプッシュされます](/help/sites-administering/msm.md)。このため、ユーザーが手動でテキストを編集できるよう、継承はキャンセルする必要があります。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 「**はい**」をクリックしてキャンセルを確定します。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 継承をキャンセルしてテキストコンポーネントを選択すると、さらに多くのオプションを使用できるようになります。「**編集**」をクリックします。

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. テキストコンポーネントに使用できる編集オプションが表示されます。

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. **ページ情報**&#x200B;メニューから「**テンプレートを編集**」を選択します。
1. ページのテンプレートエディターで、そのページの&#x200B;**レイアウトコンテナ**&#x200B;にあるテキストコンポーネントの&#x200B;**ポリシー**&#x200B;アイコンをクリックします。

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. コアコンポーネントを使用すると、テンプレート作成者は、ページ作成者がどのプロパティを使用できるかを設定できます。これには、許可されるペースト元、書式設定オプション、使用可能な段落スタイルなどの機能が含まれます。

   このようなデザインダイアログは、多くのコアコンポーネントで使用可能で、テンプレートエディターと連携して機能します。有効にした機能は、コンポーネントエディターを通じて作成者に提供されます。

   ![chlimage_1-172](assets/chlimage_1-172.png)

## その他の情報 {#further-information}

コアコンポーネントについて詳しくは、オーサリングドキュメントの[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)でコアコンポーネント機能の概要を参照し、開発者用ドキュメントの[コアコンポーネントの開発](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=ja)で技術的な概要を参照してください。

また、[編集可能テンプレート](/help/sites-developing/we-retail-editable-templates.md)も詳しく調査することをお勧めします。編集可能テンプレートについて詳しくは、オーサリングドキュメントの[ページテンプレートの作成](/help/sites-authoring/templates.md)または開発者用ドキュメントのページ[テンプレート - 編集可能](/help/sites-developing/page-templates-editable.md)を参照してください。
