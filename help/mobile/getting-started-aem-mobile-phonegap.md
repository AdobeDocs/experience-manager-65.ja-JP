---
title: AEM Adobe PhoneGap
seo-title: AEM Adobe PhoneGap
description: AEM を PhoneGap と連携し、AEM ページを使用してアプリを簡単に作成できます。このページでは、Adobe PhoneGap Enterprise の概要について説明します。
seo-description: AEM integrates with PhoneGap so that you can easily create apps using AEM pages. Follow this page to get started with Adobe PhoneGap Enterprise.
uuid: bdd90cda-2489-4763-a90a-9c409d6e68ae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: fbcdea8a-72e9-431b-9c32-dc02d4cdb9c8
exl-id: d989e235-5993-4738-8523-5b9a5f6bf712
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 49%

---

# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>アドビは、シングルページアプリケーションフレームワークをベースにしたクライアント側のレンダリング（React など）を必要とするプロジェクトには SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

AEM を PhoneGap と連携し、AEM ページを使用してアプリを簡単に作成できます。PhoneGap と連携することで、そのコンテンツを利用するユーティリティアプリを作成できます。コンテンツ同期を使用すると、アプリにバンドルするページのバージョン管理されたアーカイブを作成できます。

通常、 ***AEM Administrator*** は、作成ウィザードを使用して新しいアプリを作成するか、既存のアプリを読み込むことで、AEM Mobileカタログに新しいアプリを追加します。

ここから、 ***AEM オーサー*** ( または *マーケター*) では、標準搭載のテンプレートとコンポーネントを使用して、ページの追加と編集、コンポーネントのドラッグ&amp;ドロップ、DAM からのすべてのタイプのメディア（画像、ビデオ、テキストフラグメント）の追加をおこなえます。

AEM Mobileの真の力は *経験豊富な* ***AEM Developer*** は、カスタム web テンプレートおよびコンポーネントを拡張および作成して、 *AEM オーサー* 魅力的なモバイルエクスペリエンスを作成します。 これらのテンプレートとコンポーネントは、モバイルアプリの世界に最適化されているだけではありません。ただし、デバイスとAEMサーバー（任意のリモートサーバー）の両方をオムニチャネルサービスエンドポイントに通信します。

>[!NOTE]
>
>アプリの準備が整ったら、AEM 作成者は、まず、レビューおよび承認用に、**[Adobe Verify](/help/mobile/phonegap-mobile-quickstart.md)**（AppStore でも Play Store でも入手可能）で関係者にアプリをダウンロードしてもらうことができます。**&#x200B;緑の信号を受け取ったユーザーは、 AEM Mobile ContentSync コンテンツリリース管理ダッシュボードを使用して、この新しいコンテンツや更新されたコンテンツを直接ユーザーにリリースできます。 各個人の能力とガバナンスポリシーに合わせて、1 人のユーザーが任意の数の役割を担うことができます。

## 前提条件 {#prerequisites}

AEM Mobile は、完全な AEM プラットフォームを構成する 1 つの柱に過ぎません。

AEM Mobile を操作して、この使用の手引きに記載された手順を実行する前に、ユーザーは AEM および AEM Mobile コントロールセンターについて十分に理解しておく必要があります。以下を参照してください。

[AEM 使用の手引き](/help/sites-deploying/deploy.md)

[AEM Mobile Control Center のガイド](/help/mobile/phonegap-authoring-apps.md)

## 作成者向けクイックリンク {#quicklinks-for-authors}

詳しくは、 [AEMでのAdobe PhoneGap Enterprise 向けのオーサリング](/help/mobile/phonegap.md) 作成者の役割と責任についての説明

## 開発者向けクイックリンク {#quicklinks-for-developers}

AEM Mobile と統合でき、開発者がカスタマイズできるサンプルアプリケーションがあります。[AEM での Adobe PhoneGap Enterprise の開発](/help/mobile/developing-in-phonegap.md)を参照してください。

以降の章では、アプリケーションのホワイトラベリング、ローカリゼーション、国際化対応、コンテンツ同期、ターゲット設定、解析などの高度な概念について説明します。

## 管理者向けクイックリンク {#quicklinks-for-administrators}

詳しくは、 [AEMを使用したAdobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md) モバイルアプリケーションを設定および管理する場合。

>[!NOTE]
>
>ハイブリッドモバイルテクノロジーを使用して、 *オフラインでオンラインで実行* 実際、AEM Mobileを使用すると、多くのお客様は、オンラインまたはオフラインの状態を確認し、それに応じて動作するアプリを作成することを選択しています。
