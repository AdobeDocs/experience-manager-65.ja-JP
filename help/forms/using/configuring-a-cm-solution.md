---
title: Correspondence Management Solution の設定
seo-title: Correspondence Management Solution の設定
description: Correspondence Management Solution の設定
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 78%

---


# Correspondence Management Solution の設定 {#configuring-a-correspondence-management-solution}

## VersionRestoreManagerImpl の作成者インスタンス URL の定義 {#defining-author-instance-url-for-versionrestoremanagerimpl}

作成者インスタンスバージョンのリストアの作成者インスタンス URL を定義するには、以下の手順を実行します。

1. Go to *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*. OSGi Management Console のユーザー資格情報を使ってログインします。デフォルトの資格情報は、admin/admin です。
1. 「**[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]**」設定の横にある「**[!UICONTROL 編集]**」アイコンをクリックします。
1. In the **[!UICONTROL VersionRestoreManager Author URL]** field, specify the URL of Author instance of VersionRestoreManager.

   **URL文字列**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >If there are multiple author instances (Clustered) fronted by a Load Balancer, specify the URL to the load balancer in the **[!UICONTROL VersionRestoreManager Author URL]** field.

1. 「**[!UICONTROL 保存]**」をクリックします。

## ActivationManagerImpl（発行インスタンス Activation Manager）の発行インスタンス URL の定義 {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

発行インスタンス ActivationManager の発行インスタンス URL を定義するには、以下の手順を実行します。

1. Go to *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*. OSGi Management Console のユーザー資格情報を使ってログインします。デフォルトの資格情報は、admin/admin です。
1. 「**[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]**」設定の横にある「**[!UICONTROL 編集]**」アイコンをクリックします。
1. 「**[!UICONTROL ActivationManager Publish URL]**」フィールドで、発行インスタンス ActivationManager にアクセスするための URL を指定します。次の URL を指定できます。

   * **ロードバランサー URL（推奨）**：発行ファーム（複数の非クラスター発行インスタンス）の前にロードバランサーとして機能する Web サーバーを持っている場合は、そのロードバランサーの URL を指定します。
   * **発行インスタンス URL**: 単一の発行インスタンスのみを持っている場合、あるいは発行ファーム前段の Web サーバーが何らかの理由で作成者完了からアクセスできない場合、任意の発行インスタンス URL を指定します。指定した発行インスタンスがダウンした場合は、フォールバックメカニズムが機能して作成者側で処理します。
   * **URL文字列**:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. 「**[!UICONTROL 保存]**」をクリックします。

Correspondence Management の設定方法と詳細は、[Correspondence Management 設定プロパティ](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html)を参照してください。
