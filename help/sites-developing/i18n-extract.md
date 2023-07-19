---
title: 翻訳のための文字列の抽出
seo-title: Extracting Strings for Translating
description: xgettext-maven-plugin を使用して、翻訳が必要な文字列をソースコードから抽出します。
seo-description: Use xgettext-maven-plugin to extract strings from your source code that need translating
uuid: 2c586ecb-8494-4f8f-b31a-1ed73644d611
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 034f70f1-fbd2-4f6b-b07a-5758f0461a5b
exl-id: 4acc5f7f-0bcb-4b5a-8531-52e146cffeae
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 56%

---

# 翻訳のための文字列の抽出{#extracting-strings-for-translating}

xgettext-maven-plugin を使用して、翻訳が必要な文字列をソースコードから抽出します。 Maven プラグインは、翻訳のために送信する XLIFF ファイルに文字列を抽出します。 文字列は、次の場所から抽出されます。

* Java ソースファイル
* JavaScript ソースファイル
* SVN リソース（JCR ノード）の XML 表現

## 文字列抽出の設定 {#configuring-string-extraction}

xgettext-maven-plugin ツールでプロジェクトの文字列を抽出する方法を設定します。

```xml
/filter { }
/parsers {
   /vaultxml { }
   /javascript { }
   /regexp {
      /files {
         /java { }
         /jsp { }
         /extjstemplate { }
      }
   }
}
/potentials { }
```

| セクション | 説明 |
|---|---|
| /filter | 解析するファイルを識別します。 |
| /parsers/vaultxml | コンテナファイルの解析を設定します。外部化された文字列とローカライゼーションのヒントを含む JCR ノードを識別します。 無視する JCR ノードも識別します。 |
| /parsers/javascript | 文字列を外部化する JavaScript 関数を識別します。 このセクションを変更する必要はありません。 |
| /parsers/regexp | Java、JSP、ExtJS テンプレートファイルの解析を設定します。このセクションを変更する必要はありません。 |
| /potentials | 国際化する文字列を検出するための式。 |

### 解析するファイルの識別 {#identifying-the-files-to-parse}

i18n.any ファイルの/filter セクションは、xgettext-maven-plugin ツールが解析するファイルを識別します。 解析するファイルと無視するファイルを識別するために、include 規則と exclude 規則をいくつか追加します。すべてのファイルを含めてから、解析する必要のないファイルを除外する必要があります。通常、UI に影響を与えないファイルタイプや、UI を定義するが翻訳されていないファイルを除外します。 「含む」ルールと「除外する」ルールの形式は次のとおりです。

```
{ /include "pattern" }
{ /exclude "pattern" }
```

ルールのパターン部分は、含めるまたは除外するファイルの名前の照合に使用されます。 パターンのプレフィックスは、JCR ノード（Vault での表現）とファイルシステムのどちらと一致しているかを示します。

| プレフィックス | 効果 |
|---|---|
| / | JCR パスを指定します。したがって、このプレフィックスを指定した場合は、jcr_root ディレクトリの下のファイルと照合されます。 |
| &amp;ast; | ファイルシステム上の標準ファイルを指定します。 |
| なし | プレフィックスがない場合または pattern がフォルダーまたはファイル名で始まる場合は、ファイルシステム上の標準ファイルを指定します。 |

pattern 内で使用されている場合、「/」文字はサブディレクトリを指定し、「*」文字はすべてのファイルと照合されます。次の表に、規則の例をいくつか示します。

<table>
 <tbody>
  <tr>
   <th>規則の例</th>
   <th>効果</th>
  </tr>
  <tr>
   <td><code>{ /include "*" }</code></td>
   <td>すべてのファイルを含めます。</td>
  </tr>
  <tr>
   <td><code>{ /exclude "*.pdf" }</code></td>
   <td>すべての PDF ファイルを除外します。</td>
  </tr>
  <tr>
   <td><code> { /exclude "*/pom.xml" }</code></td>
   <td>POM ファイルを除外します。</td>
  </tr>
  <tr>
   <td><code class="code">{ /exclude "/content/*" }
      { /include "/content/catalogs/geometrixx/templatepages" }
      { /include "/content/catalogs/geometrixx/templatepages/*" }</code></td>
   <td><p>/content ノードの下にあるすべてのファイルを除外します。</p> <p>/content/catalogs/geometrixx/templatepages ノードを含めます。</p> <p>/content/catalogs/geometrixx/templatepages のすべての子ノードを含めます。</p> </td>
  </tr>
 </tbody>
</table>

### 文字列の抽出  {#extracting-the-strings}

POM なし：

```shell
mvn -N com.adobe.granite.maven:xgettext-maven-plugin:1.2.2:extract  -Dxgettext.verbose=true -Dxgettext.target=out -Dxgettext.rules=i18n.any -Dxgettext.root=.
```

POM を使用：これを POM に追加：

```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.adobe.granite.maven</groupId>
            <artifactId>xgettext-maven-plugin</artifactId>
            <version>1.1</version>
            <configuration>
                <rules>i18n.any</rules>
                <root>jcr_root</root>
                <xliff>cq.xliff</xliff>
                <verbose>true</verbose>
            </configuration>
        </plugin>
    </plugins>
</build>
```

コマンド：

```shell
mvn xgettext:extract
```

### 出力ファイル {#output-files}

* `raw.xliff`：抽出された文字列
* `warn.log`：警告（存在する場合）（`CQ.I18n.getMessage()` API が正しく使用されていない場合）。これらは常に修正が必要で、その後再実行する必要があります。

* `parserwarn.log`:パーサーの警告（存在する場合）、例えば js パーサーの問題
* `potentials.xliff`：抽出されなかったものの、翻訳が必要な、人間が判読できる文字列である可能性がある「候補」（無視してかまいません。大量の誤検出が生じます）。
* `strings.xliff`：ALF にインポートするために、フラット化された xliff ファイル。
* `backrefs.txt`：これにより、指定された文字列のソースコードの場所を簡単に調べることができます。
