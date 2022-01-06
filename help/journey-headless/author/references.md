---
title: コンテンツフラグメントでの参照の使用について説明します
description: コンテンツフラグメント、その他のフラグメント、およびその他のアセット（メディア）への参照の使用について説明します。 ヘッドレス CMS オーサリング用のネストされたフラグメントの必要性と仕組みを紹介します。
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 10%

---

# コンテンツフラグメントでの参照の使用について説明します {#author-headless-references}

## 今までの話 {#story-so-far}

の最初 [AEMヘッドレスコンテンツ作成者ジャーニー](overview.md) の [はじめに](introduction.md) ヘッドレス向けのオーサリングに関連する基本概念と用語について説明しました。

ヘッドレス CMS のオーサリングの基本、AEMaaCS でのオーサリングの概要、特にコンテンツフラグメントのオーサリングについて学びました。

この記事はこれらを基に構築され、AEMヘッドレスプロジェクトで独自のコンテンツを作成するための参照の使用方法を理解できます。

## 目的 {#objective}

* **オーディエンス**：経験者
* **目的**:ヘッドレス CMS オーサリングの参照を紹介します。 使用可能な参照の種類と目的は何ですか。

   * コンテンツ参照
   * アセット/メディア参照
   * フラグメント参照
   * テキストブロック内からのアドホック参照

## 参照とは {#what-are-references}

参照は、他のコンテンツ、アセット（画像など）、その他のフラグメントなど、リソースを接続するための単なるメカニズムです。 非常に似ていますが、いくつかの違いがあります。

一部の参照には専用のデータ型（コンテンツ参照やフラグメント参照など）があり、それ以外の参照は、テキストブロック内の参照として追加されるだけです（アセット参照やアドホック参照など）。

![コンテンツフラグメント — 参照](/help/journey-headless/author/assets/headless-journey-author-references-01.png)

## コンテンツ参照 {#content-references}

コンテンツ参照はそのような役割を果たし、他のコンテンツを参照できます。 これにより、コンテンツ項目を選択できるブラウザーが開きます。

## アセット/メディア参照 {#assets-media-references}

アセット（画像やメディアなど）は、 **アセットを挿入** オプション。 これにより、アセットを選択できるブラウザーが開きます。

![コンテンツフラグメント — アセットを挿入](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## フラグメント参照 {#fragment-references}

再びフラグメント参照でも同じ操作が行われます。この場合、別のフラグメントを参照できます。 これが重要な理由は、もう少し説明を必要とする。

例えば、次のコンテンツフラグメントモデルを定義するとします。

* City
* 会社
* Person
* awards（受賞歴）

簡単に見えますが、もちろん会社には CEO と従業員の両方がいます….これらはすべて人物で、それぞれが人物として定義されます。

また、1 人の人に賞（または 2 つ）を与えることもできます。

* 会社 — 会社
   * CEO — 担当者
   * 従業員 — 担当者
      * 個人賞 — 賞

それはスターター向けです 複雑さに応じて、賞は会社固有のものもあれば、会社が特定の都市に本社を置くこともあります。

これらの相互関係は、作成者とヘッドレスアプリケーションの両方が理解しているように、フラグメント参照を使用して実現できます。

作成者は、これらの関係の定義（コンテンツフラグメントモデルの作成時にコンテンツアーキテクトがおこなう）は担当しませんが、参照を認識し編集する方法を理解しておく必要があります。

### ネストされたフラグメントの作成方法 {#author-nested-fragment}

フラグメント参照のオーサリングは非常に簡単です ( 通常、フィールドは **フラグメント参照**) をクリックします。 参照を直接入力するか、（可能性が高い）フォルダーアイコンを選択してブラウザーを開き、必要なフラグメントに移動して選択できます。

![コンテンツフラグメント — 参照](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

コンテンツフラグメントモデルの定義は、次のように制御します。

* 複数の参照を追加できるかどうかを選択します。
* 選択できるコンテンツフラグメントのモデルタイプ。コンテンツフラグメントモデルは、参照に使用できるフラグメントモデルを定義するので、AEMは、それらのモデルに基づくフラグメントのみを表示します。

### ネストされたフラグメントのナビゲート方法 {#navigate-nested-fragment}

の使用 **構造ツリー** コンテンツフラグメントエディターの「 」タブでは、フラグメントで参照されているフラグメント間を移動した後、それらに含まれている参照間を移動できます。 参照を選択すると、そのフラグメントが編集用に開きます。

>[!NOTE]
>
>メインパネルのパンくずリストを使用して、開始点に戻ることができます。

![コンテンツフラグメント構造ツリー](/help/assets/content-fragments/assets/cfm-structuretree-02.png)

## アドホック参照 {#adhoc-references}

アドホック参照は、テキストブロック内に単純なリンクとして追加できます。

![コンテンツフラグメント — アドホック参照](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## 次の手順 {#whats-next}

これで、コンテンツフラグメントの参照と構造について学習したので、次の手順は次のとおりです。 [メタデータとタグ付けについて説明します](metadata-tagging.md). コンテンツフラグメントのメタデータとタグを定義する方法を紹介し、説明します。

## その他のリソース {#additional-resources}

* [コンテンツフラグメントの操作](/help/assets/content-fragments/content-fragments.md)

   * [コンテンツフラグメントの管理](/help/assets/content-fragments/content-fragments-managing.md)

      * [アセットフォルダーへの設定の適用](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [コンテンツフラグメントの作成](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [バリエーション — コンテンツフラグメントのオーサリング](/help/assets/content-fragments/content-fragments-variations.md)

   * [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)

      * [コンテンツフラグメントモデル — データタイプ](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [コンテンツフラグメントモデル — プロパティ](/help/assets/content-fragments/content-fragments-models.md#properties)


* 「はじめる前に」ガイド 
   * [アセットフォルダーのヘッドレス作成のクイック開始ガイド](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [AEMヘッドレスコンテンツアーキテクトジャーニー](/help/journey-headless/architect/overview.md)

* [AEMヘッドレス翻訳ジャーニー](/help/journey-headless/translation/overview.md)
