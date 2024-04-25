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

関連トピック [SRP オプションの特徴](/help/communities/working-with-srp.md#characteristics-of-srp-options) および [推奨されるトポロジ](/help/communities/topologies.md).

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

この [ストレージ設定コンソール](/help/communities/srp-config.md) デフォルトのストレージ設定を選択でき、使用する SRP の実装を識別できます。

**AEM オーサーインスタンス上：**

* グローバルナビゲーションから、に移動します。 **[!UICONTROL ツール/コミュニティ/ストレージ設定]** を選択して、 **[!UICONTROL Adobeストレージリソースプロバイダー（ASRP）]**.

![asrp-default](assets/asrp-default.png)

プロビジョニング・プロセスから得られる情報を次に示します。

* **データセンター URL**：プルダウンして、アカウント担当者が識別した実稼動データセンターを選択します。
* **デフォルトレポートスイート**：デフォルトレポートスイートの名前を入力します。
* **消費者キー**：コンシューマーキーを入力します。
* **秘密鍵**：秘密鍵を入力します。
* 「**送信**」を選択します。

パブリッシュインスタンスを準備します。

* [暗号鍵をレプリケートします](#replicate-the-crypto-key)
* [設定をレプリケートします](#publishing-the-configuration)

設定を送信したら、接続をテストします。

* を選択 **設定をテスト**.

  オーサーインスタンスとパブリッシュインスタンスごとに、ストレージ設定コンソールからデータセンターへの接続をテストします。

* 次の方法で、プロファイルデータのサイト URL をデータセンターからルーティングできることを確認します [リンクの外部化](#externalize-links).

### 暗号鍵をレプリケート {#replicate-the-crypto-key}

コンシューマーキーと秘密鍵は暗号化されます。 キーを適切に暗号化/復号化するには、プライマリ Granite 暗号キーがすべてのAEM インスタンスで同じである必要があります。

の指示に従います。 [暗号鍵をレプリケート](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### リンクを外部化 {#externalize-links}

プロファイルおよびプロファイル画像の正しいリンクについては、必ず適切に設定してください [Link Externalizer の設定](/help/sites-developing/externalizer.md).

ドメインを、データセンター URL （ASRP エンドポイント）からルーティング可能な URL に設定してください。

### 時刻の同期 {#time-synchronization}

ASRP エンドポイントとの認証を成功させるには、ホストされているAEM Communitiesを実行しているマシンを時刻同期する必要があります（例：） [ネットワークタイムプロトコル（NTP）](https://www.ntp.org/).

### 設定の公開 {#publishing-the-configuration}

ASRP は、すべてのオーサーインスタンスとパブリッシュインスタンスで共通ストアとして識別される必要があります。

パブリッシュ環境で同一の設定を使用できるようにするには：

AEM オーサーインスタンス上：

* メインメニューからに移動する **[!UICONTROL ツール]** > **[!UICONTROL デプロイメント]** > **[!UICONTROL 複製]**
* を選択 **ツリーのアクティベート**
* **開始パス**：を参照します。 `/conf/global/settings/communities/srpc/`
* 選択を解除 **変更済みのみ**
* を選択 **Activate**

## AEM 6.0 からのアップグレード {#upgrading-from-aem}

>[!CAUTION]
>
>公開済みコミュニティサイトで ASRP を有効にすると、に既に格納されている UGC はすべてになります。 [JCR](/help/communities/jsrp.md) オンプレミスストレージとクラウドストレージ間のデータの同期がないので、が表示されなくなりました。

**`AEM Communities Extension`** は、以前AEM 6.0 social communities as a cloud service で導入されました。 AEM 6.1 Communities の場合、クラウド設定は必要ありません。から ASRP を選択するだけです [ストレージ設定コンソール](/help/communities/srp-config.md).

新しいストレージ構造により、に従う必要があります。 [アップグレード](/help/communities/upgrade.md#adobe-cloud-storage) ソーシャルコミュニティからコミュニティにアップグレードする際の手順。

## ユーザーデータの管理 {#managing-user-data}

について *ユーザー*, *ユーザープロファイル* および *ユーザーグループ*（多くの場合、パブリッシュ環境で入力されます）

* [ユーザー同期](/help/communities/sync.md)
* [ユーザーとユーザーグループの管理](/help/communities/users.md)

## トラブルシューティング {#troubleshooting}

### アップグレード後に UGC が表示されなくなる {#ugc-disappears-after-upgrade}

既存のAEM 6.0 ソーシャルコミュニティサイトからアップグレードする場合は、次の手順に従ってください [アップグレード手順](/help/communities/upgrade.md#adobe-cloud-storage)そうでない場合、UGC は失われます。

### 認証エラー {#authentication-errors}

データセンター URL に対する認証エラーを受け取り、AEM error.log に古いタイムスタンプに関するメッセージが含まれている場合は、時間同期が行われていることを確認します。

次のようなツールを使用します [ネットワークタイムプロトコル（NTP）](https://www.ntp.org/) を使用して、すべてのAEM オーサーサーバーとパブリッシュサーバーを時間同期させます。

### 検索に新しいコンテンツが表示されない {#new-content-does-not-appear-in-searches}

クラウドストレージインフラストラクチャが使用するAdobe *最終的な整合性* ：スケーリングとパフォーマンスの目標を達成します。 このため、新しいコンテンツはすぐに使用できず、検索結果に表示されるまでに数秒かかります。

最終的な一貫性に影響する間隔が監視されている間、新しいコンテンツが検索で表示されるまでに数秒以上かかる場合は、アカウント担当者にお問い合わせください。

### ASRP で UGC が表示されない {#ugc-not-visible-in-asrp}

ストレージオプションの設定をチェックして、ASRP がデフォルトのプロバイダーとして設定されていることを確認します。 デフォルトでは、ストレージリソースプロバイダーは ASRP ではなく JSRP です。

すべてのオーサーインスタンスおよびパブリッシュ AEMインスタンスで、ストレージ設定コンソールに再度アクセスするか、AEM リポジトリを確認します。

JCR で次の場合： [/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* 次を含まない [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp) ノードの場合は、ストレージプロバイダーが JSRP であることを意味します。
* srpc ノードが存在し、かつが [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration) ノードで、defaultconfiguration のプロパティは ASRP をデフォルトのプロバイダーとして定義します。
