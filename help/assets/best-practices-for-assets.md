---
title: '[!DNL Assets] のベストプラクティス'
description: お客様の展開や構成に応じたベストプラクティスを特定して順守することで、負荷状態でのシステムの安定性とパフォーマンスを向上させます。
contentOwner: AG
feature: Asset Management
role: Developer, Admin
exl-id: 6b50f1b3-9c1c-47c8-a43e-6f40c42a41cc
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 100%
---
# [!DNL Assets] のベストプラクティス {#best-practices-for-assets}

[!DNL Adobe Experience Manager Assets] は、コンテンツの速度を上げることでビジネス目標の達成に貢献する、高品質のデジタルマーケティングエクスペリエンスを実現するうえできわめて重要な役割を果たします。 ビデオや Dynamic Media などのアセットを [!DNL Experience Manager Assets] 内で多数扱う場合、または定期的に大量にアップロードする場合、デジタルアセット管理のエクスペリエンスの最適化することは、システムを効率化するうえで非常に重要です。

組織における [!DNL Assets] の位置付けや、アセットの取り込み、レンディションの生成、メタデータの抽出に使用する機能に応じて、様々な領域でベストプラクティスを特定して順守することにより、負荷がかかった状態のシステムの安定性とパフォーマンスが大幅に向上します。

次のガイドを参照すると、お客様のニーズを満たすエンタープライズアセット管理システムを構築、管理するための知識とツールを得ることができます。

* [Assets パフォーマンスチューニングガイド](/help/assets/performance-tuning-guidelines.md)：実稼動環境への移行後を含めた実装のあらゆる段階において、システムから最大限のパフォーマンスを引き出すための一連のベストプラクティスが記載されています。
* [Assets サイジングガイド](/help/assets/assets-sizing-guide.md)：[!DNL Assets] 実装の予測を立てる際には、アセットのストレージ、CPU、メモリ、I/O、ネットワークスループットなどのリソースに十分な空きがあることを確認することが重要です。 これらのアイテムのサイジングには、システムに読み込まれたアセットの数を理解しておく必要があります。 このガイドには、[!DNL Assets] のデプロイに必要なインフラストラクチャやリソースを見積もるための効果的な指標を決定するためのベストプラクティスやサイジングツールが用意されています。
* [Assets 移行ガイド](/help/assets/assets-migration-guide.md)：従来使用していたシステムからアセットを Assets に移行する場合、移行プロセスを効率化するにはいくつかの手順を考慮する必要があります。 この移行ガイドには、アセットを [!DNL Experience Manager] に段階的に移行するタスクのベストプラクティスが記載されています。 これには、メタデータの適用、レンディションの生成、パブリッシュインスタンスへのアセットのアクティベートなどが含まれています。
* [Assets のネットワークに関する考慮事項のドキュメント](/help/assets/assets-network-considerations.md)：[!DNL Experience Manager] のデプロイメントを処理する際に、ネットワークのトポロジを理解することは、ネットワークのパフォーマンスを理解し、ボトルネックを特定して、期待するユーザーエクスペリエンスを説明するのに重要です。 [!DNL Assets] のネットワークに関する考慮事項のドキュメントでは、Assets のデプロイメントを設計する際のネットワークの考慮事項について説明します。
* [Assets モニタリングガイド](/help/assets/assets-monitoring-best-practices.md)：[!DNL Experience Manager] のデプロイメントの導入後は、システムの整合性およびオペレーションの効率性が確保されるよう、特定のタスクおよびシステム全般をモニタリングする必要があります。 このモニタリングガイドには、システムの様々な側面をモニタリングするためのベストプラクティスが記載されています。
* [Experience Manager デスクトップアプリケーションのベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=ja)：[!DNL Experience Manager] デスクトップアプリケーションは、デジタルアセット管理（DAM）ソリューションとユーザーのデスクトップをリンクします。ユーザーは、[!DNL Experience Manager] web ユーザーインターフェイスで使用できるファイルをデスクトップで直接開くことができます。 デスクトップアプリケーションの使いやすいワークフローは、デスクトップのオペレーティングシステムが提供するネットワーク共有テクノロジーを利用して実現しています。 このガイドには、[!DNL Experience Manager] デスクトップアプリケーションの主要な機能と推奨される使用例が記載されています。
* [Experience Manager と Creative Cloud 統合のベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)：[!DNL Experience Manager] のデプロイメントと [!DNL Creative Cloud] を複数の方法で統合できます。 ベストプラクティスに従って統合ワークフローおよびアセット転送ワークフローを効率化すると、効率を最大化することができます。 このガイドには、[!DNL Assets] と [!DNL Adobe Creative Cloud] の統合に関するベストプラクティスが含まれています。
