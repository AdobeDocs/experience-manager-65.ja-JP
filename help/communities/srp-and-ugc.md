---
title: SRP と UGC の基本事項
description: ストレージリソースプロバイダーとユーザー生成コンテンツの概要
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8279684f-23dd-4234-bf01-fd2ce74bcb4e
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%
---
# SRP と UGC の基本事項 {#srp-and-ugc-essentials}

## はじめに {#introduction}

ストレージリソースプロバイダー（SRP）と、ユーザー生成コンテンツ（UGC）との関係についてご存じない場合は、[ コミュニティコンテンツストレージ ](working-with-srp.md)および[ ストレージリソースプロバイダーの概要](srp.md)にアクセスしてください。

このセクションでは、SRPとUGCに関する重要な情報を提供します。

## StorageResourceProvider API {#storageresourceprovider-api}

SocialResourceProvider API （SRP API）は、様々なSling リソースプロバイダーAPIの拡張機能です。 ページネーションとアトミックインクリメントのサポートが含まれています（集計とスコアリングに役立ちます）。

SCF コンポーネントには、日付、有用性、投票数などで並べ替える必要があるため、クエリが必要です。 すべてのSRP オプションには、バケットに依存しない柔軟なクエリメカニズムがあります。

SRP ストレージの場所には、コンポーネントパスが組み込まれています。 ルートパスは、ASRP、MSRP、JSRPなど、選択したSRP オプションに依存するため、SRP APIを常に使用してUGCにアクセスする必要があります。

SRP APIは抽象クラスではなく、インターフェイスです。 カスタム実装は、新しいリリースにアップグレードする際に内部実装を改善するメリットを逃すため、軽く実行すべきではありません。

SRP APIを使用する手段は、SocialResourceUtilities パッケージに含まれている提供されたユーティリティを使用します。

AEM 6.0以前からアップグレードする場合は、Open Source ツールを使用できるすべてのSRPにUGCを移行する必要があります。 [AEM Communities 6.3](upgrade.md)へのアップグレードを参照してください。

>[!NOTE]
>
>従来、UGCにアクセスするためのユーティリティは、SocialUtils パッケージに含まれていましたが、このパッケージは既に存在しません。
>
>代替ユーティリティについては、[SocialUtils リファクタリング ](socialutils.md)を参照してください。

## UGCへのアクセス方法 {#utility-method-to-access-ugc}

UGCにアクセスするには、SocialResourceUtilities パッケージのメソッドを使用します。このメソッドは、SRPからUGCにアクセスするのに適したパスを返し、SocialUtils パッケージにある非推奨のメソッドを置き換えます。

次に、サーブレットでresourceToUGCStoragePath （） メソッドを使用する簡単な例を示します。

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

その他のSocialUtilsの置換については、[SocialUtils リファクタリング ](socialutils.md)を参照してください。

コーディングガイドラインについては、[SRPを使用したUGCへのアクセス ](accessing-ugc-with-srp.md)を参照してください。

>[!CAUTION]
>
>resourceToUGCStoragePath （）が返すパスは&#x200B;*not*&#x200B;です。[ACLの確認](srp.md#for-access-control-acls)に適しています。

## ACLにアクセスするためのユーティリティメソッド {#utility-method-to-access-acls}

ASRPやMSRPなどの一部のSRP実装では、ACL検証を提供しないデータベースにコミュニティ コンテンツを保存します。 シャドウノードは、ACLを適用できるローカルリポジトリ内の場所を提供します。

SRP APIを使用すると、すべてのSRP オプションは、すべてのCRUD操作の前にシャドウの場所を同じようにチェックします。

ACLをチェックするには、リソースのUGCに適用される権限のチェックに適したパスを返すメソッドを使用します。

次に、サーブレットでresourceToACLPath （） メソッドを使用する簡単な例を示します。

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
>resourceToACLPath （）によって返されるパスは、*not*&#x200B;です。これは、[UGC](#utility-method-to-access-acls)自体へのアクセスに適しています。

## UGC関連の保存場所 {#ugc-related-storage-locations}

ストレージの場所に関する以下の説明は、JSRPまたは場合によってはMSRPを使用して開発する際に役立つ可能性があります。 JSRP （[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)）およびMSRP （MongoDB ツール）に対して、ASRPに格納されているUGCにアクセスするためのUIは現在存在しません。

**コンポーネントの場所**

メンバーがパブリッシュ環境でUGCを開始すると、AEM サイトの一部としてコンポーネントと対話します。

このようなコンポーネントの例として、[ コミュニティコンポーネントガイド ](components-guide.md) サイトに存在する[ コメント コンポーネント ](http://localhost:4502/content/community-components/en/comments.html)があります。 ローカルリポジトリ内のコメントノードへのパスは次のとおりです。

* コンポーネント パス = `/content/community-components/en/comments/jcr:content/content/includable/comments`

**シャドウ ノードの場所**

UGCを作成すると、必要なACLが適用される[ シャドウ ノード ](srp.md#about-shadow-nodes-in-jcr)も作成されます。 ローカルリポジトリ内の対応するシャドウノードへのパスは、コンポーネントパスにシャドウノードルートパスを追加した結果です。

* ルート パス = `/content/usergenerated`
* コメント シャドウ ノード = `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**UGCの場所**

UGCは、どちらの場所にも作成されず、SRP APIを呼び出す[ ユーティリティメソッド ](#utility-method-to-access-ugc)を使用してのみアクセスする必要があります。

* ルート パス = `/content/usergenerated/asi/srp-choice`
* JSRPのUGC ノード = `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*注意*&#x200B;してください。JSRPの場合、UGC ノードは&#x200B;*のみ*&#x200B;が入力されたAEM インスタンス（オーサーまたはパブリッシュのいずれか）に存在します。 パブリッシュインスタンスに入力した場合、オーサーのモデレーションコンソールからモデレーションを実行できません。

## 関連する情報 {#related-information}

* [ ストレージリソースプロバイダーの概要](srp.md) – 概要とリポジトリの使用状況の概要。
* [SRPを使用したUGCへのアクセス ](accessing-ugc-with-srp.md) - コーディング ガイドライン。
* [SocialUtils リファクタリング ](socialutils.md) – 非推奨のユーティリティメソッドを現在のSRP ユーティリティメソッドにマッピングします。
