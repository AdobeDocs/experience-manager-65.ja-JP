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
translation-type: tm+mt
source-git-commit: ef57d53fc780bd222abbe994fc71e133ce8a77fc
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 33%

---


# ASRP - Adobe ストレージリソースプロバイダー {#asrp-adobe-storage-resource-provider}

## ASRP について {#about-asrp}

AEM Communitiesが共通ストアとしてASRPを使用するように設定されている場合、ユーザー生成コンテンツ(UGC)は、すべてのオーサーインスタンスとパブリッシュインスタンスからアクセスでき、同期や複製は不要です。

[SRP オプションの特性](/help/communities/working-with-srp.md#characteristics-of-srp-options)と[推奨されるトポロジ](/help/communities/topologies.md)も参照してください。

## 要件 {#requirements}

ASRP の使用には追加ライセンスが必要です。

UGCにASRPを使用するようにAEM Communitiesサイトを設定するには、次の点についてアカウント担当者にお問い合わせください。

* データセンター URL（ASRP エンドポイントのアドレス）
* 消費者キー
* 秘密鍵
* レポートスイート ID

消費者キーと秘密鍵は、企業の全レポートスイート間で共通です。テナントごとに1つのレポートスイートがあります。

## 設定 {#configuration}

### ASRP の選択 {#select-asrp}

[ストレージ設定コンソール](/help/communities/srp-config.md)では、デフォルトのストレージ設定を選択できます。これにより、使用するSRPの実装が識別されます。

**AEM作成者インスタンスで：**

* グローバルナビゲーションから、**[!UICONTROL ツール/コミュニティ/ストレージ設定]**&#x200B;に移動し、**[!UICONTROL Adobeストレージリソースプロバイダー(ASRP)]**&#x200B;を選択します。

![asrp-default](assets/asrp-default.png)

次の情報は、プロビジョニングプロセスから得られます。

* **データセンターURL**:プルダウンから、アカウント担当者が識別する本番データセンターを選択します。
* **デフォルトのレポートスイート**:デフォルトのレポートスイート名を入力します。
* **Consumer key**:Consumer keyを入力します。
* **シークレット**:シークレットを入力します。
* 「**送信**」を選択します。

以下を実行してパブリッシュインスタンスを用意します。

* [暗号化キーを複製します](#replicate-the-crypto-key)
* [設定を複製する](#publishing-the-configuration)

設定を送信したら、以下の手順で接続をテストします。

* 「**テスト構成**」を選択します。

   作成者インスタンスと発行インスタンスごとに、ストレージ設定コンソールからデータセンターへの接続をテストします。

* プロファイルデータのサイトURLがデータセンターからルーティング可能であることを[外部化リンク](#externalize-links)によって確認します。

### 暗号鍵のレプリケーション {#replicate-the-crypto-key}

消費者キーと秘密鍵は暗号化されます。キーを正しく暗号化/復号化するためには、すべてのAEMインスタンスでプライマリGranite Cryptoキーが同じである必要があります。

[暗号キーを複製](/help/communities/deploy-communities.md#replicate-the-crypto-key)の手順に従ってください。

### リンクの外部向け変換 {#externalize-links}

正しいプロファイルとプロファイルイメージのリンクを得るには、リンク外部化を正しく[設定](/help/sites-developing/externalizer.md)してください。

ドメインは、データセンターURL（ASRPエンドポイント）からルーティング可能なURLに設定してください。

### 時刻の同期 {#time-synchronization}

ASRP エンドポイントでの認証を正常におこなうには、[ネットワークタイムプロトコル（NTP）](https://www.ntp.org/)などを使用して、AEM Communities を実行しているマシンの時刻を同期する必要があります。

### 設定の公開  {#publishing-the-configuration}

すべてのオーサーインスタンスとパブリッシュインスタンスで、ASRP が共通ストアとして指定されている必要があります。

パブリッシュ環境で同一の設定を使用できるようにするには：

AEM作成者インスタンスで：

* メインメニューから&#x200B;**[!UICONTROL [ツール]>[操作]>[レプリケーション]]**&#x200B;に移動します。
* 「**ツリーをアクティブにする**」を選択します。
* **開始パス**:参照  `/etc/socialconfig/srpc/`
* 「**変更済み**&#x200B;のみ」を選択解除します。
* 「**アクティブ化**」を選択します。

## AEM 6.0 からのアップグレード {#upgrading-from-aem}

>[!CAUTION]
>
>公開済みのコミュニティサイトでASRPを有効にした場合、オンプレミスのストレージとクラウドのストレージ間でデータが同期されないので、[JCR](/help/communities/jsrp.md)に既に保存されているUGCは表示されなくなります。

**`AEM Communities Extension`** は、AEM 6.0のソーシャルコミュニティでクラウドサービスとして以前に導入されています。AEM 6.1 Communitiesでは、クラウド設定は不要です。単に[ストレージ設定コンソール](/help/communities/srp-config.md)からASRPを選択します。

新しいストレージ構造により、ソーシャルコミュニティからコミュニティにアップグレードするときは、[アップグレード](/help/communities/upgrade.md#adobe-cloud-storage)手順に従う必要があります。

## ユーザーデータの管理  {#managing-user-data}

パブリッシュ環境で頻繁に入力されるユーザー、ユーザープロファイルおよびユーザーグループについては、以下を参照してください。******

* [ユーザーの同期](/help/communities/sync.md)
* [ユーザーとユーザーグループの管理](/help/communities/users.md)

## トラブルシューティング {#troubleshooting}

### アップグレード後に UGC が表示されない {#ugc-disappears-after-upgrade}

既存のAEM 6.0ソーシャルコミュニティサイトからアップグレードする場合は、[アップグレード手順](/help/communities/upgrade.md#adobe-cloud-storage)に従ってください。そうしないと、UGCが失われてしまいます。

### 認証エラー {#authentication-errors}

データセンター URL に対する認証エラーを受け取り、また AEM error.log に古いタイムスタンプに関するメッセージが含まれている場合は、時刻の同期がおこなわれているかを確認してください。

[Network Time Protocol (NTP)](https://www.ntp.org/)などのツールを使用して、AEMの作成者やパブリッシュサーバーの時刻を同期します。

### 新しいコンテンツが検索結果に表示されない {#new-content-does-not-appear-in-searches}

Adobeクラウドのストレージインフラストラクチャは、*最終的な整合性*&#x200B;を使用して、拡張とパフォーマンスの目標を達成します。 このため、新しいコンテンツはすぐには利用できず、検索結果に表示されるまで数秒かかります。

最終的な一貫性に影響する間隔は監視されますが、新しいコンテンツが検索に表示されるまでに数秒以上かかる場合は、アカウント担当者にお問い合わせください。

### UGC が ASRP で表示されない {#ugc-not-visible-in-asrp}

ストレージオプションの設定を確認して、ASRPがデフォルトプロバイダーに設定されていることを確認します。 デフォルトでは、ストレージリソースプロバイダーはASRPではなくJSRPです。

すべての作成者および発行AEMインスタンスで、ストレージ設定コンソールに再度アクセスするか、AEMリポジトリを確認します。

JCRで、[/etc/socialconfig](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)の場合：

* [srpc](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc)ノードを含まない場合、ストレージプロバイダーがJSRPであることを意味します。
* srpcノードが存在し、ノード[defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)が含まれる場合、デフォルト設定のプロパティでASRPがデフォルトプロバイダーとして定義されます。

