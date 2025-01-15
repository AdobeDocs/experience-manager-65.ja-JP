---
title: コンテンツのプロパティとノード
description: このページでは、コンテンツのプロパティとノードについて説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 05c8c846-69cc-4075-9149-33890b3d1e08
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 24%

---

# コンテンツのプロパティとノード {#content-properties-and-nodes}

{{ue-over-mobile}}

記事、バナーおよびコレクションは、AEMでは cq:Pages として表されます。

これらは、Adobe Experience Manager（AEM） Mobile On-Demand Services のメタデータと統合に関するサポートプロパティを表す、以下に示すいくつかのプロパティに加えて、cq:Page で見つかるのと同じ共通プロパティを共有します。

次の表に、コンテンツのプロパティとノードを示します。

## 共通の統合プロパティ {#common-integration-properties}

| **プロパティ名** | **タイプ** | **デフォルトまたは想定される値** | **説明** |
|---|---|---|---|
| dps-id | 文字列 |  | AEM Mobileによって割り当てられ、AEM Mobileにアップロードされた後、またはAEM Mobileから読み込まれた後にAEMによって保存されます |
| dps-resourceType | 文字列 | dps:Article | dps:Banner | dps:Collection | エンティティタイププロパティ |
| dps-version | 文字列 |  | AEM Mobile エンティティのバージョン （完全な aemm-id 内にも含まれる） |
| dps-lastSynced | 日付 |  | AEM MobileからAEMへの最終同期/ インポート日 |
| dps-lastUploaded | 日付 |  | AEMからAEM Mobileへの最終アップロード日 |
| dps-lastUploadedBy | String:userid |  | AEMからAEM Mobileへの最後のアップロードリクエストを実行した id ユーザー |

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

| **プロパティ名** | **タイプ** | **デフォルトまたは想定される値** |
|---|---|---|
| dps-author | 文字列 |  |
| dps-authorURL | 文字列 |  |
| dps-hideFromBrowsePage | ブール値 |  |
| dps-access | 文字列 | {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;} からの ProtectedAccess |
| **ソーシャル** |  |  |
| dps-socialShareURL | 文字列 |  |
| dps-articleText | 文字列 |  |
| dps-url | 文字列 |  |

### バナー {#banners}

| **プロパティ名** | **タイプ** | **デフォルトまたは想定される値** |
|---|---|---|
| dps-tapAction |  | {webLink} の TapAction |
| dps-tapActionUrl |  |  |

### コレクション {#collections}

| プロパティ名 | タイプ | デフォルト値または期待値 |
|--- |--- |--- |
| dps-productId | 文字列 |  |
| dps-readingPosition | 文字列 | {&quot;reset&quot;,&quot;retain&quot;} から |
| dps-horizontalSwipe | ブール値 |  |
| dps-allowDownload | ブール値 |  |
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
| ソーシャル共有イメージ |  | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |

#### バナー {#banners-1}

| ノード名 | タイプ | 期待値のデフォルト | 説明 |
|---|---|---|---|
| 該当なし |  |  |  |

#### コレクション {#collections-1}

| ノード名 | タイプ | 期待値のデフォルト | 説明 |
|--- |--- |--- |--- |
| background-image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
