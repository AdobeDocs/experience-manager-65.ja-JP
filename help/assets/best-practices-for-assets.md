---
title: Best Practices for [!DNL Assets]
description: 導入と設定に依存するベストプラクティスを特定し、遵守することで、負荷中のシステムの安定性とパフォーマンスを向上させます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 25%

---


# Best Practices for [!DNL Assets] {#best-practices-for-assets}

[!DNL Adobe Experience Manager Assets] は、コンテンツベロシティを通じてビジネス目標の達成に貢献する、高品質のデジタルマーケティングエクスペリエンスを実現するうえできわめて重要な役割を果たします。If you work with a large number of assets within [!DNL Experience Manager Assets] or regularly/periodically upload numerous assets, including videos and dynamic media, optimizing your digital asset management experience is critical for system efficiency.

Depending upon how you have positioned [!DNL Assets] for your organization and the features that you use for asset ingestion, rendition generation, and metadata extraction, identifying and adhering to best practices in different areas greatly enhances system stability and performance under load.

ニーズに対応するエンタープライズアセット管理システムを構築、管理するためのプロセスとツールについては、次のガイドを参照してください。

* The [Assets performance tuning guide](/help/assets/performance-tuning-guidelines.md): This guide includes a set of best practices that can be followed at any point in your implementation, even after you go live, to ensure that you get the most out of your system.
* The [Assets sizing guide](/help/assets/assets-sizing-guide.md): When drawing up estimates for an [!DNL Assets] implementation, it is important to ensure that there are sufficient resources available in terms of asset storage, CPU, memory, IO and network throughput. これらのアイテムのサイジングには、システムに読み込まれたアセットの数を理解しておく必要があります。This guide includes best practices that help determine efficient metrics for estimating the infrastructure and resources required for deploying [!DNL Assets] as well as a sizing tool.
* The [Assets migration guide](/help/assets/assets-migration-guide.md): If you want to migrate assets from your legacy system to Assets, there are several steps to consider to streamline the migration process. The Migration guide include best practices around the tasks you perform to bring the assets into [!DNL Experience Manager] in a phase-wise manner. これには、メタデータの適用、レンディションの生成、パブリッシュインスタンスへのアセットのアクティベートなどが含まれています。
* The [Assets network considerations document](/help/assets/assets-network-considerations.md): When handling [!DNL Experience Manager] deployment, understanding the network topology is important to understand network performance, identify chokepoints, and describe the expected user experience. The [!DNL Assets] network considerations document discusses network considerations when designing your Asset deployment.
* The [Assets monitoring guide](/help/assets/assets-monitoring-best-practices.md): After your [!DNL Experience Manager] deployment is deployed, you should monitor certain tasks and the system in general to ensure system integrity and efficiency of operations. この監視ガイドには、システムの様々な側面を監視するためのベストプラクティスが記載されています。
* [Experience Managerデスクトップアプリのベストプラクティス](https://docs.adobe.com/content/help/ja-JP/experience-manager-desktop-app/using/introduction.html): [!DNL Experience Manager] デスクトップアプリでは、デジタルアセット管理(DAM)ソリューションがデスクトップにリンクされるので、 [!DNL Experience Manager] webユーザーインターフェイスで使用可能なファイルをデスクトップ上で直接開くことができます。 デスクトップアプリケーションの使いやすいワークフローは、デスクトップのオペレーティングシステムから提供されるネットワーク共有テクノロジーにより有効化されます。This guide explains key capabilities and recommended use of [!DNL Experience Manager] desktop app.
* [Experience ManagerとCreative Cloudの統合のベストプラクティス](/help/assets/aem-cc-integration-best-practices.md):デプロイメントは、複数の方法で [!DNL Experience Manager] と統合で [!DNL Creative Cloud] きます。 ベストプラクティスに従って統合ワークフローおよびアセット転送ワークフローを効率化すると、効率を最大化することができます。このガイドには、との統合に関するベストプラクティス [!DNL Assets] が含まれて [!DNL Adobe Creative Cloud]います。
