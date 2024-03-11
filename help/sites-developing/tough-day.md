---
title: タフデイ
description: タフデイテストでは、すべての操作が同時に進行する最悪のシナリオで、約 1,000 人の作成者による 1 日の負荷をシミュレートします。
topic-tags: testing
content-type: reference
exl-id: ceb9671c-57f9-4d81-94c0-0dbccd4d90a2
source-git-commit: f349c8fd9c370ba589d217cd3b1d0521ae5c5597
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 97%

---

# Tough Day{#tough-day}

## タフデイ 2 について {#what-is-tough-day}

「Tough Day 2」は、AEMインスタンスの制限に応じてテストできるアプリケーションです。 デフォルトのテストスイートを使用して出荷時の設定のまま実行することも、テストのニーズに合わせて設定することもできます。このアプリケーションのプレゼンテーションについては、[こちらの録画](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2017/aem-toughday2-stress-testing-benchmarking-tool.html?lang=ja)を参照してください。

>[!CAUTION]
>
>タフデイ 2 には Java™ 8 が必要です。

## Tough Day 2 の実行方法 {#how-to-run-tough-day}

[アドビのリポジトリ](https://repo1.maven.org/maven2/com/adobe/qe/toughday2/)から最新バージョンの Tough Day 2 をダウンロードします。アプリケーションをダウンロードしたら、`host` パラメーターを指定することでアプリケーションをそのまま実行できます。次の例では、AEM インスタンスがローカルで実行されているので、値 `localhost` が使用されています。

```xml
java -jar toughday2.jar --host=localhost
```

パラメーターを追加した後に実行されるデフォルトスイートの名前は `toughday` です。以下のユースケースが含まれます。

* ページとそのページのライブコピーを作成（ロールアウトを含む）
* ホームページを取得
* QueryBuilder でクエリを実行
* アセット階層を作成
* アセットの削除

このスイートには、15 % の書き込みアクションと 85 % の読み取りアクションが含まれています。

スイートのテストを実行するために、Tough Day 2 によってデフォルトのコンテンツパッケージがインストールされます。この動作は`installsamplecontent`パラメーターを`false`に設定することで回避できます。ただし、実行するテストのデフォルトパスを変更することも必要になります。パラメーターを指定せずに jar を実行した場合は、Tough Day 2 で[ヘルプ情報](/help/sites-developing/tough-day.md#getting-help)が表示されます。

原則として、アプリケーションを使用するには、次のパターンに従います。

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>タフデイ 2 にはクリーンアップ手順がありません。そのため、タフデイ 2 は、メインの実稼動インスタンスではなく、複製したステージングのインスタンスで実行することをお勧めします。ステージングインスタンスは、テスト後に削除する必要があります。
>

### ヘルプの表示 {#getting-help}

タフデイ 2 には、コマンドラインからアクセスできる幅広いヘルプオプションが用意されています。例：

```xml
java -jar toughday2.jar --help_full
```

次の表に、関連するヘルプパラメーターを示します。

<table>
 <tbody>
  <tr>
   <td><strong>パラメーター</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例</strong></td>
  </tr>
  <tr>
   <td>--help</td>
   <td>グローバルな情報を出力します。例えば、利用可能なアクション、事前定義済みスイート、実行モード、グローバルパラメーターなどです。</td>
   <td> </td>
  </tr>
  <tr>
   <td>--help_publish</td>
   <td>利用可能なすべてのパブリッシャーを出力します。</td>
   <td> </td>
  </tr>
  <tr>
   <td>--help_tests</td>
   <td>テストクラスとその説明を出力します。</td>
   <td> </td>
  </tr>
  <tr>
   <td>--help_full</td>
   <td>上記のすべてを出力し、さらに、テスト、パブリッシャー、スイートコンポーネントを出力します。</td>
   <td> </td>
  </tr>
  <tr>
   <td> --help --runmode/publishmode type=&lt;Mode&gt;</td>
   <td>指定した実行またはパブリッシュモードに関する情報を一覧表示します。</td>
   <td><p>Java™ -jar toughday2.jar --help --runmode type=constantload</p> <p>Java™ -jar toughday2.jar --help --publishmode type=intervals</p> </td>
  </tr>
  <tr>
   <td>--help --suite=&lt;SuiteName&gt;</td>
   <td>特定のスイートのすべてのテストと、それぞれの設定可能なプロパティを一覧表示します。</td>
   <td><br /> Java™ -jar toughday2.jar --help --suite=get_tests</td>
  </tr>
  <tr>
   <td> --help --tag=&lt;Tag&gt;</td>
   <td><br /> 指定したタグを持つすべての項目を一覧表示します。</td>
   <td>Java™ -jar toughday2.jar --help --tag=publish</td>
  </tr>
  <tr>
   <td>--help &lt;TestClass/PublisherClass&gt;</td>
   <td><br /> 特定のテストまたはパブリッシャーの設定可能なプロパティをすべて一覧表示します。</td>
   <td><p>Java™ -jar toughday2.jar --help UploadPDFTest</p> <p>Java™ -jar toughday2.jar --help CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### グローバルパラメーター {#global-parameters}

タフデイ 2 では、テストの環境を設定または変更するグローバルパラメーターを提供します。これには、ターゲットとなるホスト、ポート番号、使用するプロトコル、インスタンスのユーザーとパスワードなどが含まれます。例：

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

次のリストに、関連するパラメーターを表します。

| **パラメーター** | **説明** | **デフォルト値** | **可能な値** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | デフォルトの Tough Day 2 コンテンツパッケージをインストールまたはスキップします。 | true | true または false |
| `--protocol=<Val>` | ホストに使用するプロトコル。 | http | http または https |
| `--host=<Val>` | ターゲットにするホスト名または IP。 |  |  |
| `--port=<Val>` | ホストのポート。 | 4502 |  |
| `--user=<Val>` | インスタンスのユーザー名。 | admin |  |
| `--password=<Val>` | 指定されたユーザーのパスワード。 | admin |  |
| `--duration=<Val>` | テストの期間。で表すことができます。 **s**&#x200B;秒 **m**&#x200B;分 **h**&#x200B;我々の **d** ays. | 1d |  |
| `--timeout=<Val>` | テストが中断され、失敗としてマークされるまでのテストの実行時間。秒単位で表現できます。 | 180 |  |
| `--suite=<Val>` | 値は、事前定義済みのテストスイートの 1 つまたはリスト（コンマ区切り）にすることができます。 | toughday |  |
| `--configfile=<Val>` | ターゲットの yaml 設定ファイル。 |  |  |
| `--contextpath=<Val>` | インスタンスのコンテキストパス。 |  |  |
| `--loglevel=<Val>` | Tough Day 2 エンジンのログレベル。 | INFO | ALL、DEBUG、INFO、WARN、ERROR、FATAL、OFF |
| `--dryrun=<Val>` | true の場合は、結果の設定が出力され、テストは実行されません。 | false | true または false |

## カスタマイズ {#customizing}

カスタマイズは、コマンドラインパラメーターと yaml 設定ファイルの 2 つの方法で実行できます。**設定ファイルは大規模なカスタムスイートで使用され、タフデイ 2 のデフォルトパラメーターを上書きします。コマンドラインパラメーターは、設定ファイルとデフォルトのパラメーターの両方を上書きします。**

テスト設定を保存するには、yaml 形式でコピーする方法しかありません。

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

同じテストの複数のインスタンスを追加して実行することもできますが、各インスタンスに一意の名前を付ける必要があります。コマンドラインパラメーターまたは yaml 設定ファイルを使用して同じテストのインスタンスを 2 つ追加する方法を以下の例に示します。

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

1 つまたは複数のテストプロパティを変更する必要がある場合は、そのプロパティをコマンドラインまたは yaml 設定ファイルに追加できます。使用可能なすべてのテストプロパティを表示するには、コマンドラインに `--help <TestClass/PublisherClass>` パラメーターを追加してください。次に例を示します。

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

yaml 設定ファイルによってタフデイ 2 のデフォルトパラメーターが上書きされるので、コマンドラインパラメーターが設定ファイルとデフォルトの両方を上書きすることに注意が必要です。

コマンドラインパラメーターまたは yaml 設定ファイルを使用して `CreatePageTreeTest` テストの `template` プロパティを変更する方法を以下の例に示します。

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

### 定義済みのテストスイートの使用 {#working-with-predefined-test-suites}

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

また、特定のスイート内の既存のテストは、`config`* *パラメーターを使用して再設定することもできます。スイート名と（テストクラス名ではなく）テストの実際の名前も指定します。テスト名は、テストクラスの `name` プロパティで確認できます。テストプロパティの確認方法について詳しくは、[テストプロパティの変更](/help/sites-developing/tough-day.md#changing-the-test-properties)を参照してください。

以下の例では0、`CreatePageTreeTest` のデフォルトのアセットタイトル（名前は `UploadAsset`）を「NewAsset」に変更しています。

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

また、`exclude` パラメーターを使用して、事前に定義されたスイートからテストを削除したり、デフォルト設定から発行者を削除したりすることもできます。スイート名と（Test C `lass` 名ではなく）テストの実際の名前も指定します。テスト名は、テストクラスの `name` プロパティで確認できます。以下の例では、（`UploadAsset` という名前の）`CreatePageTreeTest` テストを toughday スイートから削除しています。

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

Tough Day 2 は、**標準**&#x200B;モードと&#x200B;**定負荷**&#x200B;モードのいずれかで実行できます。

**標準**&#x200B;実行モードには、次の 2 つのパラメーターがあります。

* `concurrency` - テストの実行のために Tough Day 2 によって作成されるスレッドの数を表します。これらのスレッドでは、実行時間が終了するか、実行するテストがなくなるまでテストが実行されます。

* `waittime` - 同じスレッド上の連続した 2 つのテスト実行の間の待機時間。値はミリ秒単位で表記する必要があります。

次の例に、コマンドライン、

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

または yaml 設定ファイルを使用してパラメーターを追加する方法を示します。

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

**定負荷**&#x200B;実行モードは、通常実行モードとは異なり、一定数のスレッドではなく一定数の開始されたテスト実行を生成します。同じ名前の実行モードパラメーターを使用して負荷を設定できます。

### テストの選択 {#test-selection}

テストの選択プロセスはどちらの実行モードでも同じで、次のように進みます。すべてのテストには `weight` プロパティがあり、これによって、スレッドでの実行の可能性が決定します。例えば、テストが 2 つあり、一方の重み付けを 5、もう一方の重み付けを 10 とした場合、後者が実行される可能性は前者の 2 倍になります。

さらに、テストには `count` プロパティを指定できます。これにより、実行回数が指定の数に制限されます。この回数に達すると、それ以上テストは実行されません。既に実行中のすべてのテストインスタンスは、設定どおりに実行を終了します。次の例に、コマンドラインに対して、または yaml 設定ファイルを使用して、これらのパラメーターを追加する方法を示します。

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
>並列実行が原因で、実際のテスト実行回数は `count` パラメーターで設定された数と正確に一致しません。偏差が（`concurrency parameter` パラメーターによって制御される）実行スレッドの数に比例することを想定してください。

### ドライラン {#dry-run}

ドライランでは、指定されたすべての入力（コマンドラインパラメーターまたは設定ファイル）を解析し、デフォルト値と統合して、結果を出力します。テストは一切実行されません。

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## 出力 {#output}

Tough Day 2 は、テスト指標とログの両方を出力します。詳しくは、次の節を参照してください。

### テスト指標 {#test-metrics}

Tough Day 2 では現在、評価できる 9 つのテスト指標がレポートされます。**&#42;** 記号が付いた指標は、実行に成功した後にのみ報告されます。

| **名前** | **説明** |
|---|---|
| Timestamp | 最後に完了したテスト実行のタイムスタンプ。 |
| 渡された | 成功した実行の数。 |
| 失敗 | 失敗した実行の数。 |
| Min&#42; | テスト実行の最短期間。 |
| Max&#42; | テスト実行の最長期間。 |
| Median&#42; | すべてのテスト実行の算出された中央値時間。 |
| 平均&#42; | すべてのテスト実行の算出された平均時間。 |
| StdDev&#42; | 標準偏差。 |
| 90p&#42; | 90 パーセンタイル。 |
| 99p&#42; | 99 パーセンタイル。 |
| 99.9p&#42; | 99.9 パーセンタイル。 |
| 実際のスループット&#42; | 実行数を経過した実行時間で割った値。 |

これらの指標は、（テストの追加と同様に）`add` パラメーターを使用して追加できる公開者を利用して記述されています。現在、次の 2 つのオプションがあります。

* **CSVPublisher** - CSV ファイルを出力します。
* **ConsolePublisher** - 出力はコンソールに表示されます。

デフォルトでは、両方の公開者が有効になっています。

さらに、指標の報告には次の 2 つのモードがあります。

* **simple** パブリッシュモード - 実行の開始から公開時点までの結果が報告されます。
* **intervals** パブリッシュモード - 特定の期間内の結果が報告されます。期間は、**interval** パブリッシュモード／パラメーターを使用して設定することができます。

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

Tough Day 2 では、Tough Day 2 を実行したディレクトリにログフォルダーが作成されます。このフォルダーには次の 2 種類のログが含まれます。

* **toughday.log**：アプリケーションの状態、デバッグ情報およびグローバルメッセージに関連するメッセージが含まれます。
* **toughday_&lt;testname>.log**：指定したテストに関連するメッセージ。

ログは上書きされません。その後の実行では、既存のログにメッセージが追加されます。ログには複数のレベルがあります。詳しくは、 [loglevel パラメーター。](#global-parameters).

<!--
#### Example Usage {#example-usage}

#### Known Issues {#known-issues}

[Get File](assets/toughday-6_1.jar)
-->
