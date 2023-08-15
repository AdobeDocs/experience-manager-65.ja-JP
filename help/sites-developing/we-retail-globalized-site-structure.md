---
title: We.Retail のグローバル化されたサイト構造の使用
description: We.Retail のグローバル化されたサイト構造の使用
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: e1de20b0-6d7a-4bda-b62f-c2808fd0af28
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 27%

---

# We.Retail のグローバル化されたサイト構造の使用{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail は、グローバル化されたサイト構造を使用して構築され、国固有の Web サイトにライブコピーできる言語マスターを提供します。 すべての設定がすぐに使用でき、この構造と組み込みの翻訳機能を試すことができます。

## 試す {#trying-it-out}

1. 次の場所からサイトコンソールを開きます。 **グローバルナビゲーション/サイト**.
1. 列表示に切り替えて（まだアクティブでない場合）、We.Retail を選択します。 例の国の構造は、スイス、米国、フランスなど、言語マスターの横に表示されます。

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. スイスを選択し、その国の言語の言語ルートを確認します。 これらのルートの下にはまだコンテンツがありません。

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. リスト表示に切り替えて、各国の言語コピーがすべてライブコピーであることを確認します。

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. 列表示に戻り、言語マスターをクリックして、コンテンツを含む言語マスタールートを表示します。 内容を持つのは英語だけです。

   We.Retail には翻訳済みのコンテンツは付属していませんが、翻訳サービスをデモするための構造と設定が用意されています。

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. 英語の言語マスターを選択した状態で、サイトコンソールで&#x200B;**参照**&#x200B;レールを開き、**言語コピー**&#x200B;を選択します。

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. の横にあるチェックボックスをオンにします。 **言語コピー** 「ラベル」は、すべての言語コピーを選択する場合に使用します。 Adobe Analytics の **言語コピーを更新** パネルの「 」セクションで、「 」オプションを選択します。 **新しい翻訳プロジェクトを作成**. プロジェクトの名前を入力し、 **更新**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 言語の翻訳ごとにプロジェクトが作成されます。 それらをの下に表示します。 **ナビゲーション/プロジェクト**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. 「ドイツ語」をクリックして、翻訳プロジェクトの詳細を表示します。 ステータスが **ドラフト**. Microsoft®の翻訳サービスで翻訳を開始するには、 **翻訳ジョブ** 見出しと選択 **開始**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. 翻訳プロジェクトが開始します。 詳細を表示するには、翻訳ジョブというラベルが付いたカードの下部にある省略記号をクリックします。 状態を含むページ **レビューの準備完了** は、翻訳サービスによって既に翻訳されています。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. リスト内のページの 1 つを選択し、ツールバーの「**サイトでプレビュー**」を選択すると、翻訳されたページがページエディターで開かれます。

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>この手順では、Microsoft®の機械翻訳との組み込みの統合について説明しました。 の使用 [AEM Translation Integration Framework](/help/sites-administering/translation.md)を使用すると、多くの標準翻訳サービスと統合して、AEMの翻訳を調整できます。

## その他の情報 {#further-information}

技術的な詳細については、オーサリングドキュメントの [多言語サイトのコンテンツの翻訳](/help/sites-administering/translation.md)を参照してください。
