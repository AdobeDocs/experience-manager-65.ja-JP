---
title: UI のテスト
seo-title: Testing Your UI
description: AEM には、AEM UI のテストを自動化するためのフレームワークが用意されています
seo-description: AEM provides a framework for automating tests for your AEM UI
uuid: 408a60b5-cba9-4c9f-abd3-5c1fb5be1c50
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
discoiquuid: 938100ad-94f9-408a-819d-72657dc115f7
docset: aem65
exl-id: 2d28cee6-31b0-4288-bad3-4d2ecad7b626
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '737'
ht-degree: 100%

---

# UI のテスト{#testing-your-ui}

>[!NOTE]
>
>AEM 6.5 以降、hobbes.js UI テストフレームワークは非推奨となります。アドビははそれ以上の機能拡張を行う予定はなく、Selenium 自動化を使用することをお客様に推奨しています。
>
>[廃止される機能および削除された機能](/help/release-notes/deprecated-removed-features.md)を参照してください。

AEM には、AEM UI のテストを自動化するためのフレームワークが用意されています。このフレームワークを使用して、Web ブラウザーで直接 UI テストを記述して実行します。このフレームワークには、テストを作成するための JavaScript API が用意されています。

AEM テストフレームワークでは、Javascript で記述されたテスト用ライブラリ Hobbes.js を使用します。Hobbes.js フレームワークは、開発プロセスの一環として AEM のテスト用に開発されたものです。このフレームワークは現在、独自の AEM アプリケーションのテスト用に一般に利用できます。

>[!NOTE]
>
>この API について詳しくは、Hobbes.js の[ドキュメント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html)を参照してください。

## テストの構造 {#structure-of-tests}

自動化されたテストを AEM 内で使用する場合は、以下の用語を理解しておくことが重要です。

| 動作 | **アクション**&#x200B;は、リンクやボタンのクリックなど、web ページ上の特定のアクティビティです。 |
|---|---|
| テストケース | **テストケース**&#x200B;は、1 つ以上の&#x200B;**アクション**&#x200B;で構成できる特定の状況です。 |
| テストスイート | **テストスイート**&#x200B;は、関連する&#x200B;**テストケース**&#x200B;を組み合わせて、特定のユースケースをテストします。 |

## テストの実行 {#executing-tests}

### テストスイートの表示 {#viewing-test-suites}

テストコンソールを開くと、登録されているテストスイートが表示されます。テストパネルには、テストスイートとそのテストケースのリストが表示されます。

ツールコンソールに移動するには、**グローバルナビゲーション／ツール／運営／テスト**&#x200B;の順に移動します。

![chlimage_1-63](assets/chlimage_1-63.png)

コンソールを開くと、左側には、テストスイートのリストと共に、すべてのテストスイートを順番に実行するためのオプションが表示されます。右側に表示される背景が格子柄のスペースは、テストの実行時にページコンテンツを表示するためのプレースホルダーです。

![chlimage_1-64](assets/chlimage_1-64.png)

### 1 つのテストスイートの実行 {#running-a-single-test-suite}

テストスイートは個別に実行できます。1 つのテストスイートを実行すると、テストケースとそのアクションの実行に応じてページが変化し、テストの完了後に結果が表示されます。アイコンによって結果が示されます。

チェックマークアイコンは、成功したテストを示します。

![](do-not-localize/chlimage_1-2.png)

「X」アイコンは、失敗したテストを示します。

![](do-not-localize/chlimage_1-3.png)

1 つのテストスイートを実行するには：

1. テストパネルで、実行するテストケースの名前をクリックまたはタップして、アクションの詳細を展開します。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 「**Run tests**」ボタンをクリックまたはタップします。

   ![](do-not-localize/chlimage_1-4.png)

1. テストが実行されると、プレースホルダーはページコンテンツに置き換えられます。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 説明をタップまたはクリックして&#x200B;**結果**&#x200B;パネルを開いて、テストケースの結果を確認します。**結果**&#x200B;パネルでテストケースの名前をタップまたはクリックすると、すべての詳細が表示されます。

   ![chlimage_1-67](assets/chlimage_1-67.png)

### 複数のテストの実行 {#running-multiple-tests}

テストスイートは、コンソールに表示された順番で実行されます。テストをドリルダウンして、詳細な結果を確認できます。

![chlimage_1-68](assets/chlimage_1-68.png)

1. テストパネルで、実行するテストスイートのタイトルの下にある「**Run all tests**」ボタンまたは「**Run tests**」ボタンをタップまたはクリックします。

   ![](do-not-localize/chlimage_1-5.png)

1. 各テストケースの結果を表示するには、そのテストケースのタイトルをタップまたはクリックします。**結果**&#x200B;パネルでテストの名前をタップまたはクリックすると、すべての詳細が表示されます。

   ![chlimage_1-69](assets/chlimage_1-69.png)

## シンプルなテストスイートの作成と使用 {#creating-and-using-a-simple-test-suite}

次の手順は、[We.Retail のコンテンツ](/help/sites-developing/we-retail.md)を使用したテストスイートの作成と実行の方法を説明するものですが、別の web ページを使用するよう簡単にテストを変更できます。

独自のテストスイートの作成について詳しくは、[Hobbes.js API のドキュメント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html)を参照してください。

1. CRXDE Lite を開きます。([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. `/etc/clientlibs` フォルダーを右クリックして、**作成／フォルダーを作成**&#x200B;をクリックしてください。名前に`myTests`と入力して、「**OK**」をクリックします。
1. `/etc/clientlibs/myTests` フォルダーを右クリックし、**作成／ノードを作成**&#x200B;をクリックしてください。以下のプロパティ値を使用して「**OK**」をクリックします。

   * 名前：`myFirstTest`
   * 型：`cq:ClientLibraryFolder`

1. myFirstTest ノードに次のプロパティを追加します。

   | 名前 | タイプ | 値 |
   |---|---|---|
   | `categories` | String[] | `granite.testing.hobbes.tests` |
   | `dependencies` | String[] | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**AEM Forms のみ**
   >
   >
   >アダプティブフォームをテストするには、categories と dependencies に次の値を追加してください。次に例を示します。
   >
   >
   >**categories**：`granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**dependencies**：`granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. 「**すべて保存**」をクリックします。
1. `myFirstTest` ノードを右クリックして、**作成／ファイルを作成**&#x200B;をクリックします。ファイル名に`js.txt`と入力して、「**OK**」をクリックします。
1. `js.txt` ファイルに次のテキストを入力します。

   ```
   #base=.
   myTestSuite.js
   ```

1. 「**すべて保存**」をクリックして、`js.txt` ファイルを閉じます。
1. `myFirstTest` ノードを右クリックして、**作成／ファイルを作成**&#x200B;をクリックします。ファイル名に`myTestSuite.js`と入力して、「**OK**」をクリックします。
1. `myTestSuite.js` ファイルに次のコードをコピーして、ファイルを保存します。

   ```
   new hobs.TestSuite("Experience Content Test Suite", {path:"/etc/clientlibs/myTests/myFirstTest/myTestSuite.js"})
      .addTestCase(new hobs.TestCase("Navigate to Experience Content")
         .navigateTo("/content/we-retail/us/en/experience/arctic-surfing-in-lofoten.html")
      )
      .addTestCase(new hobs.TestCase("Hover Over Topnav")
         .mouseover("li.visible-xs")
      )
      .addTestCase(new hobs.TestCase("Click Topnav Link")
         .click("li.active a")
   );
   ```

1. **テスト**&#x200B;コンソールに移動して、テストスイートを実行します。
