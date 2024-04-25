---
title: JSRP - JCR ストレージリソースプロバイダー
description: JSRP は、1 つのパブリッシュインスタンスと 1 つのオーサーインスタンスのデモまたは開発環境に最適です
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 5%

---

# JSRP - JCR ストレージリソースプロバイダー {#jsrp-jcr-storage-resource-provider}

## JSRP について {#about-jsrp}

AEM Communitiesで JSRP をストレージオプションとして使用する場合（デフォルト）、コミュニティコンテンツは JCR に保存され、ユーザー生成コンテンツ（UGC）には、投稿先のオーサーインスタンスまたはパブリッシュインスタンスからのみアクセスできます。

デプロイが簡単なので、JSRP は 1 つのパブリッシュインスタンスと 1 つのオーサーインスタンスのデモまたは開発環境に最適です。

関連トピック [SRP オプションの特徴](working-with-srp.md#characteristics-of-srp-options) および [推奨されるトポロジ](topologies.md).

## 設定 {#configuration}

### JSRP を選択 {#select-jsrp}

デフォルトでは、JSRP が UGC のストレージオプションです。

この [ストレージ設定コンソール](srp-config.md) デフォルトのストレージ設定を選択でき、使用する SRP の実装を識別できます。

オーサー環境で、ストレージ設定コンソールにアクセスします。

* グローバルナビゲーションから： **[!UICONTROL ツール]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL ストレージ設定]**

* を選択 **[!UICONTROL JCR ストレージリソースプロバイダー（JSRP）]**

* 「**[!UICONTROL 送信]**」を選択します。

![jsrp-configuration](assets/jsrp-configuration.png)

### 設定の公開 {#publishing-the-configuration}

JSRP はデフォルトの設定ですが、パブリッシュ環境で同じ設定が確実に指定されるようにするには、次の手順を実行します。

* グローバルナビゲーションから： **[!UICONTROL ツール]** > **[!UICONTROL デプロイメント]** > **[!UICONTROL 複製]**
* を選択 **[!UICONTROL ツリーのアクティベート]** > **[!UICONTROL 開始パス]**:

   * を参照 `/conf/global/settings/community/srpc/`

* を選択 **[!UICONTROL Activate]**

## ユーザーデータの管理 {#managing-user-data}

について *ユーザー*, *ユーザープロファイル* および *ユーザーグループ*（パブリッシュ環境で入力することが多い）次を参照してください。

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

## トラブルシューティング {#troubleshooting}

### JCR に表示されない UGC {#ugc-not-visible-in-jcr}

ストレージオプションの設定を確認して、JSRP がデフォルトのプロバイダーとして設定されていることを確認します。 デフォルトでは、ストレージリソースプロバイダーは JSRP です。

すべてのオーサーおよびパブリッシュ AEM インスタンスで、ストレージ設定コンソールに再度アクセスするか、AEM リポジトリを確認します。

* JCR で次の場合： [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * 次を含まない [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) ノードの場合は、ストレージプロバイダーが JSRP であることを意味します。
   * srpc ノードが存在し、ノードがを含む場合 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)を選択する場合は、defaultconfiguration のプロパティで JSRP をデフォルトのプロバイダーとして定義する必要があります。

### オーサーインスタンスに UGC が表示されない {#ugc-not-visible-on-author-instance}

これはバグではありません。 JSRP の特徴は、パブリッシュ環境で入力されたコミュニティコンテンツが、パブリッシュ環境でのみ表示されることです。

### パブリッシュインスタンスに UGC が表示されない {#ugc-not-visible-on-publish-instance}

1 つのパブリッシュインスタンス、またはパブリッシュクラスターがデプロイされている場合は、次の手順に従います。 [JCR に表示されない UGC](#ugc-not-visible-in-jcr).

パブリッシュファームがデプロイされている場合の JSRP の特徴は、コミュニティコンテンツが、投稿先のパブリッシュインスタンスにのみ表示されることです。

UGC を任意のパブリッシュインスタンスから表示するには、パブリッシュクラスターが必要です。
