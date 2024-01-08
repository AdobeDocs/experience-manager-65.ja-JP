---
title: We.Retail のコアコンポーネントの使用
description: We.Retail を使用してAdobe Experience Managerでコアコンポーネントを試す方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: b5f2be67-c93c-4dbc-acc0-3edd8f1a282f
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 34%

---

# We.Retail のコアコンポーネントの使用{#trying-out-core-components-in-we-retail}

コアコンポーネントは、拡張が容易な最新の柔軟なコンポーネントで、プロジェクトに簡単に統合できます。 コアコンポーネントは、HTL、すぐに使用できる操作性、設定性、バージョン管理、拡張機能など、いくつかの主要なデザイン原則に基づいて構築されています。 We.Retail は、コアコンポーネントを基に構築されています。

## 試してみる {#trying-it-out}

1. We.Retail サンプルコンテンツでAdobe Experience Manager(AEM) を起動し、 [コンポーネントコンソール](/help/sites-authoring/default-components-console.md).

   **グローバルナビゲーション/ツール/コンポーネント**

1. コンポーネントコンソールでパネルを開くと、特定のコンポーネントグループに対してフィルタリングできます。 コアコンポーネントは、

   * `.core-wcm`：標準コアコンポーネント
   * `.core-wcm-form`：フォーム送信コアコンポーネント

   `.core-wcm` を選択します。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. すべてのコアコンポーネントには、 **v1**（このコアコンポーネントの最初のバージョンであることを反映） 今後、通常のバージョンがリリースされる予定です。これは、AEMとのバージョン互換性があり、アップグレードが容易なので、最新の機能を活用できます。
1. クリック **テキスト (v1)**.

   コンポーネントの&#x200B;**リソースタイプ**&#x200B;が `/apps/core/wcm/components/text/v1/text` であることを確認します。コアコンポーネントは `/apps/core/wcm/components` の下にあり、コンポーネントごとにバージョン管理されます。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 次をクリック： **ドキュメント** 「 」タブに移動して、コンポーネントの開発者向けドキュメントを表示します。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. コンポーネントコンソールに戻ります。 グループのフィルター **We.Retail** をクリックし、 **テキスト** コンポーネント。
1. **リソースタイプ**&#x200B;が `/apps/weretail` 下の想定したコンポーネントを指していることを確認します。ただし、**リソースのスーパータイプ**&#x200B;は元のコアコンポーネント `/apps/core/wcm/components/text/v1/text` を指しています。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 次をクリック： **ライブ使用状況** タブをクリックして、このコンポーネントが使用されているページを確認します。 最初の&#x200B;**ありがとう**&#x200B;ページをクリックしてページを編集します。

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. ありがとうページで、テキストコンポーネントを選択し、コンポーネントの編集メニューで継承をキャンセルアイコンをクリックします。

   [We.Retail はグローバル化されたサイト構造を持っています](/help/sites-developing/we-retail-globalized-site-structure.md) コンテンツが言語マスターからにプッシュされる場所 [継承という仕組みを通じてのライブコピー](/help/sites-administering/msm.md). このため、継承はキャンセルして、ユーザーが手動でテキストを編集できるようにする必要があります。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 「**はい**」をクリックしてキャンセルを確定します。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 継承がキャンセルされ、テキストコンポーネントを選択すると、さらに多くのオプションを使用できます。 クリック **編集**.

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. テキストコンポーネントに使用できる編集オプションが表示されます。

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. 次から： **ページ情報** メニュー、選択 **テンプレートを編集**.
1. ページのテンプレートエディターで、 **ポリシー** アイコン **レイアウトコンテナ** 」と入力します。

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. コアコンポーネントを使用すれば、テンプレート作成者は、ページ作成者が使用できるプロパティを設定できます。 これには、許可された貼り付けソース、書式設定オプション、使用可能な段落スタイルなどの機能が含まれます。

   このようなデザインダイアログは、多くのコアコンポーネントで使用でき、テンプレートエディターと連携して作業できます。 有効にすると、コンポーネントエディターで作成者が使用できるようになります。

   ![chlimage_1-172](assets/chlimage_1-172.png)

## その他の情報 {#further-information}

コアコンポーネントについて詳しくは、オーサリングドキュメントの[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)でコアコンポーネント機能の概要を参照し、開発者用ドキュメントの[コアコンポーネントの開発](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=ja)で技術的な概要を参照してください。

また、[編集可能テンプレート](/help/sites-developing/we-retail-editable-templates.md)も詳しく調査することをお勧めします。編集可能テンプレートについて詳しくは、オーサリングドキュメントの[ページテンプレートの作成](/help/sites-authoring/templates.md)または開発者用ドキュメントのページ[テンプレート - 編集可能](/help/sites-developing/page-templates-editable.md)を参照してください。
