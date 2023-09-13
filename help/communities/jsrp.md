---
title: JSRP - JCR ストレージリソースプロバイダー
description: JSRP は、1 つのパブリッシュインスタンスと 1 つのオーサーインスタンスのデモ環境または開発環境に最適です。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
source-git-commit: 5af420c8e95fed88a8516cce27b8bbc7d3974e75
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 4%

---

# JSRP - JCR ストレージリソースプロバイダー {#jsrp-jcr-storage-resource-provider}

## JSRP について {#about-jsrp}

AEM Communitiesが JSRP をストレージオプション（デフォルト）として使用する場合、コミュニティコンテンツは JCR に保存され、ユーザー生成コンテンツ (UGC) は、その JCR の投稿先のオーサーインスタンスまたはパブリッシュインスタンスからのみアクセスできます。

デプロイメントはシンプルなので、JSRP は、1 つのパブリッシュインスタンスと 1 つのオーサーインスタンスのデモ環境または開発環境に最適です。

関連トピック [SRP オプションの特性](working-with-srp.md#characteristics-of-srp-options) および [推奨されるトポロジ](topologies.md).

## 設定 {#configuration}

### JSRP を選択 {#select-jsrp}

デフォルトでは、JSRP が UGC のストレージオプションです。

The [ストレージ設定コンソール](srp-config.md) では、使用する SRP の実装を指定するデフォルトのストレージ設定を選択できます。

オーサー環境で、ストレージ設定コンソールに移動します。

* グローバルナビゲーションから： **[!UICONTROL ツール]** > **[!UICONTROL Communities]** > **[!UICONTROL ストレージ設定]**

* 選択 **[!UICONTROL JCR ストレージリソースプロバイダー (JSRP)]**

* 「**[!UICONTROL 送信]**」を選択します。

![jsrp-configuration](assets/jsrp-configuration.png)

### 設定の公開 {#publishing-the-configuration}

JSRP がデフォルト設定ですが、パブリッシュ環境で同じ設定がおこなわれるようにするには、次の手順を実行します。

* グローバルナビゲーションから： **[!UICONTROL ツール]** > **[!UICONTROL 導入]** > **[!UICONTROL レプリケーション]**
* 選択 **[!UICONTROL ツリーをアクティベート]** > **[!UICONTROL 開始パス]**:

   * 参照先 `/conf/global/settings/community/srpc/`

* 選択 **[!UICONTROL 有効化]**

## ユーザーデータの管理 {#managing-user-data}

に関する情報 *ユーザー*, *ユーザープロファイル* および *ユーザーグループ*&#x200B;パブリッシュ環境で入力されることが多い場合は、次の場所にアクセスします。

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

## トラブルシューティング {#troubleshooting}

### UGC が JCR で表示されない {#ugc-not-visible-in-jcr}

ストレージオプションの設定を確認して、JSRP がデフォルトのプロバイダーに設定されていることを確認します。 デフォルトでは、ストレージリソースプロバイダーは JSRP です。

すべてのオーサーインスタンスとパブリッシュAEMインスタンスで、ストレージ設定コンソールに再度アクセスするか、AEMリポジトリを確認します。

* JCR で、 [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * これには [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) ノードの場合、ストレージプロバイダーが JSRP であることを意味します。
   * srpc ノードが存在し、ノードが含まれる場合 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)の場合、デフォルト設定のプロパティでは、JSRP がデフォルトのプロバイダーとして定義されている必要があります。

### UGC がオーサーインスタンスに表示されない {#ugc-not-visible-on-author-instance}

これはバグではありません。 JSRP の特徴は、パブリッシュ環境に入力されたコミュニティコンテンツがパブリッシュ環境でのみ表示されることです。

### UGC がパブリッシュインスタンスに表示されない {#ugc-not-visible-on-publish-instance}

単一のパブリッシュインスタンス、またはパブリッシュクラスターがデプロイされている場合は、次の手順に従います。 [UGC が JCR で表示されない](#ugc-not-visible-in-jcr).

パブリッシュファームがデプロイされている場合、JSRP の特徴は、コミュニティコンテンツが投稿先のパブリッシュインスタンスでのみ表示されることです。

UGC を任意のパブリッシュインスタンスから表示するには、パブリッシュクラスターが必要です。
