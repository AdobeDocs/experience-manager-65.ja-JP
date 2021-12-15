---
title: オーサリングの基本を学ぶ
description: コンテンツフラグメントを使用したヘッドレス CMS のコンテンツオーサリングの概念と仕組みについて説明します。
index: true
hide: false
hidefromtoc: false
source-git-commit: 9661061a98c31fbb74bd0716dbedc7abef298f44
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 6%

---

# AEMを使用したヘッドレス向けのオーサリングの基本 {#author-headless-basics}

## 今までの話 {#story-so-far}

の最初 [AEMヘッドレスコンテンツ作成者ジャーニー](overview.md) の [はじめに](introduction.md) ヘッドレス向けのオーサリングに関連する基本概念と用語について説明しました。

この記事はこれらを基に構築され、AEMヘッドレスプロジェクト用に独自のコンテンツを作成する方法を理解できます。

## 目的 {#objective}

* **オーディエンス**：初心者
* **目的**:ヘッドレス CMS オーサリングの基本を紹介します。
   * AEMaaCS を使用したオーサリングの概要
   * コンテンツフラグメントの概要

## 基本操作 {#basic-handling}

コンテンツフラグメントの操作方法を理解する前に、AEMの使用方法を簡単に紹介します。.しかし、実際には、ログインしてシステムを使用しようとした経験に代わるものは何もありません。

### オーサーインスタンスとパブリッシュインスタンス {#author-preview-publish}

AEM インストールは、通常、少なくとも次の 2 つの環境で構成されます。

* 作成者
* 公開

ログインし、オーサー環境を使用してコンテンツを生成します。 準備が整ったら、コンテンツを公開して、一般に利用できるようにします。 ヘッドレスの場合は、他のアプリケーションに対して、Web ページの場合は、Web 上の読者に対して行われます。

詳しくは、オーサリングの概念を参照してください。

### ログイン {#signing-in}

As with most systems you will need to login. 作成者として、次の情報が提供されます。

* User (account) name
* パスワード
* ログイン画面にアクセスするためのリンク

お使いのアカウントには、必要な権限が設定されています。 問題がある場合は、社内プロジェクトサポートチームにお問い合わせいただくことをお勧めします。

### ナビゲーション {#navigation}

小さなオンラインチュートリアルに初めてログインすると、ユーザーインターフェイスの主な機能の一部が強調表示されます。

その後、ナビゲーションパネルを使用して、AEMの主要な領域にアクセスできます。 コンテンツフラグメントの場合、 **Assets コンソール**.

The Navigation Panel can be opened by selecting Adobe icon at the top left, followed by the small compass icon:

![ナビゲーションパネル](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)

>[!NOTE]
>コンテンツフラグメントはAEMの機能ですが、 **サイト**&#x200B;の場合、 **Assets** コンソール。 これは技術的な詳細で、ユーザーに影響を与えることはありませんが、知っておくと役に立つ場合があります。

コンソール内で、コンテンツフラグメントに移動するフォルダーを選択するか、（ヘッダー内の）パンくずリストを選択してツリーの上に戻ることができます。

![パンくずリスト](/help/journey-headless/author/assets/headless-journey-author-navigation-02.png)

### アクション、選択、表示 {#actions-selecting-viewing}

この **Assets** コンソールは専用です **アクションツールバー**、および **クイックアクション** リソース（フォルダーやコンテンツフラグメントなど）を選択した後で使用できます。

クイックアクションは、1 つのリソースに対して使用できます。詳しくは、 **バーゼル** 以下の例では、

![クイックアクション](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

アクションツールバーを使用して、現在のシナリオに適用できる様々なアクションにアクセスできます。 使用可能なアクションは変更できます。例えば、場所や、複数のリソースを選択したかどうかに応じて、次のように表示されます。

![アクションツールバー](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

表示セレクターを使用して、リソースを表示する形式を選択できます。

![表示セレクター](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

パネルセレクターを使用して、項目に関する追加情報を表示できます。 追加のアクションにアクセスすることもできます。

![左レール](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)

## コンテンツフラグメントのオーサリング {#authoring-content-fragments}

これはAEMユーザーインターフェイス (UI) の簡単な紹介でしたが、ぜひ試してみて欲しいと思います。 次に、本当の興味を引く — ヘッドレス用コンテンツフラグメントを紹介します。

最初から最後まで調べる必要がありますが、お使いのインスタンスには既にフォルダーやフラグメントが作成されていて、それらが別の場所に存在している可能性があります。 原理は同じ。

### 整理とナビゲーション {#organizing-and-navigating}

コンテンツフラグメントがほとんどない場合を除き、整理して、再び見つけられるようにします。

#### フォルダーの作成 {#creating-folder}

これをおこなうには、 **ファイル** Assets コンソールの「 」セクションに移動します。 を選択します。 **作成** オプション（右上）、その後に **フォルダー**:

![「フォルダーを作成」オプション](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

詳細を入力し、次で確認できるダイアログが開きます。 **作成**:

![フォルダーを作成ダイアログ](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### パスとタグを使用したフォルダーで使用可能なコンテンツフラグメントモデルの制限 {#tags-paths-for-models-in-folder}

この節は、少し進んでいます。 単に始めて試してみるだけでは必要ありませんが、それは *非常に* フラグメントが多数ある場合に便利です。 まだ使っていなくても、知っておいて良いのです。

コンテンツアーキテクトが、現在のプロジェクトに必要なすべてのコンテンツフラグメントモデルを作成し、他のプロジェクトも作成します。 自分や他の作成者が作業を簡単におこなえるように、特定のフォルダーで使用できるモデルのリストを制限できます。

フォルダーを作成したら、そのフォルダーを開くことができます **プロパティ**. ここには、フォルダーに関する情報と設定の詳細を含む様々なタブがあります。 特に、コンテンツフラグメントの場合は、 **ポリシー** タブを使用して、このフォルダーの特定のパスやタグを定義します。 これにより、フォルダーで使用できるコンテンツフラグメントモデルが制限されます。つまり、コンテンツフラグメントモデルをこのフォルダーでフラグメントを生成する前に、これらの要件を満たす必要があります。

![フォルダーのプロパティを作成 — ポリシー](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>詳しくは、コンテンツフラグメントモデル — アセットフォルダーでのコンテンツフラグメントモデルの許可を参照してください。

次に、これらのフォルダー内を移動して、コンテンツフラグメントを作成し、編集します。

#### 念のため — フォルダーCloud Services設定 {#cloud-services-folder}

念のため…

フォルダーを作成できる初期フォルダーが表示される場合があります。 これは、一部の設定の詳細を（通常は開発者またはシステム管理者が）ルートフォルダーに適用する必要があるためです。 これはおそらく興味を引かないでしょうが、必要に応じて **設定** 内 **Cloud Services** フォルダーの **プロパティ**:

![フォルダーのプロパティを作成 — 設定](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>詳しくは、「設定をアセットフォルダーに適用する」を参照してください。

### コンテンツフラグメントの作成 {#creating-fragment}

コンテンツフラグメントの作成は非常に似ています。この場合、 **コンテンツフラグメント** 代わりにオプションを使用します。

![「コンテンツフラグメントを作成」オプション](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

今度は、ウィザードが開きます。 最初の手順では、フラグメントの基になるコンテンツフラグメントモデルを選択します。

![コンテンツフラグメントを作成 — モデルを選択](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

を続行した後 **次へ** 詳細を指定できます (**基本** および **詳細**) をフラグメントに追加します。

![Create Content Fragment - provide Name](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

次で確認： **作成** そうすれば **開く** フラグメントをエディターに表示します。

### フラグメントの編集 {#editing-fragment}

フラグメントは、作成後すぐに開くことも、Assets コンソールから選択することもできます。

エディターが最初に開くと、次のように表示されます。

* 左側のアイコンのリスト — 様々な機能領域にアクセスできます。 The editor opens in the **Variations** tab, this is where most of the editing happens. You might also be interested in the **Annotations** and **Metadata** tabs.

* フラグメントに関する情報と様々なアクションへのアクセスを含むヘッダー。

* 主な編集領域 — フラグメントの作成に使用したモデルによって異なります。

例：

* 複数の情報のみを必要とするフラグメント（一部は特定のタイプを持つもの）。 ヘッドレスコンテンツの場合、参照は重要です。これらについては、後でジャーニーで学習します。

   ![コンテンツフラグメントエディター — マイフラグメント](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* テキストの長いセクションを書き込むことができるフラグメント。 ここでは、テキストを管理および書式設定するための追加のオプションがあります。 個々のテキストフィールドを全画面表示エディターで開くこともできます（右側の小さい画面のようなアイコンを使用）。

   ![コンテンツフラグメントエディター — Alaska Spirits](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>作成者が一部のフィールドを正常に完了する方法の詳細を知るには、プロジェクト固有のドキュメントが必要になる場合があります。
>
>一般的な詳細については、コンテンツフラグメントモデル — データタイプとプロパティを参照してください。

Confirm your updates with either **Save** or **Save &amp; close**.

>[!NOTE]
>
>詳しくは、バリエーション — コンテンツフラグメントのオーサリングを参照してください。

#### （おそらく）心配する必要がないもの {#what-you-probably-do-not-need-to-worry-about}

これは少し奇妙な節に思えるかもしれませんが、コンテンツフラグメントエディターを開いて調査を開始すると、コンテンツ作成者としてヘッドレスジャーニーに適用されない（おそらく）様々なオプションが表示されます。 これは、ヘッドレスコンテキストで無視できる内容に関する簡単な説明です。

* **コンテンツフラグメントモデル**

   You will see the name of the Content Fragment Model at the top of the editor - directly under the fragment name. これは、モデルエディターに移動するリンクでもあります。
Content Fragment Models are actually vital to your Content Fragments as they define the structure that you use. However, creating and editing them is (usually) the responsibility of another persona, the Content Architect.

   >[!NOTE]
   >
   >詳しくは、 AEMヘッドレスコンテンツアーキテクトジャーニーを参照してください。

* **関連コンテンツ**

   これはエディターのタブなので明らかです

   コンテンツフラグメントは、AEMで多くのバージョンで使用できます。 もともとは、ページのオーサリング時に「従来の」使用で利用できるようになっていました。.そして、この文脈では、まだ使用されています。 これには、フラグメントに埋め込まれていないが、ページのオーサリング時に作成者が使用できる必要があるアセット（画像など）の関連付けが含まれる場合があります。

* **プレビュー**

   これはエディターの別のタブで、主に開発者向けの技術ビューを提供します。

* **ページ参照を更新**

   このアクションは、 **...** （省略記号）ドロップダウン ヘッドレス作成者はページのオーサリングに関連するので、興味深くはありません。

### 公開 {#publishing}

<!-- needs more details -->

フラグメントを完了したら、次の操作を実行できます **公開** ヘッドレスアプリケーションで使用できるようにします。

公開アクションは、エディター ( または **Assets** コンソール ):

![コンテンツフラグメントエディター — マイフラグメント](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

## 次の手順 {#whats-next}

これで、基本を学んだので、次の手順は次のとおりです。 [参照について](references.md). これにより、使用可能な様々な参照の紹介と、ヘッドレスオーサリングの主要な部分であるフラグメント参照を使用した構造のレベルの作成方法について説明します。

## その他のリソース {#additional-resources}

* [オーサリングに関する概念](/help/sites-authoring/author.md)

* [基本操作](/help/sites-authoring/basic-handling.md)  — このページは主に次の項目に基づいています **サイト** コンソールですが、多くの/ほとんどの機能もオーサリングに関連しています **コンテンツフラグメント** の下に **Assets** コンソール。

   * [ナビゲーションパネル](/help/sites-authoring/basic-handling.md#navigation-panel)

   * [ヘッダー](/help/sites-authoring/basic-handling.md#the-header)

   * [アクションツールバー](/help/sites-authoring/basic-handling.md#actions-toolbar)

   * [クイックアクション](/help/sites-authoring/basic-handling.md#quick-actions)

   * [リソースの表示と選択](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

   * [パネルセレクター](/help/sites-authoring/basic-handling.md#rail-selector)

* [コンテンツフラグメントの操作](/help/assets/content-fragments/content-fragments.md)

   * [コンテンツフラグメントの管理](/help/assets/content-fragments/content-fragments-managing.md)

      * [アセットフォルダーへの設定の適用](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [コンテンツフラグメントの作成](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [バリエーション — コンテンツフラグメントのオーサリング](/help/assets/content-fragments/content-fragments-variations.md)

   * [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)

      * [コンテンツフラグメントモデル — データタイプ](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [コンテンツフラグメントモデル — プロパティ](/help/assets/content-fragments/content-fragments-models.md#properties)

      * [コンテンツフラグメントモデル — アセットフォルダーでのコンテンツフラグメントモデルの許可](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)


* 「はじめる前に」ガイド 
   * [アセットフォルダーのヘッドレス作成のクイック開始ガイド](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [AEM Headless Content Architect Journey](/help/journey-headless/architect/overview.md)

* [AEMヘッドレス翻訳ジャーニー](/help/journey-headless/translation/overview.md)
