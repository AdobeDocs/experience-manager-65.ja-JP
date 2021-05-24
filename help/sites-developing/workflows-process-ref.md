---
title: ワークフロープロセスのリファレンス
seo-title: ワークフロープロセスのリファレンス
description: ワークフロープロセスのリファレンス
seo-description: 'null'
uuid: de367aa8-4580-4810-b665-2a7b521e36ca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: dbdf981f-791b-4ff7-8ca8-039d0bdc9c92
exl-id: a9de8ec6-6948-4643-89c3-62d9b1f6293a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 59%

---

# ワークフロープロセスのリファレンス{#workflow-process-reference}

AEM には、ワークフローモデルの作成に使用できるプロセスステップがいくつか用意されています。組み込みステップに含まれていないタスクについては、カスタムのプロセスステップを追加することができます（[ワークフローモデルの作成](/help/sites-developing/workflows-models.md)を参照）。

## プロセスの特徴  {#process-characteristics}

プロセスステップごとに特徴を説明します。

### Java クラスか ECMA パスか  {#java-class-or-ecma-path}

プロセスステップは、Java クラスまたは ECMAScript によって定義されます。

* Java クラスのプロセスの場合は、完全修飾クラス名を指定します。
* ECMAScript プロセスの場合は、スクリプトへのパスを指定します。

### ペイロード {#payload}

ペイロードは、ワークフローインスタンスの処理対象となるエンティティです。ペイロードは、ワークフローインスタンスが開始されるコンテキストによって暗黙的に選択されます。

例えば、ワークフローが AEM ページ「P **」に適用された場合は、ワークフローが進むたびに「P **」がステップからステップに引き渡され、各ステップで必要に応じて「P **」に対して何らかの処理がおこなわれます。

最も多いのは、ペイロードがリポジトリ内の JCR ノード（例えば AEM ページまたはアセット）である場合です。JCRノードのペイロードは、JCRパスまたはJCR識別子(UUID)の文字列として渡されます。 ペイロードは、JCRプロパティ（JCRパスとして渡される）、URL、バイナリオブジェクト、汎用Javaオブジェクトのいずれかになる場合があります。 ペイロードに対して動作する個々のプロセスステップは、通常、特定のタイプのペイロードを期待するか、ペイロードタイプに応じて動作が異なります。 以下に説明する各プロセスに対して、予想されるペイロードタイプ（存在する場合）が説明されます。

### 引数 {#arguments}

一部のワークフロープロセスは引数を受け取ります。引数は、ワークフローステップを設定するときに管理者が指定します。

引数は、ワークフローエディターの&#x200B;**プロパティ**&#x200B;ウィンドウの「**プロセスの引数**」プロパティに単一文字列として入力します。以下で説明する各プロセスに対して、引数文字列の形式は単純なEBNF文法で記述されます。 例えば、次の例は、引数文字列が1つ以上のコンマ区切りのペアで構成され、各ペアは名前（文字列）と値（二重コロンで区切られる）で構成されることを示します。

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### タイムアウト {#timeout}

このタイムアウト期間が経過すると、ワークフローステップは動作しなくなります。タイムアウトを適用するワークフロープロセスもありますが、タイムアウトを適用せず、無視するワークフロープロセスもあります。

### 権限 {#permissions}

`WorkflowProcess`に渡されたセッションは、ワークフロープロセスサービスのサービスユーザーによってバックアップされます。このユーザーは、リポジトリのルートに次の権限を持ちます。

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

`WorkflowProcess`実装にその権限セットで十分でない場合は、必要な権限を持つセッションを使用する必要があります。

これをおこなうには、必要な（ただし最小限の）権限のサブセットを持つよう作成されたサービスユーザーを使用する方法が推奨されます。

>[!CAUTION]
>
>AEM 6.2 より前のバージョンからアップグレードする場合は、実装の更新が必要になる場合があります。
>
>以前のバージョンでは、管理者セッションが `WorkflowProcess` 実装に渡されたので、特定の ACL を定義しなくてもリポジトリへのフルアクセスが可能でした。
>
>現在、権限は上述のように定義されています（[権限](#permissions)を参照）。実装を更新するために推奨される方法も同様です。
>
>また、コードの変更が実行不可能な場合は、後方互換性を確保する目的で、短期的なソリューションも利用できます。
>
>* Webコンソール( `/system/console/configMgr` )を使用して、**AdobeGranite Workflow Configuration Service**&#x200B;を探します。
   >
   >
* **Workflow Process Legacy Mode** を有効にします。
>
>
これにより、管理者セッションを `WorkflowProcess` 実装に渡すという古い動作に戻り、再びリポジトリ全体に無制限にアクセスできるようになります。

## ワークフロー制御プロセス {#workflow-control-processes}

次のプロセスは、コンテンツに対して何のアクションも実行しません。 ワークフロー自体の動作を制御する役割を果たします。

### AbsoluteTimeAutoAdvancer （絶対時自動アドバンサー） {#absolutetimeautoadvancer-absolute-time-auto-advancer}

`AbsoluteTimeAutoAdvancer`（絶対時刻自動アドバンサー）プロセスは、**AutoAdvancer** とまったく同じように動作します。例外は、指定された長さの時間が経過した後ではなく、指定された日時にタイムアウトする点です。

* **Java クラス**: `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **ペイロード**：なし
* **引数**：なし
* **タイムアウト**：設定された日時に達すると、プロセスはタイムアウトします。

### AutoAdvancer（自動アドバンサー） {#autoadvancer-auto-advancer}

`AutoAdvancer` プロセスは、ワークフローを次のステップに自動的に進めます。次に生じる可能性のあるステップが複数ある場合（例えば OR 分岐がある場合）、このプロセスは、デフォルトのルートが指定されているときはそのルートに沿ってワークフローを進め、指定されていないときはワークフローを進めません&#x200B;**。

* **Java クラス**: `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **ペイロード**：なし
* **引数**：なし
* **タイムアウト**：設定された時間が経過すると、プロセスはタイムアウトします。

### ProcessAssembler（プロセスアセンブラ） {#processassembler-process-assembler}

`ProcessAssembler` プロセスは、単一のワークフローステップ内で複数のサブプロセスを順番に実行します。`ProcessAssembler` を使用するには、ワークフロー内にこのタイプのステップを 1 つ作成し、実行するサブプロセスの名前と引数を示す引数を設定します。

* **Java クラス**: `com.day.cq.workflow.impl.process.ProcessAssembler`

* **ペイロード**：DAM アセット、AEM ページ、ペイロードなしのいずれか（サブプロセスの要件によって異なります）。
* **引数**：

```
        args := arg [',' arg]
        arg := processname ['::' processargs]
        processname := /* A fully qualified Java Class or absolute
        repository path to an ECMAScript */
        processargs := processarg [';' processarg]*
        processarg := '[' nobracketprocessarg ']' | nobracketprocessarg
        nobracketprocessarg := listitem [':' listitem]*
        listitem := /* A string */
```

* **タイムアウト**：適用されます。

次に例を示します。

* アセットからメタデータを抽出します。
* 指定した3つのサイズの3つのサムネールを作成します。
* アセットが元々GIFでもPNGでもない（JPEGが作成されない）と仮定して、アセットからJPEG画像を作成します。
* アセットの最終変更日を設定します。

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## 基本プロセス {#basic-processes}

以下のプロセスは単純なタスクを実行するか、例として機能します。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>これは、`/libs`のコンテンツが次回インスタンスをアップグレードすると（ホットフィックスまたは機能パックを適用すると上書きされる場合がある）ときに上書きされるからです。

### 次を削除します。 {#delete}

指定されたパスにある項目が削除されます。

* **ECMAScriptパス**:  `/libs/workflow/scripts/delete.ecma`

* **ペイロード**:JCRパス
* **引数**:なし
* **タイムアウト**:無視

### noop {#noop}

これはヌルプロセスです。処理は実行しませんが、デバッグメッセージをログに記録します。

* **ECMAScriptパス**:  `/libs/workflow/scripts/noop.ecma`

* **ペイロード**:なし
* **引数**:なし
* **タイムアウト**:無視

### rule-false {#rule-false}

これは、`check()`メソッドで`false`を返すnullプロセスです。

* **ECMAScriptパス**:  `/libs/workflow/scripts/rule-false.ecma`

* **ペイロード**:なし
* **引数**:なし
* **タイムアウト**:無視

### sample {#sample}

これは、ECMAScript プロセスのサンプルです。

* **ECMAScriptパス**:  `/libs/workflow/scripts/sample.ecma`

* **ペイロード**:なし
* **引数**:なし
* **タイムアウト**:無視

### urlcaller {#urlcaller}

これは、指定されたURLを呼び出す単純なワークフロープロセスです。 通常、URLは、単純なタスクを実行するJSP（または同等のサーブレット）への参照です。 このプロセスは開発およびデモンストレーションのときにのみ使用し、実稼動環境では使用しないようにする必要があります。引数は、URL、ログイン、パスワードを指定します。

* **ECMAScriptパス**:  `/libs/workflow/scripts/urlcaller.ecma`

* **ペイロード**:なし
* **引数**：

```
        args := url [',' login ',' password]
        url := /* The URL to be called */
        login := /* The login to access the URL */
        password := /* The password to access the URL */
```

例：`http://localhost:4502/my.jsp, mylogin, mypassword`

* **タイムアウト**:無視

### LockProcess {#lockprocess}

ワークフローのペイロードをロックします。

* **Java クラス:** `com.day.cq.workflow.impl.process.LockProcess`

* **ペイロード：** JCR_PATHおよびJCR_UUID
* **引数：**&#x200B;なし
* **タイムアウト：**&#x200B;無視されます。

次の状況下では、このステップは無効です。

* ペイロードは既にロックされています
* payloadノードにjcr:content子ノードが含まれていない

### UnlockProcess {#unlockprocess}

ワークフローのペイロードをロック解除します。

* **Java クラス:** `com.day.cq.workflow.impl.process.UnlockProcess`

* **ペイロード：** JCR_PATHおよびJCR_UUID
* **引数：**&#x200B;なし
* **タイムアウト：**&#x200B;無視されます。

次の状況下では、このステップは無効です。

* ペイロードは既にロック解除されています
* payloadノードにjcr:content子ノードが含まれていない

## バージョン管理プロセス {#versioning-processes}

以下のプロセスは、バージョン関連のタスクを実行します。

### CreateVersionProcess {#createversionprocess}

ワークフローペイロード（AEM ページまたは DAM アセット）の新しいバージョンを作成します。

* **Java クラス**: `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **ペイロード**:ページまたはDAMアセットを参照するJCRパスまたはUUID
* **引数**:なし
* **タイムアウト**:尊重
