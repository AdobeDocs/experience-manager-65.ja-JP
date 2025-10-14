---
title: SRP と UGC の基本事項
description: ストレージリソースプロバイダーとユーザー作成コンテンツの概要
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8279684f-23dd-4234-bf01-fd2ce74bcb4e
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# SRP と UGC の基本事項 {#srp-and-ugc-essentials}

## はじめに {#introduction}

ストレージリソースプロバイダー（SRP）とそのユーザー作成コンテンツ（UGC）との関係に詳しくない場合は、[&#x200B; コミュニティコンテンツストレージ &#x200B;](working-with-srp.md) および [&#x200B; ストレージリソースプロバイダーの概要 &#x200B;](srp.md) を参照してください。

ドキュメントのこの節では、SRP と UGC に関する重要な情報を提供します。

## StorageResourceProvider API {#storageresourceprovider-api}

SocialResourceProvider API （SRP API）は、様々な Sling リソースプロバイダー API の拡張機能です。 ページネーションとアトミックインクリメントのサポートが含まれます（集計とスコアリングに役立ちます）。

日付、有用性、投票数などで並べ替える必要があるので、SCF コンポーネントではクエリが必要です。 すべての SRP オプションには、バケット化に依存しない柔軟なクエリメカニズムがあります。

SRP ストレージの場所には、コンポーネントパスが組み込まれています。 ルートパスは選択した SRP オプション（ASRP、MSRP、JSRP など）に依存するので、SRP API は常に UGC にアクセスするために使用する必要があります。

SRP API は抽象クラスではなく、インターフェイスです。 カスタム実装は慎重に行うべきではありません。新しいリリースにアップグレードすると、内部実装に対する将来の改善のメリットが逃されるからです。

SRP API を使用する手段は、SocialResourceUtilities パッケージにあるような提供されているユーティリティを通じておこなわれます。

AEM 6.0 以前からアップグレードする場合は、すべての SRP について UGC を移行する必要があります。ここでも、Open Source ツールを使用できます。 [AEM Communities 6.3 へのアップグレード &#x200B;](upgrade.md) を参照してください。

>[!NOTE]
>
>これまで、UGC にアクセスするためのユーティリティは、既に存在しない SocialUtils パッケージに含まれていました。
>
>置き換えるユーティリティについては、[SocialUtils リファクタリング &#x200B;](socialutils.md) を参照してください。

## UGC にアクセスするためのユーティリティメソッド {#utility-method-to-access-ugc}

UGC にアクセスするには、SRP から UGC へのアクセスに適したパスを返す SocialResourceUtilities パッケージのメソッドを使用します。このメソッドは、SocialUtils パッケージにある非推奨メソッドを置き換えるものです。

次に、サーブレットで resourceToUGCStoragePath （） メソッドを使用する最小限の例を示します。

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String ugcPath = socialResourceUtilities.resourceToUGCStoragePath(request.getResource());
  // rest of servlet
}
```

その他の SocialUtils の置き換えについては、[SocialUtils のリファクタリング &#x200B;](socialutils.md) を参照してください。

コーディングのガイドラインについては、[SRP による UGC へのアクセス &#x200B;](accessing-ugc-with-srp.md) を参照してください。

>[!CAUTION]
>
>resourceToUGCStoragePath （）が返すパスは *ACL チェックに適していません*[&#128279;](srp.md#for-access-control-acls)。

## ACL にアクセスするためのユーティリティメソッド {#utility-method-to-access-acls}

ASRP や MSRP など、一部の SRP 実装では、ACL 検証を提供しないデータベースにコミュニティコンテンツを保存します。 シャドウノードは、ACL を適用できるローカルリポジトリ内の場所を提供します。

SRP API を使用すると、すべての SRP オプションは、すべての CRUD 操作に先立ってシャドウの場所に対して同じチェックを実行します。

ACL をチェックするには、メソッドを使用して、リソースの UGC に適用される権限をチェックするのに適したパスを返します。

次に、サーブレットで resourceToACLPath （） メソッドを使用する簡単な例を示します。

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String aclPath = socialResourceUtilities.resourceToACLPath(request.getResource());
  // rest of servlet
}
```

>[!CAUTION]
>
>resourceToACLPath （）が返すパスは *UGC へのアクセス [&#x200B; に適していません*](#utility-method-to-access-acls)。

## UGC 関連の保存場所 {#ugc-related-storage-locations}

JSRP または MSRP を使用して開発する場合は、次に示すストレージの場所の説明が役立つ場合があります。 JSRP （[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)）および MSRP （MongoDB ツール）用があるので、現在、ASRP に保存されている UGC にアクセスする UI はありません。

**コンポーネントの場所**

パブリッシュ環境でメンバーが UGC にエントリすると、AEM サイトの一部としてコンポーネントとやり取りされます。

このようなコンポーネントの例として、[&#x200B; コミュニティコンポーネントガイド &#x200B;](http://localhost:4502/content/community-components/en/comments.html) サイトに存在する [&#x200B; コメントコンポーネント &#x200B;](components-guide.md) があります。 ローカルリポジトリのコメントノードへのパスは次のとおりです。

* コンポーネントのパス = `/content/community-components/en/comments/jcr:content/content/includable/comments`

**シャドウノードの場所**

UGC の作成により、必要な ACL が適用される [&#x200B; シャドウノード &#x200B;](srp.md#about-shadow-nodes-in-jcr) も作成されます。 ローカルリポジトリ内の対応するシャドウノードへのパスは、コンポーネントパスのシャドウノードのルートパスを先頭に追加した結果です。

* ルートパス = `/content/usergenerated`
* コメント シャドウ ノード = `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**UGC の場所**

UGC は、これらの場所のいずれでも作成されず、SRP API を呼び出す [&#x200B; ユーティリティメソッド &#x200B;](#utility-method-to-access-ugc) を使用してのみアクセスする必要があります。

* ルートパス = `/content/usergenerated/asi/srp-choice`
* JSRP の UGC ノード = `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*注意*、JSRP の場合、UGC ノードは、入力されたAEM インスタンス *オーサーまたはパブリッシュ）に存在します* のみ）。 パブリッシュインスタンスで入力した場合、オーサー環境のモデレートコンソールからモデレートすることはできません。

## 関連情報 {#related-information}

* [&#x200B; ストレージリソースプロバイダーの概要 &#x200B;](srp.md) – 概要とリポジトリの使用状況の概要。
* [SRP による UGC へのアクセス &#x200B;](accessing-ugc-with-srp.md) - コーディングガイドライン。
* [SocialUtils リファクタリング &#x200B;](socialutils.md) – 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする
