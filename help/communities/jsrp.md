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
source-git-commit: e7268e43620860b7a1f7aa0a1f1a54199dadcf17
workflow-type: tm+mt
source-wordcount: '462'
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

[ストレージ設定コンソール](srp-config.md)では、デフォルトのストレージ設定を選択できます。これにより、使用するSRPの実装が識別されます。

オーサー環境でストレージ設定コンソールに移動するには、

* グローバルナビゲーションから：**[!UICONTROL ツール]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL ストレージの構成]**

* **[!UICONTROL JCRストレージリソースプロバイダー(JSRP)]**&#x200B;を選択します

* **[!UICONTROL 送信]**&#x200B;を選択

![jsrp-configuration](assets/jsrp-configuration.png)

### 設定の公開 {#publishing-the-configuration}

JSRP はデフォルト設定ですが、パブリッシュ環境で同じ設定が使用されていることを確認するには、以下の手順をおこないます。

* グローバルナビゲーションから：**[!UICONTROL ツール]** > **[!UICONTROL 導入]** > **[!UICONTROL レプリケーション]**
* **[!UICONTROL ツリーをアクティブ化]**/**[!UICONTROL 開始パス]**&#x200B;を選択します。

   * `/conf/global/settings/community/srpc/`を参照

* 「**[!UICONTROL アクティブ化]**」を選択します。

## ユーザーデータの管理 {#managing-user-data}

*ユーザー*、*ユーザープロファイル*、*ユーザーグループ*&#x200B;に関する情報は、次のページにアクセスしてください。

* [ユーザーの同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

## トラブルシューティング {#troubleshooting}

### UGC Not Visible in JCR {#ugc-not-visible-in-jcr}

ストレージオプションの設定を確認し、JSRP がデフォルトのプロバイダーに設定されているかを確認してください。デフォルトでは、ストレージリソースプロバイダーはJSRPです。

すべての作成者および発行AEMインスタンスで、ストレージ設定コンソールに再度アクセスするか、AEMリポジトリを確認します。

* JCRで、[/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc)ノードを含まない場合、ストレージプロバイダーがJSRPであることを意味します。
   * srpcノードが存在し、ノード[defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)が含まれる場合、デフォルトの設定のプロパティでJSRPをデフォルトプロバイダーとして定義する必要があります。

### UGC がオーサーインスタンスで表示されない {#ugc-not-visible-on-author-instance}

これはバグではありません。JSRPの特徴は、公開環境で入力されたコミュニティコンテンツが公開環境でのみ表示されることです。

### UGC がパブリッシュインスタンスで表示されない {#ugc-not-visible-on-publish-instance}

1 つのパブリッシュインスタンスまたはパブリッシュクラスターをデプロイした場合は、[UGC が JCR で表示されない](#ugc-not-visible-in-jcr)の手順に従ってください。

パブリッシュファームをデプロイした場合、JSRP の特性上、コミュニティコンテンツは、コンテンツが投稿されたパブリッシュインスタンス上でしか表示できません。

UGC をどのパブリッシュインスタンス上でも表示するには、パブリッシュクラスターが必要です。
