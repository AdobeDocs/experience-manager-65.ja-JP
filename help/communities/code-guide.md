---
title: コーディングのガイドライン
description: Communities 開発者向けガイドライン、ヒント、テクニック
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 3%

---

# コーディングのガイドライン {#coding-guidelines}

## ガイドライン、ヒントとテクニック {#guidelines-tips-and-tricks}

AEM Communitiesの使用は、Java Server Pages に大きく依存することから、ビジネスロジック、スタイル、ページコンテンツが互いに異なるテンプレートスクリプティング言語を柔軟に選択できるように進化しました。

ユーザー生成コンテンツ (UGC) を柔軟に操作できるのは、SocialResourceProvider API を使用することです。UGC では、どのコンテンツを認識する必要がなくなります。 [SRP](srp.md) オプションがデプロイメント用に選択されました。

AEM Communities開発者向けの様々なコーディングガイドラインおよびベストプラクティスを次に示します。

### コード {#code}

* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md) - UGC が JCR(JSRP) に格納されている場合にのみ機能するアプリケーションを記述しないようにする方法
* [SocialUtils のリファクタリング](socialutils.md) - SocialUtils に代わる SRP のユーティリティメソッド。
* [命名規則](naming-conventions.md)  — カスタム Java クラスの命名規則。

### スクリプト {#scripts}

* [コミュニティコンポーネントのサイドロード](sideloading.md)  — ページの読み込み後に、コンポーネントを動的に追加する方法。
* [リッチテキストエディターの基本事項](rte.md)  — メンバーがコンテンツを投稿するために提供するリッチテキスト UI をカスタマイズする方法。

### IDE {#ide}

* [コミュニティでの Maven の使用](maven.md)  — コミュニティ API jar を含める方法。
* [SocialUtils のリファクタリング](socialutils.md) - SocialUtils に代わる SRP のユーティリティメソッド。
