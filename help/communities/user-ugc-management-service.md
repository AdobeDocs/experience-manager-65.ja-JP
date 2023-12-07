---
title: AEM Communities のユーザーおよび UGC 管理サービス
description: API を使用して、ユーザー生成コンテンツの一括削除および一括書き出し、ユーザーアカウントの無効化をおこないます。
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
docset: aem65
role: Admin
exl-id: 526ef0fa-3f20-4de4-8bc5-f435c60df0d0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 5%

---

# AEM Communities のユーザーおよび UGC 管理サービス {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>以下の節では GDPR を例として使用していますが、詳細は、GDPR、CCPA など、すべてのデータ保護およびプライバシー規制に適用されます。

AEM Communitiesでは、ユーザープロファイルの管理やユーザー生成コンテンツ (UGC) の一括管理をおこなうための API を標準で提供しています。 有効にすると、 **UserUgcManagement** サービスを使用すると、権限を持つユーザー（コミュニティ管理者とモデレーター）がユーザープロファイルを無効にしたり、特定のユーザーに対して UGC を一括削除または一括書き出ししたりできます。 また、これらの API を使用すると、顧客データの管理者やプロセッサーが、欧州連合の一般データ保護規則 (GDPR) や、GDPR に基づくその他の GDPR に触発されたプライバシー要件に準拠できます。

詳しくは、[アドビプライバシーセンターの GDPR ページ](https://www.adobe.com/jp/privacy/general-data-protection-regulation.html)を参照してください。

>[!NOTE]
>
>設定済みの場合 [AEM CommunitiesのAdobe Analytics](/help/communities/analytics.md) サイトに保存すると、取得したユーザーデータがAdobe Analyticsサーバーに送信されます。 Adobe Analyticsには、ユーザーデータにアクセス、書き出し、削除し、GDPR に準拠できる API が用意されています。 詳しくは、 [アクセス要求および削除要求の送信](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html).

これらの API を使用するには、 `/services/social/ugcmanagement` UserUgcManagement サービスをアクティブ化してエンドポイントを作成します。 このサービスをアクティブ化するには、 [サンプルサーブレット](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) 次の日付で利用可能： [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). 次に、次のような http リクエストを使用して、コミュニティサイトのパブリッシュインスタンスでエンドポイントをヒットします。

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`。ただし、UI（ユーザーインターフェイス）を構築して、システム内のユーザープロファイルとユーザー生成コンテンツを管理することもできます。

これらの API を使用して、次の機能を実行できます。

## ユーザーの UGC の取得 {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)** は、ユーザーのすべての UGC をシステムから書き出すのに役立ちます。

* **ユーザー**：ユーザーの許可可能 ID。
* **outputStream**：結果は出力ストリームとして返されます。これは、ユーザーが生成したコンテンツ（JSON ファイル）と添付ファイル（ユーザーがアップロードした画像やビデオを含む）を含む zip ファイルです。

例えば、コミュニティサイトにログインする際に許可可能 ID としてweston.mccall@dodgit.comを使用する Weston McCall という名前のユーザーの UGC を書き出すには、次のような httpGETリクエストを送信します。

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## ユーザーの UGC を削除 {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user)** は、ユーザーのすべての UGC をシステムから削除するのに役立ちます。

* **ユーザー**：ユーザーの許可可能 ID。

例えば、許可可能 ID weston.mccall@dodgit.comを持つユーザーの UGC を http-Delect 要求を通じてPOSTするには、次のパラメーターを使用します。

* user = `weston.mccall@dodgit.com`
* operation = `deleteUgc`

### Adobe Analyticsから UGC を削除 {#delete-ugc-from-adobe-analytics}

Adobe Analyticsからユーザーデータを削除するには、 [GDPR Analytics のワークフロー](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html?lang=ja)と呼ばれ、API はAdobe Analyticsからユーザーデータを削除しません。

AEM Communitiesで使用されるAdobe Analytics変数のマッピングについては、次の画像を参照してください。

![Adobe AnalyticsでのAEM communities 変数マッピング](assets/analytics-communities-mapping.png)

## ユーザーアカウントの無効化 {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String user)** は、ユーザーアカウントを無効にするのに役立ちます。

* **ユーザー**：ユーザーの許可可能 ID。

>[!NOTE]
>
>ユーザーを無効にすると、ユーザーがサーバー上に持っているユーザー生成コンテンツがすべて削除されます。

例えば、許可可能 ID を持つユーザーのプロファイルを削除するには `weston.mccall@dodgit.com` http-request リクエストでは、次のPOSTーを使用します。

* user = `weston.mccall@dodgit.com`
* operation = `deleteUser`

>[!NOTE]
>
>deleteUserAccount() API は、システム内のユーザープロファイルを無効にし、UGC を削除するだけです。 ただし、ユーザープロファイルをシステムから削除する場合は、 **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de)の上にマウスポインターを置いて、ユーザーノードを探して削除します。
