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
role: Administrator
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 62%

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

* グローバルナビゲーションから、**[!UICONTROL ツール]** / **[!UICONTROL コミュニティ]** / **[!UICONTROL ストレージ設定]**&#x200B;を選択します。

デフォルトの JCR 以外のストレージオプションを選択するには、

* オプションを選択
* 適切な設定

   * [MSRP](msrp.md#select-msrp)の選択の詳細を参照
   * [DSRP](dsrp.md#select-dsrp)の選択の詳細を参照
   * [ASRP](asrp.md#select-asrp)の選択の詳細を参照

* 「**[!UICONTROL 送信]**」を選択します。

### JCR ストレージについて {#about-jcr-storage}

選択しなかった場合は、AEM リポジトリである JCR がデフォルトで使用されることに注意してください。

JCRは、オーサー環境とパブリッシュ環境で共有される共通ストアでは&#x200B;*ありません*。 コミュニティコンテンツは、作成先のオーサー環境またはパブリッシュ環境からのみ表示されます。

詳しくは、[JCR ストア](jsrp.md)を参照してください。

>[!NOTE]
>
>`/etc/socialconfig`の下にノード`srpc`がない場合は、デフォルトの[JCRストア](jsrp.md)を示します。
