---
title: AEM DS の設定
description: フォームを送信する前に処理サーバーの URL を指定する方法を確認します。
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin
exl-id: c43cab7b-3421-4e1b-a834-b2dd6eb23c1d
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 100%

---

# AEM DS の設定{#configuring-aem-ds-settings}

この記事では、**AEM DS 設定サービス**&#x200B;を設定する方法について説明します。この設定は、次のような複数のシナリオで使用できます。

* Correspondence Management では

   * AEM Forms Workflow を設定する場合
   * フォームポータルを使用してドラフトまたは送信をリモートで保存する場合

* アダプティブフォームでは、パブリッシュインスタンスからアダプティブフォームが送信された場合などに使用します。

次に、**[!UICONTROL AEM DS 設定]**&#x200B;を行う手順を示します。

1. 次の URL で、パブリッシュインスタンスにある Configuration Manager を開きます。\
   *https://localhost:port/system/console/configMgr*

   ![AEM web コンソールの設定](assets/web_configuration_console_new.png)

1. **[!UICONTROL Adobe Experience Manager web コンソール設定]**&#x200B;ウィンドウで、「**[!UICONTROL AEM DS 設定]**」オプションを見つけてクリックします。

   ![DS 設定](assets/ds_settings_new.png)

1. **[!UICONTROL AEM DS 設定サービス]**&#x200B;ウィンドウに、AEM DS コンポーネントの共通設定が表示されます。

   ![DS 設定サービス](assets/ds_settings_service_new.png)

1. 次の情報をそれぞれのフィールドに追加します。

   **[!UICONTROL 処理サーバー URL]**：処理サーバーは、Forms または AEM ワークフローをトリガーする必要のあるサーバーです。これは、AEM オーサーインスタンスの URL と同じか、他のサーバー URL（つまり、https://localhost:port/）になります。

   **[!UICONTROL 処理サーバーのユーザー名]**：ワークフローユーザーのユーザー名は、[使用するサーバー URL に基づいています]

   **[!UICONTROL 処理サーバーのパスワード]**：ワークフローユーザーのパスワード

   >[!NOTE]
   >
   >
   >    
   >    
   >    * Forms または AEM ワークフローを使用する場合は、パブリッシュサーバーから送信する前に、DS 設定サービスを設定する必要があります。これを設定しないと、フォームの送信が失敗します。
   >    
   >
