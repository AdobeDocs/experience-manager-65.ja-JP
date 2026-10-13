---
title: AEM DS の設定
description: フォームを送信する前に処理サーバーの URL を指定する方法を確認します。
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: c43cab7b-3421-4e1b-a834-b2dd6eb23c1d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 88%
---
# AEM DS の設定{#configuring-aem-ds-settings}

この記事では、**AEM DS 設定サービス**&#x200B;を設定する方法について説明します。 この設定は、次のような複数のシナリオで使用できます。

* Correspondence Management では

  * AEM Forms Workflow を設定する場合
  * フォームポータルを使用してドラフトまたは送信をリモートで保存する場合

* アダプティブフォームでは、パブリッシュインスタンスからアダプティブフォームが送信された場合などに使用します。

次に、**[!UICONTROL AEM DS 設定]**&#x200B;を行う手順を示します。

1. 次の URL で、パブリッシュインスタンスにある Configuration Manager を開きます。\
   *https://localhost:port/system/console/configMgr*。

   ![AEM web コンソールの設定](assets/web_configuration_console_new.png)

1. **[!UICONTROL Adobe Experience Manager web コンソール設定]**&#x200B;ウィンドウで、「**[!UICONTROL AEM DS 設定]**」オプションを見つけてクリックします。

   ![DS 設定](assets/ds_settings_new.png)

1. **[!UICONTROL AEM DS 設定サービス]**&#x200B;ウィンドウに、AEM DS コンポーネントの共通設定が表示されます。

   ![DS 設定サービス](assets/ds_settings_service_new.png)

1. 次の情報をそれぞれのフィールドに追加します。

   **[!UICONTROL 処理サーバー URL]**：処理サーバーは、Forms または AEM ワークフローをトリガーする必要のあるサーバーです。 これは、AEM オーサーインスタンスのURLまたは他のサーバーのURL （つまり、https://localhost:port/）と同じにすることができます。

   **[!UICONTROL 処理サーバーのユーザー名]**：ワークフローユーザーのユーザー名は、[使用するサーバー URL に基づいています]

   **[!UICONTROL 処理サーバーのパスワード]**：ワークフローユーザーのパスワード

   >[!NOTE]
   >
   >
   >    
   >    
   >    * Forms または AEM ワークフローを使用する場合は、パブリッシュサーバーから送信する前に、DS 設定サービスを設定する必要があります。 これを設定しないと、フォームの送信が失敗します。
   >    
   >
