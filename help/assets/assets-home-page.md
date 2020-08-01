---
title: '[!DNLAdobe Experience Managerアセット]ホームページエクスペリエンス。'
description: Personalize the [!DNL Experience Manager Assets] Home page for a rich welcome screen experience, including a snapshot of recent activities around assets.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 32%

---


# [!DNL Adobe Experience Manager Assets] ホームページ体験 {#aem-assets-home-page-experience}

Personalize the [!DNL Adobe Experience Manager Assets] home page for a rich welcome screen experience, including a snapshot of recent activities around assets.

[!DNL Assets] ホームページは、最近表示またはアップロードされたアセットなど、最近のアクティビティのスナップショットを含む、カスタマイズされた豊富なスタートアップスクリーンエクスペリエンスを提供します。

The [!DNL Assets] home page is disabled by default. ホームページを有効にするには、次の手順を実行します。

1. Open [!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Day CQ DAM Event Recorder]** service.
1. Select the **[!UICONTROL Enable this service]** to enable activity recording.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. From the **[!UICONTROL Event Types]** list, select the events to be recorded and save the changes.

   >[!CAUTION]
   >
   >「Asset viewed」、「Projects viewed」、「Collections viewed」の各オプションを有効にすると、記録対象のイベント数が大幅に増加します。

1. Open the **[!UICONTROL DAM Asset Home Page Feature Flag]** service from Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Select the `isEnabled.name` option to enable the [!DNL Assets] Home page feature. 変更内容を保存します。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. **[!UICONTROL ユーザ環境設定ダイアログを開き]** 、「アセットホームページを **[!UICONTROL 有効にする」を選択し]**&#x200B;ます。 変更内容を保存します。

   ![ユーザ環境設定ダイアログでアセットホームページを有効にする](assets/Annotation-color.png)

After enabling the [!DNL Assets] Home page, navigate to the [!DNL Assets] user interface either from the Navigation page or access it directly from the URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![アセットユーザーインターフェイスのエクスペリエンスリンクの設定](assets/config-experience-link.png)

Click the **[!UICONTROL Click here to configure your experience link]** to add your username, background image, and profile image.

The [!DNL Assets] Home page includes the following sections:

* 「ようこそ」セクション
* 「ウィジェット」セクション

**「ようこそ」セクション**

ユーザーのプロファイルが存在する場合、「ようこそ」セクションには、そのユーザー向けのようこそメッセージが表示されます。さらに、プロファイルの画像と、（既に設定されている場合は）ようこその画像が表示されます。

ユーザーのプロファイル設定が完了していない場合、「ようこそ」セクションには、一般的なようこそメッセージとプロファイル写真用のプレースホルダーが表示されます。

**「ウィジェット」セクション**

このセクションは「ようこそ」セクションの下にあり、既製ウィジェットが次のセクションに表示されます。

* アクティビティ
* 最近の表示
* 最新情報

**アクティビティ**: このセクションの下では、 **[!UICONTROL マイアクティビティ]** Widgetには、アセットのアップロード、ダウンロード、アセットの作成、編集、コメント、注釈、共有など、アセット（レンディションのないアセットを含む）と共にログインしたユーザーが実行した最新のアクティビティが表示されます。

**最新**: このセクションの **[!UICONTROL 最近表示した]** Widgetには、フォルダー、コレクション、プロジェクトなど、ログインユーザーが最近アクセスしたエンティティが表示されます。

**Discover**: このセクションの **[!UICONTROL 新しい]** Widgetには、デプロイメントに最近アップロードされたアセットとレンディションが表示され [!DNL Assets] ます。

To enable purging of user activity data, enable the **[!UICONTROL DAM Event Purge Service]** from Configuration Manager. このサービスを有効にすると、ログインユーザーのアクティビティのうち指定した数を超えたものがシステムによって削除されます。

ようこそ画面には、フォルダー、コレクション、カタログにアクセスするためのツールバー上のアイコンなど、簡単に操作するための機能が含まれています。

>[!NOTE]
>
>[!UICONTROL Day CQ DAMイベントレコーダー] および [!UICONTROL DAMイベント削除サービスを有効にすると、JCRおよび検索インデックスへの書き込み操作が増え、][!DNL Experience Manager] サーバーの負荷が大幅に増加します。 The additional load on the [!DNL Experience Manager] server can impact its performance.

>[!CAUTION]
>
>Capturing, filtering, and purging user activities required for [!DNL Assets] home page impose an overhead on performance. そのため、管理者はターゲットユーザーのためにホームページを効果的に設定する必要があります。
>
>一括操作を実行する管理者およびユーザーは、ユーザーアクティビティが増えるのを避けるため、Asset のホームページ機能を使用しないことをお勧めします。In addition, administrators can exclude recording activities for specific users by configuring [!UICONTROL Day CQ DAM Event Recorder] from [!UICONTROL Configuration Manager].
>
>この機能を使用する場合は、サーバー負荷を考慮してパージの頻度を計画することをお勧めします。
