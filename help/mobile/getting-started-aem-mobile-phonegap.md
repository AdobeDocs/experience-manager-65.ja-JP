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
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 7%

---

# AEM Adobe PhoneGap{#aem-adobe-phonegap}

{{ue-over-mobile}}

AEM を PhoneGap と連携し、AEM ページを使用してアプリを簡単に作成できます。PhoneGap を使用すると、ユーザーがコンテンツを操作できるユーティリティアプリを作成できます。 コンテンツ同期を使用すると、ページのバージョン管理されたアーカイブを作成して、アプリとバンドルできます。

通常、***AEM管理者*** は、作成ウィザードを使用してアプリを作成するか、既存のアプリを読み込むことで、新しいアプリをAEM Mobile カタログに追加する役割を担います。

ここから、***AEM オーサー*** （または *マーケター*）は、標準のテンプレートおよびコンポーネントを使用して、ページの追加と編集、コンポーネントのドラッグ&amp;ドロップ、画像、ビデオ、テキストフラグメント（コンテンツフラグメント）など、DAM からのすべてのタイプのメディアの追加を行えるようになりました。

AEM Mobileの真の特長は、*精通&#x200B;**&#x200B;**&#x200B;AEM Developer*** がカスタム web テンプレートおよびコンポーネントを拡張および作成して、*AEM オーサー* が美しく魅力的なモバイルエクスペリエンスを作成できるようにすることです。 これらのテンプレートとコンポーネントは、モバイルアプリ用に最適化されるだけでなく、デバイスとAEM サーバー（任意のリモートサーバー）の両方に通信して、オムニチャネルサービスのエンドポイントに提供されます。

>[!NOTE]
>
>*AEM オーサー* がアプリの準備が整ったと判断した場合、レビューおよび承認のために、まず関係者に **[Adobeの検証](/help/mobile/phonegap-mobile-quickstart.md)** を使用してアプリをダウンロードさせることができます（AppStore と PlayStore の両方で利用可能）。 グリーンライトを受け取ると、AEM Mobile ContentSync コンテンツリリース管理ダッシュボードを使用して、この新しいコンテンツや更新されたコンテンツを直接ユーザーにリリースできます。 1 人の担当者が任意の数の役割を引き受けることができます。役割は、お客様とガバナンスポリシーによって異なります。

## 前提条件 {#prerequisites}

AEM Mobileは、AEM プラットフォーム全体を構成する 1 つの柱にすぎません。

AEM Mobileを使用してこの入門ガイドの手順に従う前に、AEMとAEM Mobile コントロールセンターについて理解しておく必要があります。 以下を参照してください。

[AEM使用の手引き](/help/sites-deploying/deploy.md)

[AEM Mobile コントロールセンターのウォークスルー](/help/mobile/phonegap-authoring-apps.md)

## 作成者向けクイックリンク {#quicklinks-for-authors}

作成者のロールと責任については、[AEMでのAdobe PhoneGap Enterprise 向けオーサリング &#x200B;](/help/mobile/phonegap.md) を参照してください。

## 開発者向けクイックリンク {#quicklinks-for-developers}

AEM Mobileと統合され、開発者がカスタマイズできるサンプルアプリケーションがあります。 [AEMを使用したAdobe PhoneGap Enterprise の開発 &#x200B;](/help/mobile/developing-in-phonegap.md) をクリックします。

以降の章では、アプリケーションのホワイトラベル設定、ローカリゼーション、国際化、コンテンツ同期、ターゲティング、分析などの高度な概念について説明します。

## 管理者向けクイックリンク {#quicklinks-for-administrators}

モバイルアプリケーションを設定および管理するには、[AEMを使用したAdobe PhoneGap Enterprise のコンテンツの管理 &#x200B;](/help/mobile/administer-phonegap.md) を参照してください。

>[!NOTE]
>
>ハイブリッドモバイルテクノロジーを使用すると、*オフラインでもオンラインでも実行* できる機能豊富なモバイルアプリケーションを作成できます。実際、AEM Mobileを使用すると、多くのお客様は、オンラインかオフラインかを確認し、それに応じて動作するアプリを作成します。
