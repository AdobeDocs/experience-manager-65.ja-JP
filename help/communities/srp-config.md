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

* グローバルナビゲーションから、**[!UICONTROL ツール]**/**[!UICONTROL コミュニティ]**/**[!UICONTROL ストレージ設定]** を選択します。

デフォルトの JCR 以外のストレージオプションを選択するには：

* オプションを選択
* 適切に設定

   * [MSRP の選択 &#x200B;](msrp.md#select-msrp) の詳細を参照してください。
   * [DSRP の選択 &#x200B;](dsrp.md#select-dsrp) の詳細を参照してください。
   * 詳細については、[ASRP の選択 &#x200B;](asrp.md#select-asrp) を参照してください。

* 「**[!UICONTROL 送信]**」を選択します。

### JCR ストレージについて {#about-jcr-storage}

何も選択しない場合、デフォルトはAEM リポジトリ JCR です。

JCR *オーサー環境とPublish環境で共有される共通ストア* ありません）。 コミュニティコンテンツは、そのコンテンツが作成されたオーサー環境またはPublish環境からのみ表示されます。

詳しくは、[JCR ストア &#x200B;](jsrp.md) を参照してください。

>[!NOTE]
>
>`/etc/socialconfig` の下にノード `srpc` がない場合は、デフォルトの [JCR ストア &#x200B;](jsrp.md) を示します。
