---
title: ヘッドレスコンテンツの概要と AEM での翻訳方法について
description: ヘッドレスの概念、AEM へのマッピング方法、AEM 翻訳の基本概念について説明します。
exl-id: cb2e2d89-e2d2-462f-8fff-b201847d0641
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,Language Copy
role: Admin, Developer, User, Leader
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d9d38edd-df1b-480c-8f5e-72b62576f390
    internal-label: Site and page features
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: e15a4109-ae5d-497d-b301-31149e35aed4
    internal-label: Language Copy Wizard
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 100%
---
# ヘッドレスコンテンツの概要と AEM での翻訳方法について {#learn-about}

ヘッドレスの概念、AEM へのマッピング方法、AEM 翻訳の基本概念について説明します。

## 目的 {#objective}

このドキュメントを通じて、ヘッドレスコンテンツ配信、AEM によるヘッドレスのサポートおよびそうしたコンテンツの翻訳方法を理解できるようになります。 ドキュメントを読めば、以下が可能です。

* ヘッドレスコンテンツ配信の基本概念を理解する。
* AEM によるヘッドレスと翻訳のサポート方法に詳しくなる

## フルスタックコンテンツ配信 {#full-stack}

使いやすい大規模なコンテンツ管理システム（CMS）が登場して以来、多くの組織はメッセージング、ブランディング、コミュニケーションを管理する一元的な場所としてコンテンツ管理システムを活用してきました。 CMS をエクスペリエンス管理の中心として使用することで、異なるシステムでタスクを重複させる必要がなくなり、効率が向上しました。

![従来のフルスタック CMS](/help/journey-headless/developer/assets/full-stack.png)

フルスタック CMS では、コンテンツを操作する機能はすべて CMS 内にあります。 システムの機能は、CMS スタックの異なるコンポーネントを構成します。 フルスタックソリューションには多くの利点があります。

* 維持管理するシステムは 1 つである。
* コンテンツを一元的に管理できる。
* システムのすべてのサービスが統合されている。
* コンテンツのオーサリングはシームレスである。

したがって、新しいチャネルを追加したり、新しいタイプのエクスペリエンスをサポートしたりする必要がある場合は、1 つ（または複数）の新しいコンポーネントをスタックに挿入します。変更する場所は 1 つだけです。

![スタックへの新しいチャネルの追加](/help/journey-headless/developer/assets/adding-channel.png)

ただし、スタック内の他の項目を、変更に合わせて調整する必要があるので、スタック内の依存関係の複雑さがすぐに明らかになります。

## ヘッドレスのヘッド {#the-head}

システムのヘッドは、通常、そのシステムの出力レンダラーです。一般的には、GUI やその他のグラフィカル出力の形式です。

ヘッドレス CMS では、CMS がコンテンツを管理し、コンシューマーに配信します。 ただし、ヘッドレス CMS では、標準化された方法で&#x200B;**コンテンツ**&#x200B;を配信だけで、最終的な出力のレンダリングは省略され、コンテンツの&#x200B;**プレゼンテーション**&#x200B;は消費サービスに委ねられます。

![ヘッドレス CMS](/help/journey-headless/developer/assets/headless-cms.png)

消費サービス（AR エクスペリエンス、web ショップ、モバイルエクスペリエンス、プログレッシブ web アプリ（PWA）など）では、ヘッドレス CMS からコンテンツを取り込み、独自にレンダリングを提供します。 ヘッドレス CMS は、コンテンツに合わせて独自のヘッドを提供します。

ヘッドを省略することで、複雑さが減り、CMS をシンプルになります。 また、コンテンツのレンダリングの責任は、実際にコンテンツを必要とするサービスに移ります。多くの場合、サービスのほうがレンダリングに適しています。

## AEM でのヘッドレスコンテンツの翻訳 {#translating-in-aem}

従来の Web ページをフルスタック方式で作成、管理および配信する堅牢なツールに加えて、AEM では、自己完結型のコンテンツをオーサリングしてヘッドレスで提供する機能も備えています。

AEM の機能により、コンテンツをヘッドレスとフルスタックのどちらか一方で配信するか、両方のモデルで同時に配信することができます。 翻訳担当者にとっては、両方のタイプのコンテンツに同じ翻訳ツールセットを適用でき、コンテンツを翻訳するための統一されたアプローチが提供されます。

AEM によるコンテンツの翻訳方法の詳細については、このジャーニーで後ほど詳しく説明しますが、概念はシンプルです。

1. 翻訳統合フレームワークを設定して、翻訳サービスへの接続を定義します。
1. 翻訳するコンテンツを、翻訳ルールを使用して定義します。
1. 翻訳プロジェクトを作成してコンテンツを収集し、翻訳サービスに送信して、結果を受け取ります。
1. 翻訳済みコンテンツをレビューして公開します。

## 次のステップ {#what-is-next}

AEM ヘッドレス翻訳ジャーニーを開始していただきありがとうございます。 ドキュメントを読んだので、次を理解しているはずです。

* ヘッドレスコンテンツ配信の基本概念を理解する。
* AEM によるヘッドレスと翻訳のサポート方法に詳しくなる

この知識を踏まえて、次に[AEM ヘッドレス翻訳の基本を学ぶ](getting-started.md)のドキュメントを参照しながら、AEM ヘッドレス翻訳ジャーニーを続けてください。このドキュメントでは、AEM によるヘッドレスコンテンツの管理方法の概要と翻訳ツールについて説明します。

## その他のリソース {#additional-resources}

[AEM ヘッドレス翻訳の基本を学ぶ](getting-started.md)のドキュメントを確認して、ヘッドレス翻訳ジャーニーの次のステップに進むことをお勧めします。ヘッドレスジャーニーの続行に必須ではありませんが、この記事で取り上げたいくつかの概念について詳しく説明している追加のオプションリソースを以下に挙げておきます。

* [MSM と翻訳](/help/sites-administering/msm-and-translation.md) - AEM のマルチサイトマネージャーの詳細と翻訳ツールとの連携方法について説明します。
* [ヘッドレス CMS としての AEM の概要](/help/sites-developing/headless/introduction.md)
* [AEM 開発者ポータル](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=ja)
* [AEM のヘッドレスに関するチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=ja)
