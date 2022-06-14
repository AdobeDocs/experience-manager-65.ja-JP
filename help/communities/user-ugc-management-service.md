---
title: AEM Communities のユーザーおよび UGC 管理サービス
seo-title: User and UGC Management Service in AEM Communities
description: API を使用すると、ユーザー生成コンテンツの一括削除や一括書き出しをおこなったり、ユーザーアカウントを無効化したりできます。
seo-description: Use APIs to bulk delete and bulk export user generated content, and disable user account.
uuid: 91180659-617d-4f6c-9a07-e680770d0d8f
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
discoiquuid: d305821d-1371-4e4a-8b28-8eee8fafa43b
docset: aem65
role: Admin
exl-id: 526ef0fa-3f20-4de4-8bc5-f435c60df0d0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 41%

---

# AEM Communities のユーザーおよび UGC 管理サービス {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>以下の節では GDPR を例として使用していますが、詳細はすべてのデータ保護およびプライバシー規制（GDPR、CCPA など）に適用できます。

AEM Communitiesでは、ユーザープロファイルの管理やユーザー生成コンテンツ (UGC) の一括管理をおこなうための API を標準で提供しています。 有効にすると、 **UserUgcManagement** サービスを使用すると、権限を持つユーザー（コミュニティ管理者とモデレーター）がユーザープロファイルを無効にしたり、特定のユーザーに対して UGC を一括削除または一括書き出ししたりできます。 また、これらの API を使用すると、顧客データの管理者やプロセッサーが、欧州連合の一般データ保護規則 (GDPR) や、GDPR に基づくその他の GDPR に触発されたプライバシー要件に準拠できます。

詳しくは、[アドビプライバシーセンターの GDPR ページ](https://www.adobe.com/jp/privacy/general-data-protection-regulation.html?lang=ja)を参照してください。

>[!NOTE]
>
>[AEM Communities 内の Adobe Analytics](/help/communities/analytics.md) サイトを設定している場合は、収集されたユーザーデータが Adobe Analytics サーバーに送信されます。Adobe Analytics は、ユーザーデータのアクセス、書き出し、削除や、GDPR に準拠するための処理をおこなう API を提供しています。詳しくは、[アクセス要求および削除要求の送信](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html)を参照してください。

これらの API を使用するには、 `/services/social/ugcmanagement` UserUgcManagement サービスをアクティブ化してエンドポイントを作成します。 このサービスをアクティブ化するには、 [サンプルサーブレット](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) 次で利用可能： [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). 次に、次のような http リクエストを使用して、コミュニティサイトのパブリッシュインスタンスでエンドポイントをヒットします。

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`に従っていない場合に発生します。ただし、システム内のユーザープロファイルとユーザー生成コンテンツを管理するための UI（ユーザーインターフェイス）を構築することもできます。

これらの API で実行できる機能を以下に示します。

## ユーザーの UGC の取得 {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)** は、ユーザーのすべての UGC をシステムから書き出すのに役立ちます。

* **ユーザー**:ユーザーの許可可能 ID。
* **outputStream**:結果は出力ストリームとして返されます。これは、ユーザーが生成したコンテンツ（JSON ファイル）と添付ファイル（ユーザーがアップロードした画像やビデオを含む）を含む zip ファイルです。

例えば、コミュニティサイトにログインする際の許可可能 ID として weston.mccall@dodgit.com を使用する、Weston McCall という名前のユーザーの UGC を書き出すには、次のような HTTP GET リクエストを送信します。

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## ユーザーの UGC の削除 {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user)** は、ユーザーのすべての UGC をシステムから削除するのに役立ちます。

* **ユーザー**:ユーザーの許可可能 ID。

例えば、許可可能 ID weston.mccall@dodgit.comを持つユーザーの UGC を http-Delect 要求を通じてPOSTするには、次のパラメーターを使用します。

* ユーザーの = `weston.mccall@dodgit.com`
* operation = `deleteUgc`

### Adobe Analyticsから UGC を削除 {#delete-ugc-from-adobe-analytics}

Adobe Analyticsからユーザーデータを削除するには、 [GDPR Analytics のワークフロー](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html);の場合、API はAdobe Analyticsからユーザーデータを削除しません。

AEM Communitiesで使用されるAdobe Analytics変数のマッピングについては、次の画像を参照してください。

![Adobe AnalyticsでのAEM communities 変数マッピング](assets/analytics-communities-mapping.png)

## ユーザーアカウントの無効化 {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String user)** は、ユーザーアカウントを無効にするのに役立ちます。

* **ユーザー**:ユーザーの許可可能 ID。

>[!NOTE]
>
>あるユーザーを無効化すると、そのユーザーがサーバー上で所有しているユーザー生成コンテンツがすべて削除されます。

例えば、許可可能 ID を持つユーザーのプロファイルを削除するには `weston.mccall@dodgit.com` http-request リクエストでは、次のPOSTーを使用します。

* ユーザーの = `weston.mccall@dodgit.com`
* operation = `deleteUser`

>[!NOTE]
>
>deleteUserAccount() API では、ユーザープロファイルはシステム内で無効化され、その UGC が削除されるだけです。ただし、ユーザープロファイルをシステムから削除する場合は、 **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de)の上にマウスポインターを置いて、ユーザーノードを探して削除します。
