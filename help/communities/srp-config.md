---
title: ストレージ設定
seo-title: Storage Configuration
description: ストレージ設定コンソールへのアクセス方法
seo-description: How to access the Storage Configuration Console
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 61%

---

# ストレージ設定 {#storage-configuration}

ストレージ設定では、コミュニティコンテンツ用に選択されているストレージを確認できます。コミュニティコンテンツはユーザー生成コンテンツ（UGC）とも呼ばれます。

この設定では、UGC アクセス時に使用されるストレージリソースプロバイダー（SRP）の実装に関する AEM Communities のコード情報が提供されます。設定は、AEM のデプロイ時に確立したトポロジを反映している必要があります。

ストレージオプションとデプロイメントトポロジの説明については、以下を参照してください。：

* [コミュニティコンテンツストア](working-with-srp.md)
* [推奨されるトポロジ](topologies.md)

## ストレージ設定コンソール {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

オーサー環境で、ストレージ設定コンソールに移動します。

* グローバルナビゲーションから、 **[!UICONTROL ツール]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL ストレージ設定]**

デフォルトの JCR 以外のストレージオプションを選択するには、

* オプションを選択
* 適切な設定

   * 詳細を見る [MSRP の選択](msrp.md#select-msrp)
   * 詳細を見る [DSRP の選択](dsrp.md#select-dsrp)
   * 詳細を見る [ASRP の選択](asrp.md#select-asrp)

* **[!UICONTROL 送信]**&#x200B;を選択します。

### JCR ストレージについて {#about-jcr-storage}

選択しなかった場合は、AEM リポジトリである JCR がデフォルトで使用されることに注意してください。

JCR は *not* オーサー環境とパブリッシュ環境で共有される共通ストア。 コミュニティコンテンツは、作成先のオーサー環境またはパブリッシュ環境からのみ表示されます。

詳しくは、[JCR ストア](jsrp.md)を参照してください。

>[!NOTE]
>
>ノードがない `srpc` under `/etc/socialconfig` デフォルトを示します [JCR ストア](jsrp.md).
