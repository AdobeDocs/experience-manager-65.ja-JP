---
title: AEM Mobile アプリケーションのダッシュボード
description: アプリケーションおよびモバイルアプリのコンテンツは、AEM Mobile Application Dashboard またはコントロールセンターで管理できます。 このページでは、この機能について詳しく見ていきます。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: daafc8b8-3c01-4c97-a14b-f1b706600249
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 11%

---

# AEM Mobile アプリケーションのダッシュボード {#aem-mobile-application-dashboard}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

アプリケーションおよびモバイルアプリのコンテンツは、AEM Mobile Application Dashboard またはコントロールセンターで管理できます。

コントロール・センターの各タイルをドリル・インして詳細を表示または編集するには、右下隅の「。..」をクリックします。

![chlimage_1-54](assets/chlimage_1-54.png)

>[!NOTE]
>
>タイルのグラバーアイコン（左上の 9 ドット）をクリックすると、タイルの順序を並べ替えることができます。 注文の変更はユーザーごとに異なります。

アプリコンテンツの管理には、開発者、コンテンツ作成者および管理者の協力が必要です。 作成者がページを操作します。これは、アプリ開発者が生成したテンプレートやコンポーネントに基づいて無効になります。

最後に、管理者は、更新されたアプリコンテンツを戦略的に公開します。

## アプリを管理タイル {#the-manage-app-tile}

**アプリを管理** タイルに利用可能なアプリケーション情報が表示されます。

* タイトル
* 説明
* アイコン
* 最終変更日
* 最終変更者

![chlimage_1-55](assets/chlimage_1-55.png)

## 接続を管理タイル {#the-manage-connection-tile}

**接続を管理** タイルには、AEM Mobile On-demand Servicesの接続情報が表示されます。

* クラウド設定名
* プロジェクト名と ID
* 接続ステータス

>[!NOTE]
>
>右上の歯車をクリックして、Mobile On-Demand Cloud 設定をセットアップします。
>
>詳しくは、[Mobile On-Demand Services の設定 ](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md) を参照してください。

![chlimage_1-56](assets/chlimage_1-56.png)

## エンティティの管理 {#managing-entities}

次の 3 つのタイルは、アプリのコンテンツの状態の概要を示します。

* **バナー**
* **記事**
* **コレクション**

各タイルを展開すると、右下隅の省略記号（...）をクリックして、より詳細なリスト表示を提供できます。 これらのリスト表示は、プロパティの削除、アップロード、編集など、一般的なモバイルオンデマンド アクションにアクセスする代替の方法を提供します。

### バナーの管理タイル {#the-manage-banners-tile}

**バナーの管理** タイルでは、バナーのコンテンツを管理できます。 バナーには、次の情報が表示されます。

* 画像
* **タイトル**：バナーの名前
* **変更済み**：最終変更日：AEM
* **アップロード済み**：前回AEMからアップロード済み
* **公開済み**：前回公開されたリクエストフォーム AEM
* **SOURCE**: ソース （AEM ローカルまたはモバイル オンデマンドからのリモート）

次の画像は、AEM Mobile アプリケーションダッシュボードの **バナーを管理** タイルを示しています。

![chlimage_1-57](assets/chlimage_1-57.png)

>[!NOTE]
>
>バナーの作成、削除、更新については、**[バナーの管理](/help/mobile/mobile-on-demand-managing-banners.md)** を参照してください。

### 記事を管理タイル {#the-manage-articles-tile}

**記事を管理** タイルでは、記事のコンテンツを管理できます。 記事に関して次の情報が表示されます。

* 画像
* **タイトル**：記事の名前
* **変更済み**：最終変更日：AEM
* **アップロード済み**：前回AEMからアップロード済み
* **公開済み**：前回公開されたリクエストフォーム AEM
* **SOURCE**: ソース （AEM ローカルまたはモバイル オンデマンドからのリモート）

次の画像は、AEM Mobile アプリケーションダッシュボードの **記事を管理** タイルを示しています。

![chlimage_1-58](assets/chlimage_1-58.png)

>[!NOTE]
>
>記事の作成、削除、更新については、[**記事の管理**](/help/mobile/mobile-on-demand-managing-articles.md) を参照してください。

### コレクションを管理タイル {#the-manage-collections-tile}

**コレクションを管理** タイルでは、コレクションのコンテンツを管理できます。 コレクションに関する次の情報が表示されます。

* 画像
* **タイトル**：コレクションの名前
* **変更済み**：最終変更日：AEM
* **アップロード済み**：前回AEMからアップロード済み
* **公開済み**：前回公開されたリクエストフォーム AEM
* **SOURCE**: ソース （AEM ローカルまたはモバイル オンデマンドからのリモート）

次の画像は、AEM Mobile アプリケーションダッシュボードの **コレクションを管理** タイルを示しています。

![chlimage_1-59](assets/chlimage_1-59.png)

>[!NOTE]
>
>コレクションの作成、削除、更新については、**[コレクションの管理](/help/mobile/mobile-on-demand-managing-collections.md)** を参照してください。

### 次の手順 {#the-next-steps}

アプリケーションダッシュボードをよく理解したら、次のリソースを参照してモバイルアプリを作成してください。

* [アプリケーションの作成および設定アクション](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [オンデマンドアプリのクラウド設定への関連付け](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [コンテンツ管理アクション](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)

### その他のリソース {#additional-resources}

管理者と開発者の役割と責任については、以下のリソースを参照してください。

* [AEM Mobile On-demand Services用AEM コンテンツの開発](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand Servicesを使用するコンテンツの管理](/help/mobile/aem-mobile.md)
