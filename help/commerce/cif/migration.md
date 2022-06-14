---
title: AEM Commerce Integration Framework（CIF）アドオンへの移行
description: 旧バージョンから AEM Commerce Integration Framework（CIF）アドオンに移行する方法
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 100%

---

# Experience Manager アドオンの移行ガイド {#cif-migration}

このガイドは、Experience Manager アドオンの移行に向けて更新が必要な領域を特定するのに役立ちます。

## CIF アドオン

AEM 6.5 用の CIF アドオンは、[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)を通じて入手できます。このアドオンは Experience Manager as a Cloud Service 向けの CIF アドオンと互換性があり、同じ機能を提供します。

[AEM Content and Commerce 使用の手引き](getting-started.md)を参照してください。

CIF をデプロイするプロジェクトをサポートするために、アドビでは [AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)を提供しています。

## 製品カタログ

製品カタログデータのインポートは、CIF アドオンではサポートされていません。 CIF アドオンの原則に従って、製品およびカタログリクエストは、外部コマースソリューションへのリアルタイム呼び出しを通じてオンデマンドで行われます。コマースソリューションの統合について詳しくは、「統合」の章を参照してください。

>[!TIP]
>
>リアルタイム API を使用できない場合は、API を使用した外部製品キャッシュを統合に使用する必要があります。例：[Magento オープンソース](https://business.adobe.com/jp/products/magento/open-source.html)

## AEM レンダリングを使用した製品カタログエクスペリエンス

クラシック CIF でカタログブループリントを使用する場合は、製品カタログワークフローを更新する必要があります。CIF アドオンは、AEM カタログテンプレートを使用して、製品カタログエクスペリエンスをその場でレンダリングするようになりました。製品データや製品ページのレプリケーションは不要になりました。

## キャッシュ不可データとショッピングインタラクション

キャッシュ不可データおよびインタラクションについてのクライアントサイドのリクエスト（例：買い物かごへの追加、検索）は、CDN や Dispatcher を介してコマースエンドポイント（コマースソリューションまたは統合レイヤー）に直接送信する必要があります。AEM がプロキシに過ぎない呼び出しは、すべて削除します。
