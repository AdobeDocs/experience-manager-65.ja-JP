---
title: 共有リソースのアップロード
description: コンテンツ管理アクションは、アプリケーション内のコンテンツの作成と管理に役立つ構築ブロックです。 このページでは、共有リソースのアップロードについて説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 4b3acc7c-f1f7-4837-ae3a-9435d6ce1349
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 12%

---

# 共有リソースのアップロード {#uploading-shared-resources}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

コンテンツ管理アクションは、アプリケーション内のコンテンツの作成と管理に役立つ構築ブロックです。 アプリケーション内のコンテンツに対して、次のアクションが実行されます。

>[!NOTE]
>
>AEM Mobile アプリのデザインに関する考慮事項について詳しくは、 [AEM Mobile アプリの設計に関する考慮事項](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html) オンライン ヘルプで表示します。

>[!CAUTION]
>
>最初にモバイルオンデマンド接続を関連付けます。

## 共有リソースのアップロード {#uploading-shared-resources-1}

通常、記事などのコンテンツは、すべての作成者やアプリで同じルックアンドフィールを持つ必要があります。 したがって、スクリプト、CSS、フォントをすべてのユーザーが利用できるようにする必要があります。 この操作により、このような共有リソースが Mobile On-Demand に送信され、必要に応じて消費できます。

アプリを設定してクラウド設定に関連付けると、共有リソースをアップロードできます。 アプリをクラウド設定に関連付ける手順について詳しくは、 [こちら](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md).

>[!NOTE]
>
>共有リソースは、ContentSync を使用して、すべての異なるリソースを収集します。 参照： [ContentSync を使用したモバイル](/help/mobile/mobile-ondemand-contentsync.md) を参照してください。

記事用の共有リソースをアップロードするには、次の手順に従います。

1. 記事を次から選択 **記事の管理** タイル。
1. クリック **共有リソースのアップロード** で共有HTMLリソースをアップロードします。

   ![chlimage_1-133](assets/chlimage_1-133.png)

### 次のステップ {#the-next-step}

コンテンツの作成と公開について理解したら、次を参照してください。

* [AEM Mobile On-demand Services用AEM コンテンツの開発](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand Servicesを使用するコンテンツの管理](/help/mobile/aem-mobile.md)

または、オーサリングのトピックについて学習する必要があります。を参照してください。

[AEM Mobile On-demand Services アプリ用AEM コンテンツのオーサリング](/help/mobile/mobile-apps-ondemand.md)
