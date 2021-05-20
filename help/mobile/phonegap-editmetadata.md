---
title: アプリのメタデータの編集
seo-title: アプリのメタデータの編集
description: アプリケーションをベンダーのストアにリリースするには、詳細なアプリのメタデータが必要です。このページでは、アプリのデータの編集について説明します。
seo-description: アプリケーションをベンダーのストアにリリースするには、詳細なアプリのメタデータが必要です。このページでは、アプリのデータの編集について説明します。
uuid: c140be0f-8403-416e-af0f-29072a2ab942
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 07b38da6-2efa-4a43-9afa-7151a241a5ad
exl-id: 897a04b9-e357-4f1c-8aa0-2c2528f8556d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 72%

---

# アプリのメタデータの編集  {#editing-app-metadata}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

**アプリを管理**&#x200B;タイルとアプリを管理ページには、アプリケーションのメタデータを表示および編集するための手段が用意されています。アプリケーションをベンダーのストアにリリースするには、詳細なアプリのメタデータが必要です。これには、共通のメタデータ、iOSメタデータ、スクリーンショットが含まれる場合があります。 共通およびiOSメタデータについて詳しくは、[アプリを管理タイル](/help/mobile/phonegap-app-details-tile.md)を参照してください。

## アプリのデータの編集 {#editing-the-app-data}

アプリのメタデータを編集するには：

1. アプリのダッシュボードページに移動します。

   ![chlimage_1-29](assets/chlimage_1-29.png)

1. 「。..」をクリックして詳細を表示または編集するには をクリックします。****

1. 次の図に示すように、使用可能な5つのタブのいずれかで詳細を入力または表示します。

   ![chlimage_1-30](assets/chlimage_1-30.png)

## 共通メタデータと iOS メタデータの編集 {#editing-common-and-ios-metadata}

共通メタデータと iOS メタデータを編集できます。

* アプリ説明ページの「**詳細**」タブを選択します。
* 共通メタデータと iOS メタデータを編集または表示します。詳しくは、以下の図を参照してください。

![chlimage_1-31](assets/chlimage_1-31.png) ![chlimage_1-32](assets/chlimage_1-32.png)

## スクリーンショットの追加および削除 {#add-and-remove-screenshots}

アプリのスクリーンショットをメタデータのロールアップに含めることができます。ベンダーによっては、アプリをアプリストアに提出する際に正確なスクリーンショットが要求される場合があります。これらの画像は、既にAssetsに存在している必要があります。 スクリーンショットのアップロードについては、[アセットピッカー](../assets/search-assets.md#assetpicker)を参照してください。

![chlimage_1-33](assets/chlimage_1-33.png)

### スクリーンショットを追加する {#add-screenshots}

アセットをスクリーンショットとして追加するには：

1. **アプリを管理**&#x200B;ページの編集モードで、追加（プラスアイコン）をクリックします。
1. アセットを選択し、「**選択**」をクリックしてアセットを追加します。

   ![chlimage_1-34](assets/chlimage_1-34.png)

1. アセットを選択し、「**選択**」をクリックしてアセットを追加します。

>[!NOTE]
>
>スクリーンショットは、ターゲットデバイスの画面の解像度と一致している必要があります。

### スクリーンショットを削除する {#delete-screenshots}

スクリーンショットを削除するには：

アセットの削除アイコンをクリックします。

![chlimage_1-35](assets/chlimage_1-35.png)

## 次の手順 {#the-next-steps}

他のオーサリングの役割について詳しくは、以下のリソースを参照してください。

* [アプリを管理タイル](/help/mobile/phonegap-app-details-tile.md)
* [アプリの定義](/help/mobile/phonegap-app-definitions.md)
* [アプリを作成ウィザードを使用した新規アプリの作成](/help/mobile/phonegap-create-new-app.md)
* [既存のハイブリッドアプリのインポート](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [コンテンツサービス](/help/mobile/develop-content-as-a-service.md)

### その他のリソース {#additional-resources}

管理者および開発者の役割と責任について詳しくは、以下のリソースを参照してください。

* [AEM と Adobe PhoneGap Enterprise での開発](/help/mobile/developing-in-phonegap.md)
* [AEM での Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)
