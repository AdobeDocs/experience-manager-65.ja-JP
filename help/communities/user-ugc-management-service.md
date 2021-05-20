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
role: Administrator
exl-id: 526ef0fa-3f20-4de4-8bc5-f435c60df0d0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 37%

---

# AEM Communities のユーザーおよび UGC 管理サービス  {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>以下の節ではGDPRを例として使用しますが、ここで説明する詳細は、すべてのデータ保護およびプライバシー規制に適用されます。（GDPR、CCPAなど）

AEM Communitiesでは、ユーザープロファイルの管理やユーザー生成コンテンツ(UGC)の一括管理をおこなうためのAPIが標準で提供されています。 **UserUgcManagement**&#x200B;サービスを有効にすると、権限を持つユーザー（コミュニティ管理者とモデレーター）は、ユーザープロファイルを無効にし、特定のユーザーに対してUGCを一括削除または一括書き出しできます。 また、これらのAPIを使用すると、顧客データのコントローラーおよびプロセッサーが、欧州連合の一般データ保護規則(GDPR)や、その他のGDPRに触発されたプライバシー要件に準拠できます。

詳しくは、[アドビプライバシーセンターの GDPR ページ](https://www.adobe.com/jp/privacy/general-data-protection-regulation.html)を参照してください。

>[!NOTE]
>
>[AEM Communities 内の Adobe Analytics](/help/communities/analytics.md) サイトを設定している場合は、収集されたユーザーデータが Adobe Analytics サーバーに送信されます。Adobe Analytics は、ユーザーデータのアクセス、書き出し、削除や、GDPR に準拠するための処理をおこなう API を提供しています。詳しくは、[アクセス要求および削除要求の送信](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html)を参照してください。

これらのAPIを使用するには、UserUgcManagementサービスをアクティブ化して`/services/social/ugcmanagement`エンドポイントを有効にする必要があります。 このサービスをアクティブ化するには、[GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)で入手可能な[サンプルサーブレット](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)をインストールします。 次に、次のようなHTTPリクエストを使用して、コミュニティサイトのパブリッシュインスタンスでエンドポイントをヒットします。

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`」を選択します。ただし、システム内のユーザープロファイルとユーザー生成コンテンツを管理するための UI（ユーザーインターフェイス）を構築することもできます。

これらの API で実行できる機能を以下に示します。

## ユーザーの UGC の取得  {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)** は、ユーザーのすべてのUGCをシステムから書き出すのに役立ちます。

* **ユーザー**:ユーザーの認証可能ID。
* **outputStream**:結果は出力ストリームとして返されます。これは、ユーザーが生成したコンテンツ（jsonファイル）と添付ファイル（ユーザーがアップロードした画像やビデオを含む）を含むzipファイルです。

例えば、コミュニティサイトにログインする際の許可可能 ID として weston.mccall@dodgit.com を使用する、Weston McCall という名前のユーザーの UGC を書き出すには、次のような HTTP GET リクエストを送信します。

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## ユーザーの UGC の削除 {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user)** は、ユーザーのすべてのUGCをシステムから削除するのに役立ちます。

* **ユーザー**:ユーザーの認証可能ID。

例えば、認証可能ID weston.mccall@dodgit.comを持つユーザーのUGCをHTTPPOST要求を通じて削除するには、次のパラメーターを使用します。

* ユーザーの = `weston.mccall@dodgit.com`
* 操作 = `deleteUgc`

### Adobe Analytics{#delete-ugc-from-adobe-analytics}からUGCを削除

Adobe Analyticsからユーザーデータを削除するには、[GDPR Analyticsワークフロー](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)に従います。の代わりに、APIはAdobe Analyticsからユーザーデータを削除しません。

AEM Communitiesで使用されるAdobe Analytics変数のマッピングについては、次の画像を参照してください。

![Adobe AnalyticsのAEM communities変数マッピング](assets/analytics-communities-mapping.png)

## ユーザーアカウントの無効化 {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String user)** は、ユーザーアカウントを無効にするのに役立ちます。

* **ユーザー**:ユーザーの認証可能ID。

>[!NOTE]
>
>あるユーザーを無効化すると、そのユーザーがサーバー上で所有しているユーザー生成コンテンツがすべて削除されます。

例えば、認証可能ID `weston.mccall@dodgit.com`を持つユーザーのプロファイルをhttpPOST要求で削除するには、次のパラメーターを使用します。

* ユーザーの = `weston.mccall@dodgit.com`
* 操作 = `deleteUser`

>[!NOTE]
>
>deleteUserAccount() API では、ユーザープロファイルはシステム内で無効化され、その UGC が削除されるだけです。ただし、システムからユーザープロファイルを削除するには、**CRXDE Lite**&#x200B;に移動します。[https://&lt;server>/crx/de](https://localhost:4502/crx/de)で、ユーザーノードを探して削除します。
