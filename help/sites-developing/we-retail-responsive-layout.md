---
title: We.Retail のレスポンシブレイアウトの使用
seo-title: We.Retail のレスポンシブレイアウトの使用
description: 'null'
seo-description: 'null'
uuid: d9613655-f54e-458f-9175-d07bb868f58b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 2d374e88-ea09-43d5-986c-5d77b0705b93
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 74%

---


# We.Retail のレスポンシブレイアウトの使用{#trying-out-responsive-layout-in-we-retail}

すべてのWeb.Retailページで、レスポンシブデザインの実装にレイアウトコンテナコンポーネントが使用されます。 レイアウトコンテナは、レスポンシブグリッド内にコンポーネントを配置できる段落システムを提供します。このグリッドでは、デバイスやウィンドウのサイズおよび形式に従ってレイアウトを再編成できます。The component is used in conjunction with the **Layout** mode in the page editor, which allows you to create and edit your responsive layout dependent on device.

## 試してみる {#trying-it-out}

1. 言語マスターブランチの「エクスペリエンス」セクションで Arctic Surfing ページを編集します。

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html

1. **プレビュー**&#x200B;に切り替えて、Web サイトの訪問者に表示されるページを確認します。記事「Aloha spirits in Norther Norway」**&#x200B;のコンテンツまでスクロールダウンします。

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. ブラウザーウィンドウのサイズを変更し、そのサイズ変更に対してレイアウトが動的に調整されることを確認します。

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. レイアウトモードに切り替えます。エミュレーターツールバーが自動的に表示されます。このツールバーを使用して、ターゲットデバイスごとにレイアウトを計画できます。

   コンポーネントを選択すると、編集メニューにフローティングおよび非表示オプションと共に、コンポーネントのサイズ変更ハンドルが表示されます。

   ![chlimage_1-180](assets/chlimage_1-180.png)

1. コンポーネントのサイズ変更ハンドルを選択してドラッグすると、サイズ変更に役立つレイアウトグリッドが自動的に表示されます。

   ![chlimage_1-181](assets/chlimage_1-181.png)

## その他の情報 {#further-information}

For further information, refer to the authoring document [Responsive Layout](/help/sites-authoring/responsive-layout.md) or the administrator document [Configuring Layout Container and Layout Mode](/help/sites-administering/configuring-responsive-layout.md) for complete technical details.
