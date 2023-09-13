---
title: コンテンツサービス
description: コンテンツサービス
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 5%

---

# コンテンツサービス{#content-services}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

>[!CAUTION]
>
>コンテンツサービス機能は、プレビュー目的でのみドキュメントに記載されています。
>
>6.3 GA Service Pack 1 のリリースに伴って変更される場合があります。

AEM Mobile Content Services は、AEMで管理されるコンテンツをリクエストするための軽量な機能です。 これにより、AEMコンテンツリポジトリ (JCR) および Web フレームワーク (Sling) に関する深い知識を持つことなく、すべてのアプリ開発者がコンテンツを取得するパフォーマンスの高い方法を提供します。 これにより、リクエストアプリケーションをコンテンツリポジトリから切り離すことができます。

Content Services では、AEMが管理するコンテンツに、そのコンテンツのリポジトリ構造を知らずに開発者がアクセスできるようにする、新しいAEM構造がいくつか導入されています。

これらの構成は、AEMが管理するコンテンツとコンテンツを使用するモバイルアプリの間に抽象レイヤーを提供することで、柔軟性を維持し、将来の拡張を可能にするために必要です。 これにより、AEM Content Services は、ネイティブアプリケーションのコンテンツ要件とAEMコンテンツリポジトリとの間の抽象レイヤーとして機能します。

コンテンツサービスは、コンテンツをアセット、パッケージHTML(HTML/CSS/JS) またはチャネルに依存しないコンテンツとして配信できます。

>[!CAUTION]
>
>**前提条件:**
>
>Content Services を使用する前に、Content Services フラグを有効にしておく必要があります。 アプリ内でモデルの作成と管理を有効にするには、設定ブラウザーでデータモデルを有効にします。
>
>詳しくは、 **[コンテンツサービスの管理](/help/mobile/developing-content-services.md)** そして [設定ブラウザー](/help/sites-administering/configurations.md) ドキュメントを参照してください。

![chlimage_1-143](assets/chlimage_1-143.png)

Content Services フラグを設定し、設定ブラウザーでデータモデルを有効にした後、以下のリソースを参照して、AEM Mobile Content Services の使用を開始します。 モデル管理、エンティティ管理、AEM Mobile Content Services のコンテンツ配信/レンダリングなど、コンテンツサービスの概念について説明します。

* リポジトリ内のモデル
* レンダリングと配信
