---
title: AEM Adobe PhoneGap
description: AEM を PhoneGap と連携し、AEM ページを使用してアプリを簡単に作成できます。 Adobe PhoneGap Enterpriseを使い始めるには、このページに従ってください。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: d989e235-5993-4738-8523-5b9a5f6bf712
solution: Experience Manager
feature: Mobile
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 10%
---
# AEM Adobe PhoneGap{#aem-adobe-phonegap}

{{ue-over-mobile}}

AEM を PhoneGap と連携し、AEM ページを使用してアプリを簡単に作成できます。 PhoneGapでは、ユーザーがコンテンツを操作できるユーティリティ アプリを作成できます。 コンテンツ同期を使用すると、アプリにバンドルするページのバージョン管理されたアーカイブを作成できます。

通常、***AEM Administrator***&#x200B;は、作成ウィザードを使用してアプリケーションを作成するか、既存のアプリケーションを読み込むか、新しいアプリケーションをAEM Mobile カタログに追加する責任があります。

ここから、***AEM オーサー*** （または&#x200B;*マーケター*）が、すぐに使えるテンプレートとコンポーネントを使用して、ページの追加と編集、コンポーネントのドラッグ&amp;ドロップ、画像、ビデオ、テキストフラグメント（コンテンツフラグメント）を含むあらゆるタイプのメディアをDAMから追加できるようになりました。

AEM Mobileの真の力は、*経験豊富な* ***AEM Developer***&#x200B;がカスタム web テンプレートとコンポーネントを拡張および作成して、*AEM Author*&#x200B;が美しく魅力的なモバイル エクスペリエンスを作成できるようにすることです。 これらのテンプレートとコンポーネントは、モバイルアプリ環境に最適化されているだけでなく、デバイスとAEM サーバー（任意のリモートサーバー）の両方をオムニチャネルサービスエンドポイントに通信します。

>[!NOTE]
>
>*AEM作成者*&#x200B;がアプリの準備ができたと判断した場合、まず関係者に&#x200B;**[Adobe Verify](/help/mobile/phonegap-mobile-quickstart.md)** （AppStoreとPlayStoreの両方で利用可能）を使用してアプリをダウンロードしてもらい、レビューと承認を行うことができます。 許可を受けると、AEM Mobile ContentSync コンテンツリリース管理ダッシュボードを通じて、この新しいコンテンツや更新されたコンテンツをユーザーに直接リリースすることができます。 ひとりの人間がいくつもの役割を担うことができるのは、皆さんとガバナンスのポリシー次第です。

## 前提条件 {#prerequisites}

AEM Mobileは、AEMの包括的な基盤を構成する柱のひとつにすぎません。

AEM Mobileを使用する前に、この基本ガイドの手順に従う前に、AEMとAEM Mobile Control Centerについて理解しておく必要があります。 以下を参照してください。

[AEMの導入方法](/help/sites-deploying/deploy.md)

[AEM Mobileコントロールセンターのチュートリアル](/help/mobile/phonegap-authoring-apps.md)

## 作成者向けクイックリンク {#quicklinks-for-authors}

作成者の役割と責任について詳しくは、[AEMでのAdobe PhoneGap Enterpriseのオーサリング ](/help/mobile/phonegap.md)を参照してください。

## 開発者向けQuickLinks {#quicklinks-for-developers}

AEM Mobileと統合され、開発者がカスタマイズできるサンプルアプリケーションがあります。 「[AEMを使用したAdobe PhoneGap Enterpriseの開発](/help/mobile/developing-in-phonegap.md)」をクリックします。

以降の章では、アプリケーションのホワイトラベル、ローカライゼーション、国際化、ContentSync、ターゲティング、分析などの高度な概念について説明します。

## 管理者向けQuickLinks {#quicklinks-for-administrators}

モバイルアプリケーションの設定と管理については、「[Administering Content for Adobe PhoneGap Enterprise with AEM](/help/mobile/administer-phonegap.md)」を参照してください。

>[!NOTE]
>
>ハイブリッドモバイルテクノロジーを使用すると、AEM Mobileを使用してオフラインおよびオンラインで&#x200B;*実行するリッチモバイルアプリケーションを作成できます。実際、多くのお客様は、オンラインまたはオフラインの状態を確認し、それに応じて動作するアプリケーションを作成することを選択しています。*
