---
title: AEM Content and Commerce - はじめに
description: AEM Content and Commerce プロジェクトをデプロイする方法について説明します。
topics: Commerce
feature: Commerce Integration Framework
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 100%

---

# AEM Content and Commerce - はじめに {#start}

AEM Content and Commerce の使用を開始するには、AEM Content and Commerce Add-On for AEM 6.5 をインストールする必要があります。

## 最小ソフトウェア要件

[AEM 6.5 サービスパック](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7 以降が必要です。

## オンボーディング  {#onboarding}

AEM Content and Commerce のオンボードは、次の 2 つの手順で構成されています。

1. AEM Content and Commerce Add-On for AEM 6.5 をインストールする

2. お使いのコマースソリューションに AEM を接続する

### AEM Content and Commerce Add-On for AEM 6.5 をインストールする {#install-add-on}

[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)ポータルから AEM Commerce Add-On for AEM 6.5 をダウンロードしてインストールします。

必要な AEM 6.5 サービスパックをインストールして起動します。入手可能な最新のサービスパックをインストールすることをお勧めします。

>[!NOTE]
>
>AEM Managed Service のお客様の場合、これは CSE が行います。

### お使いのコマースシステムに AEM を接続 {#connect}

AEM は、AEM 用のアクセス可能な GraphQL エンドポイントを持つ任意のコマースシステムに接続できます。これらのエンドポイントは通常、公開されているか、個々のプロジェクトの設定に応じて、プライベート VPN またはローカル接続を介して接続することができます。

オプションで、認証が必要な追加の CIF 機能を使用するために認証ヘッダーを指定できます。

[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)で生成されたプロジェクトと、 [デフォルト設定](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)に既に含まれている [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)は調整が必要です。

`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` の `url` の値をコマースシステムの GraphQL エンドポイントに置き換えます。この設定を行うには、OSGi コンソールを使用するか、プロジェクトを介して OSGi 設定をデプロイします。ステージングシステムと実稼動システムは、異なる AEM 実行モードを使用して異なる設定にすることができます。

AEM Content and Commerce Add-On および CIF コアコンポーネントでは、AEM サーバーサイド接続とクライアントサイド接続の両方を使用します。クライアントサイド CIF コアコンポーネントと CIF アドオンオーサリングツールは、デフォルトで `/api/graphql` に接続されます。これは、CIF Cloud Service 設定で必要に応じて調整できます（以下を参照）。

CIF アドオンでは、`/api/graphql` に GraphQL プロキシサーブレットが用意されているので、オプションでこれを[ローカル開発](develop.md)に使用できます。実稼動デプロイメントの場合は、AEM Dispatcher を使用して、または他のネットワークレイヤー（CDN など）で、コマース GraphQL エンドポイントへのリバースプロキシを設定することを強くお勧めします。

## ストアとカタログの設定 {#catalog}

このアドオンと [CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components) は、異なるコマースストア（またはストア表示など）に接続された複数の AEM サイト構造で使用できます。デフォルトでは、CIF アドオンは、Adobe Commerce のデフォルトストアとカタログに接続するデフォルト設定でデプロイされます。

この設定は、次の手順に従って、CIF Cloud Service 設定を使用してプロジェクトに合わせて調整できます。

1. AEM で、ツール／Cloud Services／CIF 設定に移動します。

2. 変更するコマース設定を選択します。

3. アクションバーから設定プロパティを開きます。

![CIF Cloud Services の設定](/help/commerce/cif/assets/cif-cloud-service-config.png)

次のプロパティを設定できます。

- GraphQL クライアント - コマースバックエンド通信用に設定済みの GraphQL クライアントを選択します。これは通常、デフォルトのままです。
- ストア表示 - ストア表示の識別子。空の場合は、デフォルトのストア表示が使用されます。
- GraphQL プロキシパス - AEM の GraphQL プロキシが、コマースバックエンドの GraphQL エンドポイントへのリクエストをプロキシするために使用する URL パス。

   >[!NOTE]
   >
   >ほとんどの設定で、デフォルト値 `/api/graphql` は変更できません。この設定を変更するのは、指定された GraphQL プロキシを使用しない高度な設定でのみです。

- カタログ UID のサポートを有効にする - コマースバックエンドの GraphQL 呼び出しで、ID ではなく UID のサポートを有効にします。

   >[!NOTE]
   >
   >UID のサポートは、Adobe Commerce 2.4.2 で導入されました。コマースバックエンドがバージョン 2.4.2 以降の GraphQL スキーマをサポートしている場合にのみ有効にします。

- カタログのルートカテゴリ識別子 - ストアカタログルートの識別子（UID または ID）

   >[!CAUTION]
   >
   >CIF コアコンポーネントバージョン 2.0.0 以降では、`id` のサポートが削除されて `uid` に置き換えられました。プロジェクトで CIF コアコンポーネントバージョン 2.0.0 を使用している場合は、カタログ UID のサポートを有効にし、有効なカテゴリ UID を「カタログルートカテゴリ識別子」として使用する必要があります。

上記の設定は参照用です。プロジェクトは、独自の設定を行う必要があります。

複数の AEM サイト構造を異なるコマースカタログと組み合わせて使用する、より複雑な設定については、チュートリアル「[コマースマルチストアの設定](configuring/multi-store-setup.md)」を参照してください。

## その他のリソース {#additional-resources}

- [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)
- [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
- [コマースマルチストアの設定](configuring/multi-store-setup.md)
