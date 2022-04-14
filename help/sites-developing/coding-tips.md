---
title: コーディングのヒント
seo-title: Coding Tips
description: AEM のコーディングのヒント
seo-description: Tips for coding for AEM
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
exl-id: 85ca35e5-6e2b-447a-9711-b12601beacdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '867'
ht-degree: 100%

---

# コーディングのヒント{#coding-tips}

## 可能な限り taglib または HTL を使用する {#use-taglibs-or-htl-as-much-as-possible}

スクリプトレットを JSP に含めると、コード内の問題のデバッグが難しくなります。さらに、スクリプトレットを JSP に含めると、ビジネスロジックを表示レイヤーから切り離すことが難しくなり、単一責任の原則および MVC 設計パターンに違反することになります。

### わかりやすいコードを記述 {#write-readable-code}

コードを記述するのは一度ですが、何度も読まれます。あらかじめ時間をかけて、記述したコードを明確にしておくと、その後、自分自身や他の開発者がコードを読む必要がある場合に役立ちます。

### 目的を明確に表す名前を選択 {#choose-intention-revealing-names}

別のプログラマーがモジュールを開かなくても内容がわかるようにすることが理想的です。同様に、メソッドを読まなくても目的がわかるようにする必要があります。こうした考え方に忠実に従うほど、コードがわかりやすくなるとともに、コードの記述や変更をより短時間で行えるようになります。

AEM のコードベースでは、次のような規則が使用されます。


* インターフェイスの単一の実装には、`<Interface>Impl` という名前を付けます（`ReaderImpl` など）。
* インターフェイスの複数の実装には `<Variant><Interface>` という名前を付けます（`JcrReader` や `FileSystemReader` など）。
* 抽象ベースクラスには `Abstract<Interface>` または `Abstract<Variant><Interface>` という名前を付けます。
* パッケージには `com.adobe.product.module` という名前を付けます。それぞれの Maven アーティファクトまたは OSGi バンドルには独自のパッケージが必要です。
* Java 実装は、その API の下の impl パッケージに配置します。


これらの規則を必ずお客様の実装に適用しなければならないというわけではありませんが、コードをメンテナンスしやすい状態に維持できるように、規則を定義してそれに準拠することが重要です。

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

### 繰り返しを避ける  {#don-t-repeat-yourself}

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

AEM では、パラメーターを簡単にクリーンにして、クロスサイトスクリプティング攻撃に対する安全性を確保するための XSS API を提供しています。さらに、HTL では、このような保護機能がテンプレート言語に直接組み込まれています。API 参照シートは、[開発 - ガイドラインおよびベストプラクティス](/help/sites-developing/dev-guidelines-bestpractices.md)でダウンロードできます。

### 適切なログ機能を実装 {#implement-appropriate-logging}

Java コードについては、AEM では、メッセージをログに記録するための標準 API として slf4j をサポートしており、管理の一貫性を確保するために OSGi コンソールから使用可能な設定と組み合わせて使用する必要があります。Slf4j は、5 つの異なるログレベルを公開しています。メッセージをログに記録するレベルを選択する際には、次のガイドラインを使用することをお勧めします。

* ERROR：コードが中断され、処理を続行できない場合。これは多くの場合、予期しない例外の結果として発生します。通常は、これらのシナリオにスタックトレースを含めると役立ちます。
* WARN：正しく動作していない部分があるが、処理は続行できる場合。これは多くの場合、*PathNotFoundException* など、予期された例外の結果です。
* INFO：システムを監視する際に役立つ情報。これがデフォルトであり、ほとんどのお客様の環境でこの設定がそのまま使用されることに留意してください。したがって、あまり使用しないでください。
* DEBUG：処理に関するより詳細な情報。サポートを受けながら問題をデバッグする際に役立ちます。
* TRACE：メソッドの開始／終了など、最も詳細な情報。これは通常、開発者のみが使用します。

JavaScript の場合は、開発時にのみ console.log を使用し、リリース前にすべてのログステートメントを削除する必要があります&#x200B;*。*

### カーゴカルトプログラミングを避ける {#avoid-cargo-cult-programming}

内容を理解せずに、コードをコピーしないでください。確信がないときには必ず、明確でないモジュールや API の経験が豊富な人物に確認するのが最善です。
