---
title: SRP と UGC の基本事項
description: ストレージリソースプロバイダーとユーザー生成コンテンツの概要
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8279684f-23dd-4234-bf01-fd2ce74bcb4e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# SRP と UGC の基本事項 {#srp-and-ugc-essentials}

## はじめに {#introduction}

ストレージリソースプロバイダー (SRP) とユーザー生成コンテンツ (UGC) との関係に慣れていない場合は、にアクセスします。 [コミュニティコンテンツストレージ](working-with-srp.md) および [ストレージリソースプロバイダの概要](srp.md).

この節では、SRP と UGC に関する重要な情報を提供します。

## StorageResourceProvider API {#storageresourceprovider-api}

SocialResourceProvider API(SRP API) は、様々な Sling リソースプロバイダー API の拡張です。 ページネーションとアトミックな増分のサポートが含まれます（集計とスコアリングに役立ちます）。

日付、有用性、投票数などで並べ替える必要があるので、SCF コンポーネントにはクエリが必要です。 すべての SRP オプションには、バケット化に依存しない柔軟なクエリメカニズムがあります。

SRP ストレージの場所には、コンポーネントのパスが組み込まれます。 SRP API は常に UGC にアクセスするために使用する必要があります。ルートパスは、ASRP、MSRP、JSRP など、選択した SRP オプションに応じて異なるからです。

SRP API は抽象クラスではなく、インターフェイスです。 新しいリリースにアップグレードする際に、内部実装に対する今後の改善のメリットが失われるので、カスタム実装を軽くおこなわないでください。

SRP API を使用する手段は、 SocialResourceUtilities パッケージに含まれるユーティリティなど、提供されているユーティリティを通じて提供されます。

AEM 6.0 以前からアップグレードする場合は、オープンソースツールを使用できるすべての SRP に対して UGC を移行する必要があります。 詳しくは、 [AEM Communities 6.3 へのアップグレード](upgrade.md).

>[!NOTE]
>
>以前は、UGC にアクセスするユーティリティは SocialUtils パッケージに含まれていましたが、これはもはや存在していませんでした。
>
>代替ユーティリティについては、 [SocialUtils のリファクタリング](socialutils.md).

## UGC にアクセスするためのユーティリティメソッド {#utility-method-to-access-ugc}

UGC にアクセスするには、 SocialResourceUtilities パッケージのメソッドを使用します。このメソッドは、SRP から UGC にアクセスするのに適したパスを返し、 SocialUtils パッケージにある廃止されたメソッドを置き換えます。

次に、サーブレットで resourceToUGCStoragePath() メソッドを使用する最小の例を示します。

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

その他の SocialUtils の置き換えについては、 [SocialUtils のリファクタリング](socialutils.md).

コーディングのガイドラインについては、 [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>resourceToUGCStoragePath() が返すパスは次のとおりです。 *not* ～に適している [ACL チェック](srp.md#for-access-control-acls).

## ACL にアクセスするためのユーティリティメソッド {#utility-method-to-access-acls}

ASRP や MSRP などの一部の SRP 実装では、ACL 検証を提供しないデータベースにコミュニティコンテンツを格納します。 シャドウノードは、ACL を適用できるローカルリポジトリ内の場所を提供します。

SRP API を使用すると、すべての SRP オプションで、すべての CRUD 操作の前に、シャドウの場所が同じにチェックされます。

ACL を確認するには、リソースの UGC に適用される権限の確認に適したパスを返すメソッドを使用します。

次に、サーブレットで resourceToACLPath() メソッドを使用する簡単な例を示します。

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
>resourceToACLPath() が返すパスは次のとおりです。 *not* ～に適している [UGC へのアクセス](#utility-method-to-access-acls) それ自体。

## UGC 関連のストレージの場所 {#ugc-related-storage-locations}

JSRP または MSRP を使用して開発する場合は、ストレージの場所に関する次の説明が役立つ場合があります。 現在、JSRP ([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)) および MSRP（MongoDB ツール）

**コンポーネントの場所**

メンバーがパブリッシュ環境で UGC に入ると、メンバーはAEMサイトの一部としてコンポーネントとやり取りします。

このようなコンポーネントの例として、 [コメントコンポーネント](http://localhost:4502/content/community-components/en/comments.html) が [コミュニティコンポーネントガイド](components-guide.md) サイト。 ローカルリポジトリ内のコメントノードへのパスは次のとおりです。

* コンポーネントのパス= `/content/community-components/en/comments/jcr:content/content/includable/comments`

**シャドウノードの場所**

UGC を作成すると、 [シャドウノード](srp.md#about-shadow-nodes-in-jcr) 必要な ACL が適用される ローカルリポジトリ内の対応するシャドウノードへのパスは、シャドウノードのルートパスの前にコンポーネントパスのパスを付けた結果です。

* ルートパス= `/content/usergenerated`
* コメントのシャドウノード= `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**UGC の場所**

UGC は、これらの場所のどちらにも作成されず、 [実用法](#utility-method-to-access-ugc) SRP API を呼び出す

* ルートパス= `/content/usergenerated/asi/srp-choice`
* JSRP =の UGC ノード `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*注意* JSRP の場合、UGC ノードは *のみ* が、入力されたAEMインスタンス（オーサーまたはパブリッシュ）上に存在する。 パブリッシュインスタンスで入力した場合、作成者のモデレートコンソールからモデレートを実行することはできません。

## 関連情報 {#related-information}

* [ストレージリソースプロバイダの概要](srp.md)  — の概要とリポジトリの使用の概要。
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングのガイドライン。
* [SocialUtils のリファクタリング](socialutils.md)  — 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングします。
