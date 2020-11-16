---
title: Tough Day
seo-title: Tough Day
description: Tough Day テストでは、約 1,000 人の作成者がいる環境で、すべての操作が同時進行しているという最悪の状況を想定して、1 日の負荷をシミュレートします。.
seo-description: 強靱な日のテストは、すべての操作が同時に実行される、最悪の場合に1,000人前後の作成者の日々の負荷をシミュレートします。
uuid: 1b672182-40f5-4580-b038-2e3c8fbfb8b7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: ea6b40fe-b6e1-495c-b34f-8815a4e2e42e
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 53%

---


# Tough Day{#tough-day}

## Tough Day 2 について {#what-is-tough-day}

「Tough Day 2」は、AEM インスタンスの限界についてストレステストを実行するためのアプリケーションです。Tough Day 2 は、デフォルトのテストスイートを使用してそのまま実行することも、テストのニーズに合わせて設定することも可能です。このアプリケーションのプレゼンテーションについては、[こちらの録画](https://docs.adobe.com/ddc/en/gems/Toughday2---A-new-and-improved-stress-testing-and-benchmarking-tool.html)を参照してください。

## How to Run Tough Day 2 {#how-to-run-tough-day}

[アドビのリポジトリ](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/qe/toughday2/)から最新バージョンの Tough Day 2 をダウンロードします。After you download the application, you can run it out of the box by providing the `host` parameter. In the following example, the AEM instance runs locally so the `localhost` value is used:

```xml
java -jar toughday2.jar --host=localhost
```

パラメーターを追加した後に実行されるデフォルトスイートの名前は `toughday` です。このスイートには次のユースケースが含まれています。

* ページとそのページのライブコピーを作成する（ロールアウトを含む）
* ホームページを取得する
* querybuilder でクエリを実行する
* アセット階層を作成する
* アセットの削除

このスイートには、15 ％の書き込みアクションと 85 ％の読み取りアクションが含まれています。

スイートのテストを実行するために、Tough Day 2 によってデフォルトのコンテンツパッケージがインストールされます。This can be avoided by setting the `installsamplecontent`parameter to `false`, but remember that you should also change the default paths for the tests that you intend to run. If the jar is run without parameters, Tough Day 2 displays the [help information](/help/sites-developing/tough-day.md#getting-help).

原則として、アプリケーションを使用するには、次のパターンに従います。

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>Tough Day 2 にはクリーンアップステップが用意されていません。したがって、メインの実稼動インスタンスではなく、クローンされたステージングインスタンスで Tough Day 2 を実行することをお勧めします。ステージングインスタンスは、テスト後に削除する必要があります。


### ヘルプの入手 {#getting-help}

Tough Day 2 には、コマンドラインからアクセスできる幅広いヘルプオプションが用意されています。次に例を示します。

```xml
java -jar toughday2.jar --help_full
```

以下の表に、関連するヘルプパラメーターを示します。

<table>
 <tbody>
  <tr>
   <td><strong>パラメーター</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例</strong></td>
  </tr>
  <tr>
   <td>--help</td>
   <td>グローバル情報を出力します。次に例を示します。使用可能なアクション、定義済みのスイート、実行モード、およびグローバルパラメーター。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_publish</td>
   <td>使用可能なすべての発行者を印刷します。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_tests</td>
   <td>テストクラスとその説明を印刷します。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_full</td>
   <td>上記のすべて、およびテスト、パブリッシャー、スイートのコンポーネントを印刷します。</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;Mode&gt;</td>
   <td>指定した実行モードまたは公開モードに関するリスト情報。</td>
   <td><p>java -jar toughday2.jar —help —runmode type=constantload</p> <p>java -jar toughday2.jar —help —publishmode type=intervals</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;SuiteName&gt;</td>
   <td>特定のスイートのすべてのテストと、それぞれの設定可能なプロパティをリストします。</td>
   <td><br /> java -jar toughday2.jar —help —suite=get_tests</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;タグ&gt;</td>
   <td><br /> 指定したタグを持つすべての項目をリストします。</td>
   <td>java -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td>—help &lt;TestClass/PublisherClass&gt;</td>
   <td><br /> 特定のテストまたはパブリッシャーの設定可能なすべてのプロパティをリストします。</td>
   <td><p>java -jar toughday2.jar —help UploadPDFTest</p> <p>java -jar toughday2.jar —help CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### グローバルパラメーター {#global-parameters}

Tough Day 2 には、テストの環境を設定または変更するグローバルパラメーターが用意されています。これには、ターゲットのホスト、ポート番号、使用されるプロトコル、インスタンスのユーザーとパスワードなどが含まれます。次に例を示します。

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

以下のリストには、関連のあるパラメーターがあります。

| **パラメーター** | **説明** | **デフォルト値** | **可能な値** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | デフォルトのTufg Day 2コンテンツパッケージをインストールまたはスキップします。 | true | true または false |
| `--protocol=<Val>` | ホストに使用するプロトコル。 | http | httpまたはhttps |
| `--host=<Val>` | ターゲットにするホスト名またはIP。 |  |  |
| `--port=<Val>` | ホストのポート。 | 4502 |  |
| `--user=<Val>` | インスタンスのユーザー名。 | admin |  |
| `--password=<Val>` | 指定したユーザーのパスワード。 | admin |  |
| `--duration=<Val>` | テストの期間。 Can be expressed in (**s**)econds, (**m**)inutes, (**h**)ours and (**d**)ays. | 1d |  |
| `--timeout=<Val>` | テストが中断され、失敗とマークされるまでの期間。 秒単位で表現できます。 | 180 |  |
| `--suite=<Val>` | 値は、事前定義済みのテストスイートの1つまたはリスト（コンマ区切り）にすることができます。 | 厳しい日 |  |
| `--configfile=<Val>` | 対象となるyaml設定ファイル。 |  |  |
| `--contextpath=<Val>` | インスタンスのコンテキストパス。 |  |  |
| `--loglevel=<Val>` | Tufg Day 2エンジンのログレベルです。 | INFO | ALL, DEBUG, INFO, WARN, ERROR, FATAL, OFF |
| `--dryrun=<Val>` | trueの場合、結果の設定が出力され、テストは実行されません。 | false | true または false |

## カスタマイズ {#customizing}

カスタマイズの方法には、コマンドラインパラメーターを使用する方法と yaml 設定ファイルを使用する方法の 2 つがあります。**通常、設定ファイルは大規模なカスタムスイートに使用します。設定ファイルは、Tough Day 2 のデフォルトパラメーターよりも優先されます。コマンドラインパラメーターは、設定ファイルとデフォルトパラメーターの両方よりも優先されます。**

テスト設定を保存するには、yaml 形式でコピーする方法しかありません。For additional details, see this [toughday.yaml](https://repo.adobe.com/nexus/service/local/repositories/releases/content/com/adobe/qe/toughday2/0.2.1/toughday2-0.2.1.yaml) configuration and the yaml configuration examples in the sections below.

### 新規テストの追加 {#adding-a-new-test}

デフォルトの `toughday` スイートを使用しない場合は、`add` パラメーターを使用して任意のテストを追加できます。コマンドラインパラメーターまたは yaml 設定ファイルを使用して `CreateAssetTreeTest` テストを追加する方法を以下の例に示します。

コマンドラインパラメーターを使用する場合：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

yaml 設定ファイルを使用する場合：

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### 同じテストの複数のインスタンスの追加  {#adding-multiple-instances-of-the-same-test}

同じテストの複数のインスタンスを追加して実行することもできますが、そのためにはそれぞれのインスタンスに一意の名前を付ける必要があります。次の例では、コマンドラインパラメーターまたはヤム設定ファイルを使用して、同じテストの2つのインスタンスを追加する方法を示します。

コマンドラインパラメーターを使用する場合：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

yaml 設定ファイルを使用する場合：

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
    properties:
      name : FirstAssetTree
  - add : CreateAssetTreeTest
    properties:
      name : SecondAssetTree
```

### テストプロパティの変更 {#changing-the-test-properties}

1 つ以上のテストプロパティを変更する必要がある場合は、そのプロパティをコマンドラインまたは yaml 設定ファイルに追加できます。To see all the available test properties add the `--help <TestClass/PublisherClass>` parameter to the command line, for example:

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

yaml 設定ファイルによって Tough Day 2 のデフォルトのパラメーターが上書きされるので、コマンドラインパラメーターは設定ファイルとデフォルトの両方よりも優先されることに注意してください。

The examples below show how to change the `template` property for the `CreatePageTreeTest` test either by using either command line parameters or a yaml configuration file.

コマンドラインパラメーターを使用する場合：

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

yaml 設定ファイルを使用する場合：

```xml
globals:
  host : localhost
tests:
  - add : CreatePageTreeTest
    properties:
      template : /conf/toughday-templates/settings/wcm/templates/toughday-template
```

### 事前定義済みのテストスイートの使用 {#working-with-predefined-test-suites}

事前定義済みのスイートにテストを追加する方法、事前定義済みのスイートの既存のテストを再設定および除外する方法を以下の例に示します。

事前定義済みのスイートに新しいテストを追加するには、`add` パラメーターを使用して、ターゲットとなる事前定義済みのスイートを指定します。

コマンドラインパラメーターを使用する場合：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

yaml 設定ファイルを使用する場合：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

Existing tests in a given suite can also be reconfigured using the `config`* *parameter. また、（テストクラス名ではなく）スイート名とテストの実際の名前も指定する必要があります。 テスト名は、テストクラスの `name` プロパティで確認できます。テストプロパティの確認方法について詳しくは、[テストプロパティの変更](/help/sites-developing/tough-day.md#changing-the-test-properties)を参照してください。

In the example below the default asset title for the `CreatePageTreeTest` (named `UploadAsset`) is changed to &quot;NewAsset&quot;.

コマンドラインパラメーターを使用する場合：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

yaml 設定ファイルを使用する場合：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset
```

さらに、`exclude` パラメーターを使用して、事前定義済みのスイートからテストを削除したり、デフォルトの設定から公開者を削除したりできます。Please note that you must also specify the suite name and the actual name of the test (not the Test C `lass` name). You can find the test name in the `name` property of the test class. In the example below, the `CreatePageTreeTest` (named `UploadAsset`) test is removed from the toughday suite.

コマンドラインパラメーターを使用する場合：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

yaml 設定ファイルを使用する場合：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset
```

### 実行モード {#run-modes}

Tough Day 2 can run in one of the following modes: **normal** and **constant load**.

The **normal** run mode has two parameters:

* `concurrency` - concurrencyは、Tuff Day 2でテスト実行用に作成されるスレッドの数を表します。 これらのスレッドでは、実行時間が終了するか、実行するテストがなくなるまでテストが実行されます。

* `waittime` - 同じスレッド上の連続した 2 つのテスト実行の間の待機時間。この値はミリ秒単位で指定する必要があります。

次の例は、コマンドラインを使用してパラメーターを追加する方法を示しています。

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

または、yaml 設定ファイルを使用してパラメーターを追加する方法もあります。

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

The **constant load** run mode differs from the normal run mode by generating a constant number of started test executions, rather than a constant number of threads. 読み込みは、同じ名前を持つ実行モードパラメーターを使用して設定できます。

### テストの選択 {#test-selection}

The test selection process is the same for both run modes and it goes as follows: all tests have a `weight` property, which determines the likelihood of execution in a thread. 例えば、テストが 2 つあり、一方の重みを 5、もう一方の重みを 10 とした場合、後者が実行される可能性は前者の 2 倍になります。

Furthermore, tests can have a `count` property, which limits the number of executions to a given number. この回数に達すると、それ以上テストは実行されません。既に実行中のテストインスタンスはすべて、設定されたとおりに実行を終了します。次の例は、コマンドラインまたは yaml 設定ファイルを使用してこれらのパラメーターを追加する方法を示しています。

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest weight=5 --add CreatePageTreeTest weight=10 count=100 --runmode=normal concurrency=20
```

または

```xml
- add : CreateAssetTreeTest
    properties :
      name : UploadAsset
      weight : 5
      base : 3
      foldertitle : IAmAFolder
      assettitle : IAmAnAsset
      count : 100
```

>[!NOTE]
>
>Due to parallel executions, the actual number of test runs will not be exactly the amount configured in the `count` parameter. Expect a deviation proportional to the number of running threads (controlled by the `concurrency parameter`).

### ドライラン {#dry-run}

ドライランでは、指定されたすべての入力（コマンドラインパラメーターまたは設定ファイル）が解析され、デフォルト値と統合された結果が出力されます。テストは実行されません。

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## 出力 {#output}

Tough Day 2 では、テストの指標とログの両方が出力されます。詳しくは、これ以降の項を参照してください。

### テスト指標 {#test-metrics}

現在、Tough Day 2 では、ユーザーが評価できる 9 種類のテスト指標が報告されます。Metrics with the ***** symbol are reported only after successful runs:

| **名前** | **説明** |
|---|---|
| Timestamp | 最後に完了したテストの実行のタイムスタンプ。 |
| 渡された | 成功した実行の数。 |
| 失敗 | 失敗した実行の数。 |
| Min* | テスト実行の最短期間。 |
| Max* | テストの実行期間の上限。 |
| Median* | すべてのテスト実行の計算済み中央値の期間。 |
| 平均* | 計算されたすべてのテスト実行の平均期間。 |
| StdDev* | 標準偏差。 |
| 90p* | 90パーセンタイル。 |
| 99p* | 99パーセンタイル。 |
| 99.9p* | 99.9パーセンタイル。 |
| 実スループット* | 実行回数を経過した実行時間で割った値。 |

These metrics are written with the help of publishers that can be added with the `add` parameter (similarly to adding tests). 現在、次の 2 つのオプションがあります。

* **CSVPublisher** — 出力はCSVファイルです。
* **ConsolePublisher** — 出力はコンソールに表示されます。

デフォルトでは、両方の公開者が有効になっています。

さらに、指標がレポートされるモードは2つあります。

* **単純公開モード** — 実行開始から公開ポイントまでの結果をレポートします。
* The **intervals** publish mode - reports the results in a given time frame. You can set the time frame with the **interval** publish mode parameter.

次の例は、コマンドラインまたは yaml 設定ファイルを使用して `intervals` パラメーターを設定する方法を示しています。

コマンドラインパラメーターを使用する場合：

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s
```

yaml 設定ファイルを使用する場合：

```xml
publishmode:
     type : intervals
     interval : 10s
     tests:
        -add : CreatePageTreeTest
```

### ログ {#logging}

「Tuff Day 2」を選択すると、Tuff Day 2を実行したのと同じディレクトリにlogsフォルダーが作成されます。 このフォルダーには次の 2 種類のログが格納されます。

* **toughday.log**：アプリケーションの状態に関連したメッセージ、デバッグ情報およびグローバルメッセージが格納されます。
* **toughday_&lt;testname>.log**：指定したテストに関連するメッセージ。

ログは上書きされません。その後の実行では、既存のログにメッセージが追加されます。The logs have several levels, for more information see the ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`.

#### 使用例 {#example-usage}

#### 既知の問題 {#known-issues}

[ファイルを入手](assets/toughday-6_1.jar)
