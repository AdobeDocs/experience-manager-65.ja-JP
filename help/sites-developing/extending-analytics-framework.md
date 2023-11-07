---
title: Adobe Analytics Framework のカスタマイズ
description: Adobe Experience Manager用のAdobe Analyticsフレームワークをカスタマイズする方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 11c0aac6-a7f6-4d6b-a080-b04643045a64
exl-id: ab0d4f2e-f761-4510-ba51-4a2dcea49601
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 42%

---

# Adobe Analytics Framework のカスタマイズ{#customizing-the-adobe-analytics-framework}

Adobe Analytics フレームワークは、Adobe Analytics で追跡される情報を決定します。デフォルトのフレームワークをカスタマイズするには、JavaScript を使用して、カスタムトラッキングの追加、Adobe Analyticsプラグインの統合、およびトラッキングに使用するフレームワーク内での一般設定の変更をおこないます。

## フレームワーク用に生成される JavaScript について {#about-the-generated-javascript-for-frameworks}

ページがAdobe Analyticsフレームワークに関連付けられ、そのページに以下が含まれている場合 [Analytics モジュールへの参照](/help/sites-administering/adobeanalytics.md)を指定すると、analytics.sitecatalyst.js ファイルがページ用に自動的に生成されます。

ページ内の JavaScript によって、 `s_gi`オブジェクト (s_code.js Adobe Analyticsライブラリで定義されている ) を削除し、そのプロパティに値を割り当てます。 オブジェクトインスタンスの名前は `s` です。この節に示すコード例では、この `s` 変数への参照を複数作成します。

次のコード例は、analytics.sitecatalyst.js ファイルのコードに似ています。

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";

/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

カスタム JavaScript コードを使用してフレームワークをカスタマイズする場合、このファイルの内容を変更します。

## Adobe Analytics プロパティの設定 {#configuring-adobe-analytics-properties}

Adobe Analytics内には、フレームワークで設定できる定義済みの変数がいくつかあります。 変数 **charset**、**cookieLifetime**、**currencyCode** および **trackInlineStats** は、**Analytics 一般設定**&#x200B;リストにデフォルトで含まれています。

![aa-22](assets/aa-22.png)

このリストに、変数名と値を追加できます。これらの事前定義済みの変数と、追加したすべての変数を使用して、analytics.sitecatalyst.js ファイル内の `s` オブジェクトのプロパティを設定します。次の例は、 `prop10` 価値の財産 `CONSTANT` は JavaScript コードで表されます。

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.prop10= 'CONSTANT';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";
```

変数をリストに追加するには、以下の手順を実行します。

1. Adobe Analytics フレームワークページで、**Analytics の一般設定**&#x200B;領域を展開します。
1. 変数のリストの下の「項目を追加」をクリックして、新しい変数をリストに追加します。
1. 左側のセルに、変数の名前を入力します（例： ）。 `prop10`.

1. 右側の列に、変数の値を入力します（例： ）。 `CONSTANT`.

1. 変数を削除するには、変数の横にある (-) ボタンをクリックします。

>[!NOTE]
>
>変数と値を入力する際に、正しい形式とスペルが設定されていることを確認するか、 **呼び出しは送信されません** が正しい値と変数のペアになっていることを確認します。 変数と値のスペルが間違っていると、呼び出しの発生を防ぐこともできます。
>
>Adobe Analyticsの担当者に問い合わせて、これらの変数が正しく設定されていることを確認してください。

>[!CAUTION]
>
>このリストに含まれる変数の一部は次のとおりです。 **必須** ( 例えば、Adobe Analyticsの呼び出しが **currencyCode**, **charSet**)
>
>そのため、フレームワーク自体から変数を削除しても、Adobe Analytics の呼び出しがおこなわれると、デフォルト値を持つ変数が付加されます。

### Adobe Analytics Framework へのカスタム JavaScript の追加 {#adding-custom-javascript-to-an-adobe-analytics-framework}

JavaScript からの自由のボックス ( **一般的な Analytics 設定** 「 」領域では、カスタムコードをAdobe Analyticsフレームワークに追加できます。

![aa-21](assets/aa-21.png)

追加するコードは、analytics.sitecatalyst.js ファイルに付加されます。したがって、 `s` 変数に含まれます。これは、 `s_gi` で定義される JavaScript オブジェクト `s_code.js`. 例えば、次のコードの追加は、前節の例で値 `CONSTANT` の `prop10` という変数を追加することと同等です。

`s.prop10= 'CONSTANT';`

[analytics.sitecatalyst.js](/help/sites-developing/extending-analytics-components.md) ファイル（Adobe Analytics の `s-code.js` ファイルの内容を含む）のコードには、次のコードが含まれます。

`if (s.usePlugins) s.doPlugins(s)`

以下の手順では、「 JavaScript 」ボックスを使用してAdobe Analyticsトラッキングをカスタマイズする方法を示します。 JavaScript でAdobe Analyticsプラグインを使用する必要がある場合、 [統合する](/help/sites-administering/adobeanalytics.md) をAEMに追加します。

1. 次の JavaScript コードをボックスに追加し、 `s.doPlugins` が実行されました：

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >このコードは、基本のドラッグ&amp;ドロップインターフェイスや、Adobe Analytics View のインライン JavaScript では実行できない方法でカスタマイズされたAdobe Analytics呼び出しで変数を送信する場合に必要です。
   >
   >カスタム変数が s_doPlugins 関数の外にある場合は、Adobe Analytics の呼び出しで *undefined* として送信

1. に JavaScript コードを追加します。 **s_doPlugins** 関数に置き換えます。

次の例では、一般的な区切り文字「|」を使用して、ページ上でキャプチャされたデータを階層順に連結しています。

Adobe Analyticsフレームワークには、次の設定があります。

* `prop2` Adobe Analytics 変数は `pagedata.sitesection` サイトプロパティにマッピングされます。

* `prop3` Adobe Analytics 変数は `pagedata.subsection` サイトプロパティにマッピングされます。

* 次のコードが「JavaScript から解放」ボックスに追加されます。

  ```
  s.usePlugins=true;
   function s_doPlugins(s) {
   s.prop1 = s.prop2+'|'+s.prop3;
   }
   s.doPlugins=s_doPlugins;
  ```

* このフレームワークを使用する web ページが訪問される（または、編集モードでページが再読み込みまたはプレビューされる）と、Adobe Analytics への呼び出しが実行されます。

例えば、次の値が Adobe Analytics で生成されます。

![aa-20](assets/aa-20.png)

### すべての Adobe Analytics フレームワーク用のグローバルカスタムコードの追加 {#adding-global-custom-code-for-all-adobe-analytics-frameworks}

すべてのAdobe Analyticsフレームワークに統合されるカスタム JavaScript コードを提供する。 ページのAdobe Analyticsフレームワークにカスタムが含まれていない場合 [自由形式 JavaScript](/help/sites-administering/adobeanalytics.md)を指定した場合、 /libs/cq/analytics/components/sitecatalyst/config.js.jsp スクリプトで生成される JavaScript が [analytics.sitecatalyst.js](/help/sites-administering/adobeanalytics.md) ファイル。 デフォルトでは、このスクリプトはコメントアウトされているので効果はありません。また、このコードは `s.usePlugins` を `false` に設定します。

```
/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

analytics.sitecatalyst.js ファイル（Adobe Analytics の s_code.js ファイルの内容を含む）のコードには、次のコードが含まれます。

if (s.usePlugins) s.doPlugins(s)

したがって、JavaScript を `s.usePlugins` から `true` そのため、 `s_doPlugins` 関数が実行されます。 コードをカスタマイズするには、独自の JavaScript を使用するファイルでconfig.js.jsp ファイルをオーバーレイします。 JavaScript でAdobe Analyticsプラグインを使用する必要がある場合、 [統合する](/help/sites-administering/adobeanalytics.md) をAEMに追加します。

>[!NOTE]
>
>/libs/cq/analytics/components/sitecatalyst/config.js.jsp ファイルは編集しないでください。 特定のAEMアップグレードまたはメンテナンスタスクを実行すると、元のファイルを再インストールして、変更を削除できます。

1. CRXDE Liteで、 /apps/cq/analytics/components フォルダー構造を作成します。

   1. /apps フォルダーを右クリックし、作成/フォルダーを作成をクリックします。
   1. フォルダー名として「`cq`」を指定し、「OK」をクリックします。
   1. 同様に、`analytics` フォルダーと `components` フォルダーを作成します。

1. を右クリックします。 `components` 作成したフォルダーに移動し、「作成」>「コンポーネントを作成」の順にクリックします。 次のプロパティ値を指定します。

   * ラベル：`sitecatalyst`
   * タイトル：`sitecatalyst`
   * スーパータイプ：`/libs/cq/analytics/components/sitecatalyst`
   * グループ：`hidden`

1. 「OK」が有効になるまで「次へ」を繰り返しクリックしてから、「OK」をクリックします。

   sitecatalyst コンポーネントには、自動的に作成された sitecatalyst.jsp ファイルが含まれます。

1. sitecatalyst.jsp ファイルを右クリックして、「削除」をクリックします。

1. sitecatalyst コンポーネントを右クリックして、作成／ファイルを作成をクリックします。「`config.js.jsp`」という名前を指定して、「OK」をクリックします。

   config.js.jsp ファイルが自動的に編集用に開きます。

1. 次のテキストをファイルに追加して、「すべて保存」をクリックします。

   ```java
   <%@page session="true"%>
   /* Plugin Config */
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom plugin code here
   }
   s.doPlugins=s_doPlugins;
   ```

   /apps/cq/analytics/components/sitecatalyst/config.js.jsp スクリプトで生成される JavaScript コードが、Adobe Analyticsフレームワークを使用するすべてのページの analytics.sitecatalyst.js ファイルに挿入されます。

1. で実行する JavaScript コードを追加します。 `s_doPlugins` 関数を開き、[ すべて保存 ] をクリックします。

>[!CAUTION]
>
>ページのフレームワークの自由形式の JavaScript にテキストが存在する場合（空白のみ）、config.js.jsp は無視されます。

### AEM での Adobe Analytics プラグインの使用 {#using-adobe-analytics-plugins-in-aem}

Adobe Analyticsプラグインの JavaScript コードを取得し、AEMのAdobe Analyticsフレームワークに統合します。 カテゴリのクライアントライブラリフォルダーにコードを追加する `sitecatalyst.plugins` カスタム JavaScript コードで使用できるようにします。

例えば、 `getQueryParams` プラグインを使用する場合は、 `s_doPlugins` 関数を使用して、カスタム JavaScript を読み込みます。 次のコード例では、 **&quot;pid&quot;** リファラーの URL から **EVAR1**、Adobe Analytics呼び出しがトリガーされたとき。

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

AEM では次の Adobe Analytics プラグインをインストールして、デフォルトで使用できるようにします。

* getQueryParam()
* getPreviousValue()
* split()

/libs/cq/analytics/clientlibs/sitecatalyst/plugins クライアントライブラリフォルダーには、sitecatalyst.plugins カテゴリのこれらのプラグインが含まれています。

>[!NOTE]
>
>プラグイン用のクライアントライブラリフォルダーを作成します。 `/libs/cq/analytics/clientlibs/sitecatalyst/plugins` フォルダーにはプラグインを追加しないでください。こうしておけば、AEM の再インストールやアップグレードをおこなっても、`sitecatalyst.plugins` カテゴリに加えた変更が上書きされずに済みます。

次の手順を実行して、プラグインのクライアントライブラリフォルダーを作成します。 この手順は 1 回だけ実行する必要があります。 プラグインをクライアントライブラリフォルダーに追加するには、次の手順を実行します。

1. Web ブラウザーで CRXDE Lite を開きます。([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. /apps/my-app/clientlibs フォルダーを右クリックして、作成／ノードを作成をクリックします。次のプロパティ値を入力して、「OK」をクリックします。

   * 名前：クライアントライブラリフォルダーの名前（例：my-plugins）

   * タイプ：cq:ClientLibraryFolder

1. 作成したクライアントライブラリフォルダーを選択し、右下のプロパティバーを使用して、次のプロパティを追加します。

   * 名前：categories
   * タイプ：String
   * 値： sitecatalyst.plugins
   * マルチ：選択

   編集ウィンドウで「OK」をクリックして、プロパティの値を確認します。

1. 作成したクライアントライブラリフォルダーを右クリックし、作成/ファイルを作成をクリックします。 ファイル名として「js.txt」と入力し、「OK」をクリックします。

1. 「すべて保存」をクリックします。

以下の手順を実行して、プラグインのコードを取得し、AEM リポジトリ内に保存し、クライアントライブラリフォルダーに追加します。

1. Adobe Analytics アカウントを使用して [sc.omniture.com](https://sc.omniture.com/login/) にログインします。
1. ランディングページで、ヘルプ/ヘルプホームに移動します。
1. 左側の目次で、「実装プラグイン」をクリックします。
1. 追加するプラグインへのリンクをクリックし、ページが開いたら、プラグインの JavaScript ソースコードを探し、コードを選択してコピーします。

1. クライアントライブラリフォルダーを右クリックし、作成/ファイルを作成をクリックします。 ファイル名に、統合するプラグインの名前と.js を入力し、「OK」をクリックします。 例えば、getQueryParam プラグインを組み込む場合は、ファイルに getQueryParam.js という名前を付けます。

   作成したファイルを編集用に開きます。

1. プラグインの JavaScript コードをファイルに貼り付け、「すべて保存」をクリックして、ファイルを閉じます。

1. クライアントライブラリフォルダーの js.txt ファイルを開きます。

1. 新しい行に、プラグインを含むファイルの名前（例：getQueryParam.js）を追加します。 「すべて保存」をクリックして、ファイルを閉じます。

>[!NOTE]
>
>プラグインを使用する場合は、サポートするプラグインも必ず統合してください。統合しない場合、プラグイン JavaScript は、サポートするプラグインの関数に対しておこなった呼び出しを認識しません。 例えば、getPreviousValue() プラグインを正しく機能させるには、split() プラグインが必要です。
>
> サポートプラグインの名前も **js.txt** に追加する必要があります。
