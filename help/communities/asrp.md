---
title: ASRP - Adobe ストレージリソースプロバイダー
description: リレーショナルデータベースを共通ストアとして使用するようにAEM Communitiesを設定する
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 6430ed96-5d96-41b6-866f-90b34ff84f7a
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 3%

---

# ASRP - Adobe ストレージリソースプロバイダー {#asrp-adobe-storage-resource-provider}

## ASRP について {#about-asrp}

AEM Communitiesが ASRP を共通ストアとして使用するように設定されている場合、同期やレプリケーションを必要とせずに、すべてのオーサーインスタンスとパブリッシュインスタンスからユーザー生成コンテンツ (UGC) にアクセスできます。

関連トピック [SRP オプションの特性](/help/communities/working-with-srp.md#characteristics-of-srp-options) および [推奨されるトポロジ](/help/communities/topologies.md).

## 要件 {#requirements}

ASRP を使用するには、追加のライセンスが必要です。

UGC 用の ASRP を使用するようにAEM Communitiesサイトを設定するには、次のアカウント担当者にお問い合わせください。

* データセンター URL （ASRP エンドポイントのアドレス）
* 消費者キー
* 秘密鍵
* レポートスイート ID

消費者と秘密鍵は、会社のすべてのレポートスイートで共有されます。 テナントごとに 1 つのレポートスイートがあります。

## 設定 {#configuration}

### ASRP を選択 {#select-asrp}

The [ストレージ設定コンソール](/help/communities/srp-config.md) では、使用する SRP の実装を指定するデフォルトのストレージ設定を選択できます。

**AEMオーサーインスタンス上：**

* グローバルナビゲーションから、に移動します。 **[!UICONTROL ツール/コミュニティ/ストレージ設定]** を選択し、 **[!UICONTROL Adobeストレージリソースプロバイダ (ASRP)]**.

![asrp-default](assets/asrp-default.png)

次の情報は、プロビジョニングプロセスから取得されます。

* **データセンター URL**：プルダウンして、アカウント担当者が特定した実稼動データセンターを選択します。
* **デフォルトのレポートスイート**：デフォルトのレポートスイートの名前を入力します。
* **消費者キー**：消費者キーを入力します。
* **秘密鍵**：秘密鍵を入力します。
* 「**送信**」を選択します。

パブリッシュインスタンスを準備します。

* [暗号鍵のレプリケート](#replicate-the-crypto-key)
* [設定のレプリケート](#publishing-the-configuration)

設定を送信した後、接続をテストします。

* 選択 **設定をテスト**.

  オーサーインスタンスとパブリッシュインスタンスごとに、ストレージ設定コンソールからデータセンターへの接続をテストします。

* プロファイルデータのサイト URL が [リンクの外部化](#externalize-links).

### 暗号鍵のレプリケート {#replicate-the-crypto-key}

消費者キーと秘密鍵は暗号化されます。 キーを正しく暗号化/復号化するには、すべてのAEMインスタンスでプライマリ Granite 暗号キーが同じである必要があります。

次の手順に従います。 [暗号鍵のレプリケート](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### リンクを外部化 {#externalize-links}

正しいプロファイルとプロファイルイメージリンクを作成するには、 [Link Externalizer の設定](/help/sites-developing/externalizer.md).

必ず、データセンター URL（ASRP エンドポイント）からルーティング可能な URL にドメインを設定してください。

### 時間同期 {#time-synchronization}

ASRP エンドポイントでの認証を正常におこなうには、ホストされているAEM Communitiesを実行しているマシンを、と同期する必要があります ( 例： [ネットワークタイムプロトコル (NTP)](https://www.ntp.org/).

### 設定の公開 {#publishing-the-configuration}

ASRP は、すべてのオーサーインスタンスとパブリッシュインスタンスで共通ストアとして識別される必要があります。

パブリッシュ環境で同じ設定を使用できるようにするには、次の手順を実行します。

AEMオーサーインスタンス上：

* メインメニューからに移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 導入]** > **[!UICONTROL レプリケーション]**
* 選択 **ツリーをアクティベート**
* **開始パス**：参照 `/conf/global/settings/communities/srpc/`
* 選択を解除 **変更済みのみ**
* 選択 **有効化**

## AEM 6.0 からのアップグレード {#upgrading-from-aem}

>[!CAUTION]
>
>公開済みのコミュニティサイトで ASRP を有効にした場合、既ににに保存されている UGC はすべて [JCR](/help/communities/jsrp.md) は、オンプレミスストレージとクラウドストレージの間でデータを同期しないので、表示されなくなりました。

**`AEM Communities Extension`** は、以前、AEM 6.0 のソーシャルコミュニティでクラウドサービスとして導入されました。 AEM 6.1 Communities 以降、クラウド設定は必要ありません。単に [ストレージ設定コンソール](/help/communities/srp-config.md).

新しいストレージ構造により、 [アップグレード](/help/communities/upgrade.md#adobe-cloud-storage) ソーシャルコミュニティからコミュニティにアップグレードする際の手順

## ユーザーデータの管理 {#managing-user-data}

に関する情報 *ユーザー*, *ユーザープロファイル* および *ユーザーグループ*&#x200B;パブリッシュ環境に入力されることが多い場合は、次にアクセスします。

* [ユーザー同期](/help/communities/sync.md)
* [ユーザーとユーザーグループの管理](/help/communities/users.md)

## トラブルシューティング {#troubleshooting}

### アップグレード後に UGC が消える {#ugc-disappears-after-upgrade}

既存のAEM 6.0 ソーシャルコミュニティサイトからアップグレードする場合は、必ず [アップグレード手順](/help/communities/upgrade.md#adobe-cloud-storage)を含めない場合、UGC は失われたように見えます。

### 認証エラー {#authentication-errors}

データセンター URL に対する認証エラーを受け取り、AEM error.log に古いタイムスタンプに関するメッセージが含まれている場合は、時刻の同期がおこなわれていることを確認します。

次のようなツールを使用します。 [ネットワークタイムプロトコル (NTP)](https://www.ntp.org/) すべてのAEMオーサーサーバーとパブリッシュサーバーを時間同期する場合。

### 検索に新しいコンテンツが表示されない {#new-content-does-not-appear-in-searches}

Adobeクラウドストレージインフラストラクチャは、 *最終的な一貫性* スケーリングとパフォーマンスの目標を達成する。 そのため、新しいコンテンツはすぐには利用できず、検索結果に表示されるまで数秒かかります。

最終的な一貫性に影響する間隔は監視されますが、新しいコンテンツが検索に表示されるまでに数秒以上かかる場合は、アカウント担当者にお問い合わせください。

### UGC が ASRP で表示されない {#ugc-not-visible-in-asrp}

ストレージオプションの設定を確認して、ASRP がデフォルトのプロバイダーに設定されていることを確認します。 デフォルトでは、ストレージリソースプロバイダーは ASRP ではなく JSRP です。

すべてのオーサーインスタンスとパブリッシュAEMインスタンスで、ストレージ設定コンソールに再度アクセスするか、AEMリポジトリを確認します。

JCR で、 [/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* 次を含まない [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp) ノードの場合、ストレージプロバイダーが JSRP であることを意味します。
* srpc ノードが存在し、次を含む場合 [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration) ノードのデフォルト設定のプロパティでは、ASRP がデフォルトのプロバイダーとして定義されます。
