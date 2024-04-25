---
title: コーディングのガイドライン
description: Communities 開発者のガイドライン、ヒント、テクニック
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 3%

---

# コーディングのガイドライン {#coding-guidelines}

## ガイドライン、ヒントおよびテクニック {#guidelines-tips-and-tricks}

AEM Communitiesの操作は、Java Server Pages への依存度が高くなっただけでなく、ビジネスロジック、スタイル、ページコンテンツが異なるテンプレートスクリプト言語を柔軟に選択できるようになった。

ユーザー生成コンテンツ（UGC）での操作がさらに柔軟なのは、SocialResourceProvider API を通じることで、どのコンテンツがどのようになっているかを認識する必要がなくなります [SRP](srp.md) デプロイメント用にオプションが選択されました。

AEM Communities開発者向けの様々なコーディングガイドラインとベストプラクティスを以下に示します。

### コード {#code}

* [SRP による UGC へのアクセス](accessing-ugc-with-srp.md) - UGC が JCR （JSRP）に格納されている場合にのみ機能するアプリケーションの記述を回避する方法。
* [SocialUtils のリファクタリング](socialutils.md) - SocialUtils を置き換える SRP のユーティリティメソッド。
* [命名規則](naming-conventions.md) - カスタム Java クラスの命名規則。

### スクリプト {#scripts}

* [Communities コンポーネントのサイドロード](sideloading.md) - ページの読み込み後にコンポーネントを動的に追加する方法。
* [リッチテキストエディターの基本事項](rte.md) - メンバーがコンテンツを投稿するために使用できるリッチテキスト UI のカスタマイズ方法。

### IDE {#ide}

* [コミュニティでの Maven の使用](maven.md) - Communities API jar を含める方法。
* [SocialUtils のリファクタリング](socialutils.md) - SocialUtils を置き換える SRP のユーティリティメソッド。
