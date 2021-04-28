---
title: AEM Commerce Integration Framework (CIF)アドオンへの移行
description: 古いバージョンからAEM Commerce Integration Framework (CIF)アドオンに移行する方法
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 4%

---

# Experience Manager追加オンの移行ガイド{#cif-migration}

このガイドは、Experience Managerアドオンの移行に必要な更新領域の特定に役立ちます。

## CIF追加-On

CIFアドオンは、AEM 6.5では[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)から入手できます。 これは互換性があり、Cloud ServiceとしてのExperience Manager用CIFアドオンと同じ機能を提供します。

「[AEMコンテンツとコマースの使い始めに](getting-started.md)」を参照してください。

CIFを導入するプロジェクトをサポートするため、Adobeは[AEM CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components)を提供します。

## 商品カタログ

商品カタログデータの読み込みは、CIFアドオンではサポートされていません。 CIFアドオンプリンシパルを使用すると、商品およびカタログのリクエストは、外部コマースソリューションに対するリアルタイム呼び出しを介してオンデマンドで行われます。 コマースソリューションの統合について詳しくは、「統合」の章を参照してください。

>[!TIP]
>
>リアルタイムAPIが使用できない場合は、APIを使用した外部製品キャッシュを統合に使用する必要があります。 例[Magentoオープンソース](https://magento.com/products/magento-open-source)

## AEMレンダリングを使用した商品カタログエクスペリエンス

Classic CIFでカタログのブループリントを使用する場合は、商品カタログのワークフローを更新する必要があります。 CIFアドオンは、AEMカタログテンプレートを使用して、製品カタログのエクスペリエンスをその場でレンダリングするようになりました。 製品データや製品ページの複製は不要になりました。

## キャッシュ不可能なデータおよび買い物のインタラクション

キャッシュ不可能なデータおよびインタラクション（例えば、買い物かごへの追加、検索）に対するクライアント側のリクエストは、CDN/ディスパッチャーを介して、コマースエンドポイント（コマースソリューションまたは統合レイヤー）に直接送信する必要があります。 AEMが単なるプロキシであった場合は、呼び出しを削除します。
