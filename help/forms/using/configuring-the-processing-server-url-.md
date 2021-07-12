---
title: AEM DS の設定
seo-title: AEM DS の設定
description: フォームを送信する前に、処理サーバーの URL を指定する必要があります。
seo-description: フォームを送信する前に、処理サーバーの URL を指定する必要があります。
uuid: 55a6d434-7352-48a8-8387-8a5c1a48fafc
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: a7387bd3-8b31-4bd0-a861-daa8f7cb2d05
docset: aem65
role: Admin
exl-id: c43cab7b-3421-4e1b-a834-b2dd6eb23c1d
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 60%

---

# AEM DS の設定{#configuring-aem-ds-settings}

この記事では、**AEM DS Settings Service** の設定方法について説明します。この設定は、次のような場合に使用できます。

* Correspondence Management内

   * AEM Forms ワークフローを設定する場合
   * ドラフトまたは送信のリモート保存にフォームポータルを使用する場合

* アダプティブフォームにおいては、アダプティブフォームが発行インスタンスから送信される場合

次の手順に従って、「**[!UICONTROL AEM DS 設定]**」を構成します。

1. URLを使用して、パブリッシュインスタンス上のConfiguration Managerを開きます。\
   *https://localhost:port/system/console/configMgr*&#x200B;を参照してください。

   ![AEM Webコンソールの設定](assets/web_configuration_console_new.png)

1. **[!UICONTROL Adobe Experience Manager Webコンソール設定]**&#x200B;ウィンドウで、「**[!UICONTROL AEM DS設定]**」オプションを探してクリックします。

   ![DS設定](assets/ds_settings_new.png)

1. **[!UICONTROL AEM DS 設定サービス]**&#x200B;ウィンドウに、AEM DS コンポーネントの共通設定が表示されます。

   ![DS設定サービス](assets/ds_settings_service_new.png)

1. 次の情報をそれぞれのフィールドに追加します。

   **[!UICONTROL 処理サーバーURL]**:処理サーバーは、FormsまたはAEMワークフローをトリガーする必要があるサーバーです。これは、AEMオーサーインスタンスのURLまたは他のサーバーURL(つまり、https://localhost:port/)と同じです。

   **[!UICONTROL 処理サーバーのユーザー名]**:使用中のサーバーURLに基づ [くワークフローユーザーのユーザー名]

   **[!UICONTROL 処理サーバーのパスワード]**：ワークフローユーザーのパスワード

   >[!NOTE]
   >
   >
   >    
   >    
   >    * Forms または AEM ワークフローのいずれかを使用しているときは、発行サーバーから送信を行う前に、DS 設定サービスを構成する必要があります。このサービスを構成しないと、フォームの送信が失敗します。



