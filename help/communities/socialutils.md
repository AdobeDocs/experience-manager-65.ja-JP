---
title: SocialUtils のリファクタリング
description: パッケージ com.adobe.cq.social.ugcbase.SocialUtils はAEM 6.1 で非推奨になりました
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 2%

---

# SocialUtils のリファクタリング {#socialutils-refactoring}

## SocialUtils パッケージ非推奨 {#socialutils-package-deprecated}

パッケージ `com.adobe.cq.social.ugcbase.SocialUtils` はAEM 6.1 で非推奨（廃止予定）となりました。

次の表に、`SocialUtils` のメソッドの代わりに使用するメソッドを示します。

## SocialResourceUtilities パッケージ  {#socialresourceutilities-package}

| com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities のメソッド |
|---|
| Boolean checkPermission （ResourceResolver resolver, String path, String action） |  |
| SocialResourceProvider getSocialResourceProvider （リソース） |  |
| SocialResourceConfiguration getStorageConfig （リソース リソース） |  |
| リソース getUGCResource （Resource userResource） |  |
| Resource getUGCResource （Resource userResource, ResourceResolverFactory rrf） | 新規 |
| Resource getUGCResource （Resource userResource, ResourceResolverFactory rrf, String resourceTypeHint） | 新規 |
| Resource getUGCResource （Resource userResource, String resourceTypeHint） |  |
| ブール hasModeratePermissions （リソースリソース） |  |
| String resourceToACLPath （Resource resource resource） |  |
| String resourceToUGCStoragePath （Resource resource） | string resourceToUGCPath （Resource resource resource）を置換します |
| 文字列 UGCToResourcePath （リソース） |  |
| String UGCoResourcePath （String ugcPath） | メソッドの署名が変更されました |
| String UGCoResourcePath （String ugcPath, ResourceResolver resolver） | 新規 |

| `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities のメソッド |
|---|
| SocialResourceProvider getSocialResourceProvider （リソース） | socialResourceProvider getConfiguredProvider （リソース）を置き換えます |

## SCFUtilities パッケージ {#scfutilities-package}

| `com.adobe.cq.social.`utilities.scf.api.SCFUtilites のメソッド |
|---|
| String getAvatar （UserProperties userProperties） |
| String getAvatar （UserProperties userProperties, int size） |
| String getAvatar （UserProperties userProperties, String absoluteDefaultAvatar） |
| String getAvatar （UserProperties userProperties, String absoluteDefaultAvatar, SocialUtils.AVATAR_SIZE） |
| ページ getContainingPage （Resource） |
| String getSocialProfileURL （String username, ResourceResolver, Page page） |
| UserProperties getUserProperties （ResourceResolver resolver, String userId） |

## 内部使用のみ {#for-internal-use-only}

| boolean canAddNode （セッションセッション、文字列パス） |
|---|
| String createUniqueNameHint （String message） |
| String createUniqueNameHint （String message, int numRandomChars） |
| String generateRandomString （int length） |
| SocialResourceConfiguration getDefaultStorageConfig （） |
| Page getPage （String path, ResourceResolver） |
| String getPagePath （Resource resource） |
| String getPagePath （String path） |
| String getResourceTypeForIncludedResource （Resource コンポーネント，String defaultResourceType, String designPropertyName） |
| String getResourceTypeFromDesign （Resource, String styleProperty, String defaultValue） |
| boolean isResourceOwner （Resource） |
| 文字列 mapUGCPath （リソース リソース） |
| String mapUGCPath （String ugcPath, ResourceResolver） |
| boolean mayPost （ResourceResolver resolver, Resource resource） |
| String prepareUserGeneratedContent （ResourceResolver リゾルバー、文字列パス） |

## 使用できないメソッド {#methods-no-longer-available}

| Node createNode （ResourceResolver resolver, String path, String nodeType） |
|---|
| Resource getResourceAtPath （ResourceResolver resolver, String path） |
| Resource getResourceAtPath （ResourceResolver resolver, String path, String resourceType） |
| 設定 getStorageCloudServiceConfig （リソース リソース） |
| TranslationManager getTranslationManager （） |
| TranslationSaveQueue getTranslationSaveQueue （） |
| boolean mayAccessUGC （ResourceResolver） |
