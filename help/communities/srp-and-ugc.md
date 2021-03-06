---
title: SRP と UGC の基本事項
seo-title: SRP と UGC の基本事項
description: ストレージリソースプロバイダーとユーザー生成コンテンツの概要
seo-description: ストレージリソースプロバイダーとユーザー生成コンテンツの概要
uuid: a4ee8725-f554-4fcf-ac1e-34878d6c02f8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0763f236-5648-49e9-8a24-dbc8f4c77ee3
exl-id: 8279684f-23dd-4234-bf01-fd2ce74bcb4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 65%

---

# SRP と UGC の基本事項 {#srp-and-ugc-essentials}

## はじめに {#introduction}

ストレージリソースプロバイダー（SRP）および SRP とユーザー生成コンテンツ（UGC）との関係について詳しくは、[コミュニティコンテンツストレージ](working-with-srp.md)および[ストレージリソースプロバイダーの概要](srp.md)を参照してください。

ドキュメントのこの節では、SRP および UGC に関する基本情報について説明します。

## StorageResourceProvider API  {#storageresourceprovider-api}

SocialResourceProvider API（SRP API）は、様々な Sling リソースプロバイダー API の拡張です。ページネーションとアトミックインクリメントのサポートが含まれます（集計とスコアリングに役立ちます）。

日付、有用性、投票数などによる並べ替えが必要なので、SCF コンポーネントにはクエリが必要です。すべてのSRPオプションには、グループ化に依存しない柔軟なクエリメカニズムがあります。

SRP 格納場所には、コンポーネントのパスが組み込まれます。ルートパスはASRP、MSRP、JSRPなど、選択したSRPオプションに依存するので、SRP APIを常にUGCにアクセスするために使用する必要があります。

SRP API は、抽象クラスではなくインターフェイスです。新しいリリースにアップグレードする際に、内部実装の将来の改善のメリットが失われるので、カスタム実装は軽くおこなわないでください。

SRP API を使用するための手段は、提供されるユーティリティ（SocialResourceUtilities パッケージで見つかるものなど）です。

AEM 6.0 以前からアップグレードする場合、すべての SRP の UGC の移行が必要になります。そのために、オープンソースのツールを使用できます。[AEM Communities 6.3へのアップグレード](upgrade.md)を参照してください。

>[!NOTE]
>
>以前は、UGC にアクセスするためのユーティリティは SocialUtils パッケージ内にありましたが、このパッケージはなくなりました。
>
>代わりのユーティリティについては、[SocialUtils リファクタリング](socialutils.md)を参照してください。

## UGC にアクセスするためのユーティリティメソッド  {#utility-method-to-access-ugc}

UGC にアクセスするには、SRP から UGC へのアクセスに適したパスを返し、SocialUtils にあった廃止されたメソッドに替わる、SocialResourceUtilities パッケージのメソッドを使用します。

以下に、サーブレットでの resourceToUGCStoragePath() メソッドの使用の最小限の例を示します。

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

その他の SocialUtils の代替については、[SocialUtils のリファクタリング](socialutils.md)を参照してください。

コーディングのガイドラインについては、[SRP による UGC へのアクセス](accessing-ugc-with-srp.md)を参照してください。

>[!CAUTION]
>
>resourceToUGCStoragePath() によって返されるパスは、**[ACL チェック](srp.md#for-access-control-acls)には適していません。

## Utility Method to Access ACLs {#utility-method-to-access-acls}

一部の SRP 実装（ASRP や MSRP など）では、コミュニティコンテンツは ACL 検証が提供されないデータベースに格納されます。シャドウノードは、ACLを適用できるローカルリポジトリ内の場所を提供します。

SRP API を使用すると、すべての SRP オプションによって、すべての CRUD 操作の前にシャドウの場所の同じチェックが実行されます。

ACL をチェックするには、リソースの UGC に適用される権限のチェックに適したパスを返すメソッドを使用します。

以下に、サーブレットでの resourceToACLPath() メソッドの使用の単純な例を示します。

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
>resourceToACLPath()から返されるパスは&#x200B;**&#x200B;ではありません。[UGC](#utility-method-to-access-acls)自体にアクセスするのに適しています。

## UGC 関連の格納場所 {#ugc-related-storage-locations}

格納場所に関する以下の説明は、JSRP または MSRP を使用した開発時に役立つ場合があります。現在、JSRP([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md))とMSRP（MongoDBツール）用なので、ASRPに格納されたUGCにアクセスするUIはありません。

**コンポーネントの場所**

メンバーがパブリッシュ環境で UGC を入力する場合、AEM サイトの一部としてのコンポーネントとやり取りしています。

このようなコンポーネントの例として、[コミュニティコンポーネントガイド](components-guide.md)サイトに存在する[コメントコンポーネント](http://localhost:4502/content/community-components/en/comments.html)が挙げられます。 ローカルリポジトリ内のコメントノードへのパスは次のとおりです。

* コンポーネントパス = `/content/community-components/en/comments/jcr:content/content/includable/comments`

**シャドウノードの場所**

UGC の作成によって、必要な ACL が適用される[シャドウノード](srp.md#about-shadow-nodes-in-jcr)も作成されます。ローカルリポジトリ内の対応するシャドウノードへのパスは、シャドウノードのルートパスをコンポーネントのパスに先頭に配置した結果です。

* ルートパス = `/content/usergenerated`
* コメントシャドウノード= `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**UGC の場所**

UGC はこれらの場所のどちらにも作成されず、SRP API を呼び出す[ユーティリティメソッド](#utility-method-to-access-ugc)の使用によってのみアクセスする必要があります。

* ルートパス = `/content/usergenerated/asi/srp-choice`
* JSRPのUGCノード= `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

** JSRP の場合、UGC ノードはそれが入力された AEM インスタンス（オーサーまたはパブリッシュ）上にのみ存在することに注意してください。**&#x200B;パブリッシュインスタンスで入力した場合、オーサーのモデレートコンソールからモデレートはできません。

## 関連情報 {#related-information}

* [ストレージリソースプロバイダーの概要](srp.md)  — 概要とリポジトリの使用方法の概要。
* [SRPによるUGCへのアクセス](accessing-ugc-with-srp.md)  — コーディングのガイドライン
* [SocialUtilsのリファクタリング](socialutils.md)  — 非推奨のユーティリティメソッドを現在のSRPユーティリティメソッドにマッピングします。
