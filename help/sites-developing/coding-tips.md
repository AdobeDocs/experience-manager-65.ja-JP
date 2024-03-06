---
title: コーディングのヒント
description: Adobe Experience Managerでのコーディングのベストプラクティスに関するヒントをいくつか紹介します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 85ca35e5-6e2b-447a-9711-b12601beacdd
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 54%

---

# コーディングのヒント{#coding-tips}

## 可能な限り taglibs または HTL を使用 {#use-taglibs-or-htl-as-much-as-possible}

スクリプトレットを JSP に含めると、コード内の問題のデバッグが難しくなります。また、JSP にスクリプトレットを含めると、ビューレイヤーとビジネスロジックを分離するのが難しくなります。これは、単一責任原則と MVC 設計パターンの違反です。

### わかりやすいコードを記述 {#write-readable-code}

コードを記述するのは一度ですが、何度も読まれます。書かれたコードをきれいにするのに時間を費やすと、あなたや他の開発者が後で読むのと同じように、道端で配当が払われます。

### 目的を明確に表す名前を選択 {#choose-intention-revealing-names}

別のプログラマーがモジュールを開かなくても内容がわかるようにすることが理想的です。同様に、メソッドを読まなくても目的がわかるようにする必要があります。これらのアイデアを購読すれば購読するほど、コードを読みやすくなり、コードの記述と変更が速くなります。

AEM のコードベースでは、次のような規則が使用されます。


* インターフェイスの単一の実装は、 `<Interface>Impl`、つまり、 `ReaderImpl`.
* インターフェイスの複数の実装には、という名前が付けられます `<Variant><Interface>`、つまり、 `JcrReader` および `FileSystemReader`.
* 抽象ベースクラスには `Abstract<Interface>` または `Abstract<Variant><Interface>` という名前を付けます。
* パッケージの名前はです。 `com.adobe.product.module`. それぞれの Maven アーティファクトまたは OSGi バンドルには独自のパッケージが必要です。
* Java™の実装は、API の下の impl パッケージに配置されます。


これらの規則は必ずしもお客様の実装に適用されるわけではありませんが、コードを保守できる状態に維持できるように、規則を定義し、それに従うことが重要です。

名前を見れば、その目的が明らかになるようにすることが理想的です。名前が明確さに欠けるかどうかを判断するための一般的なコードテストは、変数やメソッドの目的を説明するコメントの有無です。

<table>
 <tbody>
  <tr>
   <td><p><strong>不明確</strong></p> </td>
   <td><p><strong>明確</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d; //経過時間（日単位）</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//タグ付き画像を取得<br /> public List getItems() {}</p> </td>
   <td><p>public List getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### 繰り返さないでください  {#don-t-repeat-yourself}

DRY（Don&#39;t repeat yourself）は、同じコードセットを繰り返してはならないということです。これは、文字列リテラルなどにも該当します。コードが重複していると、変更が必要な箇所を探し出して削除しなければならない場合に不具合が生じる可能性があります。

### 範囲を限定しない CSS ルールを避ける {#avoid-naked-css-rules}

CSS ルールは、アプリケーションのコンテキスト内のターゲット要素に固有でなければなりません。例えば、*.content .center* に適用される CSS ルールは過度に広範になり、最終的にシステム全体の多数のコンテンツに影響を及ぼす可能性があるので、将来、他の開発者がそのスタイルをオーバーライドしなければならなくなります。一方で、 *.myapp-centertext* 中央揃えを指定するので、より具体的なルールになります *テキスト* を設定します。

### 廃止された API を使用しない {#eliminate-usage-of-deprecated-apis}

API が廃止された場合は常に、廃止された API を使用するのではなく、推奨される新しいアプローチを確認することをお勧めします。これにより、将来、円滑にアップグレードできるようになります。

### ローカライズ可能なコードを記述 {#write-localizable-code}

作成者から提供されない文字列は、を通じてAEM i18n 辞書への呼び出しでラップする必要があります。 *I18n.get()* JSP/Java および *CQ.I18n.get()* JavaScript で使用できます。 実装が見つからなかった場合、この実装は渡された文字列を返すので、プライマリ言語で機能を実装した後でローカリゼーションを柔軟に実装できます。

### 安全のためのリソースパスのエスケープ {#escape-resource-paths-for-safety}

JCR 内のパスにスペースを含めることはできませんが、スペースが含まれていると、コードが壊れないようにする必要があります。 Jackrabbit では、*escape()* および *escapePath()* メソッドを含む Text ユーティリティクラスを提供しています。JSP については、Granite UI が *granite:encodeURIPath() EL* 関数を公開しています。

### XSS API や HTL を使用して、クロスサイトスクリプティング攻撃を防ぐ {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM では、パラメーターを簡単にクリーンにして、クロスサイトスクリプティング攻撃に対する安全性を確保するための XSS API を提供しています。また、HTL では、これらの保護がテンプレート言語に直接組み込まれています。 API 参照シートは、[開発 - ガイドラインおよびベストプラクティス](/help/sites-developing/dev-guidelines-bestpractices.md)でダウンロードできます。

### 適切なログ機能を実装 {#implement-appropriate-logging}

Java™コードの場合、AEMは、メッセージのログに標準 API として slf4j をサポートしています。管理の一貫性を保つために、OSGi コンソールで利用可能な設定と共に使用する必要があります。 Slf4j は、5 つの異なるログレベルを公開しています。Adobeは、メッセージを記録するレベルを選択する際に、次のガイドラインに従うことをお勧めします。

* ERROR：コードが中断され、処理を続行できない場合。これは多くの場合、予期しない例外の結果として発生します。これらのシナリオにスタックトレースを含めると便利です。
* WARN：正しく動作していない部分があるが、処理は続行できる場合。これは多くの場合、*PathNotFoundException* など、予期された例外の結果です。
* INFO：システムを監視する際に役立つ情報。これがデフォルトであり、ほとんどのお客様の環境でこの設定がそのまま使用されることに留意してください。したがって、過度に使用しないでください。
* DEBUG：処理に関する低レベルの情報。 サポートに関する問題をデバッグする際に役立ちます。
* TRACE：メソッドの開始/終了など、最も低いレベルの情報。 これは通常、開発者のみが使用します。

JavaScript がある場合、 *console.log* は開発時にのみ使用し、すべてのログ文はリリース前に削除する必要があります。

### カーゴカルトプログラミングの回避 {#avoid-cargo-cult-programming}

内容を理解せずに、コードをコピーしないでください。確信がないときには必ず、明確でないモジュールや API の経験が豊富な人物に確認するのが最善です。
