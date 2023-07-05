---
title: Adobe Analytics のリンクトラッキングの設定
seo-title: Configuring Link Tracking for Adobe Analytics
description: SiteCatalyst用のリンクトラッキングの設定について説明します。
seo-description: Learn about configuring link tracking for SiteCatalyst.
uuid: b6d5bd1c-f91a-4d38-9e9e-dc2bcb271dae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fe6ba6af-f500-4c0d-b984-fb617d4bf48a
exl-id: 9fa3e531-11b3-4b8d-a87c-a08faf06f5b7
source-git-commit: 5e94a0cdb363e95ce398ea4ed0bce4a6aba9e7ce
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 61%

---


# Adobe Analytics のリンクトラッキングの設定{#configuring-link-tracking-for-adobe-analytics}

ユーザーが Web サイトのページ上のリンクをクリックすると、Adobe Analyticsで関連情報を取り込むことができます。 例えば、ユーザーがサイトとどのようにやり取りするかを学習し、ファイルのダウンロード数を追跡し、出口リンクを追跡する場合に、リンクトラッキングを使用します。

## Adobe Analytics Framework のリンクトラッキングの設定 {#configuring-link-tracking-for-an-adobe-analytics-framework}

1. **ナビゲーション**&#x200B;を使用し、**導入**、**クラウドサービス**&#x200B;を介して **Adobe Analytics** セクションに移動します。

1. **設定を表示**&#x200B;を使用して、必要な Adobe Analytics フレームワークを開きます。
1. を展開します。 **リンクトラッキング設定** を参照し、必要に応じて設定します（このページでは、詳細を説明します）。

   ![分析フレームワーク](assets/aa-08.png)

## ファイルのダウンロード数の追跡 {#tracking-file-downloads}

関連ページからダウンロードしたファイルが自動的に Adobe Analytics でダウンロードとして追跡できるように、Adobe Analytics フレームワークを設定します。ダウンロードの追跡を有効にすると、指定したファイルタイプのみが追跡されます。

デフォルトでは、次のファイルタイプのダウンロードが追跡されます。

* exe
* zip
* wav
* mp3
* mov
* mpg
* avi
* wmv
* doc
* pdf
* xls

例えば、PDFファイルのダウンロードトラッキングを有効にした場合、ユーザーがPDFファイルへのリンクをクリックするたびに、PDFのダウンロードが追跡されます。

フレームワークのダウンロードトラッキングプロパティは、ページ用に生成された `analytics.sitecatalyst.js` ファイルにコードとして実装されています。次のコード例に、デフォルトのダウンロードトラッキング設定を示します。

```
s.trackDownloadLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
```

Adobe Analytics フレームワーク用のダウンロードトラッキングを有効にするには、以下を実行します。

1. [Adobe Analytics フレームワークを開き、「リンクトラッキング設定」セクションを展開します。](#configuring-link-tracking-for-an-adobe-analytics-framework)
1. 有効にする **ダウンロードを追跡**.
1. 内 **ダウンロードファイルタイプ** ボックスに、追跡するファイルの種類のファイル名拡張子を入力します。

## 外部リンクの追跡 {#tracking-external-links}

ページ上での外部リンク（出口リンク）のクリックを追跡できます。

Adobe Analytics フレームワーク用の外部リンクを追跡するには、以下を実行します。

1. [Adobe Analytics フレームワークを開き、「**リンクトラッキング設定**」セクションを展開します。](#configuring-link-tracking-for-an-adobe-analytics-framework)
1. 要件に従って、次のプロパティを設定します。

外部リンクがクリックされた際の追跡用プロパティ：

* **外部を追跡**
外部リンクトラッキングを有効にします。

* **外部フィルター** 
（任意）リンクターゲットの外部 URL に一致するフィルターを定義します。リンクターゲットがフィルターに一致する場合、リンクはトラッキングされます。 外部フィルターは、ページ上の一部の外部リンクのみを追跡する場合に役立ちます。

  追跡する外部リンクを指定するには、リンクターゲットの URL のすべてまたは一部を入力します。複数のフィルターを使用する場合はコンマで区切ります。 文字列リテラルを一重引用符で囲みます。 値がない（デフォルト値の `''`、2 つの一重引用符）場合、すべての外部リンクが追跡されます。

* **内部フィルター**
内部リンクの URL に一致するフィルターを定義します。リンクがこのフィルターに一致する URL をターゲットにする場合、そのリンクはトラッキングされません。 デフォルト値は、現在のウィンドウアドレスの URL のホスト名を返す JavaScript コマンドです。

  追跡されない内部リンクを指定するには、リンクターゲットの内部 URL のすべてまたは一部を入力します。複数のフィルターを使用する場合はコンマで区切ります。 文字列リテラルを一重引用符で囲みます。

  デフォルト値は `'javascript:,'+window.location.hostname` です。

* **クエリ文字列を維持**
内部および外部フィルターとの一致を評価する際に、URL パラメーターを含めます。

  外部および内部フィルターに対するリンクターゲット URL を評価する際に URL パラメーターを含めるには、有効にします。

外部リンクトラッキングプロパティは、ページ用に生成された `analytics.sitecatalyst.js` ファイルにコードとして実装されています。次の設定で、外部リンクトラッキングを有効にしたフレームワークに関連付けられたページ用に生成されるコード例を示します。

* 外部フィルターは `'google.com'`
* 内部フィルターは、`'javascript:,'+window.location.hostname` のデフォルト値
* フィルターに対するリンクターゲットを評価する際に、クエリ文字列は含まれません

```
s.trackExternalLinks= false;
s.linkExternalFilters= 'google.com';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.linkLeaveQueryString= false;
```

## リンククリック数を含む変数データの送信 {#sending-variable-data-with-link-clicks}

ユーザーがリンクをクリックする際にイベントおよび変数データを Adobe Analytics に送信するように、AEM を設定できます。**リンクトラッキング設定**&#x200B;プロパティを使用すると、リンククリックが発生した場合に追跡する Adobe Analytics イベントおよび変数を指定できます。

フレームワークマッピングは、イベントおよび変数の値をチェックします。リンクがクリックされた際に追跡されたデータを保存するコンテンツコンポーネントの変数に、Adobe Analytics 変数をマッピングできます。

リンククリック数を含む変数データを送信するには、以下を実行します。

1. [Adobe Analytics フレームワークを開き、「リンクトラッキング設定」セクションを展開します。](#configuring-link-tracking-for-an-adobe-analytics-framework)
1. 要件に従って、次のプロパティを設定します。

リンククリック数を含む変数データを送信するためのプロパティ：

* **リンク追跡イベント**
リンククリック数のカウントに使用したい Adobe Analytics イベント変数を入力します。

  複数の変数名をコンマで区切ります。

  デフォルト値の `None` では、イベントは追跡されません。

* **リンク追跡 var**
リンクがクリックされた際に Adobe Analytics に送信したい Adobe Analytics 変数を入力します。複数の変数名をコンマで区切ります。

  デフォルト値 `None` の場合、変数データが送信されません。

送信するイベントおよび変数を指定する場合、設定はページ用に生成された `analytics.sitecatalyst.js` ファイルにコードとして実装されています。フレームワークが `event10` イベントおよび `prop4` プロパティを追跡する場合にページ用に生成されるコード例を示します。

```
s.linkTrackEvents= 'event10';
s.linkTrackVars= 'prop4';
```

## リンクトラッキング設定の例 {#example-link-tracking-configuration}

次の手順を実行して、Adobe Analytics 統合のリンクトラッキング動作を調査します。手順は次の結果を示します。 [Adobe Marketing Cloud Debugger](https://experienceleague.adobe.com/docs/debugger/using/experience-cloud-debugger.html?lang=ja).

### 一般設定 {#general-configuration}

この例は、トラッキングとデバッガーのコンテキストにおいて、マッピングがどのように機能するかを示しています。

1. Web ページに関連付けられたフレームワークを開きます。
1. 次をドラッグ： **ページ** コンポーネントをフレームワークのマッピング領域に追加します。 **ページ**&#x200B;コンポーネントは、サイドキックの&#x200B;**一般**&#x200B;コンポーネントグループに属しています。

   >[!NOTE]
   >
   >実際のシナリオで使用する必要があるコンポーネントは、から継承されたコンポーネントに依存します（もしそうである場合）。
   >
   >そうでない場合は、（ページコンポーネントで analytics サブノードを定義することで）独自のコンポーネントをそこで公開する必要があります。

   左側のパネルから Analytics(SiteCatalyst) 変数をドラッグして、次の表に従ってマッピングを設定します。

<table>
 <tbody>
  <tr>
   <th>CQ 変数<br /> </th>
   <th>変数ブラウザーのエントリ<br /> </th>
   <th>Adobe Analytics 変数</th>
  </tr>
  <tr>
   <td>pagedata.title</td>
   <td>カスタムeVar1 (eVar1)</td>
   <td>eVar1</td>
  </tr>
  <tr>
   <td>eventdata.events.pageView</td>
   <td>カスタム 1(event1)</td>
   <td>event1</td>
  </tr>
 </tbody>
</table>

1. 検索コンポーネントをフレームワークのマッピング領域にドラッグします。 検索コンポーネントは、Sidekickの「一般」コンポーネントグループに属しています。 左側のパネルから Analytics(SiteCatalyst) 変数をドラッグして、次の表に従ってマッピングを設定します。

<table>
 <tbody>
  <tr>
   <th>CQ 変数<br /> </th>
   <th>変数ブラウザーのエントリ</th>
   <th>Adobe Analytics 変数</th>
  </tr>
  <tr>
   <td>eventdata.keyword</td>
   <td>カスタムeVar2 (eVar2)</td>
   <td>eVar2</td>
  </tr>
  <tr>
   <td>eventdata.results</td>
   <td>カスタムeVar3 (eVar3)</td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.events.search</td>
   <td>カスタム 2(event2)</td>
   <td>event2</td>
  </tr>
 </tbody>
</table>

### 外部リンクトラッキングの設定 {#configure-external-link-tracking}

1. フレームワークで、 **リンクトラッキング設定** 領域
1. **ダウンロードを追跡**&#x200B;の選択を解除します。

1. 選択 **外部を追跡**.
1. 選択を解除 **クエリー文字列をそのまま残す**.
1. **外部フィルター**&#x200B;リストに次の値を使用して、外部 URL として特定します。

   `‘yahoo.com’`

1. **リンク追跡イベント**&#x200B;フィールドに次の値を追加します。

   ```
       event1,event2
   ```

1. **リンク追跡 var** フィールドに次の値を追加します。

   ```
       eVar1,eVar2
   ```

1. フレームワークに関連付けられたページに、**テキスト**&#x200B;コンポーネントを追加します。**テキスト**&#x200B;コンポーネント内に、次のアドレスを示すハイパーリンクを追加します。

   `https://search.yahoo.com/?p=this`

1. **プレビューモード**&#x200B;に切り替えて、リンクをクリックします。

Adobe Marketing Cloud デバッガーで表示すると、呼び出しの実行は次のようになります。

![Adobe Marketing Cloud Debugger](assets/aa-leavequerysearch-blank.png)

>[!NOTE]
>
>URL には、クエリ文字列（`?p=this`）は含まれません。

### URL パラメーターを含める {#include-the-url-parameter}

1. フレームワークで、 **リンクトラッキング設定** 領域
1. 有効にする **クエリー文字列をそのまま残す**.
1. ページプレビューを再読み込みし、リンクをクリックします。

Adobe Marketing Cloud デバッガーに表示される呼び出しの詳細は、次の例のようになります。

![Adobe Marketing Cloud Debugger が再び](assets/aa-leavequerysearch-active.png)

>[!NOTE]
>
>今回は、URL にクエリ文字列（`?p=this`）が含まれます。

## アドホックリンクトラッキング {#ad-hoc-link-tracking}

アドホックリンクトラッキングを使用すると、コンテンツ作成者はコンポーネントのリンクトラッキングを設定できます。 コンポーネントの設定により、 **リンクトラッキング設定** フレームワークの、フレームワークに関連付けられたページの **テキスト** コンポーネントは、URL のリンクトラッキング用に設定できます。

アドホックリンクトラッキングを使用すると、ダウンロードリンク、外部リンクを、イベントおよび変数データと共に追跡できます。

アドホックリンクトラッキングを有効にするには、以下を実行する必要があります。

* [を含むページを関連付ける **テキスト** フレームワークを持つコンポーネント](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).
* [Adobe Analytics Framework の設定によるアドホックリンクトラッキングの有効化](#enabling-ad-hoc-link-tracking).
* [テキストコンポーネント用にリンクトラッキングを設定します](#configuring-link-tracking-for-a-text-component)。

### アドホックリンクトラッキングの有効化 {#enabling-ad-hoc-link-tracking}

Adobe Analytics フレームワークを設定して、アドホックなリンクトラッキングを有効にします。

1. Adobe Analytics フレームワークを開き、「**リンクトラッキング設定**」セクションを展開します。

1. 有効にする **アドホックリンクトラッキング**.

   >[!NOTE]
   >
   >すべてのユーザータイプがこのチェックボックスにアクセスできるわけではありません。 アクセス権が必要な場合は、サイト管理者に問い合わせてください。

>[!NOTE]
>
>XSS Antisamy 設定がパス **/libs/sling/xss.config.xml** の下の Sling にあるので、アドホックリンクが機能するには次のルールを追加する必要があります。

#### タグルール拡張機能のアンカー {#anchor-tag-rule-extension}

```xml
<attribute name="onclick">
    <literal-list>
        <literal value="CQ_Analytics.Sitecatalyst.customTrack(this)"/>
    </literal-list>
</attribute>
<attribute name="adhocenable">
    <literal-list>
        <literal value="true"/>
        <literal value="false"/>
    </literal-list>
</attribute>
<attribute name="adhocevents">
    <regexp-list>
        <regexp name="anything"/>
    </regexp-list>
</attribute>
<attribute name="adhocevars">
    <regexp-list>
        <regexp name="anything"/>
    </regexp-list>
</attribute>
```

### テキストコンポーネントのリンクトラッキングの設定 {#configuring-link-tracking-for-a-text-component}

**テキスト**&#x200B;コンポーネント自体のアドホックリンクトラッキングを設定する前に、以下の設定が既に適用されている必要があります。

* この [Adobe Analytics Framework がアドホックリンクトラッキングを有効にするように設定されています](#enabling-ad-hoc-link-tracking).
* この [ページの **テキスト** コンポーネントがフレームワークに関連付けられています](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).

次の手順を実行して、**テキスト**&#x200B;コンポーネントのリンクトラッキングを設定します。

1. ページを編集モードで開き、**テキスト**&#x200B;コンポーネントを編集します。

1. ハイパーテキストとして使用したいテキストを選択して、「ハイパーリンク」ボタンをクリックします。

   ![リンクアイコン](do-not-localize/chlimage_1.png)

1. 「リンク先」ボックスにターゲット URL を追加して、リンクトラッキング領域を展開します。

   >[!NOTE]
   >
   >カスタムリンクトラッキングは、リンク/リンク解除アクション（Analytics アイコン）の横に、別のアクションとして表示されます。
   >
   >これは、RTE で有効なリンクを選択した場合にのみ有効になります。

   ![リンクトラッキングの有効化](assets/aa-17.png)

1. 「**カスタムリンクトラッキング**」を有効にして、Adobe Analytics フレームワークのリンクトラッキング設定を上書きし、現在のリンクのリンクトラッキングを有効にします。

1. （任意）リンククリックのあるイベントを追跡するには、「**Adobe Analytics 変数を含める**」フィールドに Adobe Analytics イベント名を追加します。複数のイベント名をコンマで区切ります。例：

   `event1, event22`。

1. （任意）リンククリックのある変数データを追跡するには、「**Adobe Analytics 変数を含める**」フィールドに Adobe Analytics 変数を追加します。次のいずれかの形式を使用します。

   * *`<Variable-name>`*：*`<Dynamic Value>`*
   * *`<Variable-name>`*：*`‘CONSTANT'`*

   次に、各形式の例を示します。

   * `eVar10:pagedata.title`
   * `prop1: ‘Aubergine'`

   複数の値をコンマで区切ります。

1. 「**OK**」を選択します。
