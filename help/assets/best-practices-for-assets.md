---
title: Assets のベストプラクティス
description: AEM Assets のデプロイメントや、アセットの取り込み、レンディションの生成およびメタデータの抽出に使用した機能に応じて、様々な領域でベストプラクティスを特定して順守することで、システムの安定性と高負荷下のパフォーマンスを大幅に改善できます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# Assets のベストプラクティス {#best-practices-for-assets}

Adobe Experience Manager（AEM）Assets は、コンテンツベロシティを通じてビジネス目標の達成に貢献する、高品質のデジタルマーケティングエクスペリエンスを実現する上できわめて重要な役割を果たします。AEM Assets でビデオや Dynamic Media などの多数のアセットを操作する、または定期的に大量のアセットをアップロードする場合、システムの効率化を実現する上でデジタルアセットの管理エクスペリエンスの最適化は重要な位置を占めます。

組織における AEM Assets のデプロイ方法や、アセットの取り込み、レンディションの生成およびメタデータの抽出に使用した機能に応じて、様々な領域でベストプラクティスを特定して順守することで、システムの安定性と高負荷下のパフォーマンスを大幅に改善できます。

ニーズに対応するエンタープライズアセット管理システムを構築、管理するためのプロセスとツールについては、次のガイドを参照してください。

* The [Assets Performance Tuning guide](/help/assets/performance-tuning-guidelines.md): This guide includes a set of best practices that can be followed at any point in your implementation, even after you go live, to ensure that you get the most out of your system.
* The [Assets Sizing guide](/help/assets/assets-sizing-guide.md): When drawing up estimates for an Assets implementation, it is important to ensure that there are sufficient resources available in terms of asset storage, CPU, memory, IO and network throughput. これらのアイテムのサイジングには、システムに読み込まれたアセットの数を理解しておく必要があります。このガイドには、AEM Assetsのデプロイに必要なインフラストラクチャとリソースを見積もるための効率的な指標を決定するのに役立つ、サイジングツールに関するベストプラクティスが含まれています。
* The [Assets Migration guide](/help/assets/assets-migration-guide.md): If you want to migrate assets from your legacy system to AEM Assets, there are several steps to consider to streamline the migration process. 移行ガイドには、アセットを段階的にAEMに取り込むために実行するタスクに関するベストプラクティスが含まれています。 これには、メタデータの適用、レンディションの生成、パブリッシュインスタンスへのアセットのアクティベートなどが含まれています。
* [Assets のネットワークに関する考慮事項のドキュメント](/help/assets/assets-network-considerations.md)：AEM のインスタンスを処理する際に、ネットワークのトポロジを理解することは、ネットワークのパフォーマンスを理解し、渋滞地点を特定して、期待するユーザーエクスペリエンスを描くのに重要です。Assets のネットワークに関する考慮事項のドキュメントでは、AEM Assets のデプロイメントを設計する際のネットワークの考慮事項について説明します。
* The [Assets Monitoring guide](/help/assets/assets-monitoring-best-practices.md): After your AEM instance is deployed, you should monitor certain tasks and the system in general to ensure system integrity and efficiency of operations. この監視ガイドには、システムの様々な側面を監視するためのベストプラクティスが記載されています。
* [AEMデスクトップアプリのベストプラクティス](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app-best-practices.html):AEMデスクトップアプリは、デジタルアセット管理(DAM)ソリューションをデスクトップにリンクするので、AEM Web UIで使用できるファイルをデスクトップ上で直接開くことができます。 デスクトップアプリケーションの使いやすいワークフローは、デスクトップオペレーティングシステムが提供するネットワーク共有テクノロジーを使用して有効になります。 このガイドには、AEM デスクトップアプリケーションの主要な機能と推奨される使用例が記載されています。
* [AEMとCreative cloudの統合に関するベストプラクティス](/help/assets/aem-cc-integration-best-practices.md):AEMインスタンスは、様々な方法でCreative cloudと統合できます。 ベストプラクティスに従って統合ワークフローおよびアセット転送ワークフローを効率化すると、効率を最大化することができます。このガイドには、AEM AssetsとAdobe Creative cloudの統合に関するベストプラクティスが含まれています。
