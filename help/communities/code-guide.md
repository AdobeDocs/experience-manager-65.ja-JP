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

ユーザー生成コンテンツ（UGC）での操作がさらに柔軟なのは、SocialResourceProvider API を使用することで可能になります。これにより、デプロイメントで [SRP](srp.md) オプションが選択されたことを認識する必要がなくなります。

AEM Communities開発者向けの様々なコーディングガイドラインとベストプラクティスを以下に示します。

### コード {#code}

* [SRP による UGC へのアクセス &#x200B;](accessing-ugc-with-srp.md) - UGC が JCR （JSRP）に格納されている場合にのみ機能するアプリケーションの書き込みを回避する方法。
* [SocialUtils リファクタリング &#x200B;](socialutils.md) - SocialUtils に代わる SRP のユーティリティメソッド。
* [&#x200B; 命名規則 &#x200B;](naming-conventions.md) - カスタム Java クラスの命名規則。

### スクリプト {#scripts}

* [Communities コンポーネントのサイドローディング &#x200B;](sideloading.md) - ページの読み込み後にコンポーネントを動的に追加する方法。
* [&#x200B; リッチテキストエディターの基本事項 &#x200B;](rte.md) - メンバーに提供されるリッチテキスト UI をカスタマイズしてコンテンツを投稿する方法。

### IDE {#ide}

* [&#x200B; コミュニティでの Maven の使用 &#x200B;](maven.md) - Communities API jar を含める方法。
* [SocialUtils リファクタリング &#x200B;](socialutils.md) - SocialUtils に代わる SRP のユーティリティメソッド。
