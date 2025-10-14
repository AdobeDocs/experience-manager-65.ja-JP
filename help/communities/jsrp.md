---
title: JSRP - JCR ストレージリソースプロバイダー
description: JSRP は、1 つのPublish インスタンスと 1 つのオーサーインスタンスのデモまたは開発環境に最適です
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

簡単にデプロイできるので、JSRP は 1 つのPublish インスタンスと 1 つのオーサーインスタンスのデモや開発環境に最適です。

[SRP オプションの特性 &#x200B;](working-with-srp.md#characteristics-of-srp-options) および [&#x200B; 推奨されるトポロジ &#x200B;](topologies.md) も参照してください。

## 設定 {#configuration}

### JSRP を選択 {#select-jsrp}

デフォルトでは、JSRP が UGC のストレージオプションです。

[&#x200B; ストレージ設定コンソール &#x200B;](srp-config.md) では、デフォルトのストレージ設定を選択でき、使用する SRP の実装を識別できます。

オーサー環境で、ストレージ設定コンソールにアクセスします。

* グローバルナビゲーションから：**[!UICONTROL ツール]**/**[!UICONTROL コミュニティ]**/**[!UICONTROL ストレージ設定]**

* **[!UICONTROL JCR ストレージリソースプロバイダー（JSRP）]** を選択します。

* 「**[!UICONTROL 送信]**」を選択します。

![jsrp-configuration](assets/jsrp-configuration.png)

### 設定の公開 {#publishing-the-configuration}

JSRP はデフォルトの設定ですが、パブリッシュ環境で同じ設定が確実に指定されるようにするには、次の手順を実行します。

* グローバルナビゲーションから：**[!UICONTROL ツール]**/**[!UICONTROL 導入]**/**[!UICONTROL レプリケーション]**
* **[!UICONTROL ツリーをアクティベート]**/**[!UICONTROL 開始パス]** を選択します。

   * `/conf/global/settings/community/srpc/` を参照します

* 「**[!UICONTROL アクティブ化]**」を選択します。

## ユーザーデータの管理 {#managing-user-data}

パブリッシュ環境で入力されることが多い *ユーザー*、*ユーザープロファイル* および *ユーザーグループ* に関する情報は、次をご覧ください。

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

## トラブルシューティング {#troubleshooting}

### JCR に表示されない UGC {#ugc-not-visible-in-jcr}

ストレージオプションの設定を確認して、JSRP がデフォルトのプロバイダーとして設定されていることを確認します。 デフォルトでは、ストレージリソースプロバイダーは JSRP です。

すべてのオーサーインスタンスおよびPublish AEMインスタンスで、ストレージ設定コンソールに再度アクセスするか、AEM リポジトリを確認します。

* JCR で [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) ノードは含まれていません。これは、ストレージプロバイダーが JSRP であることを意味します。
   * srpc ノードが存在し、ノード [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration) が含まれている場合、defaultconfiguration のプロパティでは、JSRP をデフォルトのプロバイダーとして定義する必要があります。

### オーサーインスタンスに UGC が表示されない {#ugc-not-visible-on-author-instance}

これはバグではありません。 JSRP の特徴は、パブリッシュ環境で入力されたコミュニティコンテンツが、Publish環境でのみ表示されることです。

### Publish インスタンスに UGC が表示されない {#ugc-not-visible-on-publish-instance}

1 つのPublish インスタンスの場合、またはパブリッシュクラスターがデプロイされている場合は、[UGC は JCR に表示されません &#x200B;](#ugc-not-visible-in-jcr) の手順に従います。

パブリッシュファームがデプロイされている場合の JSRP の特徴は、コミュニティコンテンツが、投稿先のPublish インスタンスにのみ表示されることです。

UGC を任意のPublish インスタンスから表示するには、パブリッシュクラスターが必要です。
