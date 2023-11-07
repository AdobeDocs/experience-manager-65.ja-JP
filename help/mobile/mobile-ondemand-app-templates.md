---
title: テンプレートとコンポーネントの作成および追加
seo-title: Creating and Adding Templates and Components
description: このページでは、テンプレートとコンポーネントを作成し、アプリに追加する方法について説明します。 このページでは、Geometrixx Unlimitedアプリを、サンプルのアプリテンプレートとページテンプレートを含むアプリとして使用しています。
seo-description: Follow this page to learn about creating and adding templates and components to your app. The page uses Geometrixx Unlimited App as the app that contains a sample app template and page templates.
uuid: 3a93017c-8094-413f-a01c-9b72025a2b20
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ec4ada04-e429-4ad4-a060-2dccac847cf0
exl-id: 5f050baa-fe10-4acc-ad32-de20793edc13
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 3%

---

# テンプレートとコンポーネントの作成および追加 {#creating-and-adding-templates-and-components}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

AEM Mobile On-Demand には、完全に設定されたアプリテンプレート、記事テンプレートおよび記事コンポーネントが用意されています。

We.Unlimited App は、完全に設定可能で管理可能なAEM Mobile On-Demand アプリケーションのシェルを表すサンプルテンプレートです。

アプリを作成する際にこのサンプルテンプレートを選択すると、AEM Mobileの機能が豊富なダッシュボードが提供されます。

![chlimage_1-70](assets/chlimage_1-70.png)

>[!NOTE]
>
>AEM Mobile Apps Control Center からアプリケーションおよびモバイルアプリコンテンツを管理するには、 [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

## アプリテンプレートの作成 {#creating-app-templates}

アプリテンプレートは、アプリの作成に使用され、アプリのベースラインまたは基盤を表すページテンプレートおよびコンポーネントのコレクションとして機能します。 テンプレートは、アプリを適切な方法で導くために、いくつかの基本的なプロパティをスタンプアウトします。 一般に、顧客は作成するアプリの数が多すぎることはありません。

アプリテンプレートを使用すると、開発者が作成した既存のデザインを簡単に使用して、AEM内で新しいアプリを作成できます。

別のアプリのテンプレートに基づいてアプリを作成する場合、作成元のアプリを表す開始点を持つアプリが表示されます。

アプリテンプレートに基づいてアプリを作成する手順は次のとおりです。

1. AEM Mobileアプリカタログに移動します。 *&lt;server-url>/aem/apps.html/content/mobileapps*
1. 選択 **作成** —> **アプリ** 次に示すように

このテンプレートを使用してアプリを作成したら、記事、バナー、コレクションをアプリに追加できます。 記事、バナー、コレクションを再度作成するには、 [コンテンツ管理アクション](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

>[!NOTE]
>
>または、サンプルのアプリテンプレート（例： ）を選択することもできます。 **We.Unlimited** アプリがAEM開発者によって提供されました。 このサンプルテンプレートをアプリに使用すると、サンプル記事やコレクションを使用できます。 サンプルのテンプレートおよびコンポーネントを使用するか、既存のテンプレートおよびコンポーネントをカスタマイズするか、アプリ用に新しいテンプレートを作成するかを選択できます。

>[!CAUTION]
>
>設定 ***redirectTarget*** プロパティ
>
>アプリテンプレートの 1 つを使用する場合、開発者はアプリケーションのコンテンツを定義します。 ただし、開発者は、アプリケーションが jcr 内で作成される場所と、 ***redirectTarget*** プロパティ。
>
>The ***redirectTarget*** はアプリの作成操作の一環として計算され、アプリテンプレートの一部として redirectTarget プロパティが使用可能で、redirectTarget の値が相対パスとして定義されている場合に、パスの解決を試みます。 アプリの作成プロセスで、アプリテンプレート内の redirectTarget の相対値が見つかると、その値が、アプリが作成された解決された場所の値に追加されます。
>
>例えば、アプリテンプレートで ***redirectTarget*** の値は&quot;*lanugage-masters/en*」と表示され、アプリが「*/content/mobileapps/fooApp*「」の場合、アプリの作成後の redirectTarget の最終値は「*/content/mobileapps/fooApp/language-masters/en*&quot;.
>

## コンテンツテンプレートの作成 {#creating-content-templates}

各エンティティタイプには、標準の 2 つのテンプレートが用意されています。 以下の項目が該当します。

* **デフォルトのテンプレート：** 適用可能なデフォルトのプロパティ/構造を持つコンテンツの作成に使用
* **読み込まれたテンプレート：** 適用可能なデフォルトのプロパティ/構造を持つAEM Mobileからコンテンツを読み込むために使用されます。

### 記事テンプレート {#article-templates}

Unlimited の記事は、一般的なAEM Mobile On-Demand 記事レイアウトを表すサンプルテンプレートです。

1. In **記事を管理**&#x200B;を選択します。 **+**  をクリックして記事を作成します。 次のいずれかを選択できます。 **Unlimited の記事** または **リッチテキスト記事**. 次の画像に、これら 2 つの記事テンプレートのいずれかから選択できるオプションを示します。

1. クリック **次へ** ：記事名/タイトル、説明、作成者、要約、部門、サムネール画像、記事へのアクセスなどの記事のメタデータを定義します。
1. クリック **次へ** をクリックして、広告のプロパティを入力します。
1. クリック **次へ** 記事の画像またはソーシャルメディアの画像を入力するには
1. クリック **次へ** をクリックして、この新しい記事のコレクションリンクを選択します。
1. クリック **次へ** をクリックして、ソーシャルシェアの詳細を入力します。
1. クリック **作成** をクリックして、サンプルを使用して記事を作成するプロセスを完了します。 次のいずれかをクリックします。 **完了** または **記事を編集** をクリックして、この記事のプロパティを編集します。

![chlimage_1-71](assets/chlimage_1-71.png)

### 記事へのコンポーネントの追加 {#adding-components-to-article}

作成者は、作成後、テキストや画像などのコンポーネントを追加することで、記事のコンテンツを編集できます。 記事は、AEMページテンプレートの拡張です。

編集する記事を選択し、「 **編集** をクリックして、記事にコンポーネントを追加します。

![chlimage_1-72](assets/chlimage_1-72.png) ![chlimage_1-73](assets/chlimage_1-73.png)

「 」を選択します。**+**&#39;を左側のパネルに追加して、記事にコンポーネントを追加します。

![chlimage_1-74](assets/chlimage_1-74.png)

### 標準テンプレートの作成 {#creating-out-of-the-box-templates}

既製の記事テンプレートはありませんが、カスタムテンプレートが拡張する必要があるデフォルトのテンプレートがあります。Geometrixx Unlimitedアプリの [記事テンプレートのサンプル](http://localhost:4502/crx/de/index.jsp#/apps/geometrixx-unlimited-app/templates/article).

通常のAEMテンプレートに必要なプロパティ以外に、主なプロパティは次のとおりです。

***dps-resourceType=&quot;dps:Article&quot;***

このプロパティを使用すると、AEMページがAEM Mobileのターゲット記事ページとして認識されるようになります。

AEMテンプレートに従って、任意のデフォルトのプロパティまたは子ノードをテンプレートの ***jcr:content***.

### バナーおよびコレクションテンプレート {#banner-and-collection-templates}

>[!CAUTION]
>
>バナーとコレクションにはコンテンツがないので、作成時にカスタムテンプレートがサポートされない。

## コンポーネントの作成と追加 {#creating-and-adding-components}

コンポーネントはウィジェットを使用し、ウィジェットにアクセスできます。ウィジェットはコンテンツのレンダリングに使用されます。

コードリポジトリには単純なコンポーネントが含まれ、そのソースはAEMで見つかります。 その後、ローカルで開くこともできます。CRXDE Lite。

>[!NOTE]
>
>現在、AEM Mobile用に標準搭載されているコンポーネントはありません。
>

ページにコンポーネントを追加できます。 どのコンポーネントもAEM Mobileアプリで使用できますが、適用すると、正しくレンダリングされない場合があります。

ただし、AEMでレンダリングされるカスタム書き出しコンテンツ同期ハンドラーがないと、カスタムコンポーネントはAEM Mobile On-demand Servicesに正しく書き出しおよびアップロードできない場合があります。

コンポーネントを既にAEMページに組み込んだ後、他の構築ブロックコンポーネントと共に、ページに別のコンポーネントを追加したり、既存のコンポーネントを編集したりできます。

**ページに別のコンポーネントを追加するには、次の手順を実行します。**

1. ページを選択し、エディターのヘッダーの右上にあるドロップダウンから、編集モードになっていることを確認します。
1. エディターのヘッダーの左端のアイコンを使用して、サイドパネルを切り替えます。
1. を選択します。 **コンポーネント** タブ
1. 使用可能なコンポーネントの 1 つをページにドラッグ&amp;ドロップします

![chlimage_1-75](assets/chlimage_1-75.png)

**既存のコンポーネントを編集するには：**

1. そのページを選択し、 **編集** モードとコンポーネントを選択します。
1. レンチアイコンをタップして、コンポーネントを設定します。

>[!NOTE]
>
>AEMでコンポーネントを作成し、 [開発とCRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). 既存のコンポーネントを必要に応じてカスタマイズしたら、 **編集** 下のオプション **記事を管理** 上の図に示すように。

>[!NOTE]
>
>参照： [テンプレートとコンポーネント開発のベストプラクティス](/help/mobile/best-practices-aem-mobile.md) AEM Mobileで

### 次の手順 {#the-next-steps}

* [コンテンツのプロパティを使用したコンテンツのエクスポート](/help/mobile/on-demand-content-properties-exporting.md)
* [モバイルとコンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md)
