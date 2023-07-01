---
title: UI のテスト
description: AEMには、AEM UI のテストを自動化するためのフレームワークが用意されています
uuid: 408a60b5-cba9-4c9f-abd3-5c1fb5be1c50
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
discoiquuid: 938100ad-94f9-408a-819d-72657dc115f7
docset: aem65
exl-id: 2d28cee6-31b0-4288-bad3-4d2ecad7b626
source-git-commit: 4fd5e9a1bc603202ee52e85a1c09125b13cec315
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 49%

---

# UI のテスト{#testing-your-ui}

>[!NOTE]
>
>AEM 6.5 以降、hobbes.js UI テストフレームワークは非推奨となります。アドビははそれ以上の機能拡張を行う予定はなく、Selenium 自動化を使用することをお客様に推奨しています。
>
>[廃止される機能および削除された機能](/help/release-notes/deprecated-removed-features.md)を参照してください。

AEMは、AEM UI のテストを自動化するためのフレームワークを提供します。 このフレームワークを使用して、Web ブラウザーで直接 UI テストを記述して実行します。このフレームワークは、テストを作成するための JavaScript API を提供します。

AEMのテストフレームワークは、JavaScript で記述されたテストライブラリ Hobbes.js を使用します。 Hobbes.js フレームワークは、開発プロセスの一環として AEM のテスト用に開発されたものです。このフレームワークは現在、独自の AEM アプリケーションのテスト用に一般に利用できます。

>[!NOTE]
>
>この API について詳しくは、Hobbes.js の[ドキュメント](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html)を参照してください。

## テストの構造 {#structure-of-tests}

AEM内で自動テストを使用する場合、次の用語を理解することが重要です。

| 動作 | **アクション**&#x200B;は、リンクやボタンのクリックなど、web ページ上の特定のアクティビティです。 |
|---|---|
| テストケース | **テストケース**&#x200B;は、1 つ以上の&#x200B;**アクション**&#x200B;で構成できる特定の状況です。 |
| テストスイート | **テストスイート**&#x200B;は、関連する&#x200B;**テストケース**&#x200B;を組み合わせて、特定のユースケースをテストします。 |

## テストの実行 {#executing-tests}

### テストスイートの表示 {#viewing-test-suites}

テストコンソールを開いて、登録されているテストスイートを確認します。 テストパネルには、テストスイートとそのテストケースのリストが表示されます。

からツールコンソールに移動します。 **グローバルナビゲーション/ツール/操作/テスト**.

![chlimage_1-63](assets/chlimage_1-63.png)

コンソールを開くと、テストスイートが左側に表示され、すべてを順番に実行するオプションも表示されます。 右側のスペースにチェックマークの付いた背景が、テスト実行時にページのコンテンツを表示するためのプレースホルダーです。

![chlimage_1-64](assets/chlimage_1-64.png)

### 単一のテストスイートの実行 {#running-a-single-test-suite}

テストスイートは個別に実行できます。 テストスイートを実行すると、テストケースとそのアクションが実行され、テストの完了後に結果が表示されるにつれ、ページは変化します。 アイコンは結果を示します。

チェックマークアイコンは、合格したテストを示します。

![チェックマークアイコン](do-not-localize/chlimage_1-2.png)

「X」アイコンは、失敗したテストを示します。

![サール内の X で示される、失敗したテストアイコン。](do-not-localize/chlimage_1-3.png)

テストスイートを実行するには：

1. テストパネルで、実行するテストケースの名前をクリックまたはタップして、アクションの詳細を展開します。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. クリック **テストを実行**.

   ![「テストを実行」ボタンの画像。円内の右向きのポインターで示されます。](do-not-localize/chlimage_1-4.png)

1. テストが実行されると、プレースホルダーはページコンテンツに置き換えられます。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 説明をタップまたはクリックしてテストケースの結果を確認し、 **結果** パネル。 「 **結果** パネルには、すべての詳細が表示されます。

   ![chlimage_1-67](assets/chlimage_1-67.png)

### 複数のテストの実行 {#running-multiple-tests}

テストスイートは、コンソールに表示される順序で順番に実行されます。 テストの詳細を調べて、結果を確認できます。

![chlimage_1-68](assets/chlimage_1-68.png)

1. テストパネルで、実行するテストスイートのタイトルの下にある「**Run all tests**」ボタンまたは「**Run tests**」ボタンをタップまたはクリックします。

   ![円内の右向きのポインターで示される、「すべてのテストを実行」ボタンと「テストを実行」ボタンの画像。](do-not-localize/chlimage_1-5.png)

1. 各テストケースの結果を表示するには、テストケースのタイトルをクリックします。 テストの名前を **結果** パネルには、すべての詳細が表示されます。

   ![chlimage_1-69](assets/chlimage_1-69.png)

## シンプルなテストスイートの作成と使用 {#creating-and-using-a-simple-test-suite}

次の手順は、[We.Retail のコンテンツ](/help/sites-developing/we-retail.md)を使用したテストスイートの作成と実行の方法を説明するものですが、別の web ページを使用するよう簡単にテストを変更できます。

独自のテストスイートの作成について詳しくは、[Hobbes.js API のドキュメント](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html)を参照してください。

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
   >**AEM Formsのみ**
   >
   >
   >アダプティブフォームをテストするには、カテゴリと依存関係に次の値を追加します。 次に例を示します。
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
