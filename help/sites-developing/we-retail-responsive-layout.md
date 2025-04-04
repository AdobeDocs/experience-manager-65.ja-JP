---
title: We.Retail のレスポンシブレイアウトの使用
description: We.Retail を使用して Adobe Experience Manager でレスポンシブレイアウトを試す方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 6df5fb10-a7f1-4d5d-ac00-b4be3d5d3d18
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 100%

---

# We.Retail のレスポンシブレイアウトの使用{#trying-out-responsive-layout-in-we-retail}

We.Retail のすべてのページでは、レスポンシブデザインを実装するためにレイアウトコンテナコンポーネントが使用されています。レイアウトコンテナは、レスポンシブグリッド内にコンポーネントを配置できる段落システムを提供します。このグリッドでは、デバイスやウィンドウのサイズと形式に応じてレイアウトを並べ替えることができます。このコンポーネントを、ページエディターの&#x200B;**レイアウト**&#x200B;モードと組み合わせて使用すると、デバイスに依存するレスポンシブレイアウトを作成および編集できます。

## 試してみる {#trying-it-out}

1. 言語メインブランチの「エクスペリエンス」セクションで、Arctic Surfing ページを編集します。

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html

1. **プレビュー**&#x200B;に切り替えて、web サイトの訪問者に対して表示されるページを確認します。記事「*Aloha spirits in Norther Norway*」のコンテンツまでスクロールダウンします。

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. ブラウザーウィンドウのサイズを変更し、そのサイズ変更に対してレイアウトが動的に調整されることを確認します。

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. レイアウトモードに切り替えます。エミュレーターツールバーが自動的に表示されます。このツールバーを使用して、ターゲットデバイスごとにレイアウトを計画できます。

   コンポーネントを選択すると、編集メニューにフローティングおよび非表示オプションと共に、コンポーネントのサイズ変更ハンドルが表示されます。

   ![chlimage_1-180](assets/chlimage_1-180.png)

1. コンポーネントのサイズ変更ハンドルを選択してドラッグすると、サイズ変更に役立つレイアウトグリッドが自動的に表示されます。

   ![chlimage_1-181](assets/chlimage_1-181.png)

## その他の情報 {#further-information}

詳しくは、オーサリングドキュメントの[レスポンシブレイアウト](/help/sites-authoring/responsive-layout.md)または管理者向けドキュメントの[レイアウトコンテナとレイアウトモードの設定](/help/sites-administering/configuring-responsive-layout.md)を参照してください。
