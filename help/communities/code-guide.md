---
title: コーディングのガイドライン
seo-title: Coding Guidelines
description: Communities 開発者向けのガイドライン、ヒント、テクニック
seo-description: Communities developer guidelines, tips, and tricks
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 35%

---

# コーディングのガイドライン {#coding-guidelines}

## ガイドライン、ヒント、テクニック {#guidelines-tips-and-tricks}

AEM Communities の操作は、以前は Java Server Pages に大きく依存していましたが、ビジネスロジック、スタイルおよびページコンテンツが相互に異なる場合にテンプレートスクリプト言語を柔軟に選択できるように進化しています。

ユーザー生成コンテンツ (UGC) を柔軟に操作できるのは、SocialResourceProvider API を使用することです。UGC では、どのコンテンツを認識する必要がなくなります [SRP](srp.md) オプションがデプロイメント用に選択されました。

AEM Communities 開発者向けのさまざまなコーディングのガイドラインとベストプラクティスを次に示します。

### コード {#code}

* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md) - UGC が JCR(JSRP) に格納されている場合にのみ機能するアプリケーションを記述しないようにする方法
* [SocialUtils リファクタリング](socialutils.md) - SocialUtils に代わる SRP のユーティリティメソッド。
* [命名規則](naming-conventions.md)  — カスタム Java クラスの命名規則。

### スクリプト {#scripts}

* [コミュニティコンポーネントのサイドロード](sideloading.md)  — ページの読み込み後に、コンポーネントを動的に追加する方法。
* [リッチテキストエディターの基本事項](rte.md)  — メンバーがコンテンツを投稿するために提供するリッチテキスト UI をカスタマイズする方法。

### IDE {#ide}

* [コミュニティでの Maven の使用](maven.md)  — コミュニティ API jar を含める方法。
* [SocialUtils リファクタリング](socialutils.md) - SocialUtils に代わる SRP のユーティリティメソッド。
