---
title: '"チュートリアル：アダプティブフォームのテスト」'
seo-title: '"チュートリアル：アダプティブフォームのテスト」'
description: 自動テストを使用して、複数のアダプティブフォームを一度にテストします。
seo-description: 自動テストを使用して、複数のアダプティブフォームを一度にテストします。
uuid: 6d182bbc-b47a-4c97-af70-c960b52fdfac
contentOwner: khsingh
discoiquuid: ecddb22e-c148-441f-9088-2e5b35c7021b
docset: aem65
feature: アダプティブフォーム
exl-id: 343e2e0b-d5ef-4f01-b3d6-45f90e2430fd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 11%

---

# チュートリアル：アダプティブフォームのテスト{#tutorial-testing-your-adaptive-form}

![](do-not-localize/10-test-your-adaptive-form.png)

これは、「[最初のアダプティブフォームを作成する](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)」シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

アダプティブフォームの準備が整ったら、アダプティブフォームをエンドユーザーにロールアウトする前にテストすることが重要です。 すべてのフィールドを手動でテスト（機能テスト）したり、アダプティブフォームのテストを自動化したりできます。 複数のアダプティブフォームがある場合、すべてのアダプティブフォームのすべてのフィールドを手動でテストするのは、大変な作業です。

AEM [!DNL Forms]は、アダプティブフォームのテストを自動化するテストフレームワークCalvinを提供します。 このフレームワークを使用して、Web ブラウザーで直接 UI テストを記述して実行します。このフレームワークは、テストを作成するためのJavaScript APIを提供します。 自動テストを使用すると、アダプティブフォームの事前入力エクスペリエンス、アダプティブフォームの送信エクスペリエンス、式ルール、検証、遅延読み込み、UIの操作をテストできます。 このチュートリアルでは、アダプティブフォームで自動化されたテストを作成し、実行する手順について説明します。 このチュートリアルを完了すると、次の操作を実行できるようになります。

* [アダプティブフォームのテストスイートを作成する](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-suite)
* [アダプティブフォームのテストを作成する](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-case-to-prefill-values-in-an-adaptive-form)
* [アダプティブフォーム用に作成されたテストスイートとテストを実行する](#step-run-all-the-tests-in-a-suite-or-individual-tests-cases)

## 手順1:テストスイート{#step-create-a-test-suite}の作成

テストスイートには、テストケースの集まりがあります。 複数のテストスイートを持つことができます。 各フォームに個別のテストスイートを用意することをお勧めします。 テストスイートを作成するには：

1. のAEM [!DNL Forms]オーサーインスタンスに管理者としてログインします。 [!UICONTROL CRXDE Lite]を開きます。 AEMロゴ/**[!UICONTROL ツール]** / **[!UICONTROL 一般]** / **[!UICONTROL CRXDE Lite]**&#x200B;をタップするか、ブラウザーで[https://localhost:4502/crx/de/index.jsp](https://localhost:4502/crx/de/index.jsp) URLを開いてCRXDE Liteを開きます。

1. [!UICONTROL CRXDE Lite]の/etc/clientlibsに移動します。 /etc/clientlibs サブフォルダーを右クリックして、**[!UICONTROL 作成]**／**[!UICONTROL ノードを作成]**&#x200B;をクリックします。「**[!UICONTROL 名前]**」フィールドに、**WeRetailFormTestCases**&#x200B;と入力します。 タイプとして&#x200B;**cq:ClientLibraryFolder**&#x200B;を選択し、「**[!UICONTROL OK]**」をクリックします。 ノードが作成されます。 `WeRetailFormTestCases`の代わりに任意の名前を使用できます。
1. `WeRetailFormTestCases`ノードに次のプロパティを追加し、「**[!UICONTROL すべて保存]**」をタップします。

   <table>
    <tbody>
     <tr>
      <td><strong>プロパティ</strong></td>
      <td><strong>タイプ</strong></td>
      <td><strong>複数</strong></td>
      <td><strong>値</strong></td>
     </tr>
     <tr>
      <td>categories</td>
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

1. **[!UICONTROL WeRetailFormTestCases]**&#x200B;ノードを右クリックし、**[!UICONTROL 作成]** / **[!UICONTROL ファイルを作成]**&#x200B;をクリックします。 「**[!UICONTROL 名前]**」フィールドに「`js.txt`」と入力し、「**[!UICONTROL OK]**」をクリックします。
1. js.txtファイルを編集用に開き、次のコードを追加して、ファイルを保存します。

   ```text
   #base=.
    init.js
   ```

1. `WeRetailFormTestCases`ノードにファイルinit.jsを作成します。 ファイルに以下のコードを追加し、「**[!UICONTROL すべて保存]**」をタップします。

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

   上記のコードは、「 **We retail - Tests** 」という名前のテストスイートを作成します。

1. AEMテストUIを開きます(AEM > **[!UICONTROL ツール]** > **[!UICONTROL 操作]** > **[!UICONTROL テスト]**)。 テストスイート&#x200B;**We retail(Tests**)がUIに表示されます。

   ![we-retail-test-suite](assets/we-retail-test-suite.png)

## 手順2:アダプティブフォーム{#step-create-a-test-case-to-prefill-values-in-an-adaptive-form}に事前に値を入力するテストケースを作成する

テストケースは、特定の機能をテストするための一連のアクションです。 例えば、フォームのすべてのフィールドの事前入力や、正しい値が入力されていることを確認するためのいくつかのフィールドの検証を行います。

アクションとは、アダプティブフォーム上の特定のアクティビティのことで、ボタンのクリックなどを指します。 各アダプティブフォームフィールドのユーザー入力を検証するテストケースとアクションを作成するには：

1. [!UICONTROL CRXDE lite]で、`/content/forms/af/create-first-adaptive-form`フォルダーに移動します。 **[!UICONTROL create-first-adaptive-form]**&#x200B;フォルダーノードを右クリックし、**[!UICONTROL 作成]** **[!UICONTROL ファイルを作成]**&#x200B;をクリックします。 「**[!UICONTROL 名前]**」フィールドに「`prefill.xml`」と入力し、「**[!UICONTROL OK]**」をクリックします。 次のコードをファイルに追加しました。

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

1. `/etc/clientlibs` に移動します。`/etc/clientlibs`サブフォルダーを右クリックし、「**[!UICONTROL 作成]****[!UICONTROL ノードを作成]**」をクリックします。

   「**[!UICONTROL 名前]**」フィールドに`WeRetailFormTests`と入力します。 タイプを「`cq:ClientLibraryFolder`」と選択し、「**[!UICONTROL OK]**」をクリックします。

1. **[!UICONTROL WeRetailFormTests]**&#x200B;ノードに次のプロパティを追加します。

   <table>
    <tbody>
     <tr>
      <td><strong>プロパティ</strong></td>
      <td><strong>タイプ</strong></td>
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
      <td>dependencies</td>
      <td>文字列</td>
      <td>有効</td>
      <td>
       <ul>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     </tbody>
   </table>

1. **[!UICONTROL WeRetailFormTests]**&#x200B;ノードにjs.txtというファイルを作成します。 ファイルに以下を追加します。

   ```shell
   #base=.
   prefillTest.js
   ```

   「**[!UICONTROL すべて保存]**」をクリックします。

1. **[!UICONTROL WeRetailFormTests]**&#x200B;ノードに`prefillTest.js`ファイルを作成します。 以下のコードをファイルに追加します。 コードはテストケースを作成します。 テストケースでは、フォームのすべてのフィールドが事前に入力され、正しい値が入力されていることを確認するために一部のフィールドが検証されます。

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

   テストケースが作成され、実行する準備が整いました。 テストケースを作成して、計算スクリプトの実行確認、パターンの検証、アダプティブフォームの送信操作の検証など、アダプティブフォームの様々な側面を検証することができます。 アダプティブフォームのテストの様々な側面について詳しくは、「アダプティブフォームの自動テスト」を参照してください。

## 手順3:スイート内のすべてのテストまたは個々のテストケースを実行します。 {#step-run-all-the-tests-in-a-suite-or-individual-tests-cases}

テストスイートには複数のテストケースを含めることができます。 テストスイート内のすべてのテストケースは、一度に、または個別に実行できます。 テストを実行すると、結果が次のアイコンで示されます。

* チェックマークアイコンは、合格したテストを示します。![save_icon](assets/save_icon.svg)
* 「X」アイコンは、失敗したテストを示します。![close-icon](assets/close-icon.svg)

1. AEMアイコン/ **[!UICONTROL ツール]**> **[!UICONTROL 操作]** **[!UICONTROL テスト]**&#x200B;に移動します。
1. テストスイートのすべてのテストを実行するには：

   1. [!UICONTROL Tests]パネルで、**[!UICONTROL We retail - Tests (1)]**&#x200B;をタップします。 テストスイートが展開され、テストのリストが表示されます。
   1. 「**[!UICONTROL テストを実行]**」ボタンをタップします。 テストを実行すると、画面の右側の空白の領域がアダプティブフォームに置き換えられます。

      ![ランオールテスト](assets/run-all-test.png)

1. テストスイートから1つのテストを実行するには：

   1. テストパネルで、「 **[!UICONTROL We retail - Tests (1)]** 」をタップします。 テストスイートが展開され、テストのリストが表示されます。
   1. 「**[!UICONTROL 事前入力テスト]**」をタップし、「**[!UICONTROL テストを実行]**」ボタンをタップします。 テストを実行すると、画面の右側の空白の領域がアダプティブフォームに置き換えられます。

1. テスト名「事前入力テスト」をタップして、テストケースの結果を確認します。 [!UICONTROL 結果]パネルが開きます。 [!UICONTROL 結果]パネルでテストケースの名前をタップし、テストの詳細をすべて表示します。

   ![review-results](assets/review-results.png)

これで、アダプティブフォームの発行準備が整いました。
