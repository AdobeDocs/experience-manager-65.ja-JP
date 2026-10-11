---
title: SocialUtils のリファクタリング
description: パッケージ com.adobe.cq.social.ugcbase.SocialUtilsはAEM 6.1で廃止されました
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 3%
---
# SocialUtils のリファクタリング {#socialutils-refactoring}

## SocialUtils パッケージの非推奨（廃止予定） {#socialutils-package-deprecated}

パッケージ `com.adobe.cq.social.ugcbase.SocialUtils`はAEM 6.1で非推奨（廃止予定）となりました。

次の表に、`SocialUtils` メソッドの代わりに使用するメソッドを示します。

## SocialResourceUtilities パッケージ  {#socialresourceutilities-package}

| com.adobe.cq.social.srp.utilities.api.SocialResourceUtilitiesのメソッド | メモ |
|---|---|
| Boolean checkPermission （ResourceResolver resolver, String path, String action） |  |
| SocialResourceProvider getSocialResourceProvider （リソース） |  |
| SocialResourceConfiguration getStorageConfig （リソース） |  |
| リソース getUGCResource （リソース userResource） |  |
| Resource getUGCResource （Resource userResource, ResourceResolverFactory rrf） | 新規 |
| Resource getUGCResource （Resource userResource, ResourceResolverFactory rrf, String resourceTypeHint） | 新規 |
| Resource getUGCResource （Resource userResource, String resourceTypeHint） |  |
| boolean hasModeratePermissions （Resource resource） |  |
| String resourceToACLPath （Resource resource） |  |
| String resourceToUGCStoragePath （Resource resource） | 文字列resourceToUGCPath （Resource resource）を置換します。 |
| 文字列UGCToResourcePath （リソース リソース リソース） |  |
| String UGCToResourcePath （String ugcPath） | メソッド署名が変更されました |
| String UGCToResourcePath （String ugcPath, ResourceResolver resolver） | 新規 |

| `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilitiesのメソッド | メモ |
|---|---|
| SocialResourceProvider getSocialResourceProvider （リソース） | socialResourceProvider getConfiguredProvider （リソース リソース リソース）を置き換えます。 |

## SCFUtilities パッケージ {#scfutilities-package}

| `com.adobe.cq.social.`utilities.scf.api.SCFUtilitesのメソッド |
|---|
| String getAvatar （UserProperties userProperties） |
| String getAvatar （UserProperties userProperties, int size） |
| String getAvatar （UserProperties userProperties, String absoluteDefaultAvatar） |
| String getAvatar （UserProperties userProperties, String absoluteDefaultAvatar, SocialUtils.AVATAR_SIZE） |
| Page getContainingPage （リソース リソース リソース） |
| String getSocialProfileURL （String username, ResourceResolver resolver, Page page） |
| UserProperties getUserProperties （ResourceResolver resolver, String userId） |

## 内部使用のみ {#for-internal-use-only}

| boolean canAddNode （Session session, String path） |
|---|
| String createUniqueNameHint （String message） |
| String createUniqueNameHint （String message, int numRandomChars） |
| String generateRandomString （int length） |
| SocialResourceConfiguration getDefaultStorageConfig （） |
| Page getPage （String path, ResourceResolver resolver） |
| String getPagePath （リソースリソース） |
| String getPagePath （String path） |
| String getResourceTypeForIncludedResource （リソースコンポーネント、String defaultResourceType、String designPropertyName） |
| String getResourceTypeFromDesign （Resource, String styleProperty, String defaultValue） |
| boolean isResourceOwner （リソースリソース） |
| String mapUGCPath （リソースリソース） |
| String mapUGCPath （String ugcPath, ResourceResolver resolver） |
| boolean mayPost （ResourceResolver resolver, Resource resource） |
| String prepareUserGeneratedContent （ResourceResolver resolver, String path） |

## メソッドが使用できなくなりました {#methods-no-longer-available}

| Node createNode （ResourceResolver resolver, String path, String nodeType） |
|---|
| Resource getResourceAtPath （ResourceResolver resolver, String path） |
| Resource getResourceAtPath （ResourceResolver resolver, String path, String resourceType） |
| 設定getStorageCloudServiceConfig （リソース） |
| TranslationManager getTranslationManager （） |
| TranslationSaveQueue getTranslationSaveQueue （） |
| boolean mayAccessUGC （ResourceResolver resolver） |
