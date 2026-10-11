---
title: コンテンツサービス
description: AEM Mobile Content Servicesを使用して、AEMが管理するコンテンツをリクエストする方法を説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
solution: Experience Manager
feature: Mobile
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 3%
---
# コンテンツサービス{#content-services}

{{ue-over-mobile}}

>[!CAUTION]
>
>コンテンツサービス機能は、プレビューのみを目的として文書化されています。
>
>6.3 サービスパック 1のリリースに伴い、変更される可能性があります。

AEM Mobile Content Servicesは、AEMで管理されるコンテンツをリクエストするための軽量な機能です。 これにより、すべてのアプリ開発者は、AEMのコンテンツリポジトリ（JCR）とweb フレームワーク（Sling）に関する深い知識がなくても、パフォーマンスの高いコンテンツ取得方法を利用できます。 これにより、リクエスト側のアプリケーションをコンテンツリポジトリから切り離すことができます。

Content Servicesには、開発者がAEMで管理されているコンテンツにアクセスできる新しいAEM コンストラクトがいくつか導入されています。このコンストラクトを使用すると、そのコンテンツのリポジトリ構造を知る必要はありません。

これらの構成は、AEMで管理されるコンテンツと、コンテンツを利用するモバイルアプリとの間に抽象化レイヤーを提供することで、柔軟性を維持し、将来の拡張を可能にするために必要です。 これにより、AEM Content Servicesは、ネイティブアプリケーションのコンテンツ要件とAEM コンテンツリポジトリの間の抽象化レイヤーとして機能します。

コンテンツサービスは、アセット、パッケージ化されたHTML（HTML/CSS/JS）、またはチャネルに依存しないコンテンツとしてコンテンツを配信できます。

>[!CAUTION]
>
>**前提条件：**
>
>コンテンツサービスを開始する前に、コンテンツサービスフラグを有効にしていることを確認してください。 アプリでモデルの作成と管理を有効にするには、設定ブラウザーでデータモデルを有効にします。
>
>詳しくは、**[コンテンツサービスの管理](/help/mobile/developing-content-services.md)**&#x200B;および[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。

![chlimage_1-143](assets/chlimage_1-143.png)

Content Services フラグを設定し、Configuration Browserでデータモデルを有効にした後、AEM Mobile Content Servicesの使用を開始するには、以下のリソースを参照してください。 AEM Mobile Content Servicesのモデル管理、エンティティ管理、コンテンツ配信/レンダリングなど、コンテンツサービスの概念を理解します。

* リポジトリ内のモデル
* レンダリングと配信
