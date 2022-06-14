---
title: Correspondence Management Solution の設定
seo-title: Configuring a Correspondence Management solution
description: Correspondence Management Solution の設定
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
feature: Correspondence Management
exl-id: f7f5eb0d-a283-45ea-84d3-d6375d2bb95b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 100%

---

# Correspondence Management Solution の設定 {#configuring-a-correspondence-management-solution}

## VersionRestoreManagerImpl の作成者インスタンス URL の定義 {#defining-author-instance-url-for-versionrestoremanagerimpl}

作成者インスタンスバージョンのリストアの作成者インスタンス URL を定義するには、以下の手順を実行します。

1. *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr* に移動します。OSGi Management Console のユーザー資格情報を使ってログインします。デフォルトの資格情報は、admin/admin です。
1. 「**[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]**」設定の横にある「**[!UICONTROL 編集]**」アイコンをクリックします。
1. 「**[!UICONTROL VersionRestoreManager Author URL]**」フィールドで、オーサーインスタンス VersionRestoreManager の URL を指定します。

   **URL 文字列**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >ロードバランサーの前に複数のオーサーインスタンス（クラスター化）がある場合は、「**[!UICONTROL VersionRestoreManager Author URL]**」フィールドにその URL を指定します。

1. 「**[!UICONTROL 保存]**」をクリックします。

## ActivationManagerImpl（発行インスタンス Activation Manager）の発行インスタンス URL の定義 {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

発行インスタンス ActivationManager の発行インスタンス URL を定義するには、以下の手順を実行します。

1. *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr* に移動します。OSGi Management Console のユーザー資格情報を使ってログインします。デフォルトの資格情報は、admin/admin です。
1. 「**[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]**」設定の横にある「**[!UICONTROL 編集]**」アイコンをクリックします。
1. 「**[!UICONTROL ActivationManager Publish URL]**」フィールドで、発行インスタンス ActivationManager にアクセスするための URL を指定します。次の URL を指定できます。

   * **ロードバランサー URL（推奨）**：発行ファーム（複数の非クラスター発行インスタンス）の前にロードバランサーとして機能する Web サーバーを持っている場合は、そのロードバランサーの URL を指定します。
   * **発行インスタンス URL**: 単一の発行インスタンスのみを持っている場合、あるいは発行ファーム前段の Web サーバーが何らかの理由で作成者完了からアクセスできない場合、任意の発行インスタンス URL を指定します。指定した発行インスタンスがダウンした場合は、フォールバックメカニズムが機能して作成者側で処理します。
   * **URL 文字列**：

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. 「**[!UICONTROL 保存]**」をクリックします。

Correspondence Management の設定方法と詳細は、[Correspondence Management 設定プロパティ](https://helpx.adobe.com/jp/aem-forms/6-2/cm-configuration-properties.html)を参照してください。
