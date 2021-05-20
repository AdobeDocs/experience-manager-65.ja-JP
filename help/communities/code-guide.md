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
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 38%

---

# コーディングのガイドライン  {#coding-guidelines}

## ガイドライン、ヒント、テクニック {#guidelines-tips-and-tricks}

AEM Communities の操作は、以前は Java Server Pages に大きく依存していましたが、ビジネスロジック、スタイルおよびページコンテンツが相互に異なる場合にテンプレートスクリプト言語を柔軟に選択できるように進化しています。

ユーザー生成コンテンツ(UGC)の操作を柔軟におこなえるのは、SocialResourceProvider APIを通じてのみです。このAPIを使用すると、デプロイメント用に[SRP](srp.md)オプションを選択したかどうかを認識する必要がなくなります。

AEM Communities 開発者向けのさまざまなコーディングのガイドラインとベストプラクティスを次に示します。

### コード {#code}

* [SRPを使用したUGCへのアクセス](accessing-ugc-with-srp.md)  - UGCがJCR(JSRP)に格納されている場合にのみ機能するアプリケーションを記述しないようにする方法。
* [SocialUtilsのリファクタリング](socialutils.md)  - SocialUtilsに代わるSRPのユーティリティメソッド。
* [命名規則](naming-conventions.md)  — カスタムJavaクラスの命名規則。

### スクリプト {#scripts}

* [コミュニティコンポーネントのサイドローディング](sideloading.md)  — ページの読み込み後にコンポーネントを動的に追加する方法。
* [リッチテキストエディターの基本事項](rte.md)  — メンバーがコンテンツを投稿するために提供するリッチテキストUIのカスタマイズ方法。

### IDE {#ide}

* [コミュニティ用のMavenの使用](maven.md)  — コミュニティAPI jarを含める方法。
* [SocialUtilsのリファクタリング](socialutils.md)  - SocialUtilsに代わるSRPのユーティリティメソッド。
