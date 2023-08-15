---
title: AEM Forms の監視フォルダー
seo-title: Watched folder in AEM Forms
description: 管理者は、監視フォルダーを配置し、監視対象のフォルダーにファイルが配置されたときに、ワークフロー、サービス、またはスクリプト操作を開始できます。
seo-description: An administrator can put a folder on watch and start a workflow, service, or script operation when a file is placed in the folder being watched.
uuid: 39eac0fd-8212-46ff-b75d-8b4320d448a9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: db38972c-be3f-49fd-8cc1-45b16ed244af
docset: aem65
exl-id: fbf5c7c3-cb01-4fda-8e5d-11d56792d4bf
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '7148'
ht-degree: 25%

---

# AEM Forms の監視フォルダー{#watched-folder-in-aem-forms}

管理者は、監視PDFーと呼ばれるネットワークフォルダーを設定し、ユーザーがファイル（監視フォルダーなど）を監視フォルダーに配置すると、事前に設定されたワークフロー、サービス、スクリプトの操作が開始され、追加されたファイルが処理されます。 指定した操作を実行した後、指定した出力フォルダーに結果ファイルを保存します。 ワークフロー、サービス、スクリプトについて詳しくは、 [様々なファイル処理方法](#variousmethodsforprocessingfiles).

## 監視フォルダーの作成 {#create-a-watched-folder}

次のいずれかの方法を使用して、ファイルシステム上に監視フォルダーを作成できます。

* 監視フォルダー設定ノードのプロパティの設定中に、親ディレクトリのフルパスを folderPath プロパテイに入力し、作成する監視フォルダーの名前を追加します（例：`C:/MyPDFs/MyWatchedFolder`）。
`MyWatchedFolder` フォルダーが存在しない場合、AEM Forms は指定したパスでフォルダーの作成を試みます。

* 監視フォルダーエンドポイントを設定する前にファイルシステム上にフォルダーを作成し、 folderPath プロパティにフルパスを指定します。 folderPath プロパティについて詳しくは、 [監視フォルダーのプロパティ](#watchedfolderproperties).

>[!NOTE]
>
>クラスター環境では、監視フォルダーとして使用されるフォルダーは、ファイルシステムまたはネットワーク上でアクセス可能、書き込み可能、および共有されている必要があります。 クラスターの各アプリケーションサーバーインスタンスは、同じ共有フォルダーにアクセスできる必要があります。 Windows の場合、すべてのサーバー上にマップされたネットワークドライブを作成し、マッピングされたネットワークドライブのパスを folderPath プロパティで指定します。

## 監視フォルダー設定ノードの作成 {#create-watched-folder-configuration-node}

監視フォルダーを設定するには、監視フォルダー設定ノードを作成します。 設定ノードを作成するには、以下の手順を実行します。

1. CRX-DE lite に管理者としてログインし、/etc/fd/watchfolder/config フォルダーに移動します。 

1. `nt:unstructured`というタイプのノードを作成します。名称は仮に watchedfolder としておきましょう。 

   >[!NOTE]
   >
   >監視フォルダーノード名にスペースや特殊文字を含めることはできません。

1. ノードに次のプロパティを追加します。

   * `folderPath`
   * `inputProcessorType`
   * `inputProcessorId`
   * `outputFilePattern`

   サポートされているプロパティの完全なリストについては、「[監視フォルダーのプロパティ](#watchedfolderproperties)」を参照してください。

1. 「**すべて保存**」をクリックします。ノードの作成後、プロパティが保存されます。`input`、`result`、`failure`、`preserve`、`stage`フォルダーが、`folderPath` プロパティで指定したパスに作成されます。

   定義した時間間隔でスキャンジョブが監視フォルダのスキャンを開始します。

## 監視フォルダーのプロパティ {#watchedfolderproperties}

監視フォルダーには、次のプロパティを設定できます。

* **folderPath (String)**：定義した時間間隔でスキャンされるフォルダーのパス。 クラスター環境の場合、フォルダーは共有場所に配置し、すべてのサーバーがサーバーに対するフルアクセス権を持つ必要があります。 これは必須プロパティです。
* **inputProcessorType (String)**：開始するプロセスのタイプ。 ワークフロー、スクリプト、またはサービスを指定できます。これは必須プロパティです。
* **inputProcessorId（文字列）**:inputProcessorId プロパティの動作は、 inputProcessorType プロパティに指定された値に基づきます。 これは必須プロパティです。次のリストは、inputProcessorType プロパティのすべての可能な値と、対応する inputProcessorType プロパティの必要条件の詳細を示しています。

   * ワークフローの場合、実行するワークフローモデルを指定します。 例： /etc/workflow/models/&lt;workflow_name>/jcr:content/model
   * スクリプトの場合は、実行するスクリプトの JCR パスを指定します。 例： /etc/fd/watchfolder/test/testScript.ecma
   * サービスの場合は、OSGi サービスの特定に使用するフィルターを指定します。 サービスは com.adobe.aemfd.watchfolder.service.api.ContentProcessor インターフェイスの実装として登録されます。

* **runModes(String)[runModes(String)]**：ワークフローの実行に許可される実行モードのコンマ区切りリストです。 以下にいくつかの例を示します。

   * 作成者

   * publish

   * author, publish

   * publish, author

>[!NOTE]
>
>監視フォルダーをホストしているサーバーで実行モードが指定されていない場合、サーバー上の実行モードに関わらず、監視フォルダーはアクティブになります。

* **outputFilePattern（文字列）**：出力ファイルのパターン。 フォルダまたはファイルパターンを指定できます。 フォルダーパターンを指定した場合、出力ファイルの名前はワークフローでの説明に従います。 ファイルパターンを指定した場合、出力ファイルの名前はファイルパターンで説明されているとおりになります。 [ファイルとフォルダーのパターン](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) また、出力ファイルのディレクトリ構造を指定することもできます。 これは必須プロパティです。

* **stageFileExpirationDuration （長い形式、デフォルトは —1）**：処理のために既に取得された入力ファイルまたは入力フォルダーがタイムアウトしたと見なして、エラーとしてマークするまでの待機秒数。 この有効期限メカニズムは、このプロパティの値が正の数の場合にのみ有効になります。

>[!NOTE]
>
>注意：この機能によってタイムアウトとマークされた入力がバックグラウンドで処理され続ける場合がありますが、しばらくすると停止します。タイムアウトメカニズムが起動する前に入力コンテンツが消費された場合、後で処理が完了し、出力が結果フォルダーにダンプされる場合もあります。 タイムアウト前にコンテンツが消費されなかった場合は、後でコンテンツを消費しようとしてエラーが発生する可能性が高く、このエラーは同じ入力の失敗フォルダーにも記録されます。 一方、断続的なジョブやワークフローの失敗によって入力の処理が有効にならなかった場合（有効期限メカニズムが対処するシナリオ）、もちろん、この 2 つの結果のいずれも発生しません。 したがって、失敗フォルダー内のエントリで、タイムアウトによって失敗とマークされたもの（「File not processed after thom about the firoum the marked after for marked, marking as failure!」という形式のメッセージを探します）。 結果フォルダー（および、同じ入力の他のエントリー用の失敗フォルダー自体）をスキャンして、事前に設定されたイベントがすべて実際に発生したかどうか確認することを推奨します。

* **deleteExpiredStageFileOnlyWhenThrottled（ブール型、デフォルト値は true）**：監視フォルダーに制限がある場合にのみタイムアウト機能を有効にするかどうか指定します。このメカニズムは、スロットルが有効な場合に、未処理の状態で（断続的なジョブやワークフローの誤りによって）長引くファイルが少数あると、スロットルが有効になったときにバッチ全体の処理が停止する可能性があるので、スロットル監視フォルダーに関連性が高くなります。 このプロパティの値を true（デフォルト）に設定すると、制限のない監視フォルダーに対して有効期限のメカニズムは有効になりません。 このプロパティの値に false を指定すると、stageFileExpirationDuration プロパティの値が正の数になっている限り、この機能が常に有効になります。

* **pollInterval (Long)**：監視フォルダーをスキャンして入力を確認する間隔（秒）。 「スロットル」設定が有効になっていない場合は、ポーリング間隔は平均ジョブを処理する時間より長くする必要があります。そうしないと、システムが過負荷になる場合があります。 デフォルト値は 5 です。詳しくは、バッチサイズの説明を参照してください。 pollinterval の値は 1 以上にする必要があります。
* **excludeFilePattern （文字列）**：スキャンおよび取得の対象となるファイルとフォルダーを決定するために監視フォルダーで使用されるパターンのセミコロン (;) 区切りのリストです。 このパターンを持つファイルまたはフォルダーは、スキャンされて処理されません。 この設定は、入力が複数のファイルを含むフォルダーの場合に役立ちます。 フォルダーの内容は、監視フォルダーで取得された名前のフォルダーにコピーできます。 これにより、フォルダーが入力フォルダーに完全にコピーされる前に、監視フォルダーがフォルダーを取得して処理するのを防ぎます。 デフォルト値は null です。
  次のように、除外する[ファイルパターン](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)を指定できます。

   * 特定の拡張子をファイル名に持つファイル。例えば &#42;.dat、&#42;.xml、.pdf、&#42;.&#42;
   * 特定の文字列をファイル名に持つファイル。例えば data&#42; を指定すると、data1、data2 などの名前を持つファイルおよびフォルダーが除外されます。
   * 次のような名前および拡張子が混在する式に一致するファイル。

      * Data[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
      * &#42;。[dD][Aa]&#39;port&#39;
      * &#42;。[Xx][Mm][Ll]

ファイルパターンについて詳しくは、「[ファイルパターンについて](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)」を参照してください。

* **includeFilePattern （文字列）**：スキャンおよび取得の対象となるフォルダーとファイルを決定するために監視フォルダーで使用されるパターンのセミコロン (;) 区切りのリストです。 例えば、IncludeFilePattern に input&#42; を指定すると、input&#42; に一致する名前を持つすべてのファイルおよびフォルダーが取得されます。input1、input2 などの名前を持つファイルおよびフォルダーが含まれます。デフォルト値は &#42; です。すべてのファイルとフォルダーが対象となります。次のように、含めるファイルパターンを指定できます。

   * 特定の拡張子をファイル名に持つファイル。例えば &#42;.dat、&#42;.xml、.pdf、&#42;.&#42;
   * data.&#42; を指定すると、data1 や data2 などの名前を持つファイルおよびフォルダーが対象に含まれます。

* 次のような名前および拡張子が混在する式に一致するファイル。

   * Data[0-9][0-9][0-9].[dD][aA]&#39;port&#39;

      * &#42;。[dD][Aa]&#39;port&#39;
      * &#42;。[Xx][Mm][Ll]

ファイルパターンについて詳しくは、 [ファイルパターンについて](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)

* **waitTime (Long)**：フォルダーまたはファイルの作成後にスキャンを実行するまでに待機する時間（ミリ秒単位）です。 例えば、待機時間が 3,600,000 ミリ秒（1 時間）で、1 分前にファイルが作成された場合、このファイルは 59 分以上経過した後に取得されます。 デフォルト値は 0 です。この設定は、ファイルまたはフォルダーを入力フォルダーに完全にコピーする場合に便利です。 例えば、処理の対象となるファイルが大きく、そのファイルをダウンロードするのに 10 分かかる場合は、待機時間を 10&#42;60&#42;1000 ミリ秒に設定します。これにより、作成後 10 分でない場合は、監視フォルダーはファイルをスキャンしなくなります。
* **purgeDuration (Long)**：結果フォルダー内のファイルおよびフォルダーは、この値より古い場合、パージされます。 この値の単位は日です。この設定は、結果フォルダーがいっぱいにならないようにするのに役立ちます。 -1 日の値は、結果フォルダーを削除しないことを示します。 デフォルト値は -1 です。
* **resultFolderName (String)**：保存された結果が保存されるフォルダー。 結果がこのフォルダーに表示されない場合は、失敗フォルダーを確認します。 読み取り専用ファイルは処理されず、失敗フォルダーに保存されます。 この値は、絶対パスまたは相対パスに指定でき、次のファイルパターンを使用します。

   * %F =ファイル名のプレフィックス
   * %E =ファイル名の拡張子
   * %Y =年（全角）
   * %y =年（下 2 桁）
   * %M =月
   * %D =日（月）
   * %d =日（通日）
   * %H =時（24 時間）
   * %h =時（12 時間）
   * %m =分
   * %s =秒
   * %l =ミリ秒
   * %R =乱数 (0 ～ 9)
   * %P =プロセスまたはジョブ ID

  例えば、2009 年 7 月 17 日の午後 8 時で、C:/Test/WF0/failure/%Y/%M/%D/%H/と指定した場合、結果のフォルダは C:/Test/WF0/failure/2009/07/17/20 となります。

  絶対パスではなく相対パスを指定すると、そのフォルダーは監視フォルダー内に作成されます。 デフォルト値は result/%Y/%M/%D/です。これは、監視フォルダー内の結果フォルダーです。 ファイルパターンについて詳しくは、「[ファイルパターンについて](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)」を参照してください。

>[!NOTE]
>
>結果フォルダーのサイズが小さいほど、監視フォルダーのパフォーマンスが向上します。 例えば、監視フォルダーの推定負荷が 1 時間に 1000 個のファイルである場合は、result/%Y%M%D%H のようなパターンを試し、1 時間ごとに新しいサブフォルダーが作成されるようにします。 負荷が小さい場合（例えば、1 日に 1000 個のファイル）、result/%Y%M%D のようなパターンを使用できます。

* **failureFolderName (String)**：失敗ファイルが保存されるフォルダー。 この場所は常に監視フォルダーからの相対パスです。 「結果フォルダ」の説明に従って、ファイルパターンを使用できます。 読み取り専用ファイルは処理されず、失敗フォルダーに保存されます。 デフォルト値は failure/%Y/%M/%D/です。
* **preserveFolderName（文字列）:** 処理が正常に完了した後にファイルが保存される場所。 パスは、絶対パス、相対パス、または null のディレクトリパスにすることができます。 「結果フォルダ」の説明に従って、ファイルパターンを使用できます。 デフォルト値は preserve/%Y/%M/%D/です。
* **batchSize (Long)**:1 回のスキャンで取得されるファイルまたはフォルダーの数。 システムの過負荷を防ぐために使用します。一度にスキャンするファイルが多すぎるとクラッシュが発生する場合があります。 デフォルト値は 2 です。

  ポール間隔設定およびバッチサイズ設定では、監視フォルダーがスキャンごとに取得するファイルの数を指定します。監視フォルダーは、Quartz スレッドプールを使用して入力フォルダーをスキャンします。 スレッドプールは他のサービスと共有されます。 スキャン間隔が小さい場合、スレッドは入力フォルダーを頻繁にスキャンします。 ファイルが頻繁に監視フォルダーに配置される場合は、スキャンの間隔を小さくする必要があります。 ファイルが頻繁に配置されない場合は、他のサービスがスレッドを使用できるように、より大きなスキャン間隔を使用します。

  大量のファイルがドロップされる場合は、バッチサイズを大きくします。 たとえば、監視フォルダーエンドポイントによって開始されるサービスが毎分 700 個のファイルを処理でき、これと同じ速度でユーザーが入力フォルダーにファイルを配置するとします。このときバッチサイズに 350 を、ポール間隔に 30 秒を指定すると、過度に頻繁に監視フォルダーをスキャンするコストを発生させることなく、監視フォルダーのパフォーマンスを向上させることができます。

  ファイルが監視フォルダーに配置されると、監視フォルダーは入力中のファイルのリストを作成します。これにより、スキャンが 1 秒ごとに行われている場合、パフォーマンスが低下するおそれがあります。スキャン間隔を長くすると、パフォーマンスが向上します。 削除されるファイルの量が少ない場合は、それに応じて [ バッチサイズ ] と [ ポーリング間隔 ] を調整します。 例えば、毎秒 10 個のファイルが配置される場合は、pollInterval を 1 秒に、batchSize を 10 に設定します。

* **throttleOn（ブール値）**：このオプションを選択すると、AEM Formsが同時に処理する監視フォルダーのジョブの数が制限されます。 ジョブの最大数は、バッチサイズ値によって決まりますデフォルト値は true です。 ( 詳しくは、 [スロットルについて](../../forms/using/watched-folder-in-aem-forms.md#p-about-throttling-p).)

* **overwriteDuplicateFilename (Boolean)**:「True」に設定すると、結果フォルダーと保存用フォルダー内のファイルが上書きされます。 False に設定すると、名前には数値インデックスサフィックスを持つファイルおよびフォルダが使用されます。 デフォルト値は False です。
* **preserveOnFailure (Boolean)**：サービスで操作を実行できなかった場合に入力ファイルを保持します。 デフォルト値は true です。
* **inputFilePattern （文字列）**：監視フォルダーの入力ファイルのパターンを指定します。 ファイルの許可リストを作成します。
* **asynch（ブール値）**：呼び出しタイプを非同期型または同期型として識別します。 デフォルト値は true（非同期）です。 ファイル処理はリソースを消費するタスクです。asynch フラグの値は true のままにして、スキャンジョブのメインスレッドが停止するのを防ぎます。 クラスター環境では、フラグを true のままにして、使用可能なサーバー間で処理されるファイルのロードバランシングを有効にすることが重要です。 このフラグが false の場合、スキャンジョブは、最上位のファイル/フォルダごとに、それぞれのスレッド内で順番に処理を実行しようとします。 単一サーバーの設定に基づくワークフローベースの処理など、具体的な理由がない限り、フラグを false に設定しないでください。

>[!NOTE]
>
>設計により、ワークフローは非同期になります。 たとえ値を false に設定した場合でも、ワークフローは非同期モードで開始されます。

* **enabled(Boolean)**：監視フォルダーのスキャンを有効化し、有効化します。 監視フォルダーのスキャンを開始するには、 enabled を true に設定します。 デフォルト値は true です。
* **payloadMapperFilter：**&#x200B;任意のフォルダーを監視フォルダーとして設定すると、その監視フォルダー内にフォルダー構造が作成されます。この構造には、入力を提供し、出力を受け取る（結果）、失敗のデータを保存し、長期間有効なプロセスのデータを保存し、様々なステージのデータを保存するフォルダーがあります。 監視フォルダーのフォルダー構造は、Forms中心のワークフローのペイロードとして機能します。 ペイロードマッパーを使用すると、入力、出力および処理に監視フォルダーを使用するペイロードの構造を定義できます。 たとえば、デフォルトのマッパーを使用した場合、監視フォルダーの内容を [payload]\input と [payload]\output フォルダーにマップします。標準搭載の 2 つのペイロードマッパー実装を使用できます。 次の条件を満たしていない場合、 [カスタム実装](../../forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter)で、標準搭載の実装の 1 つを使用します。

   * **デフォルトのマッパー：**&#x200B;デフォルトのペイロードマッパーを使用して、監視フォルダーの入力と出力の内容をペイロード内の別々の入出力フォルダーに保存します。また、ワークフローのペイロードパスでは、[payload]/input/ というパスと [payload]/output というパスを使用して、コンテンツの取得と保存を行ってください。

   * **単純なファイルベースのペイロードマッパー：**&#x200B;入力と出力の内容をペイロードフォルダーに直接保存するには、単純なファイルベースのペイロードマッパーを使用してください。デフォルトのマッパーなど、余分な階層は作成されません。

### カスタム設定パラメーター {#custom-configuration-parameters}

上記の監視フォルダー設定プロパティに加えて、カスタム設定パラメーターも指定できます。 カスタムパラメーターはファイル処理コードに渡されます。 これにより、パラメーターの値に基づいてコードの動作を変更できます。 パラメーターを指定するには：

1. CRXDE-Lite にログインし、監視フォルダー設定ノードへ移動します。
1. プロパティパラメーターを追加します。&lt;property_name> 監視フォルダー設定ノードに追加します。 プロパティの型は、ブール型、日付型、小数型、倍精度浮動小数点型、長整数型、文字列型のみです。 単一値プロパティと複数値プロパティを指定できます。

>[!NOTE]
>
>プロパティのデータタイプが Double の場合は、そのようなプロパティの値に小数点を指定します。データタイプが Double で、値に小数点が指定されていないすべてのプロパティは、タイプが Long に変換されます。

これらのプロパティは、 Map 型の不変マップとして渡されます&lt;string object=&quot;&quot;> を処理コードに追加します。 処理コードは、ECMAScript、ワークフロー、サービスのいずれかです。 プロパティに指定した値は、マップでキーと値のペアとして使用できます。 キーはプロパティの名前で、値はプロパティの値です。 カスタム設定パラメーターについて詳しくは、以下の画像を参照してください。

![必須プロパテイの他、いくつかのオプションのプロパティと設定パラメーターが存在する監視フォルダー設定ノードのサンプル](assets/custom-configuration-parameters.png)

必須プロパテイの他、いくつかのオプションのプロパティと設定パラメーターが存在する監視フォルダー設定ノードのサンプル.

#### ワークフロー向けの可変変数 {#mutable-variables-for-workflows}

ワークフローベースのファイル処理方法で使用する可変変数を作成できます。 これらの変数は、ワークフローのステップ間で送られるデータのコンテナとして機能します。 このような変数を作成するには：

1. CRXDE-Lite にログインし、監視フォルダー設定ノードへ移動します。

1. workflow.var プロパティを追加します。&lt;variable_name> 監視フォルダー設定ノードに追加します。

   プロパティの型は、ブール型、日付型、小数型、倍精度浮動小数点型、長整数型、文字列型のみです。 複数の値を持つプロパティもサポートされます。 複数値のプロパティの場合、ワークフローステップに使用できる値は、指定されたタイプの配列です。

   >[!NOTE]
   >
   >プロパティのデータタイプが Double の場合は、そのようなプロパティの値に小数点を指定します。データタイプが Double で、値に小数点が指定されていないすべてのプロパティは、タイプが Long に変換されます。

>[!NOTE]
>
>JCR 仕様は、プロパティのデフォルト値を指定します。 デフォルト値は、処理するワークフローのステップで使用できます。 したがって、適切なデフォルト値を指定します。

![custom-configuration-parameters2](assets/custom-configuration-parameters2.png)

## 様々なファイル処理方法 {#variousmethodsforprocessingfiles}

ワークフロー、サービス、またはスクリプトを開始して、監視フォルダーに配置されたドキュメントを処理できます。

### サービスを使用した監視フォルダーのファイルの処理   {#using-a-service-to-process-files-of-a-watched-folder-nbsp}

サービスは `com.adobe.aemfd.watchfolder.service.api.ContentProcessor` インターフェイスのカスタム実装です。OSGi には、いくつかのカスタムプロパティと共に登録されています。 カスタムプロパティの実装は一意になるので、実装を識別するのに役立ちます。

#### ContentProcessor インターフェイスのカスタム実装 {#custom-implementation-of-the-contentprocessor-interface}

カスタム実装は、処理のコンテキスト（タイプ com.adobe.aemfd.watchfolder.service.api.ProcessorContext のオブジェクト）を受け取り、入力ドキュメントと設定パラメーターをコンテキストから読み取って入力を処理し、出力をコンテキストに追加します。ProcessorContext には次の API があります。

* **getWatchFolderId**：監視フォルダーの ID を戻します。
* **getInputMap**:Map タイプのマップを戻します。 マップのキーは、入力ファイルのファイル名と、ファイルの内容を含むドキュメントオブジェクトです。 入力ファイルを読み取るには、getinputMap API を使用します。
* **getConfigParameters**:Map 型の不変マップを戻します。 マップには
監視フォルダーの設定パラメーターが含まれています。

* **setResult**：この API は、ContentProcessor 実装が
出力ドキュメントを結果フォルダーに書き出す際に使用されます。setResult API に出力ファイルの名前を指定できます。 API では、指定した出力フォルダーまたは出力ファイルのパターンに応じて、指定したファイルを使用するか無視するかを選択できます。 フォルダーパターンを指定した場合、出力ファイルの名前はワークフローでの説明に従います。 ファイルパターンを指定した場合、出力ファイルの名前はファイルパターンで説明されているとおりになります。

例えば、次のコードは、カスタムの foo=bar プロパティを持つ ContentProcessor インターフェイスのカスタム実装です。

```java
@Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
@Service(value = {OutputWriter.class, ContentProcessor.class})
@Property(name = "foo", value = "bar")
public class OutputWriter implements ContentProcessor {
```

While [監視フォルダーの設定](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p)を指定した場合、inputProcessorId プロパティを (foo=bar) に指定し、inputProcessorType プロパティを Service に指定した場合、上記の Service（カスタム実装）が監視フォルダーの入力ファイルの処理に使用されます。

次の例は、ContentProcessor インターフェイスのカスタム実装でもあります。 この例では、サービスは入力ファイルを受け入れ、ファイルを一時的な場所にコピーし、ファイルの内容を含むドキュメントオブジェクトを返します。 ドキュメントオブジェクトの内容は結果フォルダに保存されます。 結果フォルダーの物理パスは、 [監視フォルダー設定ノード](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

```java
@Component(immediate = true)
@Service(value = ContentProcessor.class)
@Property(name = "serviceSelector", value = "testProcessor1")
public class TestContentProcessor1 implements ContentProcessor {
    @Override
    public void processInputs(ProcessorContext context) throws Exception {
        Map.Entry<String, Document> e = context.getInputMap().entrySet().iterator().next();
        File f = new File((String) context.getConfigParameters().get("tempDir"),
                context.getConfigParameters().get("outPrefix") + e.getKey());
        e.getValue().copyToFile(f);
        context.setResult(f.getName(), new Document(f, true));
    }
}
```

### スクリプトを使用した監視フォルダーのファイルの処理 {#using-scripts-to-process-files-of-a-watched-folder}

スクリプトは、監視フォルダーに配置されたドキュメントを処理するために記述される ECMAScript 苦情カスタムコードです。 スクリプトは JCR ノードとして表されます。 標準の ECMAScript 変数（log、sling など）の他に、スクリプトには processorContext 変数があります。 変数の型は ProcessorContext です。 ProcessorContext には次の API があります。

* **getWatchFolderId**：監視フォルダーの ID を戻します。
* **getInputMap**:Map タイプのマップを戻します。 マップのキーは、入力ファイルのファイル名と、ファイルの内容を含むドキュメントオブジェクトです。 入力ファイルを読み取るには、getinputMap API を使用します。
* **getConfigParameters**:Map 型の不変マップを戻します。 マップには監視フォルダーの設定パラメーターが含まれています。
* **setResult**：この API は、ContentProcessor 実装が
出力ドキュメントを結果フォルダーに書き出す際に使用されます。setResult API に出力ファイルの名前を指定できます。 API では、指定した出力フォルダーまたは出力ファイルのパターンに応じて、指定したファイルを使用するか無視するかを選択できます。 フォルダーパターンを指定した場合、出力ファイルの名前はワークフローでの説明に従います。 ファイルパターンを指定した場合、出力ファイルの名前はファイルパターンで説明されているとおりになります。

次のコードは ECMAScript のサンプルです。 入力ファイルを受け入れ、ファイルを一時的な場所にコピーし、ファイルの内容を含むドキュメントオブジェクトを返します。 ドキュメントオブジェクトの内容は結果フォルダに保存されます。 結果フォルダーの物理パスは、 [監視フォルダー設定ノード](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

>[!NOTE]
>
>出力フォルダーおよびファイル名のプレフィックスは、監視フォルダー設定パラメーターに基づいて決定されます。

```java
var inputMap = processorContext.getInputMap();
var params = processorContext.getConfigParameters();
var entry = inputMap.entrySet().iterator().next();
var tempFile = new Packages.java.io.File(params.get("tempDir"), params.get("outPrefix") + entry.getKey());
entry.getValue().copyToFile(tempFile);
processorContext.setResult(tempFile.getName(), new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true));
```

#### スクリプトの場所とセキュリティに関する考慮事項 {#location-of-scripts-and-security-considerations}

デフォルトでは、コンテナフォルダー (/etc/fd/watchfolder/scripts) が提供され、ユーザーはスクリプトを配置できます。watch-folder フレームワークで使用されるデフォルトの service-user は、この場所からスクリプトを読み取るために必要な権限を持ちます。

カスタムの場所にスクリプトを配置する予定の場合、デフォルトのサービスユーザーにはそのカスタムの場所に対する読み取り権限がない可能性があります。その場合、次の手順を実行して必要な権限をカスタムの場所に入力します。

1. プログラムによって、またはコンソール https://&#39;[server]:[port]&#39;/crx/explorer 経由によって、システムユーザーを作成します。既存のシステムユーザーを使用することもできます。 ここでは、通常のユーザーではなく、システムユーザーと連携することが重要です。
1. スクリプトが保存されるカスタムの場所で、新しく作成された、または既存のシステムユーザーに読み取り権限を付与します。 複数のカスタムの場所を設定できます。 すべてのカスタムの場所に最低でも読み取り権限を付与してください。
1. Felix 設定コンソール (/system/console/configMgr) で、watch-folders のサービスユーザーマッピングを探します。 このマッピングは、「Mapping: adobe-aemds-core-watch-folder=...」のようになります。
1. このマッピングをクリックします。エントリ「adobe-aemds-core-watch-folder:scripts=fd-service」で、fd-service をカスタムシステムユーザーの ID に変更します。「保存」をクリックします。

これで、設定したカスタムの場所を使用してスクリプトを保存できます。

### ワークフローを使用した監視フォルダーのファイルの処理 {#using-a-workflow-to-process-files-of-a-watched-folder}

ワークフローを使用すると、ワークフローアクティビティを自動化するExperience Managerを自動化できます。 ワークフローは、特定の順序で実行される一連のステップで構成されます。 各ステップで、ページのアクティベートや電子メールメッセージの送信など、個別のアクティビティが実行されます。 ワークフローは、リポジトリ内のアセット、ユーザーアカウント、Experience Managerサービスとやり取りできます。 したがって、ワークフローでは複雑な連携を行うことができます。

* ワークフローを作成する前に、次の点を考慮してください。
* 任意のステップの出力は、すべての後続のステップで使用できるようにしておく必要があります。
各ステップでは、それ以前のステップによって生成された既存の出力をアップデート（または削除）できるようにしておく必要があります。
* 可変変数は、各ステップ間におけるカスタムダイナミックデータの受け渡しに使用されます。

ワークフローを使用してファイルを処理するには、次の手順を実行します。

1. `com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextProcessor`インターフェイスの実装を作成します。これはサービスのために作成した実装と同様です。

   >[!NOTE]
   >
   >完全な実装は ECMAScript で完全に作成できます。

1. ワークフローのステップで、タイプ com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService の OSGi サービスを探し、次の引数を指定してサービスの execute() メソッドを呼び出します。

   * WorkflowContextProcessor インターフェイスのカスタム実装
   * workItem
   * workflowSession
   * メタデータ

Java プログラミング言語を使用してワークフローを実装する場合、AEMワークフローエンジンは workItem、workflowSession および metadata 変数の値を提供します。 これらの変数は、カスタム WorkflowProcess 実装の execute() メソッドに引数として渡されます。

ECMAScript を使用してワークフローを実装する場合、AEMワークフローエンジンは graniteWorkItem、graniteWorkflowSession および metadata 変数の値を提供します。 これらの変数は、WorkflowContextService.execute() メソッドに引数として渡されます。

processWorkflowContext() に対する引数は、タイプ com.adobe.aemfd.watchfolder.workflow.api.WorkflowContext のオブジェクトです。 上記のワークフロー固有の考慮事項を容易にするために、WorkflowContext インターフェイスには次の API が用意されています。

* getWorkItem: WorkItem 変数の値を返します。 各変数は WorkflowContextService.execute() メソッドに渡されます。
* getWorkflowSession：WorkflowSession 変数の値を返します。各変数は WorkflowContextService.execute() メソッドに渡されます。
* getMetadata：metadata 変数の値を返します。各変数は WorkflowContextService.execute() メソッドに渡されます。
* getCommittedVariables：読み取り専用オブジェクトマップを返します。マップには以前のステップで設定された変数が表示されます。変数が以前のステップで変更されていない場合、監視フォルダーの設定時に指定したデフォルトの値を返します。
* getCommittedResults：読み取り専用のドキュメントマップを返します。マップには以前のステップで生成された出力ファイルが表示されます。
* setVariable: WorkflowContextProcessor 実装はこの変数を使用して、ステップ間を流れるカスタム動的データを表す変数を操作します。 変数の名前と型は、 [監視フォルダーの設定](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p). 変数の値を変更するには、 setVariable API を null 以外の値で呼び出します。 変数を削除するには、 setVariable() を null 値で呼び出します。

次の ProcessorContext API も利用できます。

* getWatchFolderId：監視フォルダーの ID を返します。
* getInputMap: Map 型のマップを返します。&lt;string document=&quot;&quot;>. マップのキーは、入力ファイルのファイル名と、ファイルの内容を含むドキュメントオブジェクトです。 入力ファイルを読み取るには、getinputMap API を使用します。
* getConfigParameters: Map 型の不変マップを返します。&lt;string object=&quot;&quot;>. マップには監視フォルダーの設定パラメーターが含まれています。
* setResult: ContentProcessor 実装は、この API を使用して出力ドキュメントを結果フォルダーに書き込みます。 setResult API に出力ファイルの名前を指定できます。 API では、指定した出力フォルダーまたは出力ファイルのパターンに応じて、指定したファイルを使用するか無視するかを選択できます。 フォルダーパターンを指定した場合、出力ファイルの名前はワークフローでの説明に従います。 ファイルパターンを指定した場合、出力ファイルの名前はファイルパターンで指定した名前になります。

ワークフローで setResult API を使用する際の考慮事項は次のとおりです。

* ワークフローの出力全体に影響する出力ドキュメントを新規追加するには、setResult API を呼び出す際に、以前のステップで出力ファイル名として使用されていないファイル名を指定します。
* 以前のステップで生成された出力をアップデートするには、setResult API を呼び出す際に、以前のステップで使用したファイル名を指定します。
* 以前のステップで生成された出力を削除するには、setResult を呼び出す際に、以前のステップで使用したファイル名を指定し、null をコンテンツとして指定します。

>[!NOTE]
>
>他のすべてのシナリオにおいて setResult API の呼び出し時に null コンテンツを指定すると、エラーが発生します。

以下は、ワークフローステップの実装例です。この例では、ECMAscript で可変の stepCount を使用して、現在のワークフローインスタンスにおけるステップの呼び出し回数を追跡しています。出力フォルダー名は、現在のステップの呼び出し回数、元のファイル名、outPrefix パラメーターに指定したプレフィックスを組み合わせたものになっています。

ECMAScript は、ワークフローコンテキストサービスの参照を取得し、WorkflowContextProcessor インターフェイスの実装を作成します。 WorkflowContextProcessor 実装は、入力ファイルを受け入れ、ファイルを一時的な場所にコピーし、コピーされたファイルを表すドキュメントを返します。 現在のステップでは、ブール変数 purgePrevious の値に基づいて、現在のワークフローインスタンスでステップが開始されたときに、同じステップで最後に生成された出力が削除されます。 最後に、wfSvc.execute メソッドを呼び出して WorkflowContextProcessor 実装を実行します。 出力ドキュメントの内容は、監視フォルダー設定ノードで指定された物理パスの結果フォルダーに保存されます。

```javascript
log.error("Watch-folder workflow script called for step: " + graniteWorkItem.getNode().getTitle());
var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
// Custom WorkflowContextProcessor implementation which defines the processWorkflowContext() method purely in JS
var impl = { processWorkflowContext: function (wfContext) {
    var wfId = wfContext.getWatchFolderId();
    var inputMap = wfContext.getInputMap();
    var paramMap = wfContext.getConfigParameters();
    var preResults = wfContext.getCommittedResults();
    var preVars = wfContext.getCommittedVariables();
    log.info("WF ID: " + wfId); // workflowId of type String
    log.info("Inputs: " + inputMap); // Input map of type Map<String, Document>
    log.info("Params: " + paramMap); // Config params of type Map<String, Object>
    log.info("Old results: " + preResults);
    log.info("Old variables: " + preVars);
    var currStepNumber = new Packages.java.lang.Long(new Packages.java.lang.Long(preVars.get("stepCount")).longValue() + 1);
    log.info("Current step number: " + currStepNumber);
    wfContext.setVariable("stepCount", currStepNumber);
    var entry = inputMap.entrySet().iterator().next();
    var tempFile = new Packages.java.io.File(paramMap.get("tempDir"), paramMap.get("outPrefix") + "STEP-" + currStepNumber + "-" + entry.getKey());
    entry.getValue().copyToFile(tempFile);
    var fName = tempFile.getName();
    var outDoc = new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true);
    wfContext.setResult(tempFile.getName(), outDoc);
    var prevStepOutName = paramMap.get("outPrefix") + "STEP-" + (currStepNumber - 1) + "-" + entry.getKey();
    if (preResults.containsKey(prevStepOutName) && paramMap.get("purgePrevious").booleanValue()) {
        log.info("Purging previous step output " + prevStepOutName);
        wfContext.setResult(prevStepOutName, null);
    }
} }
wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
log.info("Exiting workflow script!")
```

### ペイロードマッパーフィルターを作成して、監視フォルダーの構造をワークフローのペイロードにマッピングします {#create-payload-mapper-filter-to-map-structure-of-a-watched-folder-to-the-payload-of-a-workflow}

監視フォルダーを作成すると、監視対象のフォルダー内にフォルダー構造が作成されます。 フォルダー構造には、stage、result、preserve、input および failure の各フォルダーが含まれます。 フォルダー構造は、ワークフローへの入力ペイロードとして機能し、ワークフローからの出力を受け取ることができます。 また、障害点がある場合は、そのリストを表示できます。

ペイロードの構造が監視フォルダーの構造と異なる場合は、監視フォルダーの構造をペイロードにマッピングするカスタムスクリプトを作成できます。 このようなスクリプトは、ペイロードマッパーフィルターと呼ばれます。 デフォルトでは、AEM Formsには、監視フォルダーの構造をペイロードにマッピングするためのペイロードマッパーフィルターが用意されています。

#### カスタムペイロードマッパーフィルターの作成 {#creating-a-custom-payload-mapper-filter}

1. ダウンロード [Adobeクライアント SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/).
1. Maven ベースのプロジェクトのビルドパスにクライアント SDK を設定します。 まず、次の Maven ベースのプロジェクトを、選択した IDE でダウンロードして開くことができます。
1. 必要に応じて、サンプルバンドルで使用可能なペイロードマッパーフィルターコードを編集します。
1. maven を使用して、カスタムのペイロードマッパーフィルターのバンドルを作成します。
1. 用途 [AEMバンドルコンソール](https://localhost:4502/system/console/bundles) をクリックしてバンドルをインストールします。

   現在、カスタムのペイロードマッパーフィルターがAEM監視フォルダー UI に表示されます。 ワークフローで使用できます。

   次のコード例では、ペイロードを基準に保存されたファイルに対して、単純なファイルベースのマッパーを実装しています。 これを使用して今すぐ始めることができます。

   ```java
   package com.adobe.aemfd.watchfolder.workflow;
   import com.adobe.aemfd.docmanager.Document;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.PayloadMapper;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowExecutionContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowInitializationContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowVariable;
   import com.adobe.granite.workflow.exec.Workflow;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.ResourceResolver;
   import javax.jcr.Binary;
   import javax.jcr.Node;
   import java.util.Collection;
   import java.util.HashMap;
   import java.util.Map;
   @Component(immediate = true)
   @Service(value = PayloadMapper.class)
   public class SimpleFileBasedPayloadMapper implements PayloadMapper {
   @Override
   public Node createPayload(WorkflowInitializationContext wfInitCtxt, Node stagingFolder, String uniquePayloadName,
   Map<String, Binary> inputs, Collection<WorkflowVariable> variableDefs) throws Exception {
   Node dirNode = stagingFolder.addNode(uniquePayloadName, "sling:Folder");
   for (Map.Entry<String, Binary> bins: inputs.entrySet()) {
   Node fileNode = dirNode.addNode(bins.getKey(), "nt:file");
   Node resNode = fileNode.addNode ("jcr:content", "nt:resource");
   resNode.setProperty("jcr:data", bins.getValue());
   }
   return dirNode;
   }
   @Override
   public Map<String, Document> getInputs(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload, ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public void setOutput(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   String fileName, Binary contents, int outputMode) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getIntermediateOutputs(WorkflowInitializationContext wfInitCtxt,
   WorkflowExecutionContext wfExecCtxt, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getFinalOutputs(WorkflowInitializationContext wfInitCtxt, Workflow workflow, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   Map<String, Object> params = wfInitCtxt.getConfigParameters();
   Map<String, Document> result = new HashMap<String, Document>();
   for (Map.Entry<String, Object> me: params.entrySet()) {
   String key = me.getKey();
   if (key.startsWith("pm.outfile.")) {
   String fName = (String) me.getValue();
   Document d = new Document(payload.getPath() + "/" + fName, resourceResolver);
   result.put(fName, d);
   }
   }
   return result;
   }
   @Override
   public void setVariable(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   WorkflowVariable variable) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Object> getVariables(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   }
   ```

## ユーザーが監視フォルダーとやり取りする方法 {#how-users-interact-with-a-watched-folder}

監視フォルダーエンドポイントの場合、ユーザーは入力ファイルやフォルダーをデスクトップから監視フォルダーにコピーまたはドラッグすることで、ファイルの処理操作を開始できます。 ファイルは到着順に処理されます。

監視フォルダーエンドポイントの場合、ジョブに必要な入力ファイルが 1 つだけの場合は、そのファイルを監視フォルダーのルートにコピーできます。

ジョブに複数の入力ファイルが含まれる場合、ユーザーは監視フォルダー階層の外側に、必要なすべてのファイルを含むフォルダーを作成する必要があります。 この新しいフォルダーには、入力ファイルが含まれている必要があります（プロセスで必要に応じて DDX ファイルも含まれます）。 ジョブフォルダーが構築されたら、ユーザーはそのフォルダーを監視フォルダーの入力フォルダーにコピーします。

>[!NOTE]
>
>アプリケーションサーバーが監視フォルダー内のファイルへのアクセスを削除したことを確認します。 スキャン後にAEM Formsが入力フォルダーからファイルを削除できない場合、関連するプロセスは無期限に開始されます。

## 監視フォルダーに関する追加情報 {#additional-information-about-the-watched-folders}

### スロットルについて {#about-throttling}

監視フォルダーエンドポイントのジョブ数の制限を有効にすると、一定時に処理される監視フォルダーのジョブ数が制限されます。 ジョブの最大数はバッチサイズの値によって決まり、監視フォルダーエンドポイントでも設定できます。 制限の上限に達すると、監視フォルダーの入力ディレクトリに入ってくるドキュメントはポーリングされません。 ドキュメントは、他の監視フォルダージョブが完了し、別のポーリングが試行されるまで、入力ディレクトリに残ります。 同期処理の場合、ジョブが単一のスレッドで連続して処理される場合でも、1 回のポーリングで処理されたすべてのジョブがスロットル制限にカウントされます。

>[!NOTE]
>
>スロットルは、クラスターでは拡大/縮小されません。 スロットルが有効な場合、クラスター全体では、いつでもバッチサイズで指定されたジョブ数を超えるジョブを処理できません。 この制限は、クラスター全体に適用され、クラスター内の各ノードに固有のものではありません。 例えば、バッチサイズが 2 の場合、2 つのジョブを処理する 1 つのノードでスロットル制限に達し、1 つのジョブが完了するまで他のノードは入力ディレクトリをポーリングしません。

#### スロットルの仕組み {#how-throttling-works}

監視フォルダーは、pollInterval のたびに入力フォルダーをスキャンし、バッチサイズで指定された数のファイルを取得し、それぞれのファイルのターゲットサービスを呼び出します。 例えば、バッチサイズが各スキャンで 4 の場合、監視フォルダーは 4 つのファイルを取得し、4 つの呼び出し要求を作成して、ターゲットサービスを呼び出します。 これらの要求が完了する前に監視フォルダーが呼び出された場合は、前の 4 つのジョブが完了しているかどうかに関係なく、再び 4 つのジョブが開始されます。

ジョブ数の制限を使用すると、前のジョブが完了していない場合に、監視フォルダーが新しいジョブを呼び出さないようにできます。 監視フォルダーは、進行中のジョブを検出し、バッチサイズから進行中のジョブを引いた値に基づいて新しいジョブを処理します。 例えば、2 回目の呼び出しでは、完了したジョブの数が 3 つで、まだ処理中のジョブが 1 つだけの場合、監視フォルダーは 3 つのジョブのみを呼び出します。

* 監視フォルダーは、ステージフォルダーに存在するファイルの数に基づいて、進行中のジョブの数を調べます。 ステージフォルダーにファイルが未処理のまま残っている場合、監視フォルダーはこれ以上ジョブを呼び出しません。 例えば、バッチサイズが 4 で、3 つのジョブが停止している場合、監視フォルダーは以降の呼び出しでジョブを 1 つだけ呼び出します。 複数のシナリオが原因で、ファイルがステージフォルダーに未処理のまま残る場合があります。 ジョブが停止している場合、管理者はプロセス管理ページでプロセスを終了し、監視フォルダーがステージフォルダーからファイルを移動できるようにします。
* 監視フォルダーがジョブを呼び出す前にAEM Formsサーバーが停止した場合は、管理者はステージフォルダーからファイルを移動できます。 詳しくは、 [障害点と回復](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).
* Job Manager サービスが呼び出しを返したときにAEM Formsサーバーが実行されているが監視フォルダーが実行されていない場合は、サービスが順序どおりに開始されない場合に発生し、管理者はステージフォルダーからファイルを移動できます。 詳しくは、 [障害点と回復](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).

### 障害点と回復障害点と回復 {#failure-points-and-recoveryfailure-points-and-recovery}

ポーリングイベントのたびに、監視フォルダーは入力フォルダーをロックし、「ファイルを含める」パターンに一致するファイルをステージフォルダーに移動し、入力フォルダーのロックを解除します。 2 つのスレッドが同じファイルのセットを取得して 2 回処理しないように、ロックが必要です。 pollInterval を小さく、バッチサイズを大きくすると、このような状況が発生する可能性が高くなります。 ファイルがステージフォルダーに移動されると、入力フォルダーはロック解除され、他のスレッドがフォルダーをスキャンできるようになります。 この手順は、あるスレッドがファイルを処理している間に他のスレッドがスキャンできるので、高いスループットを提供するのに役立ちます。

ファイルがステージフォルダーに移動されると、ファイルごとに呼び出し要求が作成され、ターゲットのサービスが呼び出されます。 監視フォルダーがステージフォルダー内のファイルを復元できない場合があります。

* 監視フォルダーが呼び出し要求を作成する前にサーバーがダウンした場合、ステージフォルダー内のファイルはステージフォルダーに残り、復元されません。

* 監視フォルダーがステージフォルダー内の各ファイルに対する呼び出し要求を正常に作成し、サーバーがクラッシュした場合、呼び出しの種類に応じて次の 2 つの動作が実行されます。

   * **同期**：監視フォルダーがサービスを同期的に呼び出すように設定されている場合、ステージフォルダー内のすべてのファイルは未処理のままステージフォルダーに残ります。
   * **非同期**：この場合、監視フォルダーは Job Manager サービスに依存します。 Job Manager Service が監視フォルダーを呼び出すと、ステージフォルダー内のファイルは、呼び出しの結果に基づいて、保存フォルダーまたは失敗フォルダーに移動されます。 Job Manager サービスが監視フォルダーを呼び出さない場合、ファイルは未処理のままステージフォルダーに残ります。 この状況は、Job Manager がコールバックする際に監視フォルダーが実行されていない場合に発生します。

#### ステージフォルダー内の未処理のソースファイルを復元します {#recover-unprocessed-source-files-in-the-stage-folder}

監視フォルダーがステージフォルダー内のソースファイルを処理できない場合は、未処理のファイルを復元できます。

1. アプリケーションサーバーまたはノードを再起動します。

1. 監視フォルダーが新しい入力ファイルを処理するのを停止します。 この手順をスキップすると、どのファイルがステージフォルダーで未処理かを判断するのがはるかに難しくなります。 監視フォルダーが新しい入力ファイルを処理しないようにするには、次のいずれかのタスクを実行します。

   * 監視フォルダーの includeFilePattern プロパティを、どの新しい入力ファイルとも一致しない値に変更します（例えば、NOMATCH と入力します）。
   * 新しい入力ファイルを作成するプロセスを休止します。

   AEM Formsがすべてのファイルを回復して処理するまで待ちます。 大部分のファイルが復元され、新しい入力ファイルが正しく処理されます。 監視フォルダーがファイルを回復して処理するまでの待ち時間の長さは、呼び出す操作の長さと回復するファイルの数によって異なります。

1. 処理できないファイルを決定します。 適切な時間待って前の手順を完了し、ステージフォルダーに未処理のファイルが残っている場合は、次の手順に進みます。

   >[!NOTE]
   >
   >ステージディレクトリ内のファイルの日付とタイムスタンプを確認できます。 ファイルの数と通常の処理時間に応じて、停止していると見なされるだけの古いファイルを判断できます。

1. 未処理のファイルをステージディレクトリから入力ディレクトリにコピーします。

1. 手順 2 で監視フォルダーが新しい入力ファイルを処理できない場合は、「ファイルパターンを含める」を以前の値に変更するか、無効にしたプロセスを再度有効にします。

### 複数の監視フォルダーを連結する {#chain-watched-folders-together}

複数の監視フォルダーを連結して、1 つの監視フォルダーの結果ドキュメントを次の監視フォルダーの入力ドキュメントにすることができます。 各監視フォルダーは、異なるサービスを呼び出すことができます。 この方法で監視フォルダーを設定すると、複数のサービスを呼び出すことができます。 例えば、1 つの監視フォルダーでPDFファイルをAdobe PostScript®に変換し、別の監視フォルダーで PostScript ファイルをPDF/A 形式に変換することができます。 これをおこなうには、最初のエンドポイントで定義された監視フォルダーの結果フォルダーを、2 番目のエンドポイントで定義された監視フォルダーの入力フォルダーを指すように設定します。

そうすると、最初の変換処理からの出力は、\path\result に送られます。2 回目の変換処理に対する入力は \path\result になり、2 回目の変換処理からの出力は \path\result\result（または 2 回目の変換処理用に「結果フォルダー」ボックスで定義したディレクトリ）に送られます。

### ファイルおよびフォルダーのパターン {#file-and-folder-patterns}

管理者は、サービスを呼び出すことができるファイルの種類を指定できます。 監視フォルダーごとに複数のファイルパターンを設定できます。 ファイルパターンは、次のファイルプロパティのいずれかになります。

* 特定の拡張子をファイル名に持つファイル。例えば &#42;.dat、&#42;.xml、.pdf、&#42;.&#42;
* data.&#42;
* 次のような名前および拡張子が混在する式に一致するファイル。

   * Data[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
   * &#42;。[dD][Aa]&#39;port&#39;
   * &#42;。[Xx][Mm][Ll]

* 管理者は、結果を保存する出力フォルダーのファイルパターンを定義できます。 出力フォルダー（結果、保存、失敗）に関しては、管理者は次のファイルパターンを指定できます。
* %Y =年（全角）
* %y =年（下 2 桁）
* %M =月
* %D =日（通日）
* %d =日（通日）
* %h =時
* %m =分
* %s =秒
* %R =乱数 (0 ～ 9)
* %J =ジョブ名

例えば、結果フォルダーのパスはC:\Adobe\AdobeLiveCycleES4\BarcodedForms\%y\%m\%d です。

出力パラメーターのマッピングでは、次のような追加のパターンも指定できます。

* %F =ソースファイル名
* %E =ソースファイル名の拡張子

出力パラメーターのマッピングパターンが「File.separator」（つまり、パスセパレーター）で終わる場合、フォルダーが作成され、コンテンツがそのフォルダーにコピーされます。パターンが「File.separator」で終わらない場合、コンテンツ（結果ファイルまたはフォルダー）がその名前で作成されます。

## 監視PDF Generatorーでのフォルダーの使用 {#using-pdf-generator-with-a-watched-folder}

監視フォルダーを設定して、入力ファイルを処理するワークフロー、サービス、またはスクリプトを開始することができます。 次の節では、ECMAScript を開始するための監視フォルダーを設定します。 ECMAScript では、PDF Generatorを使用してMicrosoft Word(.docx) ドキュメントをPDFドキュメントに変換します。

次の手順を実行して、監視フォルダーをPDF Generatorします。

1. [ECMAScript の作成](../../forms/using/watched-folder-in-aem-forms.md#p-create-an-ecmascript-p)
1. [ワークフローの作成](../../forms/using/watched-folder-in-aem-forms.md#p-create-a-workflow-p)
1. [監視フォルダーの設定](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)

### ECMAScript の作成 {#create-an-ecmascript}

ECMAScript では、PDF Generatorの createPDF API を使用して、Microsoft Word(.docx) ドキュメントをPDFドキュメントに変換します。 次の手順を実行して、スクリプトを作成します。

1. ブラウザーウィンドウで CRXDE lite を開きます。 URL は https://&#39;[server]:[port]&#39;/crx/de です。

1. /etc/workflow/scripts に移動し、PDFG という名前のフォルダーを作成します。

1. PDFG フォルダーで pdfg-openOffice-sample.ecma という名前のファイルを作成し、以下のコードをファイルに追加します。

   ```javascript
   var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
   // Custom ContentProcessor implementation which defines the processInputs() method purely in JS
   var impl = { processWorkflowContext: function (wrkfContext) {
   
     //  var logger = Packages.org.slf4j.LoggerFactory.getLogger("cmb-mergeandprint-sample.ecma");
                   var inputMap=wrkfContext.getInputMap();
   
                   var distiller = sling.getService(com.adobe.pdfg.service.api.DistillerService);
                   var generatePDF = sling.getService(com.adobe.pdfg.service.api.GeneratePDFService);
                   var pdfgConfig = sling.getService(com.adobe.pdfg.service.api.PDFGConfigService);
       var result = new Packages.java.util.HashMap();
       var entry = inputMap.entrySet().iterator().next();
       var pdfgOut = generatePDF.createPDF(entry.getValue(), ".docx", "Standard OpenOffice", "Standard", "No Security", null, null);
                   var convertedDoc = pdfgOut.get("ConvertedDoc");
   //   logger.info("SuccessFully saved the document to Ouput Node");
       wrkfContext.setResult(entry.getKey().substring(0, entry.getKey().lastIndexOf('.'))+".pdf",convertedDoc); // Ownership flag set to true for auto temp-file deletion.
   
   } }
   
   wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
   ```

1. ファイルを保存して閉じます。

### ワークフローの作成 {#create-a-workflow}

1. ブラウザーウィンドウで AEM ワークフロー UI を開きます。
   <https://[servername>]:&#39;port&#39;/workflow

1. モデルビューで、 **新規**. 新しいワークフローダイアログで、次の項目を指定します。 **タイトル**&#x200B;をクリックし、 **OK**.

   ![create-a-workflow-pdf](assets/create-a-workflow-pdf.png)

1. 新しく作成したワークフローを選択し、「 」をクリックします。 **編集**. 新しいウィンドウが開きます。

1. デフォルトのワークフローステップを削除します。 「プロセスステップ」をワークフローからSidekickにドラッグ&amp;ドロップします。

   ![create-a-workflow-pdf2](assets/create-a-workflow-pdf2.png)

1. プロセスステップを右クリックし、「 」を選択します。 **編集**. 「ステップのプロパティ」(Step Properties) ウィンドウが表示されます。

1. 「プロセス」タブで ECMAScript を選択します。例えば、「[ECMAScript の作成](#p-create-an-ecmascript-p)」で作成した pdfg-openOffice-sample.ecma スクリプトです。「**ハンドラー処理の設定**」オプションを有効にして「**OK**」をクリックします。

   ![create-a-workflow3-pdf](assets/create-a-workflow3-pdf.png)

### 監視フォルダーの設定 {#configure-the-watched-folder}

1. ブラウザーウィンドウで CRXDE lite を開きます。 https://&#39;[server]:[port]&#39;/crx/de/

1. /etc/fd/watchfolder/config/ フォルダーに移動して、nt:unstructured というタイプのノードを作成します。

   ![configure-the-watched-folder-pdf](assets/configure-the-watched-folder-pdf.png)

1. ノードに次のプロパティを追加します。

   * folderPath（文字列型）：定義した時間間隔でスキャンするフォルダーのパスです。 フォルダーが共有場所に存在し、すべてのサーバーが対象のサーバーに対するフルアクセス権を持っている必要があります。inputProcessorType（文字列型）：開始するプロセスのタイプです。このチュートリアルでは、workflow を指定します。

   * inputProcessorId( 文字列型 (String)): inputProcessorId プロパティの動作は、 inputProcessorType プロパティに指定された値に基づきます。 この例では、 inputProcessorType プロパティの値は workflow です。 そのため、inputProcessorId プロパティに PDFG ワークフローの次のパスを指定します。 /etc/workflow/models/pdfg/jcr:content/model

   * outputFilePattern（文字列型）：出力ファイルのパターンです。 フォルダまたはファイルパターンを指定できます。 フォルダーパターンを指定した場合、出力ファイルの名前はワークフローでの説明に従います。 ファイルパターンを指定した場合、出力ファイルの名前はファイルパターンで説明されているとおりになります。

   上記の必須プロパティに加えて、監視フォルダーはいくつかのオプションのプロパティもサポートしています。 オプションのプロパティの完全なリストと説明については、 [監視フォルダーのプロパティ](#watchedfolderproperties).

## 既知の問題 {#watched-folder-known-issues}

JEE 上の AEM 6.5 Forms を起動すると、JBoss が完全に起動する前にファイルの処理が開始され、ファイルの処理に失敗します。 この問題を回避するには、JBoss を起動する前に、すべての監視フォルダーを消去します。
