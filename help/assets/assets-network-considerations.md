---
title: '[!DNL Assets]ネットワークに関する考慮事項と要件です。'
description: Discusses network considerations when designing an [!DNL Adobe Experience Manager Assets] deployment.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 70%

---


# [!DNL Assets] ネットワークの考慮事項 {#assets-network-considerations}

Understanding your network is as important as understanding [!DNL Adobe Experience Manager Assets]. ネットワークはアップロード、ダウンロードおよびユーザーのエクスペリエンスに影響を与えることがあります。ネットワークトポロジを図解することで、ネットワークのパフォーマンスとユーザーエクスペリエンスの向上のために、ネットワーク上の渋滞地点や改善を要する部分を特定できます。

ネットワークの図には次の情報を含めてください。

* クライアントデバイス（コンピューター、モバイル、タブレットなど）からネットワークへの接続性。
* 企業ネットワークのトポロジ.
* Uplink to the internet from the corporate network and the [!DNL Experience Manager] environment.
* [!DNL Experience Manager] 環境のトポロジ。
* Define simultaneous consumers of the [!DNL Experience Manager] network interface.
* 定義された [!DNL Experience Manager] デプロイメントのワークフロー。

## クライアントデバイスからネットワークへの接続性 {#connectivity-from-the-client-device-to-the-corporate-network}

まず、個々のクライアントデバイスと企業ネットワークの接続性を図解します。この段階では、複数のユーザーが同じポイントにアクセスする、Wi-Fi 接続などの共有リソースや、アセットをアップロードおよびダウンロードするイーサネットスイッチを特定します。

![chlimage_1-353](assets/chlimage_1-353.png)

クライアントデバイスは、共有 Wi-Fi、共有スイッチへのイーサネット、VPN など、様々な方法で企業ネットワークに接続します。Identifying and understanding chokepoints on this network is important for [!DNL Assets] planning and to modify the network.

この図の左上では、3 つのデバイスが 48 Mbps Wi-Fi アクセスポイントを共有しています。すべてのデバイスで同時にアップロードすると、Wi-Fi ネットワークの帯域幅がデバイス間で共有されます。システム全体と比較して、3つのクライアントに対して、この分割されたチャネルで異なるチョークポイントが発生する場合がある。

低速なデバイスは同じアクセスポイントに接続する別のクライアントに影響を与えるので、Wi-Fi ネットワークの実際の速度を計測するのは困難です。アセットのやり取りに Wi-Fi を使用する場合は、複数のクライアントから同時に速度テストを実施してスループットを評価します。

図の左下には、2 つのデバイスが別個のチャネルを介して企業ネットワークに接続されています。このため、各デバイスは最低 10 Mbps および 100 Mbps の速度を利用できます。

右に表示されているコンピューターは VPN を介して企業ネットワークに接続されており、アップストリームの上限は 1 Mbps です。1 Mbps 接続と 1 Gbps 接続では、ユーザーエクスペリエンスは大幅に異なります。アセットのサイズによっては、そのタスクに対して VPN アップリンクが不十分になる可能性があります。

## 企業ネットワークのトポロジ {#topology-of-the-corporate-network}

![chlimage_1-354](assets/chlimage_1-354.png)

図では、企業ネットワーク内で使用されているアップリンクの速度が、通常使用されるものよりも高速になっています。これらのパイプは共有リソースです。50台のクライアントを処理すると予想される共有スイッチは、チョークポイントになる可能性があります。 最初の図では、2 台のコンピューターのみがその特定の接続を共有しています。

## Uplink to the internet from the corporate network and [!DNL Experience Manager] environment {#uplink-to-the-internet-from-the-corporate-network-and-aem-environment}

![chlimage_1-355](assets/chlimage_1-355.png)

インターネットや VPC 接続については、全体における帯域幅がピーク時の負荷やプロバイダーの大規模な停止により損なわれることがあるので、未知の要素を考慮に入れることが重要です。一般的に、インターネットの接続性は信頼できます。ただし、渋滞地点となることもあります。

企業ネットワークからインターネットへのアップリンクでは、他のサービスが帯域幅を使用している可能性があります。 Assets 専用または AEM Assets に優先的に割り当てる帯域幅を把握することが重要です。For example, if a 1 Gbps link is already at 80% utilization, you can only allocate a maximum of 20% of the bandwidth for [!DNL Experience Manager Assets].

企業のファイアウォールやプロキシも様々な方法で帯域幅を形成します。この種類のデバイスは QoS（Quality of Service）、ユーザーごとの帯域幅制限またはホストごとのビットレート制限を使用して帯域幅を優先的に割り当てることができます。These are important chokepoints to examine as they can significantly impact [!DNL Assets] user experience.

この例では、企業には 10 Gbps のアップリンクがあります。複数のクライアントが使用するのに十分です。また、ファイアウォールはホストに 10 Mbps のレート制限を課しています。この制限は、インターネットのアップリンクが 10 Gbps であっても、単一のホストへのトラフィックを 10 Mbps にスロットルする可能性があります。

これは、クライアント指向の最小のチョークポイントです。 ただし、このファイアウォールを担当するネットワーク操作グループとの許可リストの変更や構成を評価できます。

このサンプル図より、6 台のデバイスが 10 Mbps の概念的なチャネルを共有していると結論付けることができます。使用しているアセットのサイズによっては、これではユーザーの期待に応えるには不十分である可能性があります。

## [!DNL Experience Manager] 環境のトポロジ {#topology-of-the-aem-environment}

![chlimage_1-356](assets/chlimage_1-356.png)

Designing the topology of the [!DNL Experience Manager] environment requires detailed knowledge of the system configuration and how the network is connected within the user environment.

サンプルシナリオには、5つのサーバ、S3バイナリストア、およびDynamic Mediaが設定された発行ファームが含まれます。

The dispatcher shares it&#39;s 100Mbps connection with two entities, the outside world and the [!DNL Experience Manager] deployment. アップロードとダウンロードを同時に実行するには、この数を 2 で割る必要があります。接続された外部ストレージは別の接続を使用します。

The [!DNL Experience Manager] deployment shares it&#39;s 1Gbps connection with multiple services. ネットワークトポロジの観点では、これは単一のチャネルを異なるサービスで共有することと同じです。

Reviewing the network from the client device to the [!DNL Experience Manager] deployment, the smallest choke-point appears to be the 10 Mbit enterprise firewall throttle. You can use these values in the sizing calculator in the [Assets Sizing Guide](assets-sizing-guide.md) to determine the user experience.

## 定義済みの [!DNL Experience Manager] 導入ワークフロー {#defined-workflows-of-the-aem-deployment}

ネットワークのパフォーマンスを考慮する際には、システムで発生するワークフローや公開を考慮することが重要であることがあります。さらに、S3 などのネットワークに接続されたストレージや入出力のリクエストはネットワークの帯域幅を消費します。そのため、完全に最適化されたネットワークであっても、パフォーマンスはディスクの入出力によって制限されることがあります。

アセットの取り込み処理を効率化するには（特に大量のアセットをアップロードするとき）、アセットのワークフローを調べてその設定について詳しく理解します。

内部ワークフローのトポロジを評価する際には、次の内容を分析してください。

* アセットを書き込む手順
* アセットやメタデータが変更されたときに実行するワークフローやイベント
* アセットを読み取る手順

考慮すべき項目は次のとおりです。

* XMPメタデータの読み取り/書き込み/バック
* 自動アクティベートおよびレプリケート
* 透かし処理
* サブアセットの取り込み／ページの抽出
* ワークフローのオーバーラップ

アセットワークフローの定義に関するお客様の例は次のとおりです。

![chlimage_1-357](assets/chlimage_1-357.png)
