---
title: ストレージ設定
seo-title: ストレージ設定
description: ストレージ設定コンソールへのアクセス方法
seo-description: ストレージ設定コンソールへのアクセス方法
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# ストレージ設定 {#storage-configuration}

ストレージ設定では、コミュニティコンテンツ用に選択されているストレージを確認できます。コミュニティコンテンツはユーザー生成コンテンツ（UGC）とも呼ばれます。

この設定では、UGC アクセス時に使用されるストレージリソースプロバイダー（SRP）の実装に関する AEM Communities のコード情報が提供されます。設定は、AEM のデプロイ時に確立したトポロジを反映している必要があります。

ストレージオプションとデプロイメントトポロジの説明については、以下を参照してください。

* [コミュニティコンテンツストア](working-with-srp.md)
* [推奨されるトポロジ](topologies.md)

## ストレージ設定コンソール {#storage-configuration-console}

![chlimage_1-188](assets/chlimage_1-188.png)

オーサー環境でストレージ設定コンソールに移動するには、

* From global navigation: **[!UICONTROL Tools > Communities > Storage Configuration]**

デフォルトの JCR 以外のストレージオプションを選択するには、

* オプションを選択します。
* 適切な設定

   * See details for [selecting MSRP](msrp.md#select-msrp)
   * See details for [selecting DSRP](dsrp.md#select-dsrp)
   * See details for [selecting ASRP](asrp.md#select-asrp)

* Select **[!UICONTROL Submit]**

### JCR ストレージについて {#about-jcr-storage}

選択しなかった場合は、AEM リポジトリである JCR がデフォルトで使用されることに注意してください。

JCR is *not* a common store shared by the author and publish environments. コミュニティコンテンツは、作成された作成者または発行環境からのみ表示されます。

詳しくは、[JCR ストア](jsrp.md)を参照してください。

>[!NOTE]
>
>The absence of the node `srpc`under `/etc/socialconfig` indicates the default [JCR store](jsrp.md).

