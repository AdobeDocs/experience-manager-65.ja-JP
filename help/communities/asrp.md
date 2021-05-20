---
title: ASRP - Adobe ストレージリソースプロバイダー
seo-title: ASRP - Adobe ストレージリソースプロバイダー
description: リレーショナルデータベースを共通ストアとして使用するように AEM Communities を設定する
seo-description: リレーショナルデータベースを共通ストアとして使用するように AEM Communities を設定する
uuid: abe47ad9-9f72-4dad-a5e9-6d621a9722d4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 3e81b519-57ca-4ee1-94bd-7adac4605407
docset: aem65
role: Administrator
exl-id: 6430ed96-5d96-41b6-866f-90b34ff84f7a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 33%

---

# ASRP - Adobe ストレージリソースプロバイダー {#asrp-adobe-storage-resource-provider}

## ASRP について {#about-asrp}

AEM CommunitiesがASRPを共通ストアとして使用するように設定されている場合、同期やレプリケーションを必要とせずに、すべてのオーサーインスタンスとパブリッシュインスタンスからユーザー生成コンテンツ(UGC)にアクセスできます。

[SRP オプションの特性](/help/communities/working-with-srp.md#characteristics-of-srp-options)と[推奨されるトポロジ](/help/communities/topologies.md)も参照してください。

## 要件 {#requirements}

ASRP の使用には追加ライセンスが必要です。

UGC用のASRPを使用するようにAEM Communitiesサイトを設定するには、次の点についてアカウント担当者にお問い合わせください。

* データセンター URL（ASRP エンドポイントのアドレス）
* 消費者キー
* 秘密鍵
* レポートスイート ID

消費者キーと秘密鍵は、企業の全レポートスイート間で共通です。テナントごとに1つのレポートスイートがあります。

## 設定 {#configuration}

### ASRP の選択  {#select-asrp}

[ストレージ設定コンソール](/help/communities/srp-config.md)では、使用するSRPの実装を指定するデフォルトのストレージ設定を選択できます。

**AEMオーサーインスタンスで、次の操作を実行します。**

* グローバルナビゲーションから、**[!UICONTROL ツール/コミュニティ/ストレージ設定]**&#x200B;に移動し、**[!UICONTROL Adobeストレージリソースプロバイダー(ASRP)]**&#x200B;を選択します。

![asrp-default](assets/asrp-default.png)

次の情報は、プロビジョニングプロセスから取得されます。

* **データセンターのURL**:プルダウンして、アカウント担当者が特定した実稼動データセンターを選択します。
* **デフォルトのレポートスイート**:デフォルトのレポートスイートの名前を入力します。
* **消費者キー**:消費者キーを入力します。
* **秘密鍵**:秘密を入力します。
* 「**送信**」を選択します。

以下を実行してパブリッシュインスタンスを用意します。

* [暗号鍵のレプリケート](#replicate-the-crypto-key)
* [設定のレプリケート](#publishing-the-configuration)

設定を送信したら、以下の手順で接続をテストします。

* 「**テスト設定**」を選択します。

   オーサーインスタンスとパブリッシュインスタンスごとに、ストレージ設定コンソールからデータセンターへの接続をテストします。

* [リンク](#externalize-links)を外部化することで、プロファイルデータのサイトURLがデータセンターからルーティング可能であることを確認します。

### 暗号鍵のレプリケーション {#replicate-the-crypto-key}

消費者キーと秘密鍵は暗号化されます。キーを正しく暗号化/復号化するには、プライマリGranite暗号キーがすべてのAEMインスタンスで同じである必要があります。

[暗号鍵のレプリケーション](/help/communities/deploy-communities.md#replicate-the-crypto-key)の手順に従います。

### リンクの外部向け変換 {#externalize-links}

正しいプロファイルとプロファイルイメージリンクを得るには、Link Externalizer](/help/sites-developing/externalizer.md)を正しく設定してください。[

必ず、データセンターURL（ASRPエンドポイント）からルーティング可能なURLにするドメインを設定してください。

### 時刻の同期 {#time-synchronization}

ASRP エンドポイントでの認証を正常におこなうには、[ネットワークタイムプロトコル（NTP）](https://www.ntp.org/)などを使用して、AEM Communities を実行しているマシンの時刻を同期する必要があります。

### 設定の公開  {#publishing-the-configuration}

すべてのオーサーインスタンスとパブリッシュインスタンスで、ASRP が共通ストアとして指定されている必要があります。

パブリッシュ環境で同一の設定を使用できるようにするには：

AEMオーサーインスタンスで、次の操作を実行します。

* メインメニューから&#x200B;**[!UICONTROL ツール]** > **[!UICONTROL 操作]** > **[!UICONTROL レプリケーション]**&#x200B;に移動します。
* 「**ツリーをアクティブ化**」を選択します。
* **開始パス**:参照する  `/conf/global/settings/communities/srpc/`
* 「**変更済み**&#x200B;のみ」の選択を解除します。
* **アクティブ化**&#x200B;を選択します。

## AEM 6.0 からのアップグレード {#upgrading-from-aem}

>[!CAUTION]
>
>公開済みのコミュニティサイトでASRPを有効にした場合、オンプレミスストレージとクラウドストレージの間でデータの同期がおこなわれないので、既に[JCR](/help/communities/jsrp.md)に保存されているUGCは表示されなくなります。

**`AEM Communities Extension`** は、AEM 6.0のソーシャルコミュニティas a cloud serviceで以前に導入されました。AEM 6.1 Communities以降、クラウド設定は不要です。[ストレージ設定コンソール](/help/communities/srp-config.md)からASRPを選択するだけです。

新しいストレージ構造により、ソーシャルコミュニティからコミュニティにアップグレードするときは、[アップグレード](/help/communities/upgrade.md#adobe-cloud-storage)手順に従う必要があります。

## ユーザーデータの管理  {#managing-user-data}

パブリッシュ環境で頻繁に入力されるユーザー、ユーザープロファイルおよびユーザーグループについては、以下を参照してください。******

* [ユーザー同期](/help/communities/sync.md)
* [ユーザーとユーザーグループの管理](/help/communities/users.md)

## トラブルシューティング {#troubleshooting}

### アップグレード後に UGC が表示されない  {#ugc-disappears-after-upgrade}

既存のAEM 6.0ソーシャルコミュニティサイトからアップグレードする場合は、[アップグレード手順](/help/communities/upgrade.md#adobe-cloud-storage)に従ってください。そうしないと、UGCが失われてしまいます。

### 認証エラー {#authentication-errors}

データセンター URL に対する認証エラーを受け取り、また AEM error.log に古いタイムスタンプに関するメッセージが含まれている場合は、時刻の同期がおこなわれているかを確認してください。

[Network Time Protocol(NTP)](https://www.ntp.org/)などのツールを使用して、すべてのAEMオーサーサーバーとパブリッシュサーバーの時刻を同期します。

### 新しいコンテンツが検索結果に表示されない {#new-content-does-not-appear-in-searches}

Adobeクラウドストレージインフラストラクチャは、*最終的な整合性*&#x200B;を使用して、拡張とパフォーマンスの目標を達成します。 このため、新しいコンテンツはすぐには利用できず、検索結果に表示されるまでに数秒かかります。

最終的な整合性に影響する間隔は監視されますが、新しいコンテンツが検索で表示されるまでに数秒以上かかる場合は、アカウント担当者にお問い合わせください。

### UGC が ASRP で表示されない {#ugc-not-visible-in-asrp}

ストレージオプションの設定を確認して、ASRPがデフォルトのプロバイダーに設定されていることを確認します。 デフォルトでは、ストレージリソースプロバイダーはASRPではなくJSRPです。

すべてのオーサーインスタンスとパブリッシュAEMインスタンスで、ストレージ設定コンソールに再度アクセスするか、AEMリポジトリを確認します。

JCRで、 [/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)の場合：

* [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp)ノードが含まれない場合は、ストレージプロバイダーがJSRPであることを意味します。
* srpcノードが存在し、[defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration)ノードが含まれる場合は、defaultconfigurationのプロパティによってASRPがデフォルトのプロバイダーとして定義されます。
