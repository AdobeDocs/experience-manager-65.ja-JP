---
title: AEM Adobe PhoneGap
seo-title: AEM Adobe PhoneGap
description: AEM を PhoneGap と連携し、AEM ページを使用してアプリを簡単に作成できます。このページでは、Adobe PhoneGap Enterprise の概要について説明します。
seo-description: AEM を PhoneGap と連携し、AEM ページを使用してアプリを簡単に作成できます。このページでは、Adobe PhoneGap Enterprise の概要について説明します。
uuid: bdd90cda-2489-4763-a90a-9c409d6e68ae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: fbcdea8a-72e9-431b-9c32-dc02d4cdb9c8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 52%

---


# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

AEM を PhoneGap と連携し、AEM ページを使用してアプリを簡単に作成できます。PhoneGap と連携することで、そのコンテンツを利用するユーティリティアプリを作成できます。コンテンツ同期を使用すると、アプリにバンドルするページのバージョン管理されたアーカイブを作成できます。

Typically, an ***AEM Administrator*** is responsible for adding a new application to the AEM Mobile catalog, either by creating a new app using the creation wizard, or by importing an existing application.

From here an ***AEM Author*** (or *Marketer*) is now able to use the out-of-the-box templates and components to add and edit pages, drag and drop components and add media of all types from the DAM including images, videos and text fragments (content fragments).

The real power of AEM Mobile is that a *savvy* ***AEM Developer*** can extend and create custom web templates and components to enable the *AEM Author* to create beautful and engaging mobile experiences. これらのテンプレートとコンポーネントは、モバイルアプリの世界向けに最適化されているだけではありません。ただし、デバイスとAEMサーバ（任意のリモートサーバ）の両方に対して、オムニチャネルサービスエンドポイントと通信します。

>[!NOTE]
>
>アプリの準備が整ったら、AEM 作成者は、まず、レビューおよび承認用に、**[Adobe Verify](/help/mobile/phonegap-mobile-quickstart.md)**（AppStore でも Play Store でも入手可能）で関係者にアプリをダウンロードしてもらうことができます。**&#x200B;緑の信号を受け取ると、この新しいコンテンツや更新されたコンテンツを、AEM MobileのContentSyncコンテンツリリース管理ダッシュボードを使用してユーザに直接公開できます。 各個人の能力とガバナンスポリシーに合わせて、1 人のユーザーが任意の数の役割を担うことができます。

## 前提条件 {#prerequisites}

AEM Mobile は、完全な AEM プラットフォームを構成する 1 つの柱に過ぎません。

AEM Mobile を操作して、この使用の手引きに記載された手順を実行する前に、ユーザーは AEM および AEM Mobile コントロールセンターについて十分に理解しておく必要があります。次のページを参照してください。

[AEM 使用の手引き](/help/sites-deploying/deploy.md)

[AEM Mobileコントロールセンターのウォークスルー](/help/mobile/phonegap-authoring-apps.md)

## 作成者向けクイックリンク {#quicklinks-for-authors}

See [Authoring for Adobe PhoneGap Enterprise in AEM](/help/mobile/phonegap.md) to learn about an author&#39;s roles and responsibilities.

## 開発者向けクイックリンク {#quicklinks-for-developers}

AEM Mobile と統合でき、開発者がカスタマイズできるサンプルアプリケーションがあります。[AEM での Adobe PhoneGap Enterprise の開発](/help/mobile/developing-in-phonegap.md)を参照してください。

以降の章では、アプリケーションのホワイトラベリング、ローカリゼーション、国際化対応、コンテンツ同期、ターゲット設定、解析などの高度な概念について説明します。

## 管理者向けクイックリンク {#quicklinks-for-administrators}

See [Administering Content for Adobe PhoneGap Enterprise with AEM](/help/mobile/administer-phonegap.md) to set up and manage your mobile application.

>[!NOTE]
>
>Using hybrid mobile technologies, you can create rich mobile applications that *run offline and online* with AEM Mobile in fact, many customers choose to create apps that check for when they&#39;re online or offline and behave accordingly.
