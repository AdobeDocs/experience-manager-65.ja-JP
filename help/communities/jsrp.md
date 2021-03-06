---
title: JSRP - JCR ストレージリソースプロバイダー
seo-title: JSRP - JCR Storage Resource Provider
description: JSRP は一般的に、1 つのパブリッシュインスタンスと 1 つのオーサーインスタンスがあるデモ環境または開発環境に適しています
seo-description: JSRP is generally best suited for demonstration or development environments of one publish instance and one author instance
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 53%

---

# JSRP - JCR ストレージリソースプロバイダー {#jsrp-jcr-storage-resource-provider}

## JSRP について {#about-jsrp}

AEM Communitiesが JSRP をストレージオプションとして使用する場合（デフォルト）、コミュニティコンテンツは JCR に保存され、ユーザー生成コンテンツ (UGC) は、JSRP の投稿先のオーサーインスタンスまたはパブリッシュインスタンスからのみアクセスできます。

JSRP はデプロイメントが容易なので、一般的に、1 つのパブリッシュインスタンスと 1 つのオーサーインスタンスがあるデモ環境または開発環境に適しています。

[SRP オプションの特性](working-with-srp.md#characteristics-of-srp-options)と[推奨されるトポロジ](topologies.md)も参照してください。

## 設定 {#configuration}

### JSRP の選択 {#select-jsrp}

デフォルトでは、JSRP が UGC 用のストレージオプションとして選択されています。

この [ストレージ設定コンソール](srp-config.md) では、使用する SRP の実装を指定するデフォルトのストレージ設定を選択できます。

オーサー環境でストレージ設定コンソールに移動するには、

* グローバルナビゲーションから： **[!UICONTROL ツール]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL ストレージ設定]**

* 選択 **[!UICONTROL JCR ストレージリソースプロバイダー (JSRP)]**

* 選択 **[!UICONTROL 送信]**

![jsrp-configuration](assets/jsrp-configuration.png)

### 設定の公開 {#publishing-the-configuration}

JSRP はデフォルト設定ですが、パブリッシュ環境で同じ設定が使用されていることを確認するには、以下の手順をおこないます。

* グローバルナビゲーションから： **[!UICONTROL ツール]** > **[!UICONTROL 導入]** > **[!UICONTROL レプリケーション]**
* 選択 **[!UICONTROL ツリーをアクティベート]** > **[!UICONTROL 開始パス]**:

   * 参照先 `/conf/global/settings/community/srpc/`

* 選択 **[!UICONTROL 有効化]**

## ユーザーデータの管理 {#managing-user-data}

パブリッシュ環境で頻繁に入力されるユーザー、ユーザープロファイルおよびユーザーグループについては、以下を参照してください。******：

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

## トラブルシューティング {#troubleshooting}

### UGC が JCR で表示されない {#ugc-not-visible-in-jcr}

ストレージオプションの設定を確認し、JSRP がデフォルトのプロバイダーに設定されているかを確認してください。デフォルトでは、ストレージリソースプロバイダーは JSRP です。

すべてのオーサーインスタンスとパブリッシュAEMインスタンスで、ストレージ設定コンソールに再度アクセスするか、AEMリポジトリを確認します。

* JCR で、 [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * 次を含まない [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) ノードの場合、ストレージプロバイダーが JSRP であることを意味します。
   * srpc ノードが存在し、ノードが含まれる場合 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)の場合、デフォルト設定のプロパティでは、JSRP がデフォルトのプロバイダーとして定義されている必要があります。

### UGC がオーサーインスタンスで表示されない {#ugc-not-visible-on-author-instance}

これはバグではありません。JSRP の特徴は、パブリッシュ環境に入力されたコミュニティコンテンツがパブリッシュ環境でのみ表示されることです。

### UGC がパブリッシュインスタンスで表示されない {#ugc-not-visible-on-publish-instance}

1 つのパブリッシュインスタンスまたはパブリッシュクラスターをデプロイした場合は、[UGC が JCR で表示されない](#ugc-not-visible-in-jcr)の手順に従ってください。

パブリッシュファームをデプロイした場合、JSRP の特性上、コミュニティコンテンツは、コンテンツが投稿されたパブリッシュインスタンス上でしか表示できません。

UGC をどのパブリッシュインスタンス上でも表示するには、パブリッシュクラスターが必要です。
