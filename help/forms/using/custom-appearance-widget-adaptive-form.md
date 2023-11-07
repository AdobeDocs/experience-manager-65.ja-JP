---
title: アダプティブフォームフィールドのカスタム外観の作成
description: Adaptive Formsの標準搭載コンポーネントの外観をカスタマイズします。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 770e257a-9ffd-46a4-9703-ff017ce9caed
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1712'
ht-degree: 67%

---

# アダプティブフォームフィールドのカスタム外観の作成 {#create-custom-appearances-for-adaptive-form-fields}

## 概要 {#introduction}

アダプティブフォームは、 [外観フレームワーク](/help/forms/using/introduction-widgets.md) アダプティブフォームフィールドのカスタム外観を作成し、異なるユーザーエクスペリエンスを提供するのに役立ちます。 たとえば、ラジオボタンとチェックボックスをトグルボタンで置き換える、またはカスタムの jQuery プラグインを使用して、電話番号やメール ID といったフィールドにおけるユーザーの入力を制限するなどです。

このドキュメントでは、jQuery プラグインを使用して、アダプティブフォームフィールド用にこれらの代替エクスペリエンスを作成する方法を説明します。 さらに、数値フィールドコンポーネントが数値ステッパーまたはスライダーとして表示されるカスタム外観を作成する例を示します。

まず、この記事で使用される主な用語と概念について見てみましょう。

**アピアランス**：アダプティブフォームフィールドの様々な要素のスタイル、ルックアンドフィール、編成です。通常、ラベル、入力用のインタラクティブ領域、ヘルプアイコン、フィールドの短い説明や長い説明が含まれます。 この記事で説明する外観のカスタマイズは、フィールドの入力領域の外観に適用できます。

**jQuery プラグイン**：jQuery ウィジェットのフレームワークに基づいた、代替のアピアランスを実装するための標準的なメカニズムを提供します。

**ClientLib**：複雑な JavaScript と CSS コードにより駆動する AEM のクライアント側プロセスのライブラリシステムです。詳しくは、「クライアント側ライブラリの使用」を参照してください。

**アーキタイプ**：Maven プロジェクトのオリジナルパターンまたはモデルとして定義される Maven プロジェクトテンプレートツールキットです。詳しくは、「アーキタイプの概要」を参照してください。

**ユーザーコントロール**：フィールドの値を含み、カスタムのウィジェット UI をアダプティブフォームモデルとバインドするためのアピアランスフレームワークで使用される、ウィジェットの主な要素です。

## カスタム外観を作成する手順 {#steps-to-create-a-custom-appearance}

カスタム外観を作成する手順は、大まかに次のとおりです。

1. **プロジェクトを作成する**：AEM でデプロイするコンテンツパッケージを生成する Maven プロジェクトを作成します。
1. **既存の Widget クラスを拡張する**：既存の Widget クラスを拡張して必要なクラスをオーバーライドします。
1. **クライアントライブラリを作成する**：`clientLib: af.customwidget` ライブラリを作成して、必要な JavaScript と CSS ファイルを追加します。

1. **プロジェクトを構築してインストールする**：Maven プロジェクトを構築して、生成したコンテンツパッケージをAEM にインストールします。
1. **アダプティブフォームを更新する**：アダプティブフォームフィールドのプロパティを更新して、カスタムアピアランスを使用します。

### プロジェクトの作成 {#create-a-project}

Maven アーキタイプは、カスタム外観を作成するための出発点です。 使用するアーキタイプの詳細を次に示します。

* **リポジトリー**：https://repo1.maven.org/maven2/com/adobe/
* **アーティファクト ID**：カスタムアピアランスのアーキタイプ
* **グループ ID**：com.adobe.aemforms
* **バージョン**：1.0.4

次のコマンドを実行して、アーキタイプに基づいたローカルプロジェクトを作成します。

`mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

このコマンドは、Maven プラグインとアーキタイプの情報をリポジトリからダウンロードし、次の情報に基づいてプロジェクトを生成します。

* **groupId**：生成された Maven プロジェクトで使用されるグループ ID。
* **artifactId**：生成された Maven プロジェクトで使用されるアーティファクト ID。
* **version**：生成された Maven プロジェクトのバージョン。
* **パッケージ**：ファイル構造に使用するパッケージ。
* **artifactName**：生成されたAEMパッケージのアーティファクト名。
* **packageGroup**：生成されたAEMパッケージのパッケージグループ。
* **widgetName**：参照に使用される外観名。

生成されたプロジェクトの構造は次のようになります。

```java
─<artifactId>

 └───src

     └───main

         └───content

             └───jcr_root

                 └───etc

                     └───clientlibs

                         └───custom

                             └───<widgetName>

                                 ├───common [client library - af.customwidgets which encapsulates below clientLibs]

                                 ├───integration [client library - af.customwidgets.<widgetName>_widget which contains template files for integrating a third-party plugin with Adaptive Forms]

                                 │   ├───css

                                 │   └───javascript

                                 └───jqueryplugin [client library - af.customwidgets.<widgetName>_plugin which holds the third-party plugins and related dependencies]

                                     ├───css

                                     └───javascript
```

### 既存のウィジェットクラスの拡張 {#extend-an-existing-widget-class}

プロジェクトテンプレートを作成したら、必要に応じて次の変更を行います。

1. サードパーティのプラグインの依存関係をプロジェクトに含めます。

   1. サードパーティまたはカスタムの jQuery プラグインを `jqueryplugin/javascript` フォルダーに入れ、関連する CSS ファイルを `jqueryplugin/css` フォルダーに入れます。詳しくは、`jqueryplugin/javascript and jqueryplugin/css` フォルダーの JS ファイルと CSS ファイルを参照してください。

   1. `js.txt` および `css.txt` ファイルを変更して、jQuery プラグインの追加の JavaScript ファイルと CSS ファイルが含まれるようにします。

1. フレームワーク内でサードパーティのプラグインを統合して、カスタム外観のフレームワークと jQuery プラグインとのインタラクションを有効にします。新しいウィジェットは、次の関数を拡張またはオーバーライドした後にのみ機能するようになります。

<table>
 <tbody>
  <tr>
   <td><strong>関数</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>レンダリング関数は、ウィジェットのデフォルトのHTML要素に対する jQuery オブジェクトを返します。 デフォルトのHTML要素は、フォーカス可能なタイプである必要があります。 例えば、<code>&lt;a&gt;</code>、<code>&lt;input&gt;</code>、<code>&lt;li&gt;</code> です。返された要素は <code>$userControl</code> として使用されます。<code>$userControl</code> で上記の制約を指定する場合、<code>AbstractWidget</code> クラスの関数は問題なく機能します。そうでない場合、一部の一般的な API （フォーカス、クリック）の変更が必要です。 </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>HTML イベントを XFA イベントに変換するマップを返します。<br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> この例は、<code>blur</code> が HTML イベントであり、<code>XFA_EXIT_EVENT</code> が対応する XFA イベントであることを示しています。 </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>オプションの変更時に、実行すべきアクションの詳細を提供するマップを返します。キーはウィジェットに提供されるオプションです。値はそのオプションの変更が検出されたときに毎回呼び出される関数です。ウィジェットには、すべての一般的なオプション（<code>value</code> と <code>displayValue</code> を除く）のハンドラーが用意されています。</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>jQuery ウィジェットフレームワークは、jQuery ウィジェットの値が XFA モデルに保存されるたび（例えば、テキストフィールドの exit イベント時）に、常にこの関数を読み込みます。 実装は、ウィジェットに保存された値を返す必要があります。ハンドラーには、オプションの新しい値が与えられます。</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>デフォルトでは、XFA での enter イベント時に、フィールドの <code>rawValue</code> が表示されます。この関数が呼び出されて、<code>rawValue</code> がユーザーに表示されます。 </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>デフォルトでは、XFA での exit イベント時に、フィールドの <code>formattedValue</code> が表示されます。この関数が呼び出されて、<code>formattedValue</code> がユーザーに表示されます。 </td>
  </tr>
 </tbody>
</table>

1. 必要に応じて `integration/javascript` フォルダーの JavaScript ファイルを更新します。

   * テキスト `__widgetName__` を実際のウィジェットの名前に置き換えます。
   * 適切な標準のウィジェットクラスからウィジェットを拡張します。 ほとんどの場合、置き換えられる既存のウィジェットに対応するウィジェットクラスです。 親クラス名は複数の場所で使用されるため、ファイル内すべての文字列 `xfaWidget.textField` のインスタンスを検索して、実際使用する親クラスで置き換えることを推奨します。
   * `render` メソッドを拡張して代替の UI を設定します。その場所から jQuery プラグインが起動し、UI またはインタラクション動作を更新します。`render` メソッドは、ユーザーコントロール要素を返します。

   * `getOptionsMap` メソッドを拡張して、ウィジェット内の変更により影響を受けるオプション設定をオーバーライドします。この機能は、オプションの変更時に実行すべきアクションの詳細を提供するマッピングを返します。キーはウィジェットに提供されるオプションです。値はそのオプションの変更が検出されたときに毎回呼び出される関数です。
   * `getEventMap` メソッドは、そのウィジェットによりトリガーされるイベントを、アダプティブフォームモデルが必要とするイベントとあわせてマッピングします。デフォルト値ではデフォルトのウィジェットの標準 HTML イベントがマッピングされ、代替のイベントがトリガーされる場合は更新の必要があります。
   * `showDisplayValue` および `showValue` は、表示値を適用し、パターン形式文字列を編集します。また、別の動作にオーバーライドすることができます。

   * `getCommitValue` メソッドは `commit` イベント発生時にアダプティブフォームのフレームワークにより呼び出されます。一般に、これは exit イベントです（変更時に発生するドロップダウン、ラジオボタン、チェックボックス要素を除く）。 詳しくは、 [アダプティブForms式](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p).

   * テンプレートファイルは、様々なメソッドの実装例を提供します。 拡張しないメソッドを削除します。

### クライアントライブラリの作成 {#create-a-client-library}

Maven アーキタイプで生成されたサンプルプロジェクトは、必要なクライアントライブラリを自動で作成し、`af.customwidgets` カテゴリでそれらをクライアントライブラリに含めます。`af.customwidgets` で使用できる JavaScript および CSS ファイルは実行時に自動で含まれます。

### ビルドとインストール {#build-and-install}

プロジェクトをビルドするには、シェルで次のコマンドを実行して、AEMサーバーにインストールする必要のある CRX パッケージを生成します。

`mvn clean install`

>[!NOTE]
>
>Maven プロジェクトは、POM ファイル内のリモートリポジトリを参照します。これは単に参照目的であり、Maven 標準では、リポジトリ情報は `settings.xml` ファイルで取得されます。

### アダプティブフォームを更新する {#update-the-adaptive-form}

アダプティブフォームフィールドにカスタム外観を適用するには、次の手順を実行します。

1. アダプティブフォームを編集モードで開きます。
1. を開きます。 **プロパティ** カスタム外観を適用するフィールド用のダイアログ。
1. 「**スタイル設定**」タブで、`CSS class` プロパティを更新して `widget_<widgetName>` フォーマットにアピアランスの名前を追加します。例： **widget_numericstepper**

## 例：カスタム外観の作成   {#sample-create-a-custom-appearance-nbsp}

次に、数値フィールドが数値ステッパーまたはスライダーとして表示されるように、カスタムの外観を作成する例を見てみましょう。 以下の手順を実行します。

1. 次のコマンドを実行して、Maven アーキタイプに基づくローカルプロジェクトを作成します。

   `mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   ここでは、次のパラメーターの値の指定が求められます。
   *このサンプルで使用される値は、太字でハイライト表示されています*。

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. `customWidgets` （`artifactID` プロパティで指定された値）ディレクトリに移動して、次のコマンドを実行し Eclipse プロジェクトを生成します。

   `mvn eclipse:eclipse`

1. Eclipse ツールを開き、以下の手順を実行して Eclipse プロジェクトをインポートします。

   1. **[!UICONTROL ファイル／取り込み／既存プロジェクトをワークスペースへ]**&#x200B;を選択します。

   1. 参照して、`archetype:generate` コマンドを実行したフォルダを選択します。

   1. 「**[!UICONTROL Finish]**」をクリックします。

      ![eclipse-screenshot](assets/eclipse-screenshot.png)

1. カスタム外観に使用するウィジェットを選択します。 この例では、次の数値ステッパーウィジェットを使用しています。

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   Eclipse プロジェクトでは、`plugin.js` ファイルのプラグインコードを見直して、外観の要件を満たすようにします。このサンプルでは、外観は以下の要件を満たしています。

   * 数値ステッパーが `- $.xfaWidget.numericInput` から拡張します。
   * フィールドにフォーカスすると、ウィジェットの `set value` メソッドが値を設定します。これは、アダプティブフォームウィジェットでは必須要件です。
   * `bootstrapNumber` メソッドを起動するには、`render` メソッドをオーバーライドする必要があります。

   * プラグインのメインソースコード以外のプラグインに対する追加の依存関係はありません。
   * このサンプルはステッパーでスタイルを実行しないので、追加の CSS は必要ありません。
   * `$userControl` オブジェクトは、`render` メソッドで使用可能です。これは、`text` タイプのフィールドであり、プラグインコードで複製されます。

   * フィールドが無効の場合に「**+**」および「**-**」ボタンが無効になります。

1. `bootstrap-number-input.js`（jQuery プラグイン）のコンテンツを `numericStepper-plugin.js` ファイルのコンテンツに置き換えます。
1. `numericStepper-widget.js` ファイルで、以下のコードを追加して、プラグインを起動するレンダリングメソッドをオーバーライドし、`$userControl` オブジェクトを返します。

   ```javascript
   render : function() {
        var control = $.xfaWidget.numericInput.prototype.render.apply(this, arguments);
        var $control = $(control);
        var controlObject;
        try{
            if($control){
            $control.bootstrapNumber();
            var id = $control.attr("id");
            controlObject = $("#"+id);
            }
        }catch (exc){
             console.log(exc);
        }
        return controlObject;
   }
   ```

1. `numericStepper-widget.js` ファイルで、`getOptionsMap` プロパティをオーバーライドしてアクセスオプションを上書きし、無効モードで「+」および 「-」ボタンを非表示にします。

   ```javascript
   getOptionsMap: function(){
       var parentOptionsMap = $.xfaWidget.numericInput.prototype.getOptionsMap.apply(this,arguments),
   
       newMap = $.extend({},parentOptionsMap,
   
        {
   
              "access": function(val) {
              switch(val) {
                 case "open" :
                   this.$userControl.removeAttr("readOnly");
                   this.$userControl.removeAttr("aria-readonly");
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
                 case "nonInteractive" :
                 case "protected" :
                   this.$userControl.attr("disabled", "disabled");
                   this.$userControl.attr("aria-disabled", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
                case "readOnly" :
                   this.$userControl.attr("readOnly", "readOnly");
                   this.$userControl.attr("aria-readonly", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
               default :
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
             }
          },
      });
      return newMap;
    }
   ```

1. 変更を保存し、`pom.xml` ファイルを含むフォルダーに移動したら、次の Maven コマンドを実行してプロジェクトを構築します。

   `mvn clean install`

1. AEM パッケージマネージャーを使ってパッケージをインストールします。

1. カスタム外観を適用するアダプティブフォームを編集モードで開き、次の手順を実行します。

   1. カスタム外観を適用するフィールドを右クリックしてから、「**[!UICONTROL 編集]**」をクリックしてコンポーネントを編集ダイアログを開きます。

   1. 「スタイル設定」タブで、**[!UICONTROL CSS クラス]** プロパティを更新して `widget_numericStepper` を追加します。

作成した新しい外観を使用できるようになりました。
