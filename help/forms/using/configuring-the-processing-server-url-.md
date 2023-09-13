---
title: AEM DS の設定
description: フォームを送信する前に処理サーバーの URL を指定する方法を説明します。
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin
exl-id: c43cab7b-3421-4e1b-a834-b2dd6eb23c1d
source-git-commit: 5af420c8e95fed88a8516cce27b8bbc7d3974e75
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 37%

---

# AEM DS の設定{#configuring-aem-ds-settings}

この記事では、 **AEM DS Settings Service**. この設定は、次のような複数のシナリオで使用できます。

* Correspondence Management では

   * AEM Forms Workflow を設定する場合
   * Forms Portal を使用してドラフト/送信をリモートで保存する場合

* アダプティブフォームでは、パブリッシュインスタンスからアダプティブフォームが送信された場合などに使用します。

次に、 **[!UICONTROL AEM DS 設定]**:

1. 次の URL で、パブリッシュインスタンスにある Configuration Manager を開きます。\
   *https://localhost:port/system/console/configMgr*

   ![AEM web コンソールの設定](assets/web_configuration_console_new.png)

1. **[!UICONTROL Adobe Experience Manager web コンソール設定]**&#x200B;ウィンドウで、「**[!UICONTROL AEM DS 設定]**」オプションを見つけてクリックします。

   ![DS 設定](assets/ds_settings_new.png)

1. **[!UICONTROL AEM DS 設定サービス]**&#x200B;ウィンドウに、AEM DS コンポーネントの共通設定が表示されます。

   ![DS 設定サービス](assets/ds_settings_service_new.png)

1. 次の情報をそれぞれのフィールドに追加します。

   **[!UICONTROL 処理サーバー URL]**：処理サーバーは、FormsまたはAEMワークフローをトリガーする必要があるサーバーです。 これは、AEMオーサーインスタンスの URL と同じか、他のサーバー URL(https://localhost:port/) と同じにすることができます。

   **[!UICONTROL 処理サーバーのユーザー名]**：ワークフローユーザーのユーザー名は、[使用するサーバー URL に基づいています]

   **[!UICONTROL 処理サーバーのパスワード]**：ワークフローユーザーのパスワード

   >[!NOTE]
   >
   >
   >    
   >    
   >    * FormsまたはAEMワークフローを使用している場合、パブリッシュサーバーから送信する前に、DS 設定サービスを設定する必要があります。 そうしないと、フォームの送信が失敗します。
   >    
   >
