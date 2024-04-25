---
title: コミュニティコンポーネントガイド
description: ソーシャルコンポーネントフレームワーク（SCF）の使用を開始するためのインタラクティブな開発ツール
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 12c0eae5-fd76-4480-a012-25d3312f3570
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 1%

---

# コミュニティコンポーネントガイド  {#community-components-guide}

コミュニティコンポーネントガイドは、のインタラクティブな開発ツールです [ソーシャルコンポーネントフレームワーク（SCF）](scf.md). 使用可能なAdobe Experience Manager（AEM） Communities コンポーネントまたは複数のコンポーネントで構築されたより複雑な機能のリストが表示されます。

このガイドでは、各コンポーネントの基本情報に加えて、SCF コンポーネントや機能の動作の仕組み、およびその設定やカスタマイズの方法を実験できます。

各コンポーネントに関連する開発の基本事項については、を参照してください [機能とコンポーネントの基本事項](essentials.md).

## はじめに {#getting-started}

このガイドは、オーサーインスタンス（localhost:4502）とパブリッシュインスタンス（localhost:4503）の開発インストールでの使用を目的としています。

コミュニティコンポーネントサイトにアクセスするには、を参照します。

* [https://&lt;server>:&lt;port>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

Communities コンポーネントとのインタラクションは、以下によって異なります。

* サーバー（オーサーまたはパブリッシュ）。
* サイト訪問者がログインしているかどうか。
* ログインしている場合、メンバーに割り当てられた権限。
* デフォルトの SRP [JSRP](jsrp.md)、は使用中です。

オーサー環境で編集モードに入るには、次のいずれかを挿入します `editor.html` または `cf#` サーバー名の後の最初のパスセグメントとして：

* 標準 UI:

  [https://&lt;server>:&lt;port>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* クラシック UI：

  [https://&lt;server>:&lt;port>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>オーサーの編集モードでは、ページ上のリンクはアクティブになっていません。
>
>コンポーネントページに移動するには、まずプレビューモードを選択してリンクをアクティベートします。
>
>ブラウザーにコンポーネントページが表示された状態で、編集モードに戻ってコンポーネントの編集ダイアログを開きます。
>
>オーサリングに関する一般的な情報については、 [ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md).
>
>AEMに詳しくない場合は、次のドキュメントを参照してください [基本操作](../../help/sites-authoring/basic-handling.md).

### ホームページ {#home-page}

このガイドでは、ページの左側に、プレビューおよびプロトタイプ作成に使用できる SCF コンポーネントの一覧を示します。

編集モードのオーサーインスタンスに表示されたコンポーネントガイド：

![community-component1](assets/community-component1.png)

## コンポーネントページ {#component-pages}

ページの左側に沿ったリストからコンポーネントを選択します。

![community-component-pages](assets/community-component2.png)

ガイドの本文には、次の内容が表示されます。

1. タイトル：選択したコンポーネントの名前
1. [クライアントサイドライブラリ](#client-side-libraries):1 つ以上の必須カテゴリのリスト
1. [含める](scf.md#add-or-include-a-communities-component)：コンポーネントが動的に含まれる場合は、オーサー編集モードで状態を切り替えることができます。

   * 追加した場合は、「このコンポーネントは par ノードを介して組み込まれています」というテキストが表示されます。
   * 含める場合、表示されるテキストは「このコンポーネントは動的に含まれます」です。
   * 含めない場合、テキストは表示されません

1. コンポーネントまたはフィーチャのサンプル：コンポーネントまたはフィーチャのアクティブなインスタンス。 コンポーネントの場合は、「」タブセクションで提供されるテンプレート、CSS、データに加えられた変更によって変更される可能性があります。

>[!NOTE]
>
>左側から選択すると、ブラウザーウィンドウが狭すぎる場合、コンポーネントはコンポーネントの一覧の横ではなく下に表示されます。

### 作成者インタラクション {#author-interactions}

オーサーインスタンスでガイドを使用する際に、ダイアログを開いてコンポーネントを設定することができます。 開発者向けの情報については、を参照してください。 [コンポーネントと機能の基本事項](essentials.md) ダイアログ設定については以下で説明しますが、ドキュメントのの節 [Communities コンポーネント](author-communities.md) 作成者向けの節です。

コミュニティコンポーネントガイドでは、一部のコンポーネントダイアログ設定が [含める](scf.md#add-or-include-a-communities-component) 状態を切り替えます。 既存のリソースと、動的に含まれるリソースのどちらを使用するかを切り替えるには、編集モードでコンポーネントと含まれるテキストの両方を選択し、ダブルクリックして編集ダイアログを開きます。

![community-component3](assets/community-component3.png)

の下 **テンプレート** タブ：

![community-component4](assets/community-component4.png)

* **sling:include を使用して子コンポーネントを含める**

  オプションをオフにすると、コンポーネントガイドはリポジトリ（par ノードの子である jcr ノード）の既存のリソースを使用します。

   * 表示されるテキスト：「このコンポーネントは par ノードを介して組み込まれています。」

  オンにした場合、コンポーネントガイドは sling を使用して子ノードの resourceType （既存のリソースではない）のコンポーネントを動的に含めます。

   * 表示されるテキストは「このコンポーネントは動的に含まれます」です。

  デフォルトではオフになっています。

### インタラクションを公開 {#publish-interactions}

パブリッシュインスタンスでガイドを使用する場合、サイト訪問者（ログインしていない）として、また、ログイン時に様々な権限を持つメンバーとして、コンポーネントや機能を体験することができます。

>[!NOTE]
>
>SRP がデフォルトのままの場合は、注意が必要です。 [JSRP](jsrp.md)を選択した場合、パブリッシュインスタンスに入力された UGC は、公開時にのみ表示され、次のように表示されます *ではない* ～から見える [中和](moderate-ugc.md) オーサーインスタンスのコンソール

## クライアントサイドライブラリ {#client-side-libraries}

各コンポーネントに一覧表示されるクライアントサイドライブラリ（clientlib）は次のとおりです *必須* コンポーネントがページに配置されたときに参照されます。 clientlibs は、ブラウザーでのコンポーネントのレンダリングに使用する JavaScript と CSS のダウンロードを管理および最適化する手段を提供します。

詳しくは、次を参照してください [コミュニティコンポーネントの clientlib](clientlibs.md).

## 実行 {#impersonation}

オーサーインスタンス（多くの場合、管理者または開発者としてログインする）で、別のユーザーとしてログインしたコンポーネントを使用するには、の左側にあるテキストボックスを使用します。 **[!UICONTROL なりすます]** ボタンをクリックして、ユーザー名を入力するか、プルダウン リストから選択し、ボタンをクリックします。 「元に戻す」をクリックしてログアウトし、別のユーザーとして実行を終了します。

パブリッシュインスタンスは別のユーザーとして実行する必要はありません。 ログイン/ログアウトリンクを使用して、次のような様々なユーザーとして実行します [デモユーザー](tutorials.md#demo-users).

## カスタマイズ {#customization}

有効にすると、コンポーネントのテンプレート、CSS、データを一時的に変更することで、各 SCF コンポーネントをカスタマイズのプロトタイプ作成に使用できます。

### カスタマイズの有効化 {#enabling-customization}

>[!NOTE]
>
>**このツールは読み取り専用です**. テンプレート、CSS、データに対して行われた編集は、リポジトリには保存されません。

カスタマイズを素早く試すには、 `scg:showIde`プロパティをコンポーネントページのコンテンツ JCR ノードに追加し、true に設定する必要があります。

例えば、コメントコンポーネントを使用して、管理者権限でログインしたオーサーインスタンスまたはパブリッシュインスタンスで実行します。

1. を参照 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)

   例： [http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. コンポーネントの `jcr:content` ノード

   例えば、`/content/community-components/en/comments/jcr:content` のように指定します。

1. プロパティを追加

   * **名前** `scg:showIde`
   * **型** `String`
   * **値** `true`

1. を選択 **[!UICONTROL すべて保存]**
1. ガイドのコメントページをリロードします。

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. テンプレート、CSS、データの 3 つのタブが表示されます。

![community-component5](assets/community-component5.png)

![community-component6](assets/community-component6.png)

### 「テンプレート」タブ {#templates-tab}

「テンプレート」タブを選択して、コンポーネントに関連付けられているテンプレートを表示します。

テンプレートエディターを使用すると、リポジトリ内のコンポーネントに影響を与えることなく、ローカルの編集内容をコンパイルして、ページ上部のサンプルコンポーネントインスタンスに適用できます。

ローカル編集でコンパイルを実行すると、樋に点が配置され、テキストが赤くマークされるため、エラーが強調表示されます。

### 「CSS」タブ {#css-tab}

「CSS」タブを選択して、コンポーネントに関連付けられた CSS を表示します。

コンポーネントが複数のコンポーネントの複合である場合、一部の CSS が他のコンポーネントの 1 つの下に表示される場合があります。

CSS エディターを使用すると、CSS を変更してページ上部のサンプルコンポーネントインスタンスに適用できます。

ガター内のルールの横にあるをクリックすると、そのルールを使用する DOM の一部をハイライト表示するルールを選択できます。

### 「データ」タブ {#data-tab}

「データ」タブを選択して、.social.json エンドポイントデータを表示します。 このデータは編集可能で、サンプルコンポーネントインスタンスに適用されます。

構文エラーは、樋でマークされ、エディタでハイライト表示される場合があります。
