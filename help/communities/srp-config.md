---
title: ストレージ設定
description: コミュニティコンテンツ（ユーザー生成コンテンツとも呼ばれます）用に選択されたストレージを識別する手段としてのストレージ設定コンソールについて説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 4%

---

# ストレージ設定 {#storage-configuration}

ストレージ設定は、コミュニティコンテンツ（ユーザー生成コンテンツ（UGC）とも呼ばれます）用に選択されたストレージを識別する手段です。

この設定により、UGC へのアクセス時に使用されるストレージリソースプロバイダー（SRP）の実装がAEM Communities コードに通知されます。 Adobe Experience Manager（AEM）のデプロイ時に確立されたトポロジを反映する必要があります。

ストレージオプションとデプロイメントトポロジについては、次を参照してください。

* [コミュニティコンテンツストア](working-with-srp.md)
* [推奨されるトポロジ](topologies.md)

## ストレージ設定コンソール {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

オーサー環境で、ストレージ設定コンソールにアクセスします。

* グローバルナビゲーションから、を選択します。 **[!UICONTROL ツール]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL ストレージ設定]**

デフォルトの JCR 以外のストレージオプションを選択するには：

* オプションを選択
* 適切に設定

   * の詳細を参照 [msrp の選択](msrp.md#select-msrp)
   * の詳細を参照 [dsrp の選択](dsrp.md#select-dsrp)
   * の詳細を参照 [asrp の選択](asrp.md#select-asrp)

* 「**[!UICONTROL 送信]**」を選択します。

### JCR ストレージについて {#about-jcr-storage}

何も選択しない場合、デフォルトはAEM リポジトリ JCR です。

JCR は *ではない* オーサー環境とパブリッシュ環境で共有される共通ストア。 コミュニティコンテンツは、そのコンテンツが作成されたオーサー環境またはパブリッシュ環境からのみ表示されます。

訪問 [JCR ストア](jsrp.md) を参照してください。

>[!NOTE]
>
>ノードの欠落 `srpc` 未満 `/etc/socialconfig` デフォルトを示します [JCR ストア](jsrp.md).
