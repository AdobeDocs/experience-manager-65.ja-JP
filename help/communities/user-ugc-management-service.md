---
title: AEM Communities のユーザーおよび UGC 管理サービス
description: APIを使用して、ユーザー生成コンテンツを一括削除および一括書き出し、ユーザーアカウントを無効にします。
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
docset: aem65
role: Admin
exl-id: 526ef0fa-3f20-4de4-8bc5-f435c60df0d0
solution: Experience Manager
feature: Communities
source-git-commit: f4fc3b788d4128135ff77ebb87f1369059b1d2ec
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 5%

---

# AEM Communities のユーザーおよび UGC 管理サービス {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>以下のセクションではGDPRを例として使用しますが、説明されている詳細は、GDPR、CCPAなどのすべてのデータ保護およびプライバシー規制に適用されます。

AEM Communitiesでは、すぐに利用できるAPIを通じてユーザーのプロファイルを管理し、ユーザー生成コンテンツ（UGC）を一括管理できます。 **UserUgcManagement** サービスを有効にすると、特権ユーザー（コミュニティ管理者およびモデレーター）はユーザープロファイルを無効にし、特定のユーザーのUGCを一括削除または一括書き出しできます。 これらのAPIを使用すれば、顧客データの管理者や処理者は、欧州連合（EU）の一般データ保護規則（GDPR）などのGDPRにもとづいたプライバシー義務を遵守できます。

詳しくは、Adobe Privacy Centerの[GDPR ページを参照してください。](https://www.adobe.com/jp/privacy/general-data-protection-regulation.html)

>[!NOTE]
>
>AEM Communities](/help/communities/analytics.md) サイトで[Adobe Analyticsを設定した場合、キャプチャしたユーザーデータはAdobe Analytics サーバーに送信されます。 Adobe Analyticsには、ユーザーデータへのアクセス、書き出し、削除をおこない、GDPRに準拠するためのAPIが用意されています。 詳細については、[ アクセス要求と削除要求の送信](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html)を参照してください。

これらのAPIを使用するには、UserUgcManagement サービスをアクティブ化して`/services/social/ugcmanagement` エンドポイントを有効にする必要があります。 このサービスをアクティブにするには、[GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)で利用可能な[ サンプルサーブレット ](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)をインストールします。 次に、次のようなhttp リクエストを使用して、コミュニティサイトのパブリッシュインスタンスのエンドポイントを適切なパラメーターでクリックします。

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. ただし、ユーザープロファイルとユーザー生成コンテンツをシステムで管理するUI （ユーザーインターフェイス）を構築することもできます。

これらのAPIを使用すると、次の機能を実行できます。

## ユーザーのUGCの取得 {#retrieve-the-ugc-of-a-user}

**getUserUgc （ResourceResolver resourceResolver, String user, OutputStream outputStream）**&#x200B;は、ユーザーのすべてのUGCをシステムからエクスポートするのに役立ちます。

* **user**: ユーザーの承認可能なID。
* **outputStream**：結果は出力ストリームとして返されます。これは、ユーザーが生成したコンテンツ（json ファイル）と添付ファイル（ユーザーがアップロードした画像またはビデオを含む）を含むzip ファイルです。

例えば、Weston McCallという名前のユーザーのUGCをエクスポートし、weston.mccall@dodgit.comを認証可能なIDとして使用してコミュニティサイトにログインする場合、次のようなhttp GET リクエストを送信できます。

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## ユーザーのUGCの削除 {#delete-the-ugc-of-a-user}

**deleteUserUgc （ResourceResolver resourceResolver, String user）**&#x200B;は、ユーザーのすべてのUGCをシステムから削除するのに役立ちます。

* **user**: ユーザーの承認可能なID。

例えば、許可IDが`weston.mccall@dodgit.com`のユーザーのUGCをhttp-POST リクエストを通じて削除するには、次のパラメーターを使用します。

* ユーザー= `weston.mccall@dodgit.com`
* 操作= `deleteUgc`

### Adobe AnalyticsからUGCを削除する {#delete-ugc-from-adobe-analytics}

Adobe Analyticsからユーザーデータを削除するには、APIはAdobe Analyticsからユーザーデータを削除しないため、[GDPR Analytics ワークフロー](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html?lang=ja)に従います。

AEM Communitiesで使用されるAdobe Analytics変数マッピングについては、次の図を参照してください。

![Adobe AnalyticsのAEM communities変数マッピング ](assets/analytics-communities-mapping.png)

## ユーザーアカウントの無効化 {#disable-a-user-account}

**deleteUserAccount （ResourceResolver resourceResolver, String user）**&#x200B;は、ユーザーアカウントの無効化に役立ちます。

* **user**: ユーザーの承認可能なID。

>[!NOTE]
>
>ユーザーを無効にすると、ユーザーがサーバー上に持つすべてのユーザー生成コンテンツが削除されます。

例えば、許可IDが`weston.mccall@dodgit.com`のユーザーのプロファイルをhttp-POST リクエストで削除するには、次のパラメーターを使用します。

* ユーザー= `weston.mccall@dodgit.com`
* 操作= `deleteUser`

>[!NOTE]
>
>`deleteUserAccount()` APIは、システム内のユーザープロファイルのみを無効にし、UGCを削除します。 ただし、システムからユーザープロファイルを削除するには、`https://<server>:<port>/crx/de`の&#x200B;**CRXDE Lite**&#x200B;に移動し、ユーザーノードを見つけて削除します。
