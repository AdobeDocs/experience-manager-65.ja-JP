---
title: AEM Communities のユーザーおよび UGC 管理サービス
seo-title: AEM Communities のユーザーおよび UGC 管理サービス
description: API を使用すると、ユーザー生成コンテンツの一括削除や一括書き出しをおこなったり、ユーザーアカウントを無効化したりできます。
seo-description: API を使用すると、ユーザー生成コンテンツの一括削除や一括書き出しをおこなったり、ユーザーアカウントを無効化したりできます。
uuid: 91180659-617d-4f6c-9a07-e680770d0d8f
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
discoiquuid: d305821d-1371-4e4a-8b28-8eee8fafa43b
docset: aem65
translation-type: tm+mt
source-git-commit: 18f401babef4cb2aad47e6e4cbb0500b0f8365e2
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 37%

---


# AEM Communities のユーザーおよび UGC 管理サービス {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>以下の節ではGDPRを例に挙げていますが、詳細はデータ保護とプライバシーに関するすべての規制に適用されます。GDPR、CCPAなど


AEM CommunitiesはAPIを標準搭載で公開しており、ユーザープロファイルを管理し、ユーザー生成コンテンツ(UGC)を一括管理できます。 Once enabled, the **UserUgcManagement** service allows the privileged users (community administrators and moderators) to disable user profiles, and bulk delete or bulk export UGC for specific users. また、これらのAPIを使用すると、顧客データのコントローラとプロセッサが、欧州和集合のGDPR(General Data Protection Regulations)や、他のGDPRに基づくプライバシー要件に準拠できます。

詳しくは、[アドビプライバシーセンターの GDPR ページ](https://www.adobe.com/jp/privacy/general-data-protection-regulation.html)を参照してください。

>[!NOTE]
>
>[AEM Communities 内の Adobe Analytics](/help/communities/analytics.md) サイトを設定している場合は、収集されたユーザーデータが Adobe Analytics サーバーに送信されます。Adobe Analytics は、ユーザーデータのアクセス、書き出し、削除や、GDPR に準拠するための処理をおこなう API を提供しています。詳しくは、[アクセス要求および削除要求の送信](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html)を参照してください。


To put these APIs to use, you need to enable the `/services/social/ugcmanagement` endpoint by activating the UserUgcManagement service. To activate this service, install the [sample servlet](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) available on [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). 次に、次のようなhttpリクエストを使用して、適切なパラメーターを指定して、コミュニティサイトの発行インスタンスでエンドポイントに到達します。

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`」を選択します。ただし、システム内のユーザープロファイルとユーザー生成コンテンツを管理するための UI（ユーザーインターフェイス）を構築することもできます。

これらの API で実行できる機能を以下に示します。

## ユーザーの UGC の取得 {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)** は、ユーザーのすべてのUGCをシステムからエクスポートするのに役立ちます。

* **user**:ユーザーの承認可能なID。
* **outputStream**:結果は出力ストリームとして返されます。これは、ユーザーが生成したコンテンツ（jsonファイル）と添付ファイル（ユーザーがアップロードした画像またはビデオを含む）を含むzipファイルです。

例えば、コミュニティサイトにログインする際の許可可能 ID として weston.mccall@dodgit.com を使用する、Weston McCall という名前のユーザーの UGC を書き出すには、次のような HTTP GET リクエストを送信します。

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## ユーザーの UGC の削除 {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user)** は、ユーザーのすべてのUGCをシステムから削除するのに役立ちます。

* **user**:ユーザーの承認可能なID。

例えば、認証可能なID weston.mccall@dodgit.comを持つユーザーのUGCをhttpPOSTリクエストで削除するには、次のパラメーターを使用します。

* ユーザーの = `weston.mccall@dodgit.com`
* 操作 = `deleteUgc`

### Adobe AnalyticsからUGCを削除 {#delete-ugc-from-adobe-analytics}

ユーザーデータをAdobe Analyticsから削除するには、 [GDPR Analyticsのワークフローに従います](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)。を使用しない場合、APIはAdobe Analyticsからユーザーデータを削除しません。

AEM Communitiesが使用するAdobe Analytics変数マッピングについては、次の図を参照してください。

![AEM communitiesのAdobe Analytics変数マッピング](assets/analytics-communities-mapping.png)

## ユーザーアカウントの無効化 {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String user)** は、ユーザーアカウントを無効にするのに役立ちます。

* **user**:ユーザーの承認可能なID。

>[!NOTE]
>
>あるユーザーを無効化すると、そのユーザーがサーバー上で所有しているユーザー生成コンテンツがすべて削除されます。


For example, to delete the profile of a user having authorizable ID `weston.mccall@dodgit.com` through http-POST request, use the following parameters:

* ユーザーの = `weston.mccall@dodgit.com`
* 操作 = `deleteUser`

>[!NOTE]
>
>deleteUserAccount() API では、ユーザープロファイルはシステム内で無効化され、その UGC が削除されるだけです。However, to delete a user profile from the system, navigate to **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de), locate the user node and delete it.


