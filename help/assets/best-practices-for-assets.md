---
title: Assets のベストプラクティス
description: アセットの取り込み、レンディションの生成、メタデータの抽出に使用するExperience Managerアセットのデプロイメントと機能に応じて、異なる領域でのベストプラクティスを識別して固有にすることで、読み込み中のシステムの安定性とパフォーマンスが大幅に向上します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 678e91699523c22a7048bd7b344fa539b849ae8b
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 41%

---


# Assets のベストプラクティス {#best-practices-for-assets}

Adobe Experience Managerアセットは、コンテンツ速度を向上させることでビジネス目標の達成に貢献する高品質のデジタルマーケティングエクスペリエンスを提供する上で重要な部分です。 Experience Managerアセット内で大量のアセットを扱う場合、またはビデオやダイナミックメディアなど多数のアセットを定期的/定期的にアップロードする場合は、デジタルアセット管理の使い勝手を最適化することがシステムの効率性に不可欠です。

組織における Assets のデプロイ方法や、アセットの取り込み、レンディションの生成およびメタデータの抽出に使用した機能に応じて、様々な領域でベストプラクティスを特定して順守することで、システムの安定性と高負荷下のパフォーマンスを大幅に改善できます。

ニーズに対応するエンタープライズアセット管理システムを構築、管理するためのプロセスとツールについては、次のガイドを参照してください。

* The [Assets Performance Tuning guide](/help/assets/performance-tuning-guidelines.md): This guide includes a set of best practices that can be followed at any point in your implementation, even after you go live, to ensure that you get the most out of your system.
* The [Assets Sizing guide](/help/assets/assets-sizing-guide.md): When drawing up estimates for an Assets implementation, it is important to ensure that there are sufficient resources available in terms of asset storage, CPU, memory, IO and network throughput. これらのアイテムのサイジングには、システムに読み込まれたアセットの数を理解しておく必要があります。このガイドには、 Assets のデプロイに必要なインフラストラクチャやリソースの予測に効果的な指標の判断に役立つベストプラクティスとサイジングツールが用意されています。
* [アセット移行ガイド](/help/assets/assets-migration-guide.md)：従来使用していたシステムからアセットを Assets に移行する場合、移行プロセスを効率化するにはいくつかの手順を考慮する必要があります。移行ガイドには、アセットを段階的にExperience Managerさせるために実行するタスクに関するベストプラクティスが含まれています。 これには、メタデータの適用、レンディションの生成、パブリッシュインスタンスへのアセットのアクティベートなどが含まれています。
* The [Assets Network Considerations document](/help/assets/assets-network-considerations.md): When handling Experience Manager deployment, understanding the network topology is important to understand network performance, identify chokepoints, and describe the expected user experience. Assets のネットワークに関する考慮事項のドキュメントでは、 Assets のデプロイメントを設計する際のネットワークの考慮事項について説明します。
* The [Assets Monitoring guide](/help/assets/assets-monitoring-best-practices.md): After your Experience Manager deployment is deployed, you should monitor certain tasks and the system in general to ensure system integrity and efficiency of operations. この監視ガイドには、システムの様々な側面を監視するためのベストプラクティスが記載されています。
* [Experience Managerデスクトップアプリのベストプラクティス](https://helpx.adobe.com/jp/experience-manager/desktop-app/aem-desktop-app-best-practices.html): Experience Managerのデスクトップアプリは、デジタルアセット管理(DAM)ソリューションをデスクトップにリンクするので、Experience ManagerのWeb UIで使用できるファイルをデスクトップ上で直接開くことができます。 デスクトップアプリケーションの使いやすいワークフローは、デスクトップのオペレーティングシステムから提供されるネットワーク共有テクノロジーにより有効化されます。このガイドでは、Experience Managerのデスクトップアプリの主な機能と推奨される使用方法を説明します。
* [Experience ManagerとCreative Cloud統合のベストプラクティス](/help/assets/aem-cc-integration-best-practices.md): Experience Managerの展開は、様々な方法でCreative Cloudと統合できます。 ベストプラクティスに従って統合ワークフローおよびアセット転送ワークフローを効率化すると、効率を最大化することができます。このガイドには、 Assets と Adobe CC の統合に関するベストプラクティスが記載されています。
