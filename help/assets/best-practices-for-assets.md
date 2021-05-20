---
title: ' [!DNL Assets]のベストプラクティス'
description: デプロイメントと設定に依存するベストプラクティスを特定し、遵守することで、負荷時のシステムの安定性とパフォーマンスを向上させます。
contentOwner: AG
feature: アセット管理
role: Architect, Administrator
exl-id: 6b50f1b3-9c1c-47c8-a43e-6f40c42a41cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 25%

---

# [!DNL Assets] {#best-practices-for-assets}のベストプラクティス

[!DNL Adobe Experience Manager Assets] は、コンテンツベロシティを通じてビジネス目標の達成に貢献する、高品質のデジタルマーケティングエクスペリエンスを実現するうえできわめて重要な役割を果たします。[!DNL Experience Manager Assets]内で大量のアセットを扱う場合や、ビデオやDynamic Mediaなど多数のアセットを定期的/定期的にアップロードする場合は、システムの効率を上げるためにデジタルアセット管理のエクスペリエンスを最適化することが重要です。

組織の[!DNL Assets]の配置方法と、アセットの取り込み、レンディションの生成、メタデータの抽出に使用する機能に応じて、様々な領域でのベストプラクティスを識別して準拠することで、負荷時のシステムの安定性とパフォーマンスが大幅に向上します。

ニーズに対応するエンタープライズアセット管理システムを構築、管理するためのプロセスとツールについては、次のガイドを参照してください。

* [Assetsパフォーマンスチューニングガイド](/help/assets/performance-tuning-guidelines.md):このガイドには、実稼動環境への移行後も含め、実装内のあらゆる時点で実行できる、システムを最大限に活用するための一連のベストプラクティスが含まれています。
* [アセットのサイズ設定ガイド](/help/assets/assets-sizing-guide.md):[!DNL Assets]実装の予測を作成する場合、アセットストレージ、CPU、メモリ、IO、ネットワークスループットの観点から十分なリソースが確保されていることを確認することが重要です。 これらのアイテムのサイジングには、システムに読み込まれたアセットの数を理解しておく必要があります。このガイドには、[!DNL Assets]の導入に必要なインフラストラクチャとリソースの予測に効率的な指標を決定するのに役立つベストプラクティスとサイジングツールが含まれています。
* [アセット移行ガイド](/help/assets/assets-migration-guide.md):既存のシステムからアセットにアセットを移行する場合は、移行プロセスを効率化するためにいくつかの手順を考慮する必要があります。 移行ガイドには、アセットを[!DNL Experience Manager]に移行するタスクに関するベストプラクティスが含まれています。 これには、メタデータの適用、レンディションの生成、パブリッシュインスタンスへのアセットのアクティベートなどが含まれています。
* [Assetsのネットワークに関する考慮事項のドキュメント](/help/assets/assets-network-considerations.md):[!DNL Experience Manager]デプロイメントを処理する場合、ネットワークのパフォーマンスを理解し、渋滞地点を特定し、期待されるユーザーエクスペリエンスを説明するには、ネットワークトポロジを理解することが重要です。 [!DNL Assets]ネットワークに関する考慮事項のドキュメントでは、アセットデプロイメントを設計する際のネットワークに関する考慮事項について説明します。
* [アセット監視ガイド](/help/assets/assets-monitoring-best-practices.md):[!DNL Experience Manager]デプロイメントをデプロイした後は、システムの整合性と運用の効率を確保するために、特定のタスクとシステム全般を監視する必要があります。 この監視ガイドには、システムの様々な側面を監視するためのベストプラクティスが記載されています。
* [Experience Managerデスクトップアプリケーションのベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=ja): [!DNL Experience Manager] デスクトップアプリケーションは、デジタルアセット管理(DAM)ソリューションとデスクトップを連携させ、webユーザーインターフェイスで使用可能なファイルをデスクトップで直接開くことができま [!DNL Experience Manager] す。デスクトップアプリケーションの使いやすいワークフローは、デスクトップのオペレーティングシステムから提供されるネットワーク共有テクノロジーにより有効化されます。このガイドでは、[!DNL Experience Manager]デスクトップアプリケーションの主な機能と推奨される使用例を説明します。
* [Experience ManagerとCreative Cloudの統合のベストプラクティス](/help/assets/aem-cc-integration-best-practices.md):デプロイメントをと統合す [!DNL Experience Manager] る方法は [!DNL Creative Cloud] 複数あります。ベストプラクティスに従って統合ワークフローおよびアセット転送ワークフローを効率化すると、効率を最大化することができます。このガイドには、[!DNL Assets]と[!DNL Adobe Creative Cloud]の統合に関するベストプラクティスが含まれています。
