---
title: チュートリアル：アダプティブフォームのテスト」
seo-title: チュートリアル：アダプティブフォームのテスト」
description: 自動テストを使用して、複数のアダプティブフォームを一度にテストします。
seo-description: 自動テストを使用して、複数のアダプティブフォームを一度にテストします。
uuid: 6d182bbc-b47a-4c97-af70-c960b52fdfac
contentOwner: khsingh
discoiquuid: ecddb22e-c148-441f-9088-2e5b35c7021b
docset: aem65
translation-type: tm+mt
source-git-commit: 1a816672b3e97346f5a7a984fcb4dc0df1a5b0da
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 10%

---


# チュートリアル：アダプティブフォームのテスト{#tutorial-testing-your-adaptive-form}

![](do-not-localize/10-test-your-adaptive-form.png)

これは、「[最初のアダプティブフォームを作成する](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)」シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

アダプティブフォームの準備が整ったら、エンドユーザーにアダプティブフォームを展開する前に、そのアダプティブフォームをテストすることが重要です。 すべてのフィールドを手動でテスト（機能テスト）したり、アダプティブフォームのテストを自動化したりできます。 複数のアダプティブフォームがある場合、すべてのアダプティブフォームのすべてのフィールドを手動でテストすると、負担の大きいタスクになります。

AEM [!DNL Forms]は、アダプティブフォームのテストを自動化するテストフレームワークCalvinを提供します。 このフレームワークを使用して、Web ブラウザーで直接 UI テストを記述して実行します。フレームワークは、テストを作成するためのJavaScript APIを提供します。 自動テストでは、アダプティブフォームの事前入力エクスペリエンス、アダプティブフォームの送信エクスペリエンス、式ルール、検証からの検証、遅延読み込み、UIインタラクションをテストできます。 このチュートリアルでは、アダプティブフォームで自動テストを作成し、実行する手順について説明します。 このチュートリアルを完了すると、次の操作を実行できるようになります。

* [アダプティブフォームのテストスイートの作成](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-suite)
* [アダプティブフォームのテストの作成](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-case-to-prefill-values-in-an-adaptive-form)
* [アダプティブフォーム用に作成されたテストスイートとテストの実行](#step-run-all-the-tests-in-a-suite-or-individual-tests-cases)

## 手順1:テストスイートの作成{#step-create-a-test-suite}

テストスイートには、テストケースが集まっています。 複数のテストスイートを設定できます。 フォームごとに個別のテストスイートを作成することをお勧めします。 テストスイートを作成するには：

1. 管理者としてAEM [!DNL Forms]作成者インスタンスにログインします。 [!UICONTROL CRXDE Lite]を開きます。 ブラウザーでAEMロゴ/**[!UICONTROL ツール]**/**[!UICONTROL 一般]**/**[!UICONTROL CRXDE Lite]**&#x200B;をタップするか、[https://localhost:4502/crx/de/index.jsp](https://localhost:4502/crx/de/index.jsp)URLを開いてCRXDE Liteを開くことができます。

1. [!UICONTROL CRXDE Lite]の/etc/clientlibsに移動します。 /etc/clientlibs サブフォルダーを右クリックして、**[!UICONTROL 作成]**／**[!UICONTROL ノードを作成]**&#x200B;をクリックします。**[!UICONTROL 名前]**&#x200B;フィールドに&#x200B;**WeRetailFormTestCases**&#x200B;と入力します。 タイプを&#x200B;**cq:ClientLibraryFolder**&#x200B;として選択し、「**[!UICONTROL OK]**」をクリックします。 ノードを作成します。 `WeRetailFormTestCases`の代わりに任意の名前を使用できます。
1. &lt;a0追加/>ノードに次のプロパティを追加し、「**[!UICONTROL すべて保存]**」をタップします。`WeRetailFormTestCases`

   <table>
    <tbody>
     <tr>
      <td><strong>プロパティ</strong></td>
      <td><strong>型</strong></td>
      <td><strong>複数</strong></td>
      <td><strong>値</strong></td>
     </tr>
     <tr>
      <td>categories</td>
      <td>String</td>
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

   次に示すように、各プロパティが個別のボックスに追加されていることを確認します。

   ![dependencies](assets/dependencies.png)

1. **[!UICONTROL WeRetailFormTestCases]**&#x200B;ノードを右クリックし、**[!UICONTROL 作成]**/**[!UICONTROL ファイルを作成]**&#x200B;をクリックします。 「**[!UICONTROL 名前]**」フィールドに`js.txt`と入力し、「**[!UICONTROL OK]**」をクリックします。
1. js.txtファイルを開いて編集し、次のコードを追加し、ファイルを保存します。

   ```text
   #base=.
    init.js
   ```

1. `WeRetailFormTestCases`ノードにファイルinit.jsを作成します。 ファイル追加の下のコードをタップし、「**[!UICONTROL すべて保存]**」をタップします。

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

   上記のコードは、**We retail - Tests**&#x200B;という名前のテストスイートを作成します。

1. AEMテストUI(AEM > **[!UICONTROL ツール]** > **[!UICONTROL 操作]** > **[!UICONTROL テスト]**)を開きます。 UIにテストスイート&#x200B;**We retail - Tests**&#x200B;が表示されます。

   ![we-retail-test-suite](assets/we-retail-test-suite.png)

## 手順2:アダプティブフォーム{#step-create-a-test-case-to-prefill-values-in-an-adaptive-form}に値を事前入力するテストケースの作成

テストケースとは、特定の機能をテストする一連のアクションです。 例えば、フォームのすべてのフィールドに事前入力し、いくつかのフィールドを検証して、正しい値が入力されていることを確認します。

アクションとは、ボタンのクリックなど、アダプティブフォーム上の特定のアクティビティを指します。 各アダプティブフォームフィールドのユーザー入力を検証するテストケースとアクションを作成するには：

1. [!UICONTROL CRXDE lite]で、`/content/forms/af/create-first-adaptive-form`フォルダーに移動します。 **[!UICONTROL create-first-adaptive-form]**&#x200B;フォルダーノードを右クリックし、**[!UICONTROL 作成]****[!UICONTROL ファイルを作成]**&#x200B;をクリックします。 「**[!UICONTROL 名前]**」フィールドに`prefill.xml`と入力し、「**[!UICONTROL OK]**」をクリックします。 次のコードを ファイルに追加します。

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

1. `/etc/clientlibs` に移動します。`/etc/clientlibs`サブフォルダーを右クリックし、**[!UICONTROL 作成]****[!UICONTROL ノードを作成]**&#x200B;をクリックします。

   **[!UICONTROL 名前]**&#x200B;フィールドに`WeRetailFormTests`と入力します。 タイプを`cq:ClientLibraryFolder`として選択し、「**[!UICONTROL OK]**」をクリックします。

1. 追加&#x200B;**[!UICONTROL WeRetailFormTests]**&#x200B;ノードに対する次のプロパティです。

   <table>
    <tbody>
     <tr>
      <td><strong>プロパティ</strong></td>
      <td><strong>型</strong></td>
      <td><strong>複数</strong></td>
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
      <td>依存関係</td>
      <td>文字列</td>
      <td>有効</td>
      <td>
       <ul>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     </tbody>
   </table>

1. **[!UICONTROL WeRetailFormTests]**&#x200B;ノードにファイルjs.txtを作成します。 ファイル追加に次の情報が追加されます。

   ```shell
   #base=.
   prefillTest.js
   ```

   「**[!UICONTROL すべて保存]**」をクリックします。

1. **[!UICONTROL WeRetailFormTests]**&#x200B;ノードにファイル`prefillTest.js`を作成します。 追加次のコードをファイルに追加します。 コードはテストケースを作成します。 テストケースでは、フォームのすべてのフィールドに事前入力し、一部のフィールドを検証して、正しい値が入力されていることを確認します。

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

   テストケースが作成され、実行できる状態になります。 テストケースを作成して、計算スクリプトの実行の確認、パターンの検証、アダプティブフォームの送信エクスペリエンスの検証など、アダプティブフォームの様々な要素を検証できます。 アダプティブフォームの様々な側面のテストについて詳しくは、「アダプティブフォームのテストの自動化」を参照してください。

## 手順3:スイートまたは個々のテストケースですべてのテストを実行{#step-run-all-the-tests-in-a-suite-or-individual-tests-cases}

テストスイートには複数のテストケースを含めることができます。 テストスイート内のすべてのテストケースは、一度に実行することも、個別に実行することもできます。 テストを実行すると、アイコンに結果が示されます。

* チェックマークのアイコンは、テストに合格したことを示します。![save_icon](assets/save_icon.svg)
* 「X」アイコンは、失敗したテストを示します。![閉じる —icon](assets/close-icon.svg)

1. AEMアイコン/**[!UICONTROL ツール]****[!UICONTROL 操作]** **[!UICONTROL テスト]**&#x200B;に移動します。
1. テストスイートのすべてのテストを実行するには：

   1. [!UICONTROL テスト]パネルで、**[!UICONTROL We retail - Tests (1)]**&#x200B;をタップします。 スイートが展開され、テストのリストが表示されます。
   1. 「**[!UICONTROL テストを実行]**」ボタンをタップします。 画面の右側の空白の領域は、テストの実行時にアダプティブフォームに置き換えられます。

      ![全試験の](assets/run-all-test.png)

1. テストスイートから1つのテストを実行するには：

   1. テストパネルで、**[!UICONTROL We retail - Tests (1)]**&#x200B;をタップします。 スイートが展開され、テストのリストが表示されます。
   1. 「**[!UICONTROL 事前入力テスト]**」をタップし、「**[!UICONTROL テストを実行]**」ボタンをタップします。 画面の右側の空白の領域は、テストの実行時にアダプティブフォームに置き換えられます。

1. テスト名「Prefill test」をタップして、テストケースの結果を確認します。 [!UICONTROL 結果]パネルが開きます。 [!UICONTROL 結果]パネルでテストケースの名前をタップし、テストのすべての詳細を表示します。

   ![レビュー結果](assets/review-results.png)

これでアダプティブフォームの発行準備が整いました。
