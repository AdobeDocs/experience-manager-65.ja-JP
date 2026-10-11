---
title: ストレージ設定
description: コミュニティ コンテンツ用に選択されたストレージ（ユーザー生成コンテンツとも呼ばれます）を識別する方法として、ストレージ設定コンソールについて説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
solution: Experience Manager
feature: Communities
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
source-wordcount: '213'
ht-degree: 4%
---
# ストレージ設定 {#storage-configuration}

ストレージ設定とは、コミュニティコンテンツに選択されたストレージを特定する手段です。UGC （ユーザー生成コンテンツ）とも呼ばれます。

この設定は、UGCへのアクセス時にストレージリソースプロバイダー（SRP）の実装を使用するAEM Communities コードに通知します。 Adobe Experience Manager（AEM）のデプロイ時に確立されたトポロジを反映する必要があります。

ストレージ・オプションとデプロイメント・トポロジについては、次のサイトを参照してください。

* [コミュニティコンテンツストア](working-with-srp.md)
* [推奨トポロジ](topologies.md)

## ストレージ設定コンソール {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

オーサー環境で、ストレージ設定コンソールにアクセスします。

* グローバルナビゲーションから、**[!UICONTROL ツール]**/**[!UICONTROL コミュニティ]**/**[!UICONTROL ストレージ設定]**&#x200B;を選択します

デフォルトのJCR以外のストレージオプションを選択するには、次の手順に従います。

* オプションを選択
* 適切な設定

  * [MSRPの選択](msrp.md#select-msrp)の詳細を参照してください
  * [DSRPの選択](dsrp.md#select-dsrp)の詳細を参照してください
  * [ASRPの選択](asrp.md#select-asrp)の詳細を参照してください

* 「**[!UICONTROL 送信]**」を選択します。

### JCR ストレージについて {#about-jcr-storage}

選択が行われない場合、デフォルトはAEM リポジトリ JCRです。

JCRは、オーサー環境とパブリッシュ環境で共有される共通ストアである&#x200B;*not*&#x200B;です。 コミュニティコンテンツは、作成されたオーサー環境またはパブリッシュ環境からのみ表示されます。

詳細については、[JCR Store](jsrp.md)にアクセスしてください。

>[!NOTE]
>
>`/etc/socialconfig`の下にノード `srpc`がないことは、デフォルトの[JCR ストア &#x200B;](jsrp.md)を示します。
