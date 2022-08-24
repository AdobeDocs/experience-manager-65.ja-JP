---
title: ' [!DNL Assets] のベストプラクティス'
description: お客様の展開や構成に応じたベストプラクティスを特定して順守することで、負荷状態でのシステムの安定性とパフォーマンスを向上させます。
contentOwner: AG
feature: Asset Management
role: Architect, Admin
exl-id: 6b50f1b3-9c1c-47c8-a43e-6f40c42a41cc
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 100%

---

# [!DNL Assets] のベストプラクティス {#best-practices-for-assets}

[!DNL Adobe Experience Manager Assets] は、コンテンツの速度を上げることでビジネス目標の達成に貢献する、高品質のデジタルマーケティングエクスペリエンスを実現するうえできわめて重要な役割を果たします。ビデオや Dynamic Media などのアセットを [!DNL Experience Manager Assets] 内で多数扱う場合、または定期的に大量にアップロードする場合、デジタルアセット管理のエクスペリエンスの最適化することは、システムを効率化するうえで非常に重要です。

組織における [!DNL Assets] の位置付けや、アセットの取り込み、レンディションの生成、メタデータの抽出に使用する機能に応じて、様々な領域でベストプラクティスを特定して順守することにより、負荷がかかった状態のシステムの安定性とパフォーマンスが大幅に向上します。

次のガイドを参照すると、お客様のニーズを満たすエンタープライズアセット管理システムを構築、管理するための知識とツールを得ることができます。

* [Assets パフォーマンスチューニングガイド](/help/assets/performance-tuning-guidelines.md)：実稼動環境への移行後を含めた実装のあらゆる段階において、システムから最大限のパフォーマンスを引き出すための一連のベストプラクティスが記載されています。
* [Assets サイジングガイド](/help/assets/assets-sizing-guide.md)：[!DNL Assets] 実装の予測を立てる際には、アセットのストレージ、CPU、メモリ、I/O、ネットワークスループットなどのリソースに十分な空きがあることを確認することが重要です。これらのアイテムのサイジングには、システムに読み込まれたアセットの数を理解しておく必要があります。このガイドには、[!DNL Assets] のデプロイに必要なインフラストラクチャやリソースを見積もるための効果的な指標を決定するためのベストプラクティスや、サイジングツールが用意されています。
* [Assets 移行ガイド](/help/assets/assets-migration-guide.md)：従来使用していたシステムからアセットを Assets に移行する場合、移行プロセスを効率化するにはいくつかの手順を考慮する必要があります。この移行ガイドには、アセットを [!DNL Experience Manager] に段階的に移行するタスクのベストプラクティスが記載されています。これには、メタデータの適用、レンディションの生成、パブリッシュインスタンスへのアセットのアクティベートなどが含まれています。
* [Assets のネットワークに関する考慮事項のドキュメント](/help/assets/assets-network-considerations.md)：[!DNL Experience Manager] のデプロイメントを処理する際に、ネットワークのトポロジを理解することは、ネットワークのパフォーマンスを理解し、ボトルネックを特定して、期待するユーザーエクスペリエンスを説明するのに重要です。[!DNL Assets] のネットワークに関する考慮事項のドキュメントでは、Assets のデプロイメントを設計する際のネットワークの考慮事項について説明します。
* [Assets 監視ガイド](/help/assets/assets-monitoring-best-practices.md)：[!DNL Experience Manager] のデプロイメントの導入後は、システムの整合性およびオペレーションの効率性が確保されるよう、特定のタスクおよびシステム全般を監視する必要があります。この監視ガイドには、システムの様々な側面を監視するためのベストプラクティスが記載されています。
* [Experience Manager デスクトップアプリケーションのベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=ja)：[!DNL Experience Manager] デスクトップアプリケーションは、デジタルアセット管理（DAM）ソリューションとユーザーのデスクトップをリンクします。ユーザーは、[!DNL Experience Manager] web ユーザーインターフェイスで使用できるファイルをデスクトップで直接開くことができます。デスクトップアプリケーションの使いやすいワークフローは、デスクトップのオペレーティングシステムが提供するネットワーク共有テクノロジーを利用して実現しています。このガイドには、[!DNL Experience Manager] デスクトップアプリケーションの主要な機能と推奨される使用例が記載されています。
* [Experience Manager と Creative Cloud 統合のベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)：[!DNL Experience Manager] のデプロイメントと [!DNL Creative Cloud] を複数の方法で統合できます。ベストプラクティスに従って統合ワークフローおよびアセット転送ワークフローを効率化すると、効率を最大化することができます。このガイドには、[!DNL Assets] と [!DNL Adobe Creative Cloud] の統合に関するベストプラクティスが含まれています。
