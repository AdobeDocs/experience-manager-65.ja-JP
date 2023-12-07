---
title: コンテンツのプロパティとノード
description: このページでは、コンテンツのプロパティとノードについて説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 05c8c846-69cc-4075-9149-33890b3d1e08
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 23%

---

# コンテンツのプロパティとノード {#content-properties-and-nodes}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

記事、バナー、コレクションは、AEMでは cq:Pages として表されます。

これらは、任意の cq:Page で見つかる共通のプロパティに加えて、Adobe Experience Manager(AEM)Mobile On-Demand サービスのメタデータおよび統合サポートプロパティを表す他のいくつかの共通のプロパティを共有します。

次の表に、コンテンツのプロパティとノードを示します。

## 共通の統合プロパティ {#common-integration-properties}

| **プロパティ名** | **タイプ** | **デフォルト値または期待値** | **説明** |
|---|---|---|---|
| dps-id | 文字列 |  | AEM Mobileに割り当てられ、AEMによって保存され、AEM MobileにアップロードまたはAEM Mobileから読み込まれた後にによって割り当てられ、 |
| dps-resourceType | 文字列 | dps:Article | dps:Banner | dps:Collection | エンティティタイププロパティ |
| dps-version | 文字列 |  | AEM Mobileエンティティのバージョン（aem-id の完全な内部にも含まれる） |
| dps-lastSynced | 日付 |  | AEM MobileからAEMへの最後の同期/インポート日 |
| dps-lastUploaded | 日付 |  | AEMからAEM Mobileへの最後のアップロード日 |
| dps-lastUploadedBy | String:userid |  | AEMからAEM Mobileへの最後のアップロード要求を実行した id ユーザー |

## コアメタデータのプロパティ {#core-metadata-properties}

| プロパティ名 | タイプ | デフォルト値または期待値 |
|--- |--- |--- |
| dps-title | 文字列 |  |
| dps-shortTitle | 文字列 |  |
| dps-abstract | 文字列 |  |
| dps-shortAbstract | 文字列 |  |
| dps-department | 文字列 |  |
| dps-category | 文字列 |  |
| dps-keywords | 文字列[] |  |
| dps-internalKeywords | 文字列[] |  |
| dps-importance | 文字列[] | {&quot;low&quot;, &quot;normal&quot;, &quot;high&quot;} からの重要度 |

### 記事 {#articles}

| **プロパティ名** | **タイプ** | **デフォルト値または期待値** |
|---|---|---|
| dps-author | 文字列 |  |
| dps-authorURL | 文字列 |  |
| dps-hideFromBrowsePage | ブーリアン |  |
| dps-access | 文字列 | {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;} からの ProtectedAccess |
| **Social** |  |  |
| dps-socialShareURL | 文字列 |  |
| dps-articleText | 文字列 |  |
| dps-url | 文字列 |  |

### バナー {#banners}

| **プロパティ名** | **タイプ** | **デフォルト値または期待値** |
|---|---|---|
| dps-tapAction |  | 次の TapAction {webLink} |
| dps-tapActionUrl |  |  |

### コレクション {#collections}

| プロパティ名 | タイプ | デフォルト値または期待値 |
|--- |--- |--- |
| dps-productId | 文字列 |  |
| dps-readingPosition | 文字列 | {&quot;reset&quot;,&quot;retain&quot;} から |
| dps-horizontalSwipe | ブーリアン |  |
| dps-allowDownload | ブーリアン |  |
| dps-openDefault | 文字列 | {&quot;browsePage&quot;,&quot;contentView&quot;} から |
| dps-layout | 文字列 |  |

## コンテンツノード {#content-nodes}

### 共通ノード {#common-nodes}

| ノード名 | タイプ | デフォルト値または期待値 | 説明 |
|--- |--- |--- |--- |
| 画像 | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |

### エンティティ {#entities}

#### 記事 {#articles-1}

| ノード名 | タイプ | 期待値のデフォルト | 説明 |
|--- |--- |--- |--- |
| social-share-image |  | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |

#### バナー {#banners-1}

| ノード名 | タイプ | 期待値のデフォルト | 説明 |
|---|---|---|---|
| 該当なし |  |  |  |

#### コレクション {#collections-1}

| ノード名 | タイプ | 期待値のデフォルト | 説明 |
|--- |--- |--- |--- |
| background-image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
