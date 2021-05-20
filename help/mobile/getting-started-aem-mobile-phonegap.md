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
exl-id: d989e235-5993-4738-8523-5b9a5f6bf712
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 52%

---

# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

AEM を PhoneGap と連携し、AEM ページを使用してアプリを簡単に作成できます。PhoneGap と連携することで、そのコンテンツを利用するユーティリティアプリを作成できます。コンテンツ同期を使用すると、アプリにバンドルするページのバージョン管理されたアーカイブを作成できます。

通常、***AEM Administrator***&#x200B;は、作成ウィザードを使用して新しいアプリを作成するか、既存のアプリを読み込むことで、AEM Mobileカタログに新しいアプリを追加します。

ここから、***AEMオーサー***（または&#x200B;*マーケター*）が、標準のテンプレートとコンポーネントを使用して、ページの追加と編集、コンポーネントのドラッグ&amp;ドロップ、DAMからのすべてのタイプのメディアの追加が可能になります。

AEM Mobileの本当の力は、*経験豊富な* ***AEM開発者***&#x200B;がカスタムのWebテンプレートとコンポーネントを拡張して作成し、*AEMオーサー*&#x200B;が見栄えの良い魅力的なモバイルエクスペリエンスを作成できることです。 これらのテンプレートとコンポーネントは、モバイルアプリの世界に最適化されているだけではありません。ただし、デバイスとAEMサーバー（リモートサーバー）の両方をオムニチャネルサービスエンドポイントに通信します。

>[!NOTE]
>
>アプリの準備が整ったら、AEM 作成者は、まず、レビューおよび承認用に、**[Adobe Verify](/help/mobile/phonegap-mobile-quickstart.md)**（AppStore でも Play Store でも入手可能）で関係者にアプリをダウンロードしてもらうことができます。**&#x200B;緑の信号を受け取ったユーザーは、 AEM Mobile ContentSyncコンテンツリリース管理ダッシュボードを使用して、新しいコンテンツや更新されたコンテンツを直接ユーザーにリリースできます。 各個人の能力とガバナンスポリシーに合わせて、1 人のユーザーが任意の数の役割を担うことができます。

## 前提条件 {#prerequisites}

AEM Mobile は、完全な AEM プラットフォームを構成する 1 つの柱に過ぎません。

AEM Mobile を操作して、この使用の手引きに記載された手順を実行する前に、ユーザーは AEM および AEM Mobile コントロールセンターについて十分に理解しておく必要があります。次のページを参照してください。

[AEM 使用の手引き](/help/sites-deploying/deploy.md)

[AEM Mobile Control Centerのガイド](/help/mobile/phonegap-authoring-apps.md)

## 作成者向けクイックリンク {#quicklinks-for-authors}

作成者の役割と責務について詳しくは、 AEM](/help/mobile/phonegap.md)でのAdobe PhoneGap Enterprise向けのオーサリング[を参照してください。

## 開発者向けクイックリンク {#quicklinks-for-developers}

AEM Mobile と統合でき、開発者がカスタマイズできるサンプルアプリケーションがあります。[AEM での Adobe PhoneGap Enterprise の開発](/help/mobile/developing-in-phonegap.md)を参照してください。

以降の章では、アプリケーションのホワイトラベリング、ローカリゼーション、国際化対応、コンテンツ同期、ターゲット設定、解析などの高度な概念について説明します。

## 管理者向けクイックリンク  {#quicklinks-for-administrators}

モバイルアプリケーションの設定と管理については、「 AEM](/help/mobile/administer-phonegap.md)を使用したAdobe PhoneGap Enterpriseのコンテンツの管理」を参照してください。[

>[!NOTE]
>
>ハイブリッドモバイルテクノロジーを使用すると、AEM Mobileで&#x200B;*オフラインおよびオンライン*&#x200B;を実行するリッチモバイルアプリケーションを作成できます。多くのお客様は、オンラインまたはオフラインで動作を確認するアプリを作成します。
