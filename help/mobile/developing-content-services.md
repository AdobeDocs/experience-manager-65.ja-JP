---
title: コンテンツサービス
description: AEM Mobile Content Services を使用して、AEMによって管理されるコンテンツをリクエストする方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 9%

---

# コンテンツサービス{#content-services}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

>[!CAUTION]
>
>コンテンツサービス機能は、プレビューのみを目的としてドキュメントに記載されています。
>
>6.3 サービスパック 1 のリリースで変更される可能性があります。

AEM Mobile コンテンツサービスは、AEMで管理されるコンテンツをリクエストするための軽量の機能です。 これにより、すべてのアプリ開発者は、AEM コンテンツリポジトリ（JCR）と web フレームワーク（Sling）に関する深い知識がなくても、コンテンツを取得できる高パフォーマンスな方法を利用できます。 これにより、要求元のアプリケーションをコンテンツリポジトリから切り離すことができます。

Content Services では、AEMが管理するコンテンツに、そのコンテンツのリポジトリ構造を知らずに開発者がアクセスできる、AEMの新しい構造がいくつか導入されています。

これらの構造は、AEMが管理するコンテンツと、コンテンツを使用するモバイルアプリの間に抽象レイヤーを提供することで、柔軟性を維持し、将来の拡張を可能にするために必要です。 これにより、AEM コンテンツサービスは、ネイティブアプリケーションのコンテンツ要件とAEM コンテンツリポジトリの間の抽象化レイヤーとして機能します。

コンテンツサービスは、アセット、パッケージ化されたHTML（HTML/CSS/JS）またはチャネルに依存しないコンテンツとしてコンテンツを配信できます。

>[!CAUTION]
>
>**前提条件：**
>
>コンテンツサービスの使用を開始する前に、必ずコンテンツサービスフラグを有効にしてください。 アプリでモデルの作成と管理を有効にするには、設定ブラウザーでデータモデルを有効にします。
>
>詳しくは、**[コンテンツサービスの管理](/help/mobile/developing-content-services.md)** および [ 設定ブラウザー ](/help/sites-administering/configurations.md) ドキュメントを参照してください。

![chlimage_1-143](assets/chlimage_1-143.png)

コンテンツサービスフラグを設定し、設定ブラウザーでデータモデルを有効にしたら、AEM Mobile コンテンツサービスの使用を開始するために、以下のリソースを参照してください。 AEM Mobile コンテンツサービスのモデル管理、エンティティ管理、コンテンツ配信/レンダリングなど、コンテンツサービスの概念について理解します。

* リポジトリ内のモデル
* レンダリングと配信
