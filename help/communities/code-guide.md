---
title: コーディングのガイドライン
description: Communitiesの開発者向けガイドライン、ヒント、テクニック
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 3%
---
# コーディングのガイドライン {#coding-guidelines}

## ガイドライン、ヒント、テクニック {#guidelines-tips-and-tricks}

AEM Communitiesの使用は、Java Server Pagesに大きく依存することから、ビジネスロジック、スタイル、ページコンテンツが異なるテンプレートスクリプト言語の選択の柔軟性へと進化しました。

ユーザー生成コンテンツ（UGC）の操作に関する柔軟性をさらに高めるために、SocialResourceProvider APIを使用します。これにより、デプロイメントに選択された[SRP](srp.md) オプションを認識する必要がなくなります。

以下に、AEM Communities開発者向けの様々なコーディングガイドラインとベストプラクティスを示します。

### コード {#code}

* [SRPを使用したUGCへのアクセス &#x200B;](accessing-ugc-with-srp.md) - UGCがJCR （JSRP）に保存されている場合にのみ機能するアプリケーションの書き込みを避ける方法。
* [SocialUtils リファクタリング &#x200B;](socialutils.md) - SocialUtilsを置き換えるSRPのユーティリティ メソッド。
* [命名規則](naming-conventions.md) - カスタム Java クラスの命名規則。

### スクリプト {#scripts}

* [Sideloading Communities Components](sideloading.md) - ページの読み込み後にコンポーネントを動的に追加する方法。
* [&#x200B; リッチテキストエディターの基本](rte.md) - コンテンツを投稿するためにメンバーに提供されるリッチテキスト UIをカスタマイズする方法。

### IDE {#ide}

* [Maven for Communitiesの使用](maven.md) - Communities API jarを含める方法。
* [SocialUtils リファクタリング &#x200B;](socialutils.md) - SocialUtilsを置き換えるSRPのユーティリティ メソッド。
