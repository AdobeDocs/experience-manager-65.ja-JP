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
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# AEM Communities のユーザーおよび UGC 管理サービス{#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>以下の節ではGDPRを例として挙げているが、詳細はデータ保護とプライバシーに関する規制に適用される。（GDPR、CCPAなど）

AEM Communitiesは、ユーザープロファイルを管理し、ユーザー生成コンテンツ(UGC)を一括管理するためのAPIをすぐに使用できます。 Once enabled, the **UserUgcManagement** service allows the privileged users (community administrators and moderators) to disable user profiles, and bulk delete or bulk export UGC for specific users. また、これらのAPIを使用すると、顧客データのコントローラやプロセッサーが、EUのGDPR(General Data Protection Regulations)や、GDPRに基づくプライバシーに関するその他の規制に準拠できます。

詳しくは、[アドビプライバシーセンターの GDPR ページ](https://www.adobe.com/privacy/general-data-protection-regulation.html)を参照してください。

>[!NOTE]
>
>[AEM Communities 内の Adobe Analytics](/help/communities/analytics.md) サイトを設定している場合は、収集されたユーザーデータが Adobe Analytics サーバーに送信されます。Adobe Analytics は、ユーザーデータのアクセス、書き出し、削除や、GDPR に準拠するための処理をおこなう API を提供しています。詳しくは、[アクセス要求および削除要求の送信](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/gdpr_submit_access_delete.html)を参照してください。

To put these APIs to use, you need to enable the **/services/social/ugcmanagement** endpoint by activating the UserUgcManagement service. To activate this service, install the [sample servlet](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-ugc-management-servlet) available on [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-ugc-management-servlet). 次に、コミュニティサイトのパブリッシュインスタンスでそのエンドポイントにアクセスします。その際、次のような HTTP リクエストを使用し、適切なパラメーターを指定します。

**https://localhost:port/services/social/ugcmanagement?user=&lt;authorizable ID>&amp;operation=&lt;getUgc>**. ただし、システム内のユーザープロファイルとユーザー生成コンテンツを管理するための UI（ユーザーインターフェイス）を構築することもできます。

これらの API で実行できる機能を以下に示します。

## ユーザーの UGC の取得 {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, outputStream outputStream) **は、ユーザーのすべてのUGCをシステムからエクスポートするのに役立ちます。

* **user**:ユーザーの許可可能なID。
* **outputStream**：結果は出力ストリームとして返されます。このストリームは、ユーザー生成コンテンツ（JSON ファイル）と（ユーザーがアップロードした画像またはビデオを含む）添付ファイルを含んだ zip ファイルになります。

例えば、コミュニティサイトにログインする際の許可可能 ID として weston.mccall@dodgit.com を使用する、Weston McCall という名前のユーザーの UGC を書き出すには、次のような HTTP GET リクエストを送信します。

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## ユーザーの UGC の削除 {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user) **は、ユーザーのすべてのUGCをシステムから削除するのに役立ちます。

* **user**：ユーザーの許可可能 ID。

例えば、許可可能なID weston.mccall@dodgit.comを持つユーザーのUGCをhttp-POSTリクエストで削除するには、次のパラメーターを使用します。

* user= weston.mccall@dodgit.com
* operation= deleteUgc

### Adobe AnalyticsからUGCを削除 {#delete-ugc-from-adobe-analytics}

Adobe Analyticsからユーザーデータを削除するには、 [GDPR Analyticsワークフローに従います](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/an_gdpr_workflow.html)。の代わりに、APIはAdobe Analyticsからユーザーデータを削除しません。

AEM Communitiesで使用されるAdobe Analytics変数マッピングについては、次の画像を参照してください。

![Adobe AnalyticsのAEMコミュニティ変数マッピング](assets/analytics-communities-mapping.png)

## ユーザーアカウントの無効化 {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String user) **は、ユーザーアカウントの無効化に役立ちます。

* **user**：ユーザーの許可可能 ID。

>[!NOTE]
>
>あるユーザーを無効化すると、そのユーザーがサーバー上で所有しているユーザー生成コンテンツがすべて削除されます。

例えば、http-POSTリクエストを使用して許可可能なID weston.mccall@dodgit.comを持つユーザーのプロファイルを削除するには、次のパラメーターを使用します。

* user= weston.mccall@dodgit.com
* operation= deleteUser

>[!NOTE]
>
>deleteUserAccount() API では、ユーザープロファイルはシステム内で無効化され、その UGC が削除されるだけです。However, to delete a user profile from the system, navigate to **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de), locate the user node and delete it.

