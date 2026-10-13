---
title: ソフトウェアのアーキテクチャ
description: Adobe Experience Manager 用のソフトウェアの設計に関するベストプラクティスについて説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 95%
---
# ソフトウェアのアーキテクチャ{#software-architecture}

## アップグレード用のデザイン {#design-for-upgrades}

標準動作を拡張するときは、アップグレードを念頭に置いておくことが重要です。 常に/apps ディレクトリにカスタマイズを適用し、/libs ディレクトリ内の対応するノードの上にオーバーレイするか、sling:resourceSuperTypeを使用して標準動作を拡張します。 新しい AEM バージョンをサポートするためにいくつかの変更が必要になることがありますが、このプラクティスに従えば、新しいバージョンでカスタマイズされた内容が上書きされることはありません。

### 可能な場合はテンプレートおよびコンポーネントを再利用 {#reuse-template-and-components-when-possible}

これにより、サイトのルックアンドフィールをより一貫性のあるものにし、コードのメンテナンスを簡素化できます。 新しいテンプレートが必要なときは、共有基本テンプレートから拡張してください。このようにすると、clientlib のインクルードといったグローバルな要件を 1 箇所でコーディングできます。 新しいコンポーネントが必要な場合は、既存のコンポーネントからの拡張を検討してください。

### テンプレートデザイン {#design-template-designs}

ページで各 parsys にどのコンポーネントを含めることができるかを定義することで、サイトの外観と操作性における一貫性を制御できます。 ページ上でのデザインへのアクセスを制限することにより、他の作成者が企業の標準を遵守しながら、「スーパー作成者」は開発者の介入なしでページごとに許可されたコンポーネントを変更できるようになります。

### SOLID アーキテクチャを開発 {#develop-a-solid-architecture}

SOLID は、従うべき 5 つのアーキテクチャ原則を表す頭字語です。

* **S**（単一責任の原則）- 各モジュール、クラス、メソッドなどにはそれぞれ責務を 1 つずつのみ割り当てるようにします。
* **O**（オープン／クローズドの原則 ）- モジュールは、拡張に対してはオープンにし、変更に対してはクローズドにします。
* **L**（リスコフの置換原則） - タイプは、サブタイプに置き換え可能である必要があります。
* **I**（インターフェイス分離の原則） - クライアントに対して、利用していないメソッドへの依存を強制しないようにします。
* **D**（依存性逆転の原則） - 上位のモジュールは、下位のモジュールに依存しないようにします。 どちらも、抽象化に依存する必要があります。 抽象化が詳細に依存しないようにします。 詳細は抽象化に依存する必要があります。

この 5 つの原則に遵守に努めることで、懸念事項が厳密に分離されたシステムが確立できるはずです。

>[!TIP]
>
>SOLID はオブジェクト指向プログラミングで一般的に使用される概念で、各要素については業界文献で広く議論されています。
>
>この情報は、あくまでも理解のために提示された簡単な要約であり、これらの概念についてはさらに詳しく学ぶことをお勧めします。

### 堅牢性の原則に準拠する {#follow-the-robustness-principle}

堅牢性原則では、送信するものに関しては厳密に、受信するものに関しては寛容になることと規定しています。 つまり、サードパーティにメッセージを送信する際には、仕様に完全に準拠する必要があります。 ただし、サードパーティからメッセージを受信した場合は、メッセージの意味が明確である限り、準拠していないメッセージでも受け入れる必要があります。

### 独自のモジュールにスパイクを実装する {#implement-spikes-in-their-own-modules}

スパイクとテストコードは、アジャイルソフトウェアの実装の一部です。 ただし、適切な管理レベルがない場合は、実稼動環境のコードベースに侵入しないようにする必要があります。 その結果、独自のモジュールでスパイクを作成することをお勧めします。

### 独自のモジュールにデータ移行スクリプトを実装 {#implement-data-migration-scripts-in-their-own-module}

データ移行スクリプトは実稼動環境のコードで、サイトの初期起動時に 1 回のみ実行されます。 したがって、サイトがライブになると、スクリプトはデッドコードになります。 移行スクリプトに依存する実装コードをビルドしないようにするには、移行スクリプトをそのモジュール自体に実装する必要があります。 こうすると、起動直後にこのコードを削除して廃棄できるので、システムからデッドコードが排除されます。

### POM ファイルで公開済みの Maven 表記規則に従う {#follow-published-maven-conventions-in-pom-files}

Apache が [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html) でスタイル規則を公開しています。 新しいリソースを期待される水準にすることが容易になるので、この規則に従うことをお勧めします。
