---
title: コンテンツのプロパティとノード
seo-title: コンテンツのプロパティとノード
description: このページでは、コンテンツのプロパティとノードについて説明します。
seo-description: このページでは、コンテンツのプロパティとノードについて説明します。
uuid: 2dad52c8-5b6c-4b90-8498-62217a9a27fc
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: f5721ddc-df5c-496c-be61-38d1cab63ad4
translation-type: tm+mt
source-git-commit: 50c0bdfc3203410d392e53536bc7cd00245406e5
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 51%

---


# コンテンツのプロパティとノード  {#content-properties-and-nodes}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

記事、バナーおよびコレクションは、AEM では cq:Pages として表されます。

これらは、すべての cq:Pages に共通するプロパティを共有するとともに、以下に示す Adobe Experience Manager（AEM）Mobile On-Demand Services のメタデータおよび統合をサポートする他のプロパティも備えています。

以下の表では、コンテンツのプロパティとノードについて説明します。

## 共通統合プロパティ  {#common-integration-properties}

| **プロパティ名** | **型** | **デフォルト値または期待値** | **説明** |
|---|---|---|---|
| dps-id | String |  | aem mobileによって割り当てられ、1度AEM MobileにアップロードされるかAEM Mobileから輸入され、AEMによって保管される |
| dps-resourceType | 文字列 | dps:Article | dps:Banner | dps:Collection | entity typeプロパティ |
| dps-version | 文字列 |  | aem mobileエンティティのバージョン（完全なaemm-idに含まれる） |
| dps-lastSynced | 日付 |  | aem mobileからAEMへの最後の同期/インポートの日付 |
| dps-lastUploaded | 日付 |  | aemからAEM Mobileへの最後のアップロード日 |
| dps-lastUploadedBy | String:userid |  | aemからAEM Mobileへの最後のアップロード要求を実行したidユーザー |

## コアメタデータプロパティ {#core-metadata-properties}

| プロパティ名 | 型 | デフォルト値または期待値 |
|--- |--- |--- |
| dps-title | 文字列 |  |
| dps-shortTitle | 文字列 |  |
| dps-abstract | 文字列 |  |
| dps-shortAbstract | 文字列 |  |
| dps-department | 文字列 |  |
| dps-カテゴリ | 文字列 |  |
| dps-keywords | String[] |  |
| dps-internalKeywords | 文字列[] |  |
| dps-importance | 文字列[] | {&quot;low&quot;、&quot;normal&quot;、&quot;high&quot;}からの重要度 |

### 記事 {#articles}

| **プロパティ名** | **型** | **デフォルト値または期待値** |
|---|---|---|
| dps-author | 文字列 |  |
| dps-authorURL | 文字列 |  |
| dps-hideFromBrowsePage | Boolean |  |
| dps-access | 文字列 | ProtectedAccess from {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;} |
| **Social** |  |  |
| dps-socialShareURL | 文字列 |  |
| dps-articleText | 文字列 |  |
| dps-url | 文字列 |  |

### バナー {#banners}

| **プロパティ名** | **型** | **デフォルト値または期待値** |
|---|---|---|
| dps-tapAction |  | {webLink}からのTapAction |
| dps-tapActionUrl |  |  |

### コレクション {#collections}

| プロパティ名 | 型 | デフォルト値または期待値 |
|--- |--- |--- |
| dps-productId | 文字列 |  |
| dps-readingPosition | 文字列 | {&quot;reset&quot;,&quot;retain&quot;}から |
| dps-horizontalSwipe | ブール値 |  |
| dps-allowDownload | ブール値 |  |
| dps-openDefault | 文字列 | {&quot;browsePage&quot;,&quot;contentView&quot;}から |
| dps-layout | 文字列 |  |

## コンテンツノード {#content-nodes}

### 共通ノード {#common-nodes}

| ノード名 | 型 | デフォルト値または期待値 | 説明 |
|--- |--- |--- |--- |
| 画像 | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |

### エンティティ {#entities}

#### 記事 {#articles-1}

| ノード名 | 型 | 期待値のデフォルト | 説明 |
|--- |--- |--- |--- |
| ソーシャルシェアの画像 |  | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |

#### バナー {#banners-1}

| ノード名 | 型 | 期待値のデフォルト | 説明 |
|---|---|---|---|
| 該当なし |  |  |  |

#### コレクション {#collections-1}

| ノード名 | 型 | 期待値のデフォルト | 説明 |
|--- |--- |--- |--- |
| background-image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
