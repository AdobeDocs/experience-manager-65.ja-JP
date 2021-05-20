---
title: AEM Commerce Integration Framework(CIF)アドオンへの移行
description: 古いバージョンからAEM Commerce Integration Framework(CIF)アドオンに移行する方法
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 4%

---

# Experience Managerアドオンの移行ガイド{#cif-migration}

このガイドは、Experience Managerアドオン移行のために更新する必要がある領域を特定するのに役立ちます。

## CIFアドオン

AEM 6.5では、CIFアドオンは[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)を通じて使用できます。 互換性があり、Cloud ServiceとしてのExperience Manager用CIFアドオンと同じ機能を提供します。

[AEMコンテンツとコマースの使用の手引き](getting-started.md)を参照してください。

CIFをデプロイするプロジェクトをサポートするために、Adobeは[AEM CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components)を提供します。

## 製品カタログ

製品カタログデータの読み込みは、CIFアドオンではサポートされていません。 CIFアドオンプリンシパルを使用すると、製品およびカタログのリクエストは、外部コマースソリューションへのリアルタイム呼び出しを介してオンデマンドでおこなわれます。 コマースソリューションの統合について詳しくは、「統合」の章を参照してください。

>[!TIP]
>
>リアルタイムAPIが使用できない場合は、APIを使用した外部製品キャッシュを統合に使用する必要があります。 例：[Magentoオープンソース](https://magento.com/products/magento-open-source)

## AEM Renderingを使用した製品カタログエクスペリエンス

クラシックCIFでカタログブループリントを使用する場合は、製品カタログワークフローを更新する必要があります。 CIFアドオンは、AEMカタログテンプレートを使用して、製品カタログエクスペリエンスをその場でレンダリングするようになりました。 製品データや製品ページのレプリケーションは不要になりました。

## キャッシュ不可能なデータと買い物とのやり取り

キャッシュ不能なデータおよびインタラクション（例えば、買い物かごへの追加、検索）に対するクライアント側のリクエストは、CDN/Dispatcherを介して、コマースエンドポイント（コマースソリューションまたは統合レイヤー）に直接送信する必要があります。 AEMがプロキシに過ぎない呼び出しをすべて削除します。
