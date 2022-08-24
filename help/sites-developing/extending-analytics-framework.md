---
title: Adobe Analytics Framework のカスタマイズ
seo-title: Customizing the Adobe Analytics Framework
description: Adobe Analytics Framework のカスタマイズ
seo-description: null
uuid: 444a29c2-3b4e-4d21-adc0-5f317ece2b77
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 11c0aac6-a7f6-4d6b-a080-b04643045a64
exl-id: ab0d4f2e-f761-4510-ba51-4a2dcea49601
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1618'
ht-degree: 100%

---

# Adobe Analytics Framework のカスタマイズ{#customizing-the-adobe-analytics-framework}

Adobe Analytics フレームワークは、Adobe Analytics で追跡される情報を決定します。デフォルトのフレームワークをカスタマイズするには、Javascript を使用してカスタムトラッキングを追加し、Adobe Analytics プラグインを組み込み、トラッキングに使用するフレームワーク内の一般設定を変更します。

## フレームワーク用に生成される Javascript について {#about-the-generated-javascript-for-frameworks}

ページを Adobe Analytics フレームワークと関連付け、そのページに [Analytics モジュールへの参照](/help/sites-administering/adobeanalytics.md)を含めると、analytics.sitecatalyst.js ファイルがそのページ用に自動的に生成されます。

ページ内の Javascript が `s_gi` オブジェクト（s_code.js Adobe Analytics ライブラリが定義）を作成し、そのプロパティに値を割り当てます。オブジェクトインスタンスの名前は `s` です。この節に示すコード例では、この `s` 変数への参照を複数作成します。

次のコード例は、analytics.sitecatalyst.js ファイルのコードによく似ています。

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

カスタム Javascript コードを使用してフレームワークをカスタマイズする場合は、このファイルの内容を変更します。

## Adobe Analytics プロパティの設定 {#configuring-adobe-analytics-properties}

Adobe Analytics には、フレームワーク上で設定できる事前定義済みの変数が数多くあります。変数 **charset**、**cookieLifetime**、**currencyCode** および **trackInlineStats** は、**Analytics 一般設定**&#x200B;リストにデフォルトで含まれています。

![aa-22](assets/aa-22.png)

このリストに、変数名と値を追加できます。これらの事前定義済みの変数と、追加したすべての変数を使用して、analytics.sitecatalyst.js ファイル内の `s` オブジェクトのプロパティを設定します。次の例は、追加された値 `CONSTANT` の `prop10` プロパティが、Javascript のコードでどのように表現されるかを示しています。

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
1. 左側のセルに変数の名前（例：`prop10`）を入力します。

1. 右側の列に変数の値（例：`CONSTANT`）を入力します。

1. 変数を削除するには、変数の横の（-）ボタンをクリックします。

>[!NOTE]
>
>変数と値を入力する際は、形式とスペルが正しいことを確認してください。そうでない場合は、正しい値と変数のペアを使用して&#x200B;**呼び出しが送信されません**。変数や値のスペルが間違っていると、呼び出しを実行することさえできない場合があります。
>
>これらの変数が正しく設定されていることを確認するには、Adobe Analytics の担当者に相談してください。

>[!CAUTION]
>
>このリストの変数の一部は、Adobe Analytics の呼び出しを正しく機能させるうえで&#x200B;**必須**&#x200B;です（**currencyCode**、**charSet** など）。
>
>そのため、フレームワーク自体から変数を削除しても、Adobe Analytics の呼び出しがおこなわれると、デフォルト値を持つ変数が付加されます。

### Adobe Analytics フレームワークへのカスタム JavaScript の追加 {#adding-custom-javascript-to-an-adobe-analytics-framework}

**Analytics の一般設定**&#x200B;領域にあるフリーフォームの Javascript ボックスを使用して、Adobe Analytics フレームワークにカスタムコードを追加できます。

![aa-21](assets/aa-21.png)

追加するコードは、analytics.sitecatalyst.js ファイルに付加されます。そのため、`s` 変数にアクセスできます。この変数は、`s_code.js` で定義されている `s_gi` Javascript オブジェクトのインスタンスです。例えば、次のコードの追加は、前節の例で値 `CONSTANT` の `prop10` という変数を追加することと同等です。

`s.prop10= 'CONSTANT';`

[analytics.sitecatalyst.js](/help/sites-developing/extending-analytics-components.md) ファイル（Adobe Analytics の `s-code.js` ファイルの内容を含む）のコードには、次のコードが含まれます。

`if (s.usePlugins) s.doPlugins(s)`

以下の手順は、Javascript ボックスを使用して Adobe Analytics の追跡機能をカスタマイズする方法を示しています。Javascript で Adobe Analytics プラグインを使用する必要がある場合は、AEM に[プラグインを組み込んでください](/help/sites-administering/adobeanalytics.md)。

1. `s.doPlugins` を実行するように、次の Javascript コードをボックスに追加します。

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >何らかの方法でカスタマイズ済みで、基本のドラッグ＆ドロップインターフェイスまたは Adobe Analytics ビューのインライン Javascript からは実行できない Adobe Analytics の呼び出しに変数を含めて送信する場合は、このコードが必要です。
   >
   >カスタム変数が s_doPlugins 関数の外にある場合は、Adobe Analytics の呼び出しで *undefined* として送信

1. Javascript コードを **s_doPlugins** 関数に追加します。

次の例では、一般的な区切り文字「|」を使用して、ページ上でキャプチャされたデータを階層順に連結しています。

Adobe Analytics フレームワークには、以下の設定があります。

* `prop2` Adobe Analytics 変数は `pagedata.sitesection` サイトプロパティにマッピングされます。

* `prop3` Adobe Analytics 変数は `pagedata.subsection` サイトプロパティにマッピングされます。

* 次のコードがフリーフォームの Javascript ボックスに追加されます。

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

すべての Adobe Analytics フレームワークに組み込むカスタム Javascript コードを指定します。ページの Adobe Analytics フレームワークにカスタムの[フリーフォームの Javascript](/help/sites-administering/adobeanalytics.md) が含まれていない場合、/libs/cq/analytics/components/sitecatalyst/config.js.jsp スクリプトが生成する Javascript が [analytics.sitecatalyst.js](/help/sites-administering/adobeanalytics.md) ファイルに付加されます。デフォルトでは、このスクリプトはコメントアウトされているので効果はありません。また、このコードは `s.usePlugins` を `false` に設定します。

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

したがって、`s_doPlugins` 関数内のすべてのコードが実行されるように、Javascript で `s.usePlugins` を `true` に設定する必要があります。このコードをカスタマイズするには、独自の Javascript を使用するファイルで config.js.jsp ファイルをオーバーレイします。Javascript で Adobe Analytics プラグインを使用する必要がある場合は、AEM に[プラグインを組み込んでください](/help/sites-administering/adobeanalytics.md)。

>[!NOTE]
>
>/libs/cq/analytics/components/sitecatalyst/config.js.jsp ファイルは編集しないでください。特定の AEM アップグレードタスクまたはメンテナンスタスクによって、元のファイルが再インストールされ、変更内容が削除されることがあります。

1. CRXDE Lite で、/apps/cq/analytics/components フォルダー構造を作成します。

   1. /apps フォルダーを右クリックして、作成／フォルダーを作成をクリックします。
   1. フォルダー名として「`cq`」を指定し、「OK」をクリックします。
   1. 同様に、`analytics` フォルダーと `components` フォルダーを作成します。

1. 作成した `components` フォルダーを右クリックし、作成／コンポーネントを作成をクリックします。次のプロパティ値を指定します。

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

   /apps/cq/analytics/components/sitecatalyst/config.js.jsp スクリプトによって生成される Javascript コードが、 Adobe Analytics フレームワークを使用するすべてのページ用の analytics.sitecatalyst.js ファイルに挿入されます。

1. `s_doPlugins` 関数で実行する Javascript コードを追加して、「すべて保存」をクリックします。

>[!CAUTION]
>
>ページのフレームワークのフリーフォームの Javascript に何らかのテキストが存在する場合（スペースのみでも）、config.js.jsp は無視されます。

### AEM での Adobe Analytics プラグインの使用 {#using-adobe-analytics-plugins-in-aem}

Adobe Analytics プラグイン用の Javascript コードを取得して、AEM で Adobe Analytics フレームワークに組み込みます。カスタム Javascript コードで使用できるよう、コードを `sitecatalyst.plugins` カテゴリのクライアントライブラリフォルダーに追加します。

例えば、`getQueryParams` プラグインを組み込む場合、カスタム Javascript の `s_doPlugins` 関数からプラグインを呼び出すことができます。次のコード例では、Adobe Analytics の呼び出しがトリガーされると、リファラーの URL の **pid** 内のクエリ文字列を **eVar1** として送信します。

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
>プラグイン用の新しいクライアントライブラリフォルダーを作成します。`/libs/cq/analytics/clientlibs/sitecatalyst/plugins` フォルダーにはプラグインを追加しないでください。こうしておけば、AEM の再インストールやアップグレードをおこなっても、`sitecatalyst.plugins` カテゴリに加えた変更が上書きされずに済みます。

以下の手順を実行して、プラグイン用のクライアントライブラリフォルダーを作成します。この手順を実行する必要があるのは 1 回だけです。プラグインをクライアントライブラリフォルダーに追加するには、次の手順を実行します。

1. Web ブラウザーで CRXDE Lite を開きます。([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. /apps/my-app/clientlibs フォルダーを右クリックして、作成／ノードを作成をクリックします。次のプロパティ値を入力して、「OK」をクリックします。

   * 名前：クライアントライブラリフォルダーの名前（例：my-plugins）

   * タイプ：cq:ClientLibraryFolder

1. 作成したクライアントライブラリフォルダーを選択し、右下のプロパティバーを使用して、次のプロパティを追加します。

   * 名前：categories
   * タイプ：String
   * 値：sitecatalyst.plugins
   * マルチ：selected

   編集ウィンドウで「OK」をクリックして、プロパティの値を確認します。

1. 作成したクライアントライブラリフォルダーを右クリックし、作成／ファイルを作成をクリックします。ファイル名として「js.txt」と入力し、「OK」をクリックします。

1. 「すべて保存」をクリックします。

以下の手順を実行して、プラグインのコードを取得し、AEM リポジトリ内に保存し、クライアントライブラリフォルダーに追加します。

1. Adobe Analytics アカウントを使用して [sc.omniture.com](https://sc.omniture.com) にログインします。
1. ランディングページで、ヘルプ／ヘルプホームに移動します。
1. 左側の目次で、「実装プラグイン」をクリックします。
1. 追加するプラグインへのリンクをクリックし、ページが表示されたら、プラグインの JavaScript ソースコードを探して、そのコードを選択し、コピーします。

1. クライアントライブラリフォルダーを右クリックして、作成／ファイルを作成をクリックします。ファイル名として、組み込むプラグインの名前に「.js」を付けて入力し、「OK」をクリックします。例えば、getQueryParam プラグインを組み込む場合は、ファイルに getQueryParam.js という名前を付けます。

   作成したファイルを編集用に開きます。

1. プラグインの JavaScript コードをファイルに貼り付け、「すべて保存」をクリックし、ファイルを閉じます。

1. クライアントライブラリフォルダーの js.txt ファイルを開きます。

1. 新しい行に、プラグインを格納しているファイルの名前（例：getQueryParam.js）を追加します。「すべて保存」をクリックして、ファイルを閉じます。

>[!NOTE]
>
>プラグインの使用時は、サポートプラグインも必ず組み込んでください。さもないと、プラグインの Javascript がサポートプラグイン内の関数に対しておこなわれる呼び出しを認識しません。例えば、getPreviousValue() プラグインを正しく機能させるには、split() プラグインが必要です。
>
> サポートプラグインの名前も **js.txt** に追加する必要があります。
