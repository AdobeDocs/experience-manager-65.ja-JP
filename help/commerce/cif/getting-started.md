---
title: AEMコンテンツとコマースの使用の手引き
description: AEMコンテンツおよびコマースプロジェクトを展開する方法を説明します。
topics: Commerce
feature: Commerce統合フレームワーク
thumbnail: 37843.jpg
translation-type: tm+mt
source-git-commit: 8ead3d1b24177effa4d40141408c5676eaabcc30
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 6%

---

# AEMコンテンツとコマースの使い始めに{#start}

AEMコンテンツとコマースを使い始めるには、AEM 6.5用AEMコンテンツとコマース追加オンをインストールする必要があります。

## 最小ソフトウェア要件

[AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7以降が必要です。

## オンボーディング {#onboarding}

AEMコンテンツとコマースのオンボーディングは、次の2つの手順で構成されます。

1. AEM 6.5向けAEMコンテンツ追加とコマースオンのインストール

2. AEMとコマースソリューションの接続

### AEM 6.5用AEM Content and Commenceアドオンのインストール

AEM 6.5用のAEM Commerce 追加-Onを[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)ポータルからダウンロードしてインストールします。

必要なAEM 6.5 Service Packを開始してインストールします。 最後に使用可能なService Packをインストールすることをお勧めします。

    >[!NOTE]
    >
    >これは、AEM Managed Serviceのお客様向けにCSEが行います。

### AEMをコマースシステムに接続する

AEMは、AEM用のアクセス可能なGraphQLエンドポイントを持つ任意のコマースシステムに接続できます。 これらのエンドポイントは通常、公開されている状態で使用できます。また、個々のプロジェクトの設定に応じて、プライベートVPNまたはローカル接続を介して接続することもできます。

オプションで、認証が必要な追加のCIF機能を使用するために、認証ヘッダーを提供できます。

[AEMプロジェクトのアーキタイプ](https://github.com/adobe/aem-project-archetype)で生成されたプロジェクトと、[デフォルトの設定](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)に既に含まれている[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)を調整する必要があります。

`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`の`url`の値を、コマースシステムのGraphQLエンドポイントに置き換えます。 この設定は、OSGIコンソールを使用するか、プロジェクトを介してOSGI設定をデプロイすることで行うことができます。 ステージングシステムと実稼働システムの設定は、AEMの実行モードを変えてサポートします。

AEM Content and Commerce 追加-OnおよびCIF Core Componentsは、AEMサーバー側接続とクライアント側接続の両方を使用します。 クライアント側のCIFコアコンポーネントとCIF追加-Onオーサリングツールは、デフォルトで`/api/graphql`に接続します。 これは、必要に応じてCIFCloud Service設定で調整できます（以下を参照）。

CIFアドオンは`/api/graphql`にGraphQLプロキシサーブレットを提供します。このサーブレットは、[ローカル開発](develop.md)で使用することもできます。 実稼働環境でのデプロイメントでは、AEM Dispatcher経由または他のネットワーク層（CDNなど）で、コマースGraphQLエンドポイントへのリバースプロキシを設定することを強くお勧めします。

## ストアとカタログの設定{#catalog}

アドオンと[CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、異なるコマースストア(またはストア表示など)に接続された複数のAEMサイト構造で使用できます。 デフォルトでは、CIFアドオンは、Adobeコマースのデフォルトのストアとカタログ(Magento)に接続するデフォルトの設定を使用してデプロイされます。

この設定は、次の手順に従って、CIFCloud Service設定を使用してプロジェクトに合わせて調整できます。

1. AEMで、ツール/Cloud Services/CIF設定に移動します。

2. 変更するコマース構成を選択します

3. アクションバーで設定プロパティを開く

![CIFCloud Servicesの設定](/help/commerce/cif/assets/cif-cloud-service-config.png)

次のプロパティを設定できます。

- GraphQL Client — コマースバックエンド通信用に設定済みのGraphQLクライアントを選択します。 通常はデフォルトのままです。
- ストア表示- (Magento)ストア表示ID。 空の場合は、デフォルトのストア表示が使用されます。
- GraphQL Proxy Path - AEMのURLパスGraphQL Proxyは、コマースバックエンドGraphQLエンドポイントにリクエストをプロキシするために使用します。
   >[!NOTE]
   >
   > ほとんどの設定では、デフォルト値`/api/graphql`は変更できません。 指定されたGraphQLプロキシを使用しない高度な設定のみが、この設定を変更する必要があります。
- カタログUIDのサポートを有効にする — コマースバックエンドGraphQL呼び出しで、IDではなくUIDのサポートを有効にします。
   >[!NOTE]
   >
   > UIDのサポートがAdobeコマース(Magento) 2.4.2で導入されました。コマースバックエンドでバージョン2.4.2以降のGraphQLスキーマがサポートされている場合にのみ有効にしてください。
- カタログルートカテゴリID — ストアカタログルートの識別子（UIDまたはID）

上記の設定は参考用です。 プロジェクトは独自の設定を提供する必要があります。

複数のAEMサイト構造を様々なコマースカタログと組み合わせて使用するより複雑な設定については、[コマースマルチストアの設定](configuring/multi-store-setup.md)チュートリアルを参照してください。

## その他のリソース {#additional-resources}

- [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)
- [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
- [コマースマルチストアの設定](configuring/multi-store-setup.md)
