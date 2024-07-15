---
title: ASRP - Adobe ストレージリソースプロバイダー
description: リレーショナルデータベースを共通ストアとして使用するようにAEM Communitiesを設定します
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 6430ed96-5d96-41b6-866f-90b34ff84f7a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 3%

---

# ASRP - Adobe ストレージリソースプロバイダー {#asrp-adobe-storage-resource-provider}

## ASRP について {#about-asrp}

ASRP を共通ストアとして使用するようにAEM Communitiesが設定されている場合、ユーザー生成コンテンツ（UGC）には、すべてのオーサーインスタンスとパブリッシュインスタンスからアクセスでき、同期やレプリケーションの必要はありません。

[SRP オプションの特性 ](/help/communities/working-with-srp.md#characteristics-of-srp-options) および [ 推奨されるトポロジ ](/help/communities/topologies.md) も参照してください。

## 要件 {#requirements}

ASRP を使用するには、追加のライセンスが必要です。

UGC に ASRP を使用するようにAEM Communities サイトを設定するには、アカウント担当者にお問い合わせください。

* データセンター URL （ASRP エンドポイントのアドレス）
* 消費者キー
* 秘密鍵
* レポートスイート ID

消費者キーと秘密鍵は、1 つの会社のすべてのレポートスイートで共有されます。 テナントごとに 1 つのレポートスイートがあります。

## 設定 {#configuration}

### ASRP の選択 {#select-asrp}

[ ストレージ設定コンソール ](/help/communities/srp-config.md) では、デフォルトのストレージ設定を選択でき、使用する SRP の実装を識別できます。

**AEM オーサーインスタンスの場合：**

* グローバルナビゲーションから **[!UICONTROL ツール/Communities/ストレージ設定]** に移動し、**[!UICONTROL Adobeストレージリソースプロバイダー（ASRP）]** を選択します。

![asrp-default](assets/asrp-default.png)

プロビジョニング・プロセスから得られる情報を次に示します。

* **データセンター URL**：プルダウンして、アカウント担当者が識別した実稼動データセンターを選択します。
* **デフォルトレポートスイート**: デフォルトレポートスイートの名前を入力します。
* **コンシューマーキー**：コンシューマーキーを入力します。
* **秘密鍵**：秘密鍵を入力します。
* 「**送信**」を選択します。

パブリッシュインスタンスを準備します。

* [暗号鍵をレプリケートします](#replicate-the-crypto-key)
* [設定をレプリケートします](#publishing-the-configuration)

設定を送信したら、接続をテストします。

* **設定をテスト** を選択します。

  オーサーインスタンスとパブリッシュインスタンスごとに、ストレージ設定コンソールからデータセンターへの接続をテストします。

* [ リンクを外部化 ](#externalize-links) して、プロファイルデータのサイト URL がデータセンターからルーティング可能であることを確認します。

### 暗号鍵をレプリケート {#replicate-the-crypto-key}

コンシューマーキーと秘密鍵は暗号化されます。 キーを適切に暗号化/復号化するには、プライマリ Granite 暗号キーがすべてのAEM インスタンスで同じである必要があります。

[ 暗号鍵をレプリケート ](/help/communities/deploy-communities.md#replicate-the-crypto-key) の手順に従います。

### リンクを外部化 {#externalize-links}

プロファイルおよびプロファイル画像の正しいリンクを使用するには、適切に [Link Externalizer を設定 ](/help/sites-developing/externalizer.md) してください。

ドメインを、データセンター URL （ASRP エンドポイント）からルーティング可能な URL に設定してください。

### 時刻の同期 {#time-synchronization}

ASRP エンドポイントでの認証を成功させるには、ホストされているAEM Communitiesを実行しているマシンを時刻同期する必要があります（例：[Network Time Protocol （NTP） ](https://www.ntp.org/)）。

### 設定の公開 {#publishing-the-configuration}

ASRP は、すべてのオーサーインスタンスとパブリッシュインスタンスで共通ストアとして識別される必要があります。

パブリッシュ環境で同一の設定を使用できるようにするには：

AEM オーサーインスタンス上：

* メインメニューから **[!UICONTROL ツール]**/**[!UICONTROL デプロイメント]**/**[!UICONTROL レプリケーション]** に移動します。
* **ツリーのアクティブ化** を選択します。
* **開始パス**: `/conf/global/settings/communities/srpc/` を参照します
* 選択解除 **変更済みのみ**
* 「**アクティブ化**」を選択します。

## AEM 6.0 からのアップグレード {#upgrading-from-aem}

>[!CAUTION]
>
>公開されたコミュニティサイトで ASRP を有効にすると、[JCR](/help/communities/jsrp.md) に既に保存されている UGC は、オンプレミスストレージとクラウドストレージの間でデータが同期されないため、表示されなくなります。

**`AEM Communities Extension`** は、以前AEM 6.0 social communities as a cloud service で導入されました。 AEM 6.1 Communities の場合、クラウドの設定は必要ありません。[ ストレージ設定コンソール ](/help/communities/srp-config.md) から ASRP を選択するだけです。

新しいストレージ構造により、ソーシャルコミュニティから Communities にアップグレードする際は、[ アップグレード ](/help/communities/upgrade.md#adobe-cloud-storage) の手順に従う必要があります。

## ユーザーデータの管理 {#managing-user-data}

パブリッシュ環境で入力されることが多い *ユーザー*、*ユーザープロファイル* および *ユーザーグループ* に関する情報は、次をご覧ください。

* [ユーザー同期](/help/communities/sync.md)
* [ユーザーとユーザーグループの管理](/help/communities/users.md)

## トラブルシューティング {#troubleshooting}

### アップグレード後に UGC が表示されなくなる {#ugc-disappears-after-upgrade}

既存のAEM 6.0 ソーシャルコミュニティサイトからアップグレードする場合は、[ アップグレードの手順 ](/help/communities/upgrade.md#adobe-cloud-storage) に従ってください。従わないと、UGC が失われるようです。

### 認証エラー {#authentication-errors}

データセンター URL に対する認証エラーを受け取り、AEM error.log に古いタイムスタンプに関するメッセージが含まれている場合は、時間同期が行われていることを確認します。

[Network Time Protocol （NTP） ](https://www.ntp.org/) などのツールを使用して、すべてのAEM オーサーサーバーとパブリッシュサーバーの時刻を同期します。

### 検索に新しいコンテンツが表示されない {#new-content-does-not-appear-in-searches}

Adobeのクラウドストレージインフラストラクチャは、スケーリングとパフォーマンスの目標を達成するために *最終的な一貫性* を使用します。 このため、新しいコンテンツはすぐに使用できず、検索結果に表示されるまでに数秒かかります。

最終的な一貫性に影響する間隔が監視されている間、新しいコンテンツが検索で表示されるまでに数秒以上かかる場合は、アカウント担当者にお問い合わせください。

### ASRP で UGC が表示されない {#ugc-not-visible-in-asrp}

ストレージオプションの設定をチェックして、ASRP がデフォルトのプロバイダーとして設定されていることを確認します。 デフォルトでは、ストレージリソースプロバイダーは ASRP ではなく JSRP です。

すべてのオーサーインスタンスおよびパブリッシュ AEMインスタンスで、ストレージ設定コンソールに再度アクセスするか、AEM リポジトリを確認します。

JCR で [/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp) ノードが含まれていない場合は、ストレージプロバイダーが JSRP であることを意味します。
* srpc ノードが存在し、[defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration) ノードが含まれている場合、defaultconfiguration のプロパティは、ASRP をデフォルトのプロバイダーとして定義します。
