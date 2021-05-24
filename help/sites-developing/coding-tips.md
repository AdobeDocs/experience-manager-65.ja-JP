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
exl-id: 85ca35e5-6e2b-447a-9711-b12601beacdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 52%

---

# コーディングのヒント{#coding-tips}

## 可能な限り taglib または HTL を使用する {#use-taglibs-or-htl-as-much-as-possible}

スクリプトレットを JSP に含めると、コード内の問題のデバッグが難しくなります。また、JSPにスクリプトレットを含めると、ビジネスロジックをビューレイヤーから分離するのが難しくなります。ビューレイヤーは、単一責任の原則とMVCの設計パターンに違反しています。

### わかりやすいコードを記述する {#write-readable-code}

コードを記述するのは一度ですが、何度も読まれます。我々が書いたコードをきれいにするのに少し時間を費やすと、我々や他の開発者は後で読む必要があるので、道路の配当を払う。

### 目的を明確に表す名前を選択する {#choose-intention-revealing-names}

別のプログラマーがモジュールを開かなくても内容がわかるようにすることが理想的です。同様に、メソッドを読まずに何を行うかを知ることができるはずです。 こうしたアイデアを購読すれば購読するほど、コードを読みやすくなり、コードを書いて変更するのが速くなります。

AEM のコードベースでは、次のような規則が使用されます。


* インターフェイスの1つの実装は、`<Interface>Impl`という名前です。`ReaderImpl`.
* 1つのインターフェイスの複数の実装には、`<Variant><Interface>`という名前が付けられます。`JcrReader`と`FileSystemReader`。
* 抽象基本クラスの名前は`Abstract<Interface>`または`Abstract<Variant><Interface>`です。
* パッケージ名は`com.adobe.product.module`です。  各MavenアーティファクトまたはOSGiバンドルには、独自のパッケージが必要です。
* Java 実装は、その API の下の impl パッケージに配置します。


これらの規則を必ずお客様の実装に適用しなければならないというわけではありませんが、コードをメンテナンスしやすい状態に維持できるように、規則を定義してそれに準拠することが重要です。

名前を見れば、その目的が明らかになるようにすることが理想的です。名前が本来のように明確でない場合にテストされる一般的なコードは、変数やメソッドの目的を説明するコメントの存在です。

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

### 繰り返しを避ける   {#don-t-repeat-yourself}

DRY（Don&#39;t repeat yourself）は、同じコードセットを繰り返してはならないということです。これは、文字列リテラルなどにも当てはまります。 コードの複製は、何かが変更される必要があり、探し出され、削除される必要がある場合に、欠陥の扉を開きます。

### 範囲を限定しない CSS ルールを避ける {#avoid-naked-css-rules}

CSS ルールは、アプリケーションのコンテキスト内のターゲット要素に固有でなければなりません。例えば、*.content .center*&#x200B;に適用されるCSSルールは過度に広く、システム全体の多数のコンテンツに影響を与え、将来、他のユーザーがこのスタイルを上書きする必要が生じる可能性があります。 *.myapp-centertextは、ア* プリケーションのコンテキスト内で中央のテキストを指定す ** るため、より具体的な規則になります。

### 廃止された API を使用しない {#eliminate-usage-of-deprecated-apis}

API が廃止された場合は常に、廃止された API を使用する代わりに、推奨される新しいアプローチを確認することをお勧めします。これにより、今後のアップグレードをよりスムーズに行うことができます。

### ローカライズ可能なコードを記述する {#write-localizable-code}

作成者によって指定されない文字列は、JSP/Java の I18n.get() および JavaScript の CQ.I18n.get() を使用して AEM の i18n ディクショナリへの呼び出しでラップする必要があります。****&#x200B;この実装は、実装が見つからない場合に渡された文字列を返すので、プライマリ言語で機能を実装した後に、柔軟にローカライゼーションを実装できます。

### 安全のためにリソースパスをエスケープする {#escape-resource-paths-for-safety}

JCR のパスにスペースを使用することはできませんが、スペースが使用されていても、コードが中断しないようにする必要があります。Jackrabbit では、escape() および escapePath() メソッドを含む Text ユーティリティクラスを提供しています。**** JSPの場合、Granite UIは&#x200B;*granite:encodeURIPath() EL*&#x200B;関数を公開します。

### XSS API や HTL を使用して、クロスサイトスクリプティング攻撃を防ぐ {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM では、パラメーターを簡単にクリーンにして、クロスサイトスクリプティング攻撃に対する安全性を確保するための XSS API を提供しています。さらに、HTLではこれらの保護機能がテンプレート言語に直接組み込まれています。 APIチートシートは、[Development - Guidelines and Best Practices](/help/sites-developing/dev-guidelines-bestpractices.md)からダウンロードできます。

### 適切なログ機能を実装する {#implement-appropriate-logging}

Java コードについては、AEM では、メッセージをログに記録するための標準 API として slf4j をサポートしており、管理の一貫性を確保するために OSGi コンソールから使用可能な設定と組み合わせて使用する必要があります。Slf4jは、5つの異なるログレベルを公開します。 メッセージをログに記録するレベルを選択する際には、次のガイドラインを使用することをお勧めします。

* ERROR：コードが中断され、処理を続行できない場合。これは、多くの場合、予期しない例外の結果として発生します。 通常、このシナリオにスタックトレースを含めると便利です。
* WARN：正しく動作していない部分があるが、処理は続行できる場合。これは、多くの場合、*PathNotFoundException*&#x200B;など、予期された例外の結果です。
* INFO：システムを監視する際に役立つ情報。これがデフォルトであり、ほとんどのお客様が環境にこの設定を残すことに注意してください。 したがって、あまり使用しないでください。
* DEBUG：処理に関するより詳細な情報。サポートを受けながら問題をデバッグする際に役立ちます。
* TRACE：メソッドの開始／終了など、最も詳細な情報。これは通常、開発者のみが使用します。

JavaScript の場合は、開発時にのみ console.log を使用し、リリース前にすべてのログステートメントを削除する必要があります。**

### カーゴカルトプログラミングを避ける  {#avoid-cargo-cult-programming}

内容を理解せずに、コードをコピーしないでください。不確かな場合は、不明なモジュールやAPIの経験がある人に尋ねるのが常です。
