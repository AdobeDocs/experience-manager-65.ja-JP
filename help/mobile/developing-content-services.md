---
title: コンテンツサービス
seo-title: Content Services
description: コンテンツサービス
seo-description: null
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 77%

---

# コンテンツサービス{#content-services}

>[!NOTE]
>
>アドビは、シングルページアプリケーションフレームワークをベースにしたクライアント側のレンダリング（React など）を必要とするプロジェクトには SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

>[!CAUTION]
>
>コンテンツサービス機能は、プレビューのみを目的として文書化されています。
>
>6.3 GA Service Pack 1 のリリースで変更されることがあります。

AEM Mobile Content Services は、AEMで管理されるコンテンツをリクエストするための軽量な機能です。 これにより、AEMコンテンツリポジトリ (JCR) および Web フレームワーク (Sling) に関する深い知識を持つことなく、すべてのアプリ開発者がコンテンツを取得するパフォーマンスの高い方法を提供します。 これにより、リクエストアプリケーションをコンテンツリポジトリから切り離すことができます。

コンテンツサービスで導入されるいくつかの新しい AEM 構成要素を使用して、開発者は、コンテンツのリポジトリ構造を知らなくても AEM の管理対象アセットにアクセスできます。

これらの構成要素は、柔軟性を維持し、今後の拡張を可能にするために必要なもので、AEM の管理対象アセットと、コンテンツを使用するモバイルアプリとの間に抽象レイヤーを提供します。これにより、AEM コンテンツサービスは、ネイティブアプリケーションのコンテンツ要件と AEM コンテンツリポジトリの間の抽象レイヤーとして機能できます。

コンテンツサービスは、コンテンツをアセット、パッケージド HTML（HTML／CSS／JS）またはチャネル独立コンテンツとして配信できます。

>[!CAUTION]
>
>**前提条件:**
>
>コンテンツサービスの使用を始める前に、コンテンツサービスのフラグを有効にしてください。アプリ内でモデルの作成および管理を有効にするには、設定ブラウザーでデータモデルを有効にする必要があります。
>
>詳しくは、 **[コンテンツサービスの管理](/help/mobile/developing-content-services.md)** そして [設定ブラウザー](/help/sites-administering/configurations.md) ドキュメントを参照してください。

![chlimage_1-143](assets/chlimage_1-143.png)

コンテンツサービスのフラグを設定し、設定ブラウザーでデータモデルを有効にしたら、以下のリソースを参照してください。これらのリソースで、AEM Mobile コンテンツサービスの使用と、モデル管理やエンティティ管理、AEM Mobile コンテンツサービスのコンテンツ配信／レンダリングなどのコンテンツサービスの概念について学習することができます。

* リポジトリ内のモデル
* レンダリングと配信
