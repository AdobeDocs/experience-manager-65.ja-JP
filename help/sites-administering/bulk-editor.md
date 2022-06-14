---
title: Bulk Editor
seo-title: The Bulk Editor
description: Bulk Editor の使用方法について説明します。
seo-description: Learn how to use the Bulk Editor.
uuid: 5f5e4190-d9b2-40a6-8cf4-4b7aebe35ad3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3649cffb-418a-4ad6-862f-56346a831b0b
docset: aem65
exl-id: c63e044c-4d2a-44d3-853b-8e7337e1ee03
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 100%

---

# Bulk Editor{#the-bulk-editor}

Bulk Editor を使用すると、以下のことができるので、視覚的なページコンテンツが不要な場合に非常に効率的な編集が可能になります。

* 複数のページからコンテンツを検索（および表示）。これは GQL（Google Query Language）を使用して行います。
* このコンテンツを Bulk Editor で直接編集。
* 変更を（元のページに）保存。
* このコンテンツをタブ区切り（.tsv）スプレッドシートファイルに書き出し。

>[!NOTE]
>
>コンテンツをリポジトリに読み込むこともできますが、デフォルトでは、**ツール**&#x200B;コンソールで使用できる Bulk Editor では無効になっています。

ここでは、**ツール**&#x200B;コンソールで Bulk Editor を操作する方法について説明します。通常、管理者は、Bulk Editor を使用して複数の項目を検索および編集します。これを行うには、GQL クエリを使用してテーブルに値を入力してから、作業対象のコンテンツ項目を選択します。作成者は通常、[製品リスト](/help/sites-authoring/default-components.md#productlist)コンポーネントを使用してアクセス可能なカスタマイズされた Bulk Editor アプリケーションの一部として Bulk Editor を使用します。

>[!CAUTION]
>
>AEM 6.4 の[クラシック UI の廃止](/help/release-notes/deprecated-removed-features.md) により、Bulk Editor も廃止もされました。したがって、今後、Bulk Editor が強化される予定はありません。

## Bulk Editor の使用例 {#example-use-case-for-the-bulk-editor}

例えば、特定のサーベイに回答したユーザーの名前と電子メールアドレスがすべて必要な場合は、Bulk Editor で提供可能な情報をスプレッドシートに書き出すことができます。

このような使用例の説明が、Geometrixx Web サイトに含まれています。

1. **サポート**&#x200B;ページに移動して、**Customer Service Satisfaction** サーベイに移動します。
1. 「**フォームの最初**」の段落を&#x200B;**編集**&#x200B;します。ダイアログで「**詳細**」タブをクリックし、「**アクションの設定**」を展開して、「**データを表示**」をクリックします。

   ![](assets/custsatsurvey.png)

1. Bulk Editor は完全にカスタマイズ可能ですが、この例では、ユーザーはコンテンツの編集はできず、情報をスプレッドシートに書き出すことのみ可能です。

   ![](assets/bulkeditor.png)

## Bulk Editor を使用する方法 {#how-to-use-the-bulk-editor}

Bulk Editor では次のことが可能です。

* [クエリパラメーターに基づいてコンテンツを検索し、指定した結果のプロパティを列に表示し、このコンテンツを編集して変更を保存します。](#searching-and-editing-content)
* [このコンテンツをタブ区切りスプレッドシートに書き出します。](#exporting-content)

* [コンテンツをタブ区切りスプレッドシートから読み込みます。](#importing-content)

### コンテンツの検索と編集 {#searching-and-editing-content}

Bulk Editor を使用して複数の項目を同時に編集するには：

1. **ツール**&#x200B;コンソールで、**Importers** フォルダーをクリックして展開します。
1. 「**Bulk Editor**」をダブルクリックして開きます。
1. 選択要件を入力します。

<table>
 <tbody>
  <tr>
   <td>フィールド</td>
   <td>プロパティ</td>
  </tr>
  <tr>
   <td>ルートパス</td>
   <td>バルクエディターで検索するルートパスを示します（<br />例：<code>/content/geometrixx/en</code>）。バルクエディターはすべての子ノードを検索します。</td>
  </tr>
  <tr>
   <td>クエリのパラメーター</td>
   <td>GQL パラメーターを使用して、リポジトリ内でバルクエディターが検索する検索文字列を入力します。例えば、「<code>type:Page</code>」と入力すると、ルートパス内のすべてのページを検索し、「<code>text:professional</code>」と入力すると、「professional」という単語が含まれているすべてのページを検索し、「<code>"jcr:title":English</code>」と入力すると、タイトルが「English」となっているすべてのページを検索します。文字列のみを検索できます。</td>
  </tr>
  <tr>
   <td>「コンテンツモード」チェックボックス</td>
   <td>このチェックボックスをオンにして、 <code>jcr:content</code> 検索結果のサブノード（存在する場合）内のプロパティを読み取ります。 ページにのみ使用します。プロパティ名の前には <code>"jcr:content/"</code></td>
  </tr>
  <tr>
   <td>プロパティ／列</td>
   <td>Bulk Editor で返すプロパティのチェックボックスをチェックします。選択したプロパティは、結果ウィンドウの列見出しとなります。デフォルトでは、結果にはノードパスが表示されます。</td>
  </tr>
  <tr>
   <td>カスタムプロパティ／列</td>
   <td>「<strong>プロパティ/列</strong>」フィールドのリストにない他のプロパティを入力します。これらのカスタムプロパティは、結果ウィンドウに表示されます。複数のプロパティを追加する場合は、コンマでプロパティを区切ります。 <i>メモ：</i>まだ存在していないカスタムプロパティを追加すると、AEM WCM には空白のセルが表示されます。空白のセルを変更して保存すると、そのプロパティがノードに追加されます。新しく作成されたプロパティは、ノードタイプの制約とプロパティの名前空間に従う必要があります。</td>
  </tr>
 </tbody>
</table>

次に例を示します。

![](assets/searchfilter.png)

1. 「**検索**」をクリックします。バルクエディターに結果が表示されます。
前述の例の場合は、指定した検索条件を満たすすべてのページが返され、要求した列を含めて表示されます。

   ![](assets/chlimage_1-39.png)

1. 任意のセル内でダブルクリックして、必要な変更を行います。

   ![](assets/srchresultedit.png)

1. 「**保存**」をクリックして変更を保存します（「**保存**」ボタンは、セルを編集後に有効になります）。

   >[!CAUTION]
   >
   >ここで行った変更は、リポジトリコンテンツ（「**パス**」で参照されているページなど）に書き込まれます。

#### その他の GQL クエリパラメーター {#additional-gql-query-parameters}

* **path:** このパスの下のノードのみを検索します。1 つの path プレフィックスで複数の用語を指定した場合は、最後の用語のみが考慮されます。
* **type:** 指定したノードタイプのノードのみを返します。これには、primary や mixin などのタイプが含まれます。複数のノードタイプをコンマで区切って指定できます。GQL は、指定したいずれかのタイプに該当するノードを返します。
* **order：**&#x200B;指定したプロパティを基準として結果を並べます。複数のプロパティ名をコンマで区切って指定できます。結果を降順で並べるには、プロパティ名にマイナス記号のプレフィックスを付けます（例：order:-name）。プラス記号を使用すると、結果は昇順に戻ります。これはデフォルトでもあります。
* **limit:** 間隔を使用して結果の数を制限します（例：limit:10..20）。間隔は 0 を基準とし、start はその値を含み、end はその値を含みません。開いた間隔を指定することもできます（例：:limit:10..または limit:..20）。ドットを省略し、値を 1 つだけ指定した場合、GQL は最大でこの数の結果を返します。例：limit:10（最初の 10 件の結果を返します）

### コンテンツの書き出し {#exporting-content}

コンテンツを書き出して、Excel のスプレッドシートで変更を加えることが必要になる場合があります。例えば、メーリングリストを書き出して、リストされているすべての電話番号の市外局番を Excel で直接変更したり、行を追加したりする場合などです。

コンテンツを書き出すには：

1. [コンテンツの検索と編集](#searching-and-editing-content)の説明に従ってコンテンツを検索します。
1. 「**書き出し**」をクリックして、変更をタブ区切りの Excel スプレッドシートに書き出します。AEM WCM でファイルのダウンロード場所が確認されます。

   >[!NOTE]
   >
   >デフォルトでは、変更は [Windows-1252](https://en.wikipedia.org/wiki/Windows-1252)（CP-1252 とも呼ばれる）でエンコードされます。「UTF-8」をチェックすると、変更を UTF-8 で書き出すことができます。

   ![](assets/srchrsesultexport.png)

1. 場所を選択して、ファイルのダウンロードを確認します。
1. ファイルをダウンロードしたら、Microsoft Excel などのスプレッドシートプログラムから開くことができます。スプレッドシートプログラムにファイルが読み込まれ、スプレッドシート形式に変換されます。

   ![](assets/exportinexcel.png)

### コンテンツの読み込み {#importing-content}

デフォルトでは、バルクエディターを開くと、読み込み機能は非表示になります。パラメーター `hib=false` を URL に追加すれば、バルクエディターページに「**読み込み**」ボタンが表示されます。コンテンツは、任意のタブ区切り（`.tsv`）ファイルから読み込むことがでめます。読み込みが正常に機能するには、列見出し（セルの最初の行）が、読み込み先のテーブルの列見出しと一致している必要があります。

>[!NOTE]
>
>コンテンツを再読み込みする場合は、該当するノードの以前のコンテンツをすべて削除します。重要な情報を上書きしないように注意してください。

コンテンツを読み込むには：

1. Bulk Editor を開きます。
1. 例えば、次のような手順を実行して、`?hib=false` を URL に追加します。
   `https://localhost:4502/etc/importers/bulkeditor.html?hib=false`
1. 「**読み込み**」をクリックします。
1. `.tsv` ファイルを選択します。データがリポジトリーに読み込まれます。
