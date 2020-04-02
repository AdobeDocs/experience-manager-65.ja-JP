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

---


# コンテンツのプロパティとノード {#content-properties-and-nodes}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

記事、バナーおよびコレクションは、AEM では cq:Pages として表されます。

これらは、すべての cq:Pages に共通するプロパティを共有するとともに、以下に示す Adobe Experience Manager（AEM）Mobile On-Demand Services のメタデータおよび統合をサポートする他のプロパティも備えています。

以下の表では、コンテンツのプロパティとノードについて説明します。

## 共通統合プロパティ {#common-integration-properties}

| **プロパティ名** | **タイプ** | **デフォルトまたは期待値** | **説明** |
|---|---|---|---|
| dps-id | String |  | AEM Mobileにアップロードされたか、AEM Mobileから読み込まれた後、AEMによって割り当てられ、保存されます。 |
| dps-resourceType | String | dps:Article | dps:Banner | dps:Collection | エンティティタイププロパティ |
| dps-version | String |  | AEM Mobileエンティティのバージョン（完全なaemm-idにも含まれます） |
| dps-lastSynced | 日付 |  | AEM MobileからAEMへの最後の同期/読み込みの日付 |
| dps-lastUploaded | 日付 |  | aemからAEM Mobileへの最後のアップロード日 |
| dps-lastUploadedBy | 文字列：userid |  | AEMからAEM Mobileへの最後のアップロード要求を実行したIDユーザー |

## コアメタデータプロパティ {#core-metadata-properties}

| プロパティ名 | タイプ | デフォルトまたは期待値 |
|--- |--- |--- |
| dps-title | String |  |
| dps-shortTitle | String |  |
| dps-abstract | String |  |
| dps-shortAbstract | String |  |
| DPS部門 | String |  |
| dps-カテゴリ | String |  |
| dps-keywords | String[] |  |
| dps-internalKeywords | String[] |  |
| dps-importance | String[] | {&quot;low&quot;、&quot;normal&quot;、&quot;high&quot;}からの重要度 |

### 記事 {#articles}

| **プロパティ名** | **タイプ** | **デフォルトまたは期待値** |
|---|---|---|
| dps-author | String |  |
| dps-authorURL | String |  |
| dps-hideFromBrowsePage | Boolean |  |
| dps-access | String | ProtectedAccess from {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;} |
| **Social** |  |  |
| dps-socialShareURL | String |  |
| dps-articleText | String |  |
| dps-url | String |  |

### バナー {#banners}

| **プロパティ名** | **タイプ** | **デフォルトまたは期待値** |
|---|---|---|
| dps-tapAction |  | {webLink}からのTapAction |
| dps-tapActionUrl |  |  |

### コレクション {#collections}

| プロパティ名 | タイプ | デフォルトまたは期待値 |
|--- |--- |--- |
| dps-productId | String |  |
| dps-readingPosition | String | {&quot;reset&quot;,&quot;retain&quot;}から |
| dps-horizontalSwipe | Boolean |  |
| dps-allowDownload | Boolean |  |
| dps-openDefault | String | {&quot;browsePage&quot;,&quot;contentView&quot;}から |
| dps-layout | String |  |

## コンテンツノード {#content-nodes}

### 共通ノード {#common-nodes}

| ノード名 | タイプ | デフォルトまたは期待値 | 説明 |
|--- |--- |--- |--- |
| image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |

### エンティティ {#entities}

#### 記事 {#articles-1}

| ノード名 | タイプ | 期待値のデフォルト | 説明 |
|--- |--- |--- |--- |
| ソーシャルシェアの画像 |  | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |

#### バナー {#banners-1}

| ノード名 | タイプ | 期待値のデフォルト | 説明 |
|---|---|---|---|
| 該当なし |  |  |  |

#### コレクション {#collections-1}

| ノード名 | タイプ | 期待値のデフォルト | 説明 |
|--- |--- |--- |--- |
| background-image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
