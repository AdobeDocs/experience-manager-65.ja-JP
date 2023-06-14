---
title: ハイブリッドアプリの AEM Mobile 対応
description: ハイブリッドアプリの詳細。 Experience Managerのアプリは、一般に 2 つの部分に分かれます。 「シェル」と「コンテンツ」およびこのページでは、これらのトピックに関する詳細なインサイトを提供します。
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
exl-id: 4625890c-2b76-4c78-88e8-23741bc09f5b
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 2%

---

# ハイブリッドアプリはAdobe Experience Manager Mobile用に準備できていますか？{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

ハイブリッド PhoneGap または Cordova アプリをAEMに読み込みました。 認証可能なコンテンツをアプリに追加する場合があります。 このタスクを実行するには、AEMアプリの構造に関する一般的な理解が必要です。 AEMのアプリは、通常、2 つの部分に分かれています。 「シェル」と「コンテンツ」。 「シェル」は、アプリの静的部分で構成されます。（PhoneGap 設定ファイル、アプリフレームワーク、ナビゲーションコントロールなど）。 読み込んだアーカイブの内容は、シェルの一部として保存されます。 このドキュメントのコンテキストでは、シェルは、アプリ開発者が構築したハイブリッド PhoneGap アプリのAEM以外で作成したコンテンツです。

コンテンツとは、AEM開発者が構築したAEMで作成したコンポーネント、テンプレート、オーサリング済みページを指します。 コンテンツは、開発者向けコンテンツまたは作成済みコンテンツのどちらかに分類されます。 コンポーネント、デザイン、ページテンプレートは開発者が構築するので、開発コンテンツと見なされます。 オーサーコンテンツは、コンポーネントとテンプレートを使用して作成されたページです。 これらのページは通常、デザイナーまたはマーケターがおこないます。

作成したAEMページをハイブリッドアプリに追加するには、アプリ開発者とAEM開発者の間で調整が必要です。 アプリ内で作成したコンテンツを追加する場所であれば、どこでも、アプリ開発者は、Experience Managerでオーバーレイできる構造にこれらのページを整理する必要があります。 アプリ開発者は、Experience Managerが作成したコンテンツを追加する場所へのパスをExperience Manager開発者に提供できる必要があります。 次に、ハイブリッドアプリで、ページコンテンツの作成後に置き換わるExperience Managerページを指定します。

説明を簡単に追跡できるように、AEMExperience Cloudを使用しています。AEM Mobileハイブリッドリファレンスを参照して、概念を説明します。 ハイブリッド参照アプリは、サイドメニュー付きのようこそページで構成されています。

![chlimage_1-76](assets/chlimage_1-76.png)

この例では、アプリのようこそページが作成されます。 ソースの確認 [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). アプリ開発者がようこそページを定義し、アプリでレンダリングされるページのテンプレートを提供していることに注意してください。 このページでは、アプリ開発者とAEM開発者が連携する必要があります。 ハイブリッド参照アプリのようこそページテンプレートへのパスは、「content/mobileapps/hybrid-reference-app/en/welcome.template.html」と定義されています。 このパスは重要です。AEM開発者は、AEMリポジトリ内で同じパスを使用してようこそページを作成するからです。

![chlimage_1-77](assets/chlimage_1-77.png)

ハイブリッドアプリとAEMオーサリング済みコンテンツは、コンテンツ同期を使用してコンテンツをオーバーレイし、ハイブリッドアプリに新しいページを追加する機能に依存するので、同じパスを使用することが重要です。 ハイブリッドアプリをAEMに読み込む際、読み込みプロセスの一環として、コンテンツ同期の設定がおこなわれます。

![chlimage_1-78](assets/chlimage_1-78.png)

アプリダッシュボードから「ソースをダウンロード」すると、これらのコンテンツ同期スクリプトが実行され、ハイブリッドアプリのアーカイブが組み立てられます。

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync は、まず、ハイブリッドアプリのすべてのアプリ開発コンテンツが格納されるアプリの「シェル」を取り込みます。 次に、アプリの「コンテンツ」を取り込みます。 これで、「content」と同じパスを持つ「shell」内のページが存在する場合、「shell」内のページは「content」内のページに置き換えられます。 したがって、ハイブリッド参照アプリのサンプルでは、「content/mobileapps/hybrid-reference-app/en/welcome.template.html」と同じパスを持つAEMでページが作成された場合、ContentSync が実行されると、ハイブリッド参照アプリの一部であったページがオーバーレイされます。 その場所にあるAEM内の内容でオーバーレイ表示します。 オーバーレイは ContentSync によって処理されるので、アプリを使用しているユーザーにとっては、AEMが作成したコンテンツを含むアプリの更新がシームレスに行われ、アプリを再構築する必要はありません。 その結果、アプリを実行すると、ようこそページが次のように表示されます。

![chlimage_1-80](assets/chlimage_1-80.png)
