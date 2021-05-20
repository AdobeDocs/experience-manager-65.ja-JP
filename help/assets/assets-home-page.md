---
title: '[!DNL Assets] ホームページエクスペリエンス'
description: ' [!DNL Experience Manager Assets] ホームページをパーソナライズして、アセットに関する最近のアクティビティのスナップショットなど、豊富なようこそ画面エクスペリエンスを実現します。'
contentOwner: AG
feature: 開発者ツール/アセット管理
role: Administrator, Business Practitioner
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 32%

---

# [!DNL Adobe Experience Manager Assets] ホームページエクスペリエンス  {#aem-assets-home-page-experience}

[!DNL Adobe Experience Manager Assets]ホームページをパーソナライズして、アセットに関する最近のアクティビティのスナップショットなど、豊富なようこそ画面エクスペリエンスを実現します。

[!DNL Assets] ホームページには、最近表示またはアップロードされたアセットなど、最近のアクティビティのスナップショットが含まれ、パーソナライズされたリッチでパーソナライズされたようこそ画面のエクスペリエンスが表示されます。

[!DNL Assets]ホームページはデフォルトで無効になっています。 ホームページを有効にするには、次の手順を実行します。

1. [!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`を開きます。
1. **[!UICONTROL Day CQ DAM Event Recorder]**&#x200B;サービスを開きます。
1. 「**[!UICONTROL このサービスを有効にする]**」を選択して、アクティビティの記録を有効にします。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 「**[!UICONTROL イベントタイプ]**」リストから、記録するイベントを選択し、変更を保存します。

   >[!CAUTION]
   >
   >「Asset viewed」、「Projects viewed」、「Collections viewed」の各オプションを有効にすると、記録対象のイベント数が大幅に増加します。

1. Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`から&#x200B;**[!UICONTROL DAM Asset Home Page Feature Flag]**&#x200B;サービスを開きます。
1. `isEnabled.name`オプションを選択して、[!DNL Assets]ホームページ機能を有効にします。 変更内容を保存します。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. **[!UICONTROL ユーザーの環境設定]**&#x200B;ダイアログを開き、「**[!UICONTROL アセットのホームページを有効にする]**」を選択します。 変更内容を保存します。

   ![ユーザーの環境設定ダイアログでのアセットのホームページの有効化](assets/Annotation-color.png)

[!DNL Assets]ホームページを有効にした後、ナビゲーションページから[!DNL Assets]ユーザーインターフェイスに移動するか、URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`から直接アクセスします。

![Assetsユーザーインターフェイスのエクスペリエンスリンクの設定](assets/config-experience-link.png)

**[!UICONTROL ここをクリックして、エクスペリエンスリンク]**&#x200B;を設定し、ユーザー名、背景画像、プロファイル画像を追加します。

[!DNL Assets]ホームページには、次のセクションが含まれます。

* 「ようこそ」セクション
* 「ウィジェット」セクション

**「ようこそ」セクション**

ユーザーのプロファイルが存在する場合、「ようこそ」セクションには、そのユーザー向けのようこそメッセージが表示されます。さらに、プロフィール画像とようこそ画像（既に設定されている場合）が表示されます。

ユーザーのプロファイル設定が完了していない場合、「ようこそ」セクションには、一般的なようこそメッセージとプロファイル写真用のプレースホルダーが表示されます。

**「ウィジェット」セクション**

このセクションは「ようこそ」セクションの下にあり、既製ウィジェットが次のセクションに表示されます。

* アクティビティ
* 最近の表示
* 最新情報

**アクティビティ**:このセクションの下で、 **[!UICONTROL マイアクティビティウィジェッ]** トには、アセットのアップロード、ダウンロード、アセットの作成、編集、コメント、注釈、共有など、アセット（レンディションのないアセットを含む）を持つログインユーザーが実行した最近のアクティビティが表示されます。

**最近の**:このセクシ **[!UICONTROL ョ]** ンの最近表示されたウィジェットには、フォルダー、コレクション、プロジェクトなど、ログインユーザーが最近アクセスしたエンティティが表示されます。

**検出**:このセク **** ションの新しいウィジェットには、デプロイメントに最近アップロードされたアセットとレンディションが表 [!DNL Assets] 示されます。

ユーザーアクティビティデータのパージを有効にするには、Configuration Managerから&#x200B;**[!UICONTROL DAM Event Purge Service]**&#x200B;を有効にします。 このサービスを有効にすると、ログインユーザーのアクティビティのうち指定した数を超えたものがシステムによって削除されます。

ようこそ画面には、フォルダー、コレクション、カタログにアクセスするためのツールバー上のアイコンなど、簡単に操作するための機能が含まれています。

>[!NOTE]
>
>[!UICONTROL Day CQ DAM Event Recorder]および[!UICONTROL DAM Event Purge]サービスを有効にすると、JCRへの書き込み操作とインデックス検索操作が増加し、[!DNL Experience Manager]サーバーの負荷が大幅に増加します。 [!DNL Experience Manager]サーバーの追加負荷は、そのパフォーマンスに影響を与える場合があります。

>[!CAUTION]
>
>[!DNL Assets]ホームページで必要なユーザーアクティビティのキャプチャ、フィルタリングおよびパージは、パフォーマンスにオーバーヘッドを課します。 そのため、管理者はターゲットユーザーのためにホームページを効果的に設定する必要があります。
>
>一括操作を実行する管理者およびユーザーは、ユーザーアクティビティが増えるのを避けるため、Asset のホームページ機能を使用しないことをお勧めします。さらに、管理者は、[!UICONTROL 設定マネージャー]から[!UICONTROL Day CQ DAM Event Recorder]を設定することで、特定のユーザーの記録アクティビティを除外できます。
>
>この機能を使用する場合は、サーバー負荷を考慮してパージの頻度を計画することをお勧めします。
