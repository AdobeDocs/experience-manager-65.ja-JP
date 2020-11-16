---
title: コーディングのガイドライン
seo-title: コーディングのガイドライン
description: Communities 開発者向けのガイドライン、ヒント、テクニック
seo-description: Communities 開発者向けのガイドライン、ヒント、テクニック
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 38%

---


# コーディングのガイドライン {#coding-guidelines}

## ガイドライン、ヒント、テクニック {#guidelines-tips-and-tricks}

AEM Communities の操作は、以前は Java Server Pages に大きく依存していましたが、ビジネスロジック、スタイルおよびページコンテンツが相互に異なる場合にテンプレートスクリプト言語を柔軟に選択できるように進化しています。

Further flexibility in working with user generated content (UGC) is through the SocialResourceProvider API, which eliminates the need for awareness of which [SRP](srp.md) option was chosen for the deployment.

AEM Communities 開発者向けのさまざまなコーディングのガイドラインとベストプラクティスを次に示します。

### コード {#code}

* [SRPを使用したUGCへのアクセス](accessing-ugc-with-srp.md) - UGCがJCR(JSRP)に格納されている場合にのみ機能するアプリケーションの記述を回避する方法。
* [SocialUtilsリファクタリング](socialutils.md) - SocialUtilsを置き換えるSRPのユーティリティメソッド。
* [命名規則](naming-conventions.md) — カスタムJavaクラスの命名規則。

### スクリプト {#scripts}

* [Communitiesコンポーネントのサイドロード](sideloading.md) — ページの読み込み後にコンポーネントを動的に追加する方法。
* [リッチテキストエディター](rte.md) — コンテンツを投稿するためにメンバーに提供されるリッチテキストUIをカスタマイズする方法。

### IDE {#ide}

* [Maven for Communitiesの使用](maven.md) - Communities API jarを含める方法。
* [SocialUtilsリファクタリング](socialutils.md) - SocialUtilsを置き換えるSRPのユーティリティメソッド。

