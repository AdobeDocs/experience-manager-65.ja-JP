---
title: コーディングのヒント
seo-title: コーディングのヒント
description: AEM のコーディングのヒント
seo-description: AEM のコーディングのヒント
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# コーディングのヒント{#coding-tips}

## 可能な限り taglib または HTL を使用する {#use-taglibs-or-htl-as-much-as-possible}

スクリプトレットを JSP に含めると、コード内の問題のデバッグが難しくなります。さらに、JSPにスクリプトレットを含めることで、ビューレイヤーとビジネスロジックを分離するのが難しくなります。これは、Single Responsibility PrincipleとMVCのデザインパターンの違反です。

### わかりやすいコードを記述する {#write-readable-code}

コードを記述するのは一度ですが、何度も読まれます。私たちが書いたコードをきれいにするのに少し時間を費やすと、私たちや他の開発者は後で読む必要があるので、配当金を払うことになる。

### 目的を明確に表す名前を選択する {#choose-intention-revealing-names}

別のプログラマーがモジュールを開かなくても内容がわかるようにすることが理想的です。同様に、メソッドを読み取らずにメソッドの動作を知ることができるはずです。 こうしたアイデアに登録すれば登録するほど、コードを読みやすくなり、コードの記述や変更が速くなります。

AEM のコードベースでは、次のような規則が使用されます。


* A single implementation of an interface is named `<Interface>Impl`, i.e. `ReaderImpl`.
* Multiple implementations of an interface are named `<Variant><Interface>`, i.e. `JcrReader` and `FileSystemReader`.
* 抽象ベースクラスには、またはという名 `Abstract<Interface>` 前が付けられま `Abstract<Variant><Interface>`す。
* Packages are named `com.adobe.product.module`.  MavenアーティファクトまたはOSGiバンドルは、それぞれ独自のパッケージを持つ必要があります。
* Java 実装は、その API の下の impl パッケージに配置します。


これらの規則を必ずお客様の実装に適用しなければならないというわけではありませんが、コードをメンテナンスしやすい状態に維持できるように、規則を定義してそれに準拠することが重要です。

名前を見れば、その目的が明らかになるようにすることが理想的です。名前が本来より明確でない場合の一般的なコードテストは、変数やメソッドが何を目的とするのかを説明するコメントが存在することです。

<table>
 <tbody>
  <tr>
   <td><p><strong>不明確</strong></p> </td>
   <td><p><strong>消去</strong></p> </td>
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

DRY（Don&#39;t repeat yourself）は、同じコードセットを繰り返してはならないということです。これは文字列リテラルなどにも当てはまります。 コードの複製は、何かが変更される必要があり、探し出され、排除されるべき場合に、欠陥の扉を開く。

### 範囲を限定しない CSS ルールを避ける {#avoid-naked-css-rules}

CSS ルールは、アプリケーションのコンテキスト内のターゲット要素に固有でなければなりません。For example, a CSS rule applied to *.content .center* would be overly broad and could potentially end up impacting lots of content across your system, requiring others to override this style in the future. *.myapp-centertextは* 、アプリケーションのコンテキストで中央揃えのテキストを指 *定する* 、より具体的なルールです。

### 廃止された API を使用しない {#eliminate-usage-of-deprecated-apis}

API が廃止された場合は常に、廃止された API を使用する代わりに、推奨される新しいアプローチを確認することをお勧めします。これにより、将来のアップグレードがスムーズになります。

### ローカライズ可能なコードを記述する {#write-localizable-code}

作成者によって指定されない文字列は、JSP/Java の I18n.get() および JavaScript の CQ.I18n.get() を使用して AEM の i18n ディクショナリへの呼び出しでラップする必要があります。****&#x200B;実装が見つからない場合、この実装は渡された文字列を返すので、主要言語で機能を実装した後に柔軟にローカリゼーションを実装できます。

### 安全のためにリソースパスをエスケープする {#escape-resource-paths-for-safety}

JCR のパスにスペースを使用することはできませんが、スペースが使用されていても、コードが中断しないようにする必要があります。Jackrabbit では、escape() および escapePath() メソッドを含む Text ユーティリティクラスを提供しています。**** For JSPs, Granite UI exposes a *granite:encodeURIPath() EL* function.

### XSS API や HTL を使用して、クロスサイトスクリプティング攻撃を防ぐ {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM では、パラメーターを簡単にクリーンにして、クロスサイトスクリプティング攻撃に対する安全性を確保するための XSS API を提供しています。また、HTLはこれらの保護をテンプレート言語に直接組み込んでいます。 An API cheat sheet is available for download at [Development - Guidelines and Best Practices](/help/sites-developing/dev-guidelines-bestpractices.md).

### 適切なログ機能を実装する {#implement-appropriate-logging}

Java コードについては、AEM では、メッセージをログに記録するための標準 API として slf4j をサポートしており、管理の一貫性を確保するために OSGi コンソールから使用可能な設定と組み合わせて使用する必要があります。Slf4jは5つの異なるログレベルを公開します。 メッセージをログに記録するレベルを選択する際には、次のガイドラインを使用することをお勧めします。

* ERROR：コードが中断され、処理を続行できない場合。これは、予期しない例外の結果としてよく発生します。 通常、これらのシナリオにスタックトレースを含めると便利です。
* WARN：正しく動作していない部分があるが、処理は続行できる場合。This will often be the result of an exception that we expected, such as a *PathNotFoundException*.
* INFO：システムを監視する際に役立つ情報。これはデフォルトの設定であり、ほとんどのお客様はこの設定を環境に適用します。 したがって、あまり使用しないでください。
* DEBUG：処理に関するより詳細な情報。サポートを受けながら問題をデバッグする際に役立ちます。
* TRACE：メソッドの開始／終了など、最も詳細な情報。これは通常、開発者のみが使用します。

JavaScript の場合は、開発時にのみ console.log を使用し、リリース前にすべてのログステートメントを削除する必要があります。**

### カーゴカルトプログラミングを避ける {#avoid-cargo-cult-programming}

内容を理解せずに、コードをコピーしないでください。疑わしい場合は、モジュールまたはAPIに関する経験が豊富なユーザーに対して、明確ではないユーザーに問い合わせることをお勧めします。
