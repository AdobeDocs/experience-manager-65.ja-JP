---
title: Correspondence Management Solution の設定
description: AEM Forms環境で Correspondence Management ソリューションを設定する方法を説明します。
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
feature: Correspondence Management
exl-id: f7f5eb0d-a283-45ea-84d3-d6375d2bb95b
source-git-commit: 000c22028259eb05a61625d43526a2e8314a1d60
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 38%

---

# Correspondence Management Solution の設定 {#configuring-a-correspondence-management-solution}

## VersionRestoreManagerImpl のオーサーインスタンス URL の定義 {#defining-author-instance-url-for-versionrestoremanagerimpl}

オーサーインスタンスのバージョンを復元するオーサーインスタンスの URL を定義するには、次の手順を実行します。

1. *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr* に移動します。OSGi Management Console のユーザー資格情報を使ってログインします。デフォルトの資格情報は、admin/admin です。
1. 「**[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]**」設定の横にある「**[!UICONTROL 編集]**」アイコンをクリックします。
1. 「**[!UICONTROL VersionRestoreManager Author URL]**」フィールドで、オーサーインスタンス VersionRestoreManager の URL を指定します。

   **URL 文字列**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >ロードバランサーの前に複数のオーサーインスタンス（クラスター化）がある場合は、「**[!UICONTROL VersionRestoreManager Author URL]**」フィールドにその URL を指定します。

1. 「**[!UICONTROL 保存]**」をクリックします。

## ActivationManagerImpl のパブリッシュインスタンス URL の定義（パブリックインスタンスアクティベーションマネージャー） {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

パブリックインスタンスアクティベーションマネージャーのパブリッシュインスタンス URL を定義できるようにするには、次の手順に従います。

1. *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr* に移動します。OSGi Management Console のユーザー資格情報を使ってログインします。デフォルトの資格情報は、admin/admin です。
1. を検索して、 **[!UICONTROL 編集]** 横のアイコン **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** 設定。
1. Adobe Analytics の **[!UICONTROL ActivationManager 公開 URL]** 「 」フィールドで、パブリッシュインスタンスの ActivationManager にアクセスするための URL を指定します。 次の URL を指定できます。

   * **ロードバランサー URL （推奨）**：ロードバランサー URL を指定します。パブリッシュファーム（複数の非クラスターパブリッシュインスタンス）の前にロードバランサーとして機能する Web サーバーがある場合は、
   * **パブリッシュインスタンス URL**：任意のパブリッシュインスタンス URL を指定します。1 つのパブリッシュインスタンスがある場合、またはパブリッシュファームを前面に配置している Web サーバーが、制限によりオーサー環境からアクセスできない場合です。 指定したパブリッシュインスタンスが停止した場合は、オーサー側で対処するフォールバックメカニズムがあります。
   * **URL 文字列**：

     `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. 「**[!UICONTROL 保存]**」をクリックします。

Correspondence Management の設定について詳しくは、 [Correspondence Management 設定プロパティ](https://helpx.adobe.com/jp/aem-forms/6-2/cm-configuration-properties.html).
