---
title: SPAの概要とチュートリアル
seo-title: SPAの概要とチュートリアル
description: この記事では、SPAの概念を紹介し、基本的なSPAアプリケーションを使用したオーサリングの手順を説明し、基礎となるAEM SPAエディターとの関連を示します。
seo-description: この記事では、SPAの概念を紹介し、基本的なSPAアプリケーションを使用したオーサリングの手順を説明し、基礎となるAEM SPAエディターとの関連を示します。
uuid: 4b0a9e53-3892-4d60-8bd3-7ff740d2f137
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 0478afcb-b029-4ce6-b3e6-cee4bb5408ce
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPAの概要とチュートリアル{#spa-introduction-and-walkthrough}

単一ページアプリケーション（SPA）により、Web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者は SPA フレームワークを使用してサイトを構築したいと考え、作成者はそうして構築されたサイトのコンテンツを AEM 内でシームレスに編集したいと考えています。

SPA エディターには、AEM 内で SPA をサポートするための包括的なソリューションが用意されています。この記事では、オーサリング用の基本SPAアプリケーションの使用方法と、基になるAEM SPAエディターとの関係を説明します。

>[!NOTE]
>
>SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトには、SPA Editorが推奨されるソリューションです。

## 概要 {#introduction}

### 記事の目的 {#article-objective}

この記事では、読者をSPAエディターのチュートリアルに進める前に、単純なSPAアプリケーションを使用して基本的なコンテンツ編集のデモを行うSPAの基本概念を紹介します。 次に、ページの構築と、SPAアプリケーションとAEM SPA editorとの関連付け方法、およびAEM SPA editorとの対話方法に移動します。

この概要とチュートリアルの目的は、SPAが関連する理由、一般的な動作、AEM SPA editorでのSPAの処理方法、および標準のAEMアプリケーションとの違いを、AEM開発者に説明することです。

チュートリアルは、標準のAEM機能とサンプルのWe.Retail Journalアプリに基づいています。 以下の要件を満たす必要があります。

* [AEMバージョン6.4（サービスパック2以降）
   ](/help/release-notes/sp-release-notes.md)
* [GitHubで入手可能なサンプルのWe.Retail Journalアプリケーションをここにインストールします。](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

### SPAとは {#what-is-a-spa}

シングルページアプリケーション(SPA)は、クライアント側でレンダリングされ、主にJavaScript駆動型で、Ajax呼び出しに依存してデータを読み込み、ページを動的に更新する点で、従来のページとは異なります。 ほとんどまたはすべてのコンテンツは、ユーザーによるページの操作に基づいて、必要に応じて非同期で読み込まれた追加のリソースを含む、単一のページ読み込みで1回取得されます。

これにより、ページを更新する必要性が減り、シームレスで迅速なユーザーエクスペリエンスを提供し、ネイティブアプリのエクスペリエンスに似た感じになります。

AEM SPA Editorを使用すると、フロントエンド開発者はAEMサイトに統合できるSPAを作成でき、コンテンツ作成者はSPAコンテンツを他のAEMコンテンツと同様に簡単に編集できます。

### なぜSPAなの？ {#why-a-spa}

SPAは、より速く、流動的で、ネイティブアプリケーションと似た、非常に魅力的なエクスペリエンスとなり、Webページの訪問者だけでなく、SPAの動作の性質上、マーケターや開発者にとっても魅力的です。

![screen_shot_2018-08-20at135550](assets/screen_shot_2018-08-20at135550.png)

**訪問者数**

* 訪問者は、コンテンツとのインタラクション時にネイティブなエクスペリエンスを求めています。
* ページが速くなるほどコンバージョンが発生する可能性が高いという明確なデータが存在します。

**マーケター**

* マーケターは、リッチでネイティブなエクスペリエンスを提供して、訪問者をコンテンツに完全に関与させたいと考えています。
* パーソナライゼーションは、これらのエクスペリエンスをさらに魅力的にします。

**開発者向け**

* 開発者は、コンテンツとプレゼンテーションの間の懸念事項を明確に分ける必要があります。
* クリーンな分離により、システムの拡張性が向上し、独立したフロントエンド開発が可能になります。

### SPAの仕組み {#how-does-a-spa-work}

SPAの主な考え方は、サーバ呼び出しによる遅延を最小限に抑え、SPAがネイティブアプリケーションの応答性に近づくように、サーバへの呼び出しと依存関係を低減することです。

従来の順次Webページでは、即時ページに必要なデータのみが読み込まれます。 つまり、訪問者が別のページに移動すると、追加のリソースに対してサーバーが呼び出されます。 訪問者がページ上の要素とやり取りする際には、追加の呼び出しが必要になる場合があります。 これらの複数の呼び出しは、ページが訪問者のリクエストに追い付く必要があるので、遅延や遅延の感覚を与える可能性があります。

![screen_shot_2018-08-20at140449](assets/screen_shot_2018-08-20at140449.png)

より流動的なエクスペリエンスを実現するために、訪問者がモバイルやネイティブアプリから期待する内容に近いSPAは、初回の読み込み時に訪問者に必要なすべてのデータを読み込みます。 この処理は、最初は少し時間がかかる場合がありますが、サーバーコールを追加する必要はありません。

クライアント側でレンダリングすると、ページ要素の反応が速くなり、訪問者によるページとのインタラクションが直ちに発生します。 ページの速度を最大化するために、必要になる可能性のある追加データはすべて非同期に呼び出されます。

>[!NOTE]
>
>AEMでのSPAの動作方法に関する技術的な詳細については、「AEMでのSPAの使用の手引き」 [の記事を参照してください](/help/sites-developing/spa-getting-started-react.md)。
>
>SPA Editorのデザイン、アーキテクチャ、および技術的なワークフローについて詳しくは、「 [SPA Editor Overview」を参照してください](/help/sites-developing/spa-overview.md)。

## SPAを使用したコンテンツ編集エクスペリエンス {#content-editing-experience-with-spa}

AEM SPA editorを利用するSPAが構築されている場合、コンテンツの作成者は、コンテンツの編集と作成の際に違いがないことに気づきます。 共通のAEM機能を使用でき、作成者のワークフローに対する変更は必要ありません。

>[!NOTE]
>
>チュートリアルは、標準のAEM機能とサンプルのWe.Retail Journalアプリに基づいています。 以下の要件を満たす必要があります。
>
>* [AEMバージョン6.4（サービスパック2）](/help/release-notes/sp-release-notes.md)
>* [GitHubで入手可能なサンプルのWe.Retail Journalアプリケーションをここにインストールします。](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)
>



1. AEMでWe.Retail Journalアプリを編集します。

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at142533](assets/screen_shot_2018-06-07at142533.png)

1. 見出しコンポーネントを選択すると、他のコンポーネントと同様にツールバーが表示されます。 「**編集**」を選択します。

   ![screen_shot_2018-06-07at142937](assets/screen_shot_2018-06-07at142937.png)

1. AEM内で通常どおりにコンテンツを編集し、変更内容は維持されることに注意してください。

   ![screen_shot_2018-06-07at143419](assets/screen_shot_2018-06-07at143419.png)

1. アセットブラウザを使用して、新しい画像を画像コンポーネントにドラッグ&amp;ドロップします。

   ![screen_shot_2018-06-07at143530](assets/screen_shot_2018-06-07at143530.png)

1. この変更は持続する

   ![screen_shot_2018-06-07at143732](assets/screen_shot_2018-06-07at143732.png)

ページ上の追加のコンポーネントのドラッグ&amp;ドロップ、コンポーネントの並べ替え、レイアウトの変更などの追加のオーサリングツールは、SPA以外のアプリケーションと同様にサポートされます。

>[!NOTE]
>
>SPAエディターは、アプリケーションのDOMを変更しません。 SPA自体がDOMを処理します。
>
>この機能を確認するには、この記事の「 [SPA Apps」と「AEM SPA Editor」の次のセクションに進みます](/help/sites-developing/spa-walkthrough.md#spa-apps-and-the-aem-spa-editor)。

## SPAアプリとAEM SPAエディター {#spa-apps-and-the-aem-spa-editor}

エンドユーザーに対してSPAの動作を確認し、SPAページを調べると、AEMのSPA editorでのSAPアプリの動作をより深く理解できます。

### SPAアプリケーションの使用 {#using-an-spa-application}

1. We.Retail Journalアプリケーションを公開サーバーで読み込むか、ページエディターの **Page Information** (ページ情報 **** )メニューから「公開済みとして表示」オプションを使用します。

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-08at102650](assets/screen_shot_2018-06-08at102650.png)

   子ページへのナビゲーション、ウェザーウィジェット、記事など、ページ構造をメモしておきます。

1. メニューを使用して子ページに移動し、更新を行うことなく、ページが直ちに読み込まれることを確認します。

   ![screen_shot_2018-06-08at102815](assets/screen_shot_2018-06-08at102815.png)

1. ブラウザーに組み込まれている開発者ツールを開き、子ページを移動する際にネットワークアクティビティを監視します。

   ![screen_shot_2018-06-08at103922](assets/screen_shot_2018-06-08at103922.png)

   アプリ内でページ間を移動する際のトラフィックはほとんどありません。 ページはリロードされず、新しい画像のみが要求されます。

   SPAは、コンテンツとルーティングをクライアント側で完全に管理します。

子ページをナビゲートする際にページがリロードされない場合、どのようにロードされますか。

次のセクション「 [SPAアプリケーションの読み込み](/help/sites-developing/spa-walkthrough.md#loading-an-spa-application)」では、SPAの読み込みの仕組みと、コンテンツの同期的および非同期的な読み込み方法を詳しく説明します。

### SPAアプリケーションの読み込み {#loading-an-spa-application}

1. まだ読み込まれていない場合は、We.Retail Journalアプリケーションを公開サーバーに読み込むか、ページエディターの **Page Information** (ページ情報 **** )メニューから「発行済みとして表示」オプションを使用します。

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at144736](assets/screen_shot_2018-06-07at144736.png)

1. ブラウザーの組み込みツールを使用して、ページのソースを表示します。
1. ソースのコンテンツは非常に限られています。

   ```
   <!DOCTYPE HTML>
   <html lang="en-CH">
       <head>
       <meta charset="UTF-8">
       <title>We.Retail Journal</title>
   
       <meta name="template" content="we-retail-react-template"/>
   
   <link rel="stylesheet" href="/etc.clientlibs/we-retail-journal/react/clientlibs/we-retail-journal-react.css" type="text/css">
   
   <link rel="stylesheet" href="/libs/wcm/foundation/components/page/responsive.css" type="text/css">
   
   </head>
       <body class="page basicpage">
   
   <div id="page"></div>
   
   <script type="text/javascript" src="/etc.clientlibs/we-retail-journal/react/clientlibs/we-retail-journal-react.js"></script>
   
       </body>
   </html>
   ```

   ページの本文にはコンテンツが含まれていません。 主にスタイルシートとReactスクリプトの呼び出しで構成されます `we-retail-journal-react.js`。

   このReactスクリプトは、このアプリケーションの主なドライバーで、すべてのコンテンツをレンダリングします。

1. ブラウザーの組み込みツールを使用してページを調査します。 完全に読み込まれたDOMのコンテンツを表示します。

   ![screen_shot_2018-06-07at151848](assets/screen_shot_2018-06-07at151848.png)

1. インスペクタの[ネットワーク]タブに切り替え、ページを再読み込みします。

   イメージ要求を無視する場合、ページに対して読み込まれる主なリソースは、ページ自体、CSS、React Javascript、その依存関係、およびページのJSONデータです。

   ![screen_shot_2018-06-07at152155](assets/screen_shot_2018-06-07at152155.png)

1. を新しいタ `react.model.json` ブに読み込みます。

   `/content/we-retail-journal/react.model.json`

   ![screen_shot_2018-06-07at152636](assets/screen_shot_2018-06-07at152636.png)

   AEM SPA editorは、 [AEM Content Servicesを利用して](/help/assets/content-fragments.md) 、ページのコンテンツ全体をJSONモデルとして配信します。

   特定のインターフェイスを実装することで、SlingモデルはSPAに必要な情報を提供します。 JSONデータの配信は、各コンポーネント（ページから段落、コンポーネントなど）に下方に委任されます。

   各コンポーネントは、公開内容とレンダリング方法を選択します（HTLを使用するサーバー側またはReactを使用するクライアント側）。 もちろん、この記事では、Reactを使用したクライアント側のレンダリングに焦点を当てます。

1. また、モデルではページをグループ化して同期的に読み込むことができ、必要なページリロードの数を減らすことができます。

   We.Retail Journalの例では、訪問者は一般的にこれらのペ `home`ージすべ `blog`てを訪問するの `aboutus` で、、、およびの各ページは同期的に読み込まれます。 ただし、訪問 `weather` 者がページを訪問する可能性が低いので、ページは非同期で読み込まれます。

   この動作は必須ではなく、完全に定義できます。

   ![screen_shot_2018-06-07at153945](assets/screen_shot_2018-06-07at153945.png)

1. この動作の違いを表示するには、ページを再読み込みし、インスペクタのネットワークアクティビティをクリアします。 ページメニューでブログやアドビに関するページに移動し、ネットワークアクティビティが報告されないことを確認します。

   天気予報ページに移動し、が非同期で呼び出され `weather.model.json` ることを確認します。

   ![screen_shot_2018-06-07at155738](assets/screen_shot_2018-06-07at155738.png)

### SPAエディタとの対話 {#interaction-with-the-spa-editor}

サンプルのWe.Retail Journalアプリケーションを使用すると、JSONコンテンツ配信のコンテンツサービスとリソースの非同期読み込みを利用して、アプリケーションの動作と公開時の読み込みが明確になります。

また、コンテンツ作成者の場合、SPAエディターを使用したコンテンツの作成はAEM内でシームレスに行われます。

次のセクションでは、SPAエディターがSPA内のコンポーネントをAEMコンポーネントに関連付け、このシームレスな編集操作を実現できる契約を検討します。

1. エディターでWe.Retail Journalアプリケーションを読み込み、プレビューモードに **切り替え** ます。

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

1. ブラウザーに組み込まれている開発者ツールを使用して、ページのコンテンツを調べます。 選択ツールを使用して、ページ上の編集可能なコンポーネントを選択し、要素の詳細を表示します。

   コンポーネントには新しいデータ属性があることに注意してくださ `data-cq-data-path`い。

   ![screen_shot_2018-06-08at095124](assets/screen_shot_2018-06-08at095124.png)

   例：

   `data-cq-data-path="root/responsivegrid/paragraph_1`

   このパスを使用して、各コンポーネントの編集コンテキスト設定オブジェクトの取得と関連付けを行うことができます。

   これは、エディタがSPA内の編集可能コンポーネントとして認識するために必要な唯一のマークアップ属性です。 この属性に基づいて、SPAエディタは、どの編集可能な設定がコンポーネントに関連付けられ、正しいフレーム、ツールバーなどが作成されるかを判断します。 が読み込まれます。

   また、マークプレースホルダーやアセットのドラッグ&amp;ドロップ機能用に、特定のクラス名が追加されています。

   >[!NOTE]
   >
   >これは、AEMのサーバー側でレンダリングされたページでの動作の変更で、編集可能な各コンポーネントに `cq` 要素が挿入されます。
   >
   >
   >SPAのこのアプローチでは、カスタム要素を挿入する必要がなくなり、追加のデータ属性のみを使用するので、フロントエンド開発者にとってマークアップがより簡単になります。

## 次の手順 {#next-steps}

AEMでのSPAの編集エクスペリエンスとSPAとSPAエディターとの関係を理解したら、SPAの構築方法を詳しく説明します。

* [AEMのSPA使用の手引き](/help/sites-developing/spa-getting-started-react.md) （英語）は、AEMのSPAエディターで動作する基本SPAの構築方法を示しています
* [SPA Editor Overviewでは](/help/sites-developing/spa-overview.md) 、AEMとSPA間の通信モデルについて詳しく説明しています。
* [AEM用SPAの開発では](/help/sites-developing/spa-architecture.md) 、フロントエンド開発者と連携してAEM用SPAを開発する方法と、SPAがAEMのアーキテクチャとやり取りする方法について説明します。
