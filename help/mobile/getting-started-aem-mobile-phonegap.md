---
title: AEM Adobe PhoneGap
description: AEMは PhoneGap と統合されているので、AEMページを使用して簡単にアプリを作成できます。 このページでは、Adobe PhoneGap Enterprise の概要について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: d989e235-5993-4738-8523-5b9a5f6bf712
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 2%

---

# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

AEMは PhoneGap と統合されているので、AEMページを使用して簡単にアプリを作成できます。 PhoneGap を使用すると、ユーザーがコンテンツを操作するためのユーティリティアプリを作成できます。 コンテンツ同期を使用すると、アプリとのバンドル用に、バージョン管理されたページのアーカイブを作成できます。

通常、 ***AEM Administrator*** は、作成ウィザードを使用してアプリを作成するか、既存のアプリを読み込むことで、AEM Mobileカタログに新しいアプリを追加します。

ここから、 ***AEM Author*** ( または *マーケター*) では、標準搭載のテンプレートとコンポーネントを使用して、ページの追加と編集、コンポーネントのドラッグ&amp;ドロップ、DAM からのすべてのタイプのメディア（画像、ビデオ、テキストフラグメント）の追加をおこなえます。

AEM Mobileの真の力は *経験豊富な* ***AEM Developer*** は、カスタム web テンプレートおよびコンポーネントを拡張および作成して、 *AEM Author* 魅力的なモバイルエクスペリエンスを作成します。 これらのテンプレートとコンポーネントは、モバイルアプリの世界に最適化されているだけでなく、デバイスとAEMサーバー（任意のリモートサーバー）の両方とオムニチャネルサービスエンドポイントとの通信も可能です。

>[!NOTE]
>
>次の場合に *AEM Author* アプリの準備が整ったと考えるときは、まず関係者に、 **[Adobeの検証](/help/mobile/phonegap-mobile-quickstart.md)** （AppStore と PlayStore の両方で利用可能）レビューと承認をおこないます。 緑の信号を受け取ったユーザーは、 AEM Mobile ContentSync コンテンツリリース管理ダッシュボードを使用して、この新しいコンテンツや更新されたコンテンツを直接ユーザーにリリースできます。 1 人の担当者が任意の数の役割を引き受けることができます。これは、お客様とガバナンスポリシーに基づきます。

## 前提条件 {#prerequisites}

AEM Mobileは、AEMプラットフォーム全体を構成する 1 つの柱に過ぎません。

AEM Mobileを使用し、この入門ガイドの手順に従う前に、AEMとAEM Mobileコントロールセンターに関する十分な知識が必要です。 以下を参照してください。

[AEMの概要](/help/sites-deploying/deploy.md)

[AEM Mobile Control Center のガイド](/help/mobile/phonegap-authoring-apps.md)

## 作成者向けクイックリンク {#quicklinks-for-authors}

詳しくは、 [AEMでのAdobe PhoneGap Enterprise 向けのオーサリング](/help/mobile/phonegap.md) 作成者の役割と責任についての説明

## 開発者向けクイックリンク {#quicklinks-for-developers}

AEM Mobileと統合され、開発者がカスタマイズできるサンプルアプリケーションがあります。 クリック： [AEMを使用したAdobe PhoneGap Enterprise の開発](/help/mobile/developing-in-phonegap.md).

以降の章では、アプリケーションのホワイトラベル設定、ローカライゼーション、国際化、コンテンツ同期、ターゲティング、Analytics などの高度な概念について説明します。

## 管理者向けクイックリンク {#quicklinks-for-administrators}

詳しくは、 [AEMを使用したAdobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md) モバイルアプリケーションを設定および管理する場合。

>[!NOTE]
>
>ハイブリッドモバイルテクノロジーを使用して、 *オフラインでオンラインで実行* 実際、AEM Mobileを使用すると、多くのお客様は、オンラインまたはオフラインの状態を確認し、それに応じて動作するアプリを作成することを選択しています。
