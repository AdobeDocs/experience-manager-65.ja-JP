---
title: AEM Adobe PhoneGap
description: AEM を PhoneGap と連携し、AEM ページを使用してアプリを簡単に作成できます。このページでは、Adobe PhoneGap Enterprise の概要を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: d989e235-5993-4738-8523-5b9a5f6bf712
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 11%

---

# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

AEM を PhoneGap と連携し、AEM ページを使用してアプリを簡単に作成できます。PhoneGap を使用すると、ユーザーがコンテンツを操作できるユーティリティアプリを作成できます。 コンテンツ同期を使用すると、ページのバージョン管理されたアーカイブを作成して、アプリとバンドルできます。

通常、 ***AEM管理者*** は、作成ウィザードを使用してアプリを作成するか、既存のアプリを読み込むことで、新しいアプリをAEM Mobile カタログに追加する役割を担っています。

ここから ***AEM オーサー*** （または *マーケター*）で、標準のテンプレートとコンポーネントを使用して、ページの追加と編集、コンポーネントのドラッグ&amp;ドロップ、DAM からのすべてのタイプのメディア（画像、ビデオ、テキストフラグメント（コンテンツフラグメント）など）の追加ができるようになりました。

AEM Mobileの真のパワーは、 *精通した* ***AEM開発者*** カスタム web テンプレートおよびコンポーネントを拡張および作成して、 *AEM オーサー* 美しく魅力的なモバイルエクスペリエンスを作成する。 これらのテンプレートとコンポーネントは、モバイルアプリ用に最適化されるだけでなく、デバイスとAEM サーバー（任意のリモートサーバー）の両方に通信して、オムニチャネルサービスのエンドポイントに提供されます。

>[!NOTE]
>
>いつ *AEM オーサー* では、アプリの準備が整ったと想定しています。関係者は最初に、を使用してアプリをダウンロードできます **[Adobeの検証](/help/mobile/phonegap-mobile-quickstart.md)** （AppStore と PlayStore の両方で利用可能）レビューと承認のために。 グリーンライトを受け取ると、AEM Mobile ContentSync コンテンツリリース管理ダッシュボードを使用して、この新しいコンテンツや更新されたコンテンツを直接ユーザーにリリースできます。 1 人の担当者が任意の数の役割を引き受けることができます。役割は、お客様とガバナンスポリシーによって異なります。

## 前提条件 {#prerequisites}

AEM Mobileは、AEM プラットフォーム全体を構成する 1 つの柱にすぎません。

AEM Mobileを使用してこの入門ガイドの手順に従う前に、AEMとAEM Mobile コントロールセンターについて理解しておく必要があります。 以下を参照してください。

[AEM使用の手引き](/help/sites-deploying/deploy.md)

[AEM Mobile コントロールセンターのウォークスルー](/help/mobile/phonegap-authoring-apps.md)

## 作成者向けクイックリンク {#quicklinks-for-authors}

参照： [AEMでのAdobe PhoneGap Enterprise 向けオーサリング](/help/mobile/phonegap.md) 作成者の役割および責務について説明します。

## 開発者向けクイックリンク {#quicklinks-for-developers}

AEM Mobileと統合され、開発者がカスタマイズできるサンプルアプリケーションがあります。 クリックする [AEMを使用したAdobe PhoneGap Enterprise の開発](/help/mobile/developing-in-phonegap.md).

以降の章では、アプリケーションのホワイトラベル設定、ローカリゼーション、国際化、コンテンツ同期、ターゲティング、分析などの高度な概念について説明します。

## 管理者向けクイックリンク {#quicklinks-for-administrators}

参照： [AEMを使用したAdobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md) でモバイルアプリケーションを設定および管理します。

>[!NOTE]
>
>ハイブリッドモバイルテクノロジーを使用すると、次のような豊富なモバイルアプリケーションを作成できます *オフラインおよびオンラインでの実行* 実際、AEM Mobileを使用すると、多くのお客様は、オンラインかオフラインかを確認し、それに応じて動作するアプリを作成します。
