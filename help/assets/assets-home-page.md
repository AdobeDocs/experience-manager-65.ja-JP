---
title: '"[!DNL Assets] ホームページエクスペリエンス»'
description: パーソナライズ [!DNL Experience Manager Assets] アセットに関する最近のアクティビティのスナップショットを含む、豊富なようこそ画面エクスペリエンスのホームページ。
contentOwner: AG
feature: Developer Tools, Asset Management
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 32%

---

# [!DNL Adobe Experience Manager Assets] ホームページエクスペリエンス {#aem-assets-home-page-experience}

パーソナライズ [!DNL Adobe Experience Manager Assets] アセットに関する最近のアクティビティのスナップショットを含む、豊富なようこそ画面エクスペリエンスのホームページ。

[!DNL Assets] ホームページには、最近表示されたアセットやアップロードされたアセットなど、最近のアクティビティのスナップショットが含まれ、パーソナライズされた豊富なスクリーンエクスペリエンスが提供されます。

この [!DNL Assets] ホームページはデフォルトで無効になっています。 ホームページを有効にするには、次の手順を実行します。

1. 開く [!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. を開きます。 **[!UICONTROL Day CQ DAM Event Recorder]** サービス。
1. を選択します。 **[!UICONTROL このサービスを有効にする]** アクティビティの記録を有効にします。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 次の **[!UICONTROL イベントタイプ]** リストで、記録するイベントを選択し、変更を保存します。

   >[!CAUTION]
   >
   >「Asset viewed」、「Projects viewed」、「Collections viewed」の各オプションを有効にすると、記録対象のイベント数が大幅に増加します。

1. を開きます。 **[!UICONTROL DAM アセットホームページ機能フラグ]** Configuration Manager からのサービス `https://[aem_server]:[port]/system/console/configMgr`.
1. を選択します。 `isEnabled.name` オプションを使用して [!DNL Assets] ホームページ機能。 変更内容を保存します。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. を開きます。 **[!UICONTROL ユーザーの環境設定]** ダイアログで、 **[!UICONTROL アセットのホームページを有効にする]**. 変更内容を保存します。

   ![ユーザーの環境設定ダイアログでアセットのホームページを有効にする](assets/Annotation-color.png)

を有効にした後 [!DNL Assets] ホームページで、 [!DNL Assets] ナビゲーションページから、または URL から直接アクセスできるユーザーインターフェイス `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![Assets ユーザーインターフェイスでの experience link の設定](assets/config-experience-link.png)

次をクリック： **[!UICONTROL エクスペリエンスリンクを設定するには、ここをクリックしてください]** ユーザー名、背景画像、プロファイル画像を追加します。

この [!DNL Assets] ホームページには、次のセクションが含まれます。

* 「ようこそ」セクション
* 「ウィジェット」セクション

**「ようこそ」セクション**

ユーザーのプロファイルが存在する場合、「ようこそ」セクションには、そのユーザー向けのようこそメッセージが表示されます。さらに、プロフィール画像とようこそ画像（設定済みの場合）が表示されます。

ユーザーのプロファイル設定が完了していない場合、「ようこそ」セクションには、一般的なようこそメッセージとプロファイル写真用のプレースホルダーが表示されます。

**「ウィジェット」セクション**

このセクションは「ようこそ」セクションの下にあり、既製ウィジェットが次のセクションに表示されます。

* アクティビティ
* 最近の表示
* 最新情報

**アクティビティ**:このセクションでは、 **[!UICONTROL マイアクティビティ]** ウィジェットには、アセットのアップロード、ダウンロード、アセットの作成、編集、コメント、注釈、共有など、アセット（レンディションのないアセットを含む）を含む、ログインしたユーザーが実行した最近のアクティビティが表示されます。

**最近**:この **[!UICONTROL 最近表示された項目]** このセクションのウィジェットには、フォルダ、コレクション、プロジェクトなど、ログインしたユーザーが最近アクセスしたエンティティが表示されます。

**Discover**:この **[!UICONTROL 新規]** このセクションのウィジェットには、 [!DNL Assets] デプロイメント。

ユーザーアクティビティデータのパージを有効にするには、 **[!UICONTROL DAM イベントパージサービス]** を Configuration Manager から開きます。 このサービスを有効にすると、ログインユーザーのアクティビティのうち指定した数を超えたものがシステムによって削除されます。

ようこそ画面には、フォルダー、コレクション、カタログにアクセスするためのツールバー上のアイコンなど、簡単に操作するための機能が含まれています。

>[!NOTE]
>
>の有効化 [!UICONTROL Day CQ DAM Event Recorder] および [!UICONTROL DAM イベントのパージ] サービスは、JCR への書き込み操作と検索インデックス作成操作を増やし、インデックス作成の負荷が大幅に増加します。 [!DNL Experience Manager] サーバー。 追加の [!DNL Experience Manager] サーバは、パフォーマンスに影響を与える可能性があります。

>[!CAUTION]
>
>に必要なユーザーアクティビティのキャプチャ、フィルタリングおよびパージ [!DNL Assets] ホームページはパフォーマンスにオーバーヘッドを課します。 そのため、管理者はターゲットユーザーのためにホームページを効果的に設定する必要があります。
>
>一括操作を実行する管理者およびユーザーは、ユーザーアクティビティが増えるのを避けるため、Asset のホームページ機能を使用しないことをお勧めします。また、管理者は、特定のユーザーの記録アクティビティを除外するために、 [!UICONTROL Day CQ DAM Event Recorder] から [!UICONTROL Configuration Manager].
>
>この機能を使用する場合は、サーバー負荷を考慮してパージの頻度を計画することをお勧めします。
