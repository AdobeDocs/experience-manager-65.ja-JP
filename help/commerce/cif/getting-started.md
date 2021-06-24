---
title: AEM Content and Commerce - はじめに
description: AEM Content and Commerceプロジェクトをデプロイする方法について説明します。
topics: Commerce
feature: コマース統合フレームワーク
thumbnail: 37843.jpg
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
source-git-commit: 61b8d0bf960bd03a19d22061f3c897a56259dd24
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 38%

---

# AEM Content and Commerce - はじめに {#start}

AEMコンテンツとコマースの使用を開始するには、AEM Content and Commerce Add-On for AEM 6.5をインストールする必要があります。

## 最小ソフトウェア要件

[AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)  7以降が必要です。

## オンボーディング {#onboarding}

AEMコンテンツとコマースのオンボーディングは、次の2つの手順で構成されます。

1. AEM 6.5用AEMコンテンツおよびコマースアドオンのインストール

2. AEMとコマースソリューションの接続

### AEM 6.5用AEMコンテンツおよびコマースアドオンのインストール {#install-add-on}

AEM 6.5用AEM Commerce Add-Onを[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)ポータルからダウンロードしてインストールします。

必要なAEM 6.5サービスパックを起動してインストールします。 最新の利用可能なサービスパックをインストールすることをお勧めします。

>[!NOTE]
>
>これは、AEM Managed Serviceのお客様向けに、CSEがおこないます。

### AEMをコマースシステムに接続する {#connect}

AEMは、AEM用のアクセス可能なGraphQLエンドポイントを持つ任意のコマースシステムに接続できます。 これらのエンドポイントは通常、公開されている場合と、個々のプロジェクトの設定に応じて、プライベートVPNまたはローカル接続を介して接続する場合があります。

オプションで、認証が必要な追加のCIF機能を使用するために認証ヘッダーを提供できます。

[AEM Project Archetype](https://github.com/adobe/aem-project-archetype)で生成されるプロジェクトと、[デフォルト設定](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)に既に含まれている[AEM Venia参照用ストア](https://github.com/adobe/aem-cif-guides-venia)を調整する必要があります。

`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`の`url`の値を、コマースシステムのGraphQLエンドポイントに置き換えます。 この設定は、OSGiコンソールを使用するか、プロジェクトを介してOSGi設定をデプロイすることでおこなえます。 ステージングシステムと実稼動システムでは、異なるAEM実行モードを使用して異なる設定がサポートされています。

AEM ContentとCommerceアドオンおよびCIFコアコンポーネントは、AEMサーバー側接続とクライアント側接続の両方を使用します。 クライアント側のCIFコアコンポーネントとCIFアドオンオーサリングツールは、デフォルトで`/api/graphql`に接続されます。 これは、必要に応じてCIFCloud Service設定で調整できます（以下を参照）。

CIFアドオンは、`/api/graphql`にGraphQLプロキシサーブレットを提供します。このサーブレットは、オプションで[ローカル開発](develop.md)に使用できます。 実稼動デプロイメントの場合は、AEM Dispatcherを介する、または他のネットワークレイヤー（CDNなど）でコマースGraphQLエンドポイントへのリバースプロキシを設定することを強くお勧めします。

## ストアとカタログの設定 {#catalog}

アドオンと[CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、異なるコマースストア（またはストア表示など）に接続された複数のAEMサイト構造で使用できます。 デフォルトでは、CIFアドオンは、Adobeコマースのデフォルトのストアおよびカタログ(Magento)に接続するデフォルト設定を使用してデプロイされます。

この設定は、次の手順に従って、CIF Cloud Service 設定を使用してプロジェクトに合わせて調整できます。

1. AEM で、ツール／Cloud Services／CIF 設定に移動します。

2. 変更するコマース設定を選択します。

3. アクションバーから設定プロパティを開きます。

![CIF Cloud Services の設定](/help/commerce/cif/assets/cif-cloud-service-config.png)

次のプロパティを設定できます。

- GraphQL クライアント - コマースバックエンド通信用に設定済みの GraphQL クライアントを選択します。これは通常、デフォルトのままです。
- ストア表示 -（Magento）ストア表示の識別子。空の場合は、デフォルトのストア表示が使用されます。
- GraphQL プロキシパス - AEM の GraphQL プロキシが、コマースバックエンドの GraphQL エンドポイントへのリクエストをプロキシするために使用する URL パス。
   >[!NOTE]
   >
   > ほとんどの設定で、デフォルト値 `/api/graphql` は変更できません。この設定を変更するのは、指定された GraphQL プロキシを使用しない高度な設定でのみです。
- カタログ UID のサポートを有効にする - コマースバックエンドの GraphQL 呼び出しで、ID ではなく UID のサポートを有効にします。
   >[!NOTE]
   >
   > UID のサポートは、Adobe Commerce（Magento）2.4.2 で導入されました。コマースバックエンドがバージョン 2.4.2 以降の GraphQL スキーマをサポートしている場合にのみ有効にします。
- カタログのルートカテゴリ識別子 - ストアカタログルートの識別子（UID または ID）
   >[!CAUTION]
   >
   > CIFコアコンポーネントバージョン2.0.0以降、`id`のサポートは削除され、`uid`に置き換えられました。 プロジェクトでCIFコアコンポーネントバージョン2.0.0を使用している場合は、カタログUIDのサポートを有効にし、有効なカテゴリUIDを「カタログルートカテゴリ識別子」として使用する必要があります。

上記の設定は参照用です。プロジェクトは独自の設定を提供する必要があります。

複数の AEM サイト構造を異なるコマースカタログと組み合わせて使用する、より複雑な設定については、チュートリアル「[コマースマルチストアの設定](configuring/multi-store-setup.md)」を参照してください。

## その他のリソース {#additional-resources}

- [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)
- [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
- [コマースマルチストアの設定](configuring/multi-store-setup.md)
