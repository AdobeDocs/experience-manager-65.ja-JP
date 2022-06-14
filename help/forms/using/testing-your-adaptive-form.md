---
title: 「チュートリアル：アダプティブフォームのテスト」
seo-title: 'Tutorial: Testing your adaptive form'
description: 自動化されたテストを使用して、複数のアダプティブフォームを一度にテストします。
seo-description: Use automated testing to test multiple adaptive forms at once.
uuid: 6d182bbc-b47a-4c97-af70-c960b52fdfac
contentOwner: khsingh
discoiquuid: ecddb22e-c148-441f-9088-2e5b35c7021b
docset: aem65
feature: Adaptive Forms
exl-id: 343e2e0b-d5ef-4f01-b3d6-45f90e2430fd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 100%

---

# チュートリアル：アダプティブフォームのテスト {#tutorial-testing-your-adaptive-form}

![](do-not-localize/10-test-your-adaptive-form.png)

これは、「[最初のアダプティブフォームを作成する](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)」シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

アダプティブフォームの準備が整ったら、アダプティブフォームをエンドユーザーにロールアウトする前にテストすることが重要です。アダプティブフォームのすべてのフィールドを手動でテスト（機能テスト）したり、テストを自動化したりできます。複数のアダプティブフォームがある場合、すべてのアダプティブフォームの各フィールドを手動でテストすると、大変な作業になります。

AEM [!DNL Forms] は、アダプティブフォームのテストを自動化するテストフレームワーク「Calvin」を備えています。このフレームワークを使用して、Web ブラウザーで直接 UI テストを記述して実行します。このフレームワークでは、テストを作成するための JavaScript API が用意されています。自動テストを使用すると、アダプティブフォームの事前入力エクスペリエンス、アダプティブフォームの送信エクスペリエンス、式ルール、検証からの検証、遅延読み込み、UI の操作をテストできます。このチュートリアルでは、アダプティブフォーム上で自動化されたテストを作成し、実行する手順について説明します。このチュートリアルを完了すると、次の操作を実行できるようになります。

* [アダプティブフォームのテストスイートを作成する](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-suite)
* [アダプティブフォームのテストを作成する](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-case-to-prefill-values-in-an-adaptive-form)
* [アダプティブフォーム用に作成されたテストスイートとテストを実行する](#step-run-all-the-tests-in-a-suite-or-individual-tests-cases)

## 手順 1：テストスイートを作成 {#step-create-a-test-suite}

テストスイートには、テストケースのコレクションがあります。複数のテストスイートを設定できます。各フォームに別々のテストスイートを作成することをお勧めします。テストスイートを作成するには：

1. AEM [!DNL Forms] オーサーインスタンスに管理者としてログインします。[!UICONTROL CRXDE Lite] を開きます。AEM ロゴ／**[!UICONTROL ツール]**／**[!UICONTROL 一般]**／**[!UICONTROL CRXDE Lite]** をタップして、または、ブラウザーで URL [https://localhost:4502/crx/de/index.jsp](https://localhost:4502/crx/de/index.jsp) を開いて、CRXDELite を開きます。

1. [!UICONTROL CRXDE Lite] の /etc/clientlibs に移動します。/etc/clientlibs サブフォルダーを右クリックして、**[!UICONTROL 作成]**／**[!UICONTROL ノードを作成]**&#x200B;をクリックします。「**[!UICONTROL 名前]**」フィールドに「**WeRetailFormTestCases**」と入力します。タイプを **cq:ClientLibraryFolder** として選択して「**[!UICONTROL OK]**」をクリックします。ノードが作成されます。`WeRetailFormTestCases` の代わりに任意の名前を使用できます。
1. 次のプロパティを `WeRetailFormTestCases` ノードに追加して、「**[!UICONTROL すべて保存]**」をクリックします。

   <table>
    <tbody>
     <tr>
      <td><strong>プロパティ</strong></td>
      <td><strong>タイプ</strong></td>
      <td><strong>マルチ</strong></td>
      <td><strong>値</strong></td>
     </tr>
     <tr>
      <td>カテゴリ</td>
      <td>文字列</td>
      <td>Enabled</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.tests<br /> </li>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     <tr>
      <td>dependencies</td>
      <td>文字列</td>
      <td>有効</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.testrunner <br /> </li>
        <li>granite.testing.calvin <br /> </li>
        <li>apps.testframework.all</li>
       </ul> </td>
     </tr>
    </tbody>
   </table>

   次に示すように、各プロパティが別々のボックスに追加されていることを確認します。

   ![dependencies](assets/dependencies.png)

1. **[!UICONTROL WeRetailFormTestCases]** ノードを右クリックして、**[!UICONTROL 作成]**／**[!UICONTROL ファイルを作成]**&#x200B;をクリックします。**[!UICONTROL 名前]** フィールドに「`js.txt`」と入力して「**[!UICONTROL OK]**」をクリックします。
1. js.txt ファイルを編集用に開き、次のコードを追加して、ファイルを保存します。

   ```text
   #base=.
    init.js
   ```

1. init.js ファイルを `WeRetailFormTestCases` ノードに作成します。ファイルに以下のコードを追加して「**[!UICONTROL すべて保存]**」をタップします。

   ```javascript
   (function(window, hobs) {
       'use strict';
       window.testsuites = window.testsuites || {};
     // Registering the test form suite to the sytem
     // If there are other forms, all registration should be done here
       window.testsuites.testForm3 = new hobs.TestSuite("We retail - Tests", {
           path: '/etc/clientlibs/WeRetailFormTestCases/init.js',
           register: true
       });
    // window.testsuites.testForm2 = new hobs.TestSuite("testForm2");
   }(window, window.hobs));
   ```

   上記のコードを使用すると、 **We retail - テスト** という名前のテストスイートが作成されます。

1. AEM テスト UI を開きます（AEM／**[!UICONTROL ツール]**／**[!UICONTROL 運用]**／**[!UICONTROL テスト]**）。テストスイート（**We retail - テスト**）が UI にリストされます。

   ![we-retail-test-suite](assets/we-retail-test-suite.png)

## 手順 2：アダプティブフォームの値を事前に入力するためのテストケースを作成する {#step-create-a-test-case-to-prefill-values-in-an-adaptive-form}

テストケースは、特定の機能をテストするための一連のアクションです。例えば、フォームのすべてのフィールドへの事前入力や、正しい値が入力されていることを確認するためのいくつかのフィールドの検証を行います。

アクションとは、ボタンのクリックなど、アダプティブフォーム上の特定のアクティビティのことです。各アダプティブフォームフィールドのユーザー入力を検証するテストケースとアクションを作成するには、次の手順を実行します。

1. [!UICONTROL CRXDE lite] で `/content/forms/af/create-first-adaptive-form` フォルダーに移動します。**[!UICONTROL create-first-adaptive-form]** フォルダーノードを右クリックし、**[!UICONTROL 作成]**／**[!UICONTROL ファイルを作成]**&#x200B;をクリックします。**[!UICONTROL 名前]**&#x200B;フィールドに「`prefill.xml`」と入力して「**[!UICONTROL OK]**」をクリックします。次のコードをファイルに追加しました。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?><afData>
     <afUnboundData>
       <data>
         <customer_ID>371767</customer_ID>
         <customer_Name>John Jacobs</customer_Name>
         <customer_Shipping_Address>1657 1657 Riverside Drive Redding</customer_Shipping_Address>
         <customer_State>California</customer_State>
         <customer_ZIPCode>096001</customer_ZIPCode>
        </data>
     </afUnboundData>
     <afBoundData>
       <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"/>
     </afBoundData>
   </afData>
   ```

1. `/etc/clientlibs` に移動します。`/etc/clientlibs` サブフォルダーを右クリックして、**[!UICONTROL 作成]**／**[!UICONTROL ノードを作成]**&#x200B;をクリックします。

   **[!UICONTROL 名前]**&#x200B;フィールドタイプで「`WeRetailFormTests`」を入力します。タイプを `cq:ClientLibraryFolder` として選択し、「**[!UICONTROL OK]**」をクリックします。

1. **[!UICONTROL WeRetailFormTests]** ノードに次のプロパティを追加します。

   <table>
    <tbody>
     <tr>
      <td><strong>プロパティ</strong></td>
      <td><strong>タイプ</strong></td>
      <td><strong>マルチ</strong></td>
      <td><strong>値</strong></td>
     </tr>
     <tr>
      <td>カテゴリ</td>
      <td>文字列</td>
      <td>有効</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.tests<br /> </li>
        <li>granite.testing.hobbes.tests.testForm</li>
       </ul> </td>
     </tr>
     <tr>
      <td>依存</td>
      <td>文字列</td>
      <td>有効</td>
      <td>
       <ul>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     </tbody>
   </table>

1. ファイル js.txt を **[!UICONTROL WeRetailFormTests]** ノードに作成します。 次の項目をファイルに追加します。

   ```shell
   #base=.
   prefillTest.js
   ```

   「**[!UICONTROL すべて保存]**」をクリックします。

1. ファイル `prefillTest.js` を **[!UICONTROL WeRetailFormTests]** ノードに作成します。 次のコードをファイルに追加します。コードによってテストケースが作成されます。 テストケースでは、フォームのすべてのフィールドが事前に入力され、一部のフィールドが正しい値が入力されていることを確認します。

   ```javascript
   (function (window, hobs) {
       'use strict';
   
       var ts = new hobs.TestSuite("Prefill Test", {
           path: '/etc/clientlibs/WeRetailFormTests/prefillTest.js',
           register: false
       })
   
       .addTestCase(new hobs.TestCase("Prefill Test")
           // navigate to the testForm which is to be test
           .navigateTo("/content/forms/af/create-first-adaptive-form/shipping-address-add-update-form.html?wcmmode=disabled&dataRef=crx:///content/forms/af/create-first-adaptive-form/prefill.xml")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
           .asserts.isTrue(function () {
               return calvin.model("customer_ID").value == 371767;
           })
           .asserts.isTrue(function () {
               return calvin.model("customer_ZIPCode").value == 96001;
           })
       );
   
       // register the test suite with testForm
       window.testsuites.testForm3.add(ts);
   
   }(window, window.hobs));
   ```

   テストケースが作成され、実行する準備が整いました。 テストケースを作成して、計算スクリプトの実行の確認、パターンの検証、アダプティブフォームの送信操作の検証など、アダプティブフォームの様々な側面を検証できます。 アダプティブフォームのテストの様々な側面について詳しくは、「アダプティブフォームの自動テスト」を参照してください。

## 手順 3：スイート内のすべてのテストまたは個々のテストケースを実行する {#step-run-all-the-tests-in-a-suite-or-individual-tests-cases}

1 つのテストスイートに複数のテストケースを含めることができます。テストスイート内のすべてのテストケースは、一度に、または個別に実行できます。テストを実行すると、結果が次のアイコンで示されます。

* チェックマークのアイコン ![save_icon](assets/save_icon.svg) は、合格したテストを示しています。
* 「X」アイコン ![close-icon](assets/close-icon.svg) は、失敗したテストを示します。

1. AEM アイコン／**[!UICONTROL ツール]**／**[!UICONTROL 運用]**／**[!UICONTROL テスト]**&#x200B;に移動します
1. テストスイートのすべてのテストを実行するには、次を行います。

   1. [!UICONTROL テスト]パネルで、「**[!UICONTROL We retail - Tests (1)]**」をタップします。テストスイートが展開され、テストのリストが表示されます。
   1. 「**[!UICONTROL テストを実行]** 」ボタンをタップします。 テストを実行すると、画面の右側の空白の領域がアダプティブフォームに置き換えられます。

      ![run-all-test](assets/run-all-test.png)

1. テストスイートから 1 つのテストを実行するには、次の手順を実行します。

   1. テストパネルで、「**[!UICONTROL We retail - Tests (1)]**」をタップします。テストスイートが展開され、テストのリストが表示されます。
   1. 「**[!UICONTROL 事前入力テスト]**」をタップしてから「**[!UICONTROL テストを実行]**」ボタンをタップします。 テストを実行すると、画面の右側の空白の領域がアダプティブフォームに置き換えられます。

1. テスト名「事前入力テスト」をタップして、テストケースの結果を確認します。 [!UICONTROL 結果]パネルが開きます。[!UICONTROL 結果]パネルでテストケースの名前をタップして、テストのすべての詳細を表示します。

   ![review-results](assets/review-results.png)

これで、アダプティブフォームの発行準備が整いました。
