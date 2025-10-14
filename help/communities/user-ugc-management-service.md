---
title: AEM Communities のユーザーおよび UGC 管理サービス
description: API を使用して、ユーザー生成コンテンツを一括削除および一括書き出しし、ユーザーアカウントを無効にします。
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
docset: aem65
role: Admin
exl-id: 526ef0fa-3f20-4de4-8bc5-f435c60df0d0
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 10%

---

# AEM Communities のユーザーおよび UGC 管理サービス {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>以下の節では GDPR を例として使用していますが、詳細はすべてのデータ保護およびプライバシー規制（GDPR、CCPA など）に適用できます。

AEM Communitiesは、ユーザープロファイルを管理したり、ユーザー生成コンテンツ（UGC）を一括管理したりするための API を標準で公開しています。 有効にすると、**UserUgcManagement** サービスを使用して、権限のあるユーザー（コミュニティ管理者とモデレーター）はユーザープロファイルを無効にしたり、特定のユーザーの UGC を一括削除または一括書き出ししたりできます。 また、これらの API により、顧客データの管理者や処理者は、欧州連合（EU）の一般データ保護規則（GDPR）や、GDPR に影響を受けたその他のプライバシー要件に準拠することができます。

詳しくは、[アドビプライバシーセンターの GDPR ページ](https://www.adobe.com/jp/privacy/general-data-protection-regulation.html)を参照してください。

>[!NOTE]
>
>AEM Communities[&#128279;](/help/communities/analytics.md) サイトで Adobe Analyticsを設定した場合、取り込んだユーザーデータはAdobe Analytics サーバーに送信されます。 Adobe Analyticsは、ユーザーデータへのアクセス、書き出し、削除と、GDPR への準拠を可能にする API を提供します。 詳しくは、[&#x200B; アクセスリクエストと削除リクエストの送信 &#x200B;](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html?lang=ja) を参照してください。

これらの API を使用するには、UserUgcManagement サービスをアクティベートして、`/services/social/ugcmanagement` エンドポイントを有効にする必要があります。 このサービスをアクティブにするには、[GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) で利用可能な [&#x200B; サンプルサーブレット &#x200B;](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) をインストールします。 次に、http リクエストを使用して、次のような適切なパラメーターを使用して、communities サイトのパブリッシュインスタンスのエンドポイントにアクセスします。

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`といったアドバイスを耳にしたことがある方もいるでしょう。ただし、UI （ユーザーインターフェイス）を構築して、システム内のユーザープロファイルとユーザー生成コンテンツを管理することもできます。

これらの API により、次の機能を実行できます。

## ユーザーの UGC の取得 {#retrieve-the-ugc-of-a-user}

**getUserUgc （ResourceResolver resourceResolver, String user, OutputStream outputStream）** は、システムからユーザーのすべての UGC を書き出すのに役立ちます。

* **ユーザー**：ユーザーの許可可能な ID。
* **outputStream**：結果は、出力ストリームとして返されます。出力ストリームとは、ユーザーが生成したコンテンツ（json ファイル）と添付ファイル（ユーザーがアップロードした画像やビデオを含む）を含んだ zip ファイルです。

例えば、Weston McCall というユーザーの UGC を書き出し、認証可能な ID としてweston.mccall@dodgit.comを使用して Communities サイトにログインする場合、次のような http GETリクエストを送信できます。

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## ユーザーの UGC の削除 {#delete-the-ugc-of-a-user}

**deleteUserUgc （ResourceResolver resourceResolver, String user）** ユーザーのすべての UGC をシステムから削除するのに役立ちます。

* **ユーザー**：ユーザーの認証可能な ID。

例えば、認証可能な ID weston.mccall@dodgit.comを持つユーザーの UGC を http POSTリクエストによって削除したい場合、以下のパラメーターを使用してください。

* ユーザー= `weston.mccall@dodgit.com`
* operation = `deleteUgc`

### Adobe Analyticsからの UGC の削除 {#delete-ugc-from-adobe-analytics}

API はAdobe Analyticsからユーザーデータを削除しないので、Adobe Analyticsからユーザーデータを削除するには、[GDPR 分析ワークフロー &#x200B;](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html?lang=ja) に従います。

AEM Communitiesで使用されるAdobe Analytics変数のマッピングについては、次の図を参照してください。

![Adobe AnalyticsのAEM communities 変数マッピング &#x200B;](assets/analytics-communities-mapping.png)

## ユーザーアカウントの無効化 {#disable-a-user-account}

**deleteUserAccount （ResourceResolver resourceResolver, String user）** は、ユーザーアカウントを無効にするのに役立ちます。

* **ユーザー**：ユーザーの認証可能な ID。

>[!NOTE]
>
>ユーザーを無効にすると、サーバー上でそのユーザーが持つすべてのユーザー生成コンテンツが削除されます。

例えば、http POSTリクエストを通じて認証可能な ID `weston.mccall@dodgit.com` を持つユーザーのプロファイルを削除するには、次のパラメーターを使用します。

* ユーザー= `weston.mccall@dodgit.com`
* operation = `deleteUser`

>[!NOTE]
>
>deleteUserAccount （） API は、システムでユーザープロファイルを無効にするだけで、UGC を削除します。 ただし、システムからユーザープロファイルを削除するには、**server**: [https://&lt;CRXDE Lite>/crx/de](https://localhost:4502/crx/de) に移動し、ユーザーノードを見つけて削除します。
