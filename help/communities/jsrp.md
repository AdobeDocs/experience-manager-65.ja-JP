---
title: JSRP - JCR ストレージリソースプロバイダー
seo-title: JSRP - JCR ストレージリソースプロバイダー
description: JSRP は一般的に、1 つのパブリッシュインスタンスと 1 つのオーサーインスタンスがあるデモ環境または開発環境に適しています
seo-description: JSRP は一般的に、1 つのパブリッシュインスタンスと 1 つのオーサーインスタンスがあるデモ環境または開発環境に適しています
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
translation-type: tm+mt
source-git-commit: c798eb79dc9f8e58cef86cf90af02622c3a2ed78
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 52%

---


# JSRP - JCR ストレージリソースプロバイダー {#jsrp-jcr-storage-resource-provider}

## JSRP について {#about-jsrp}

AEM CommunitiesがJSRPをストレージオプションとして使用する場合（デフォルト）、コミュニティコンテンツはJCRに保存され、ユーザー生成コンテンツ(UGC)は、そのコンテンツが投稿された作成者インスタンスまたは発行インスタンスからのみアクセスできます。

JSRP はデプロイメントが容易なので、一般的に、1 つのパブリッシュインスタンスと 1 つのオーサーインスタンスがあるデモ環境または開発環境に適しています。

[SRP オプションの特性](working-with-srp.md#characteristics-of-srp-options)と[推奨されるトポロジ](topologies.md)も参照してください。

## 設定 {#configuration}

### JSRP の選択 {#select-jsrp}

デフォルトでは、JSRP が UGC 用のストレージオプションとして選択されています。

[ストレージ設定コンソール](srp-config.md) では、デフォルトのストレージ設定を選択できます。これにより、使用するSRPの実装が識別されます。

オーサー環境でストレージ設定コンソールに移動するには、

* From global navigation: **[!UICONTROL Tools]** > **[!UICONTROL Communities]** > **[!UICONTROL Storage Configuration]**

* Select **[!UICONTROL JCR Storage Resource Provider (JSRP)]**

* Select **[!UICONTROL Submit]**

![chlimage_1-234](assets/chlimage_1-234.png)

### 設定の公開 {#publishing-the-configuration}

JSRP はデフォルト設定ですが、パブリッシュ環境で同じ設定が使用されていることを確認するには、以下の手順をおこないます。

* 作成者：

   * From global navigation: **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**
   * 「 **[!UICONTROL Activate Tree]** / **[!UICONTROL 開始パス]**」を選択します。

      * 参照先 `/conf/global/settings/community/srpc/`
   * Select **[!UICONTROL Activate]**


## ユーザーデータの管理 {#managing-user-data}

For information regarding *users*, *user profiles* and *user groups*, often entered in the publish environment, visit:

* [ユーザーの同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

## トラブルシューティング {#troubleshooting}

### UGC Not Visible in JCR {#ugc-not-visible-in-jcr}

ストレージオプションの設定を確認し、JSRP がデフォルトのプロバイダーに設定されているかを確認してください。デフォルトでは、ストレージリソースプロバイダーはJSRPです。

すべての作成者および発行AEMインスタンスで、ストレージ設定コンソールに再度アクセスするか、AEMリポジトリを確認します。

* JCRで、/conf/ [global/settings/communityの場合](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Does not contain an [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) node, it means the storage provider is JSRP.
   * If the srpc node exists and contains node [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration), the defaultconfiguration&#39;s properties should define JSRP to be the default provider.

### UGC がオーサーインスタンスで表示されない {#ugc-not-visible-on-author-instance}

これはバグではありません。JSRPの特徴は、公開環境で入力されたコミュニティコンテンツが公開環境でのみ表示されることです。

### UGC がパブリッシュインスタンスで表示されない {#ugc-not-visible-on-publish-instance}

1 つのパブリッシュインスタンスまたはパブリッシュクラスターをデプロイした場合は、[UGC が JCR で表示されない](#ugc-not-visible-in-jcr)の手順に従ってください。

パブリッシュファームをデプロイした場合、JSRP の特性上、コミュニティコンテンツは、コンテンツが投稿されたパブリッシュインスタンス上でしか表示できません。

UGC をどのパブリッシュインスタンス上でも表示するには、パブリッシュクラスターが必要です。
