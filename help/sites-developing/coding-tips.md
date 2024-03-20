---
title: コーディングのヒント
description: Adobe Experience Manager でのコーディングのベストプラクティスに関するヒントをいくつか紹介します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 85ca35e5-6e2b-447a-9711-b12601beacdd
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 96%

---

# コーディングのヒント{#coding-tips}

## 可能な限り taglib または HTL を使用する {#use-taglibs-or-htl-as-much-as-possible}

スクリプトレットを JSP に含めると、コード内の問題のデバッグが難しくなります。また、スクリプトレットを JSP に含めると、ビジネスロジックを表示レイヤーから切り離すことが難しくなり、単一責任の原則および MVC 設計パターンに違反することになります。

### わかりやすいコードを記述 {#write-readable-code}

コードを記述するのは一度ですが、何度も読まれます。あらかじめ時間をかけて、記述したコードを明確にしておくと、その後、自分自身や他の開発者がコードを読む場合に役立ちます。

### 目的を明確に表す名前を選択 {#choose-intention-revealing-names}

別のプログラマーがモジュールを開かなくても内容がわかるようにすることが理想的です。同様に、メソッドを読まなくても目的がわかるようにする必要があります。こうした考え方に忠実に従うほど、コードがわかりやすくなると共に、コードの記述や変更をより短時間で行えるようになります。

AEM のコードベースでは、次のような規則が使用されます。


* インターフェイスの単一の実装の名前は `<Interface>Impl` となります（例：`ReaderImpl`）。
* インターフェイスの複数の実装の名前は `<Variant><Interface>` となります（例：`JcrReader` や `FileSystemReader`）、
* 抽象ベースクラスの名前は `Abstract<Interface>` または `Abstract<Variant><Interface>` となります。
* パッケージの名前は `com.adobe.product.module` となります。それぞれの Maven アーティファクトまたは OSGi バンドルには独自のパッケージが必要です。
* Java™ 実装は、その API の下の impl パッケージに配置します。


これらの規則は必ずしもお客様の実装に適用されるわけではありませんが、コードを保守できる状態に維持できるように、規則を定義し、それに従うことが重要です。

名前を見れば、その目的が明らかになるようにすることが理想的です。名前が明確さに欠けるかどうかを判断するための一般的なコードテストは、変数やメソッドの目的を説明するコメントの有無です。

<table>
 <tbody>
  <tr>
   <td><p><strong>不明確</strong></p> </td>
   <td><p><strong>明確</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d; //elapsed time in days</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//get tagged images<br /> public List getItems() {}</p> </td>
   <td><p>public List getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### 繰り返さないでください  {#don-t-repeat-yourself}

DRY（Don&#39;t repeat yourself）は、同じコードセットを繰り返してはならないということです。これは、文字列リテラルなどにも該当します。コードが重複していると、変更が必要な箇所を探し出して削除しなければならない場合に不具合が生じる可能性があります。

### 範囲を限定しない CSS ルールを避ける {#avoid-naked-css-rules}

CSS ルールは、アプリケーションのコンテキスト内のターゲット要素に固有でなければなりません。例えば、*.content .center* に適用される CSS ルールは過度に広範になり、最終的にシステム全体の多数のコンテンツに影響を及ぼす可能性があるので、将来、他の開発者がそのスタイルをオーバーライドしなければならなくなります。*.myapp-centertext* とすると、アプリケーションのコンテキスト内で中央に配置される&#x200B;*テキスト*&#x200B;を指定するので、より具体的なルールになります。

### 廃止された API を使用しない {#eliminate-usage-of-deprecated-apis}

API が廃止された場合は常に、廃止された API を使用するのではなく、推奨される新しいアプローチを確認することをお勧めします。これにより、将来、円滑にアップグレードできるようになります。

### ローカライズ可能なコードを記述 {#write-localizable-code}

作成者によって指定されない文字列は、JSP/Java の *I18n.get()* および JavaScript の *CQ.I18n.get()* を使用して AEM の i18n ディクショナリへの呼び出しでラップする必要があります。実装が見つからなかった場合、この実装は渡された文字列を返すので、プライマリ言語で機能を実装した後でローカリゼーションを柔軟に実装できます。

### 安全のためにリソースパスをエスケープする {#escape-resource-paths-for-safety}

JCR のパスにスペースを使用することはできませんが、スペースが使用されていても、コードが中断しないようにする必要があります。Jackrabbit では、*escape()* および *escapePath()* メソッドを含む Text ユーティリティクラスを提供しています。JSP については、Granite UI が *granite:encodeURIPath() EL* 関数を公開しています。

### XSS API や HTL を使用して、クロスサイトスクリプティング攻撃を防ぐ {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM では、パラメーターを簡単にクリーンにして、クロスサイトスクリプティング攻撃に対する安全性を確保するための XSS API を提供しています。また、HTL では、このような保護機能がテンプレート言語に直接組み込まれています。API 参照シートは、[開発 - ガイドラインおよびベストプラクティス](/help/sites-developing/dev-guidelines-bestpractices.md)でダウンロードできます。

### 適切なログ機能を実装 {#implement-appropriate-logging}

Java™ コードについては、AEM では、メッセージをログに記録するための標準 API として slf4j をサポートしており、管理の一貫性を確保するために OSGi コンソールから使用可能な設定と使用する必要があります。Slf4j は、5 つの異なるログレベルを公開しています。アドビでは、メッセージをログに記録するレベルを選択する際には、次のガイドラインを使用することをお勧めします。

* ERROR：コードが中断され、処理を続行できない場合。これは多くの場合、予期しない例外の結果として発生します。これらのシナリオにスタックトレースを含めると役立ちます。
* WARN：正しく動作していない部分があるが、処理は続行できる場合。これは多くの場合、*PathNotFoundException* など、予期された例外の結果です。
* INFO：システムを監視する際に役立つ情報。これがデフォルトであり、ほとんどのお客様の環境でこの設定がそのまま使用されることに留意してください。したがって、あまり使用しないでください。
* DEBUG：処理に関するより詳細な情報。サポートを受けながら問題をデバッグする際に役立ちます。
* TRACE：メソッドの開始／終了など、最も詳細な情報。これは通常、開発者のみが使用します。

JavaScript の場合は、開発時にのみ *console.log* を使用し、リリース前にすべてのログステートメントを削除する必要があります。

### カーゴカルトプログラミングを避ける {#avoid-cargo-cult-programming}

内容を理解せずに、コードをコピーしないでください。確信がないときには必ず、明確でないモジュールや API の経験が豊富な人物に確認するのが最善です。
