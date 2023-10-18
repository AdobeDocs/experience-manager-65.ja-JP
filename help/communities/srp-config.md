---
title: ストレージ設定
description: コミュニティコンテンツ（ユーザー生成コンテンツ）用に選択されたストレージを識別する手段として、ストレージ設定コンソールについて説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
source-git-commit: 00b6f2f03470aca7f87717818d0dfcd17ac16bed
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 4%

---

# ストレージ設定 {#storage-configuration}

ストレージ設定は、コミュニティコンテンツ ( ユーザー生成コンテンツ (UGC) とも呼ばれます ) 用に選択されたストレージを識別する手段です。

この設定は、UGC へのアクセス時にストレージリソースプロバイダー (SRP) の実装を使用する際に、AEM Communitiesコードに通知します。 Adobe Experience Manager(AEM) のデプロイ時に確立されたトポロジを反映する必要があります。

ストレージ・オプションとデプロイメント・トポロジーの詳細は、次を参照してください。

* [コミュニティコンテンツストア](working-with-srp.md)
* [推奨されるトポロジ](topologies.md)

## ストレージ設定コンソール {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

オーサー環境で、ストレージ設定コンソールに移動します。

* グローバルナビゲーションから、「 」を選択します。 **[!UICONTROL ツール]** > **[!UICONTROL Communities]** > **[!UICONTROL ストレージ設定]**

デフォルトの JCR 以外のストレージオプションを選択するには：

* オプションを選択
* 適切な設定

   * 詳細を見る [MSRP の選択](msrp.md#select-msrp)
   * 詳細を見る [DSRP の選択](dsrp.md#select-dsrp)
   * 詳細を見る [ASRP の選択](asrp.md#select-asrp)

* 「**[!UICONTROL 送信]**」を選択します。

### JCR ストレージについて {#about-jcr-storage}

何も選択しない場合、デフォルトはAEMリポジトリ (JCR) です。

JCR は *not* オーサー環境とパブリッシュ環境で共有される共通ストア。 コミュニティコンテンツは、作成先のオーサー環境またはパブリッシュ環境からのみ表示されます。

訪問 [JCR ストア](jsrp.md) を参照してください。

>[!NOTE]
>
>ノードがない場合 `srpc` under `/etc/socialconfig` デフォルトを示します。 [JCR ストア](jsrp.md).
