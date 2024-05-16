---
title: We.Retail のグローバル化されたサイト構造の使用
description: We.Retail を使用して、Adobe Experience Manager でグローバル化されたサイト構造を試す方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: e1de20b0-6d7a-4bda-b62f-c2808fd0af28
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: ht
source-wordcount: '428'
ht-degree: 100%

---

# We.Retail のグローバル化されたサイト構造の使用{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail は、グローバル化されたサイト構造を使用して構築され、国固有の web サイトにライブコピーできる言語メインを提供します。すべての設定がすぐに使用でき、この構造と組み込みの翻訳機能を試すことができます。

## 試してみる {#trying-it-out}

1. **グローバルナビゲーション／Sites** から Sites コンソールを開きます。
1. 列表示に切り替えて（まだアクティブでない場合）、We.Retail を選択します。サンプルの国の構造には、言語メインに加えてスイス、アメリカ、フランスなどが含まれています。

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. スイスを選択し、その国の言語の言語ルートを確認します。これらのルートの下にはまだコンテンツがありません。

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. リスト表示に切り替えて、各国の言語コピーがすべてライブコピーであることを確認します。

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. 列表示に戻り、言語メインをクリックして、コンテンツを含む言語メインルートを表示します。コンテンツがあるのは英語だけです。

   We.Retail には翻訳されたコンテンツがありません。ただし、構造と設定は用意されているので、翻訳サービスを試すことができます。

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. 英語の言語マスターを選択した状態で、サイトコンソールで&#x200B;**参照**&#x200B;レールを開き、**言語コピー**&#x200B;を選択します。

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. **言語コピー**&#x200B;ラベルの横のチェックボックスを選択し、すべての言語コピーを選択します。レールの「**言語コピーを更新**」セクションで、「**新しい翻訳プロジェクトを作成**」オプションを選択します。プロジェクトの名前を入力し、「**更新**」をクリックします。

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 各言語の翻訳用にプロジェクトが作成されます。作成されたプロジェクトは、**ナビゲーション／プロジェクト**&#x200B;に表示されます。

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. 「ドイツ語」をクリックして、その翻訳プロジェクトの詳細を表示します。ステータスは&#x200B;**ドラフト**&#x200B;になっています。Microsoft® の翻訳サービスを使用して翻訳を開始するには、**翻訳ジョブ**&#x200B;という見出しの横にある山形括弧をクリックし、「**開始**」を選択します。

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. 翻訳プロジェクトが開始されます。「翻訳ジョブ」というラベルの付いたカードの下部にある省略記号をクリックして、詳細を表示します。状態に「**レビューへの準備完了**」と表示されているページは、既に翻訳サービスによって翻訳済みです。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. リスト内のページの 1 つを選択し、ツールバーの「**サイトでプレビュー**」を選択すると、翻訳されたページがページエディターで開かれます。

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>この手順では、組み込みの Microsoft® の機械翻訳との統合を示しました。[AEM 翻訳統合フレームワーク](/help/sites-administering/translation.md)を使用すると、多くの標準的な翻訳サービスと統合して AEM の翻訳を調整できます。

## 詳細情報 {#further-information}

技術的な詳細について詳しくは、オーサリングドキュメントの[多言語サイトのコンテンツの翻訳](/help/sites-administering/translation.md)を参照してください。
