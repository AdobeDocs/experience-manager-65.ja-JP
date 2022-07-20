---
title: ワークフロープロセスのリファレンス
seo-title: Workflow Process Reference
description: ワークフロープロセスのリファレンス
seo-description: null
uuid: de367aa8-4580-4810-b665-2a7b521e36ca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: dbdf981f-791b-4ff7-8ca8-039d0bdc9c92
exl-id: a9de8ec6-6948-4643-89c3-62d9b1f6293a
source-git-commit: cf3b739fd774bc860d9906b9884d22fd532fd5dd
workflow-type: ht
source-wordcount: '1075'
ht-degree: 100%

---

# ワークフロープロセスのリファレンス{#workflow-process-reference}

AEM には、ワークフローモデルの作成に使用できるプロセスステップがいくつか用意されています。組み込みステップに含まれていないタスクについては、カスタムのプロセスステップを追加することができます（[ワークフローモデルの作成](/help/sites-developing/workflows-models.md)を参照）。

## プロセスの特徴 {#process-characteristics}

プロセスステップごとに特徴を説明します。

### Java クラスか ECMA パスか {#java-class-or-ecma-path}

プロセスステップは、Java クラスまたは ECMAScript によって定義されます。

* Java クラスのプロセスの場合は、完全修飾クラス名を指定します。
* ECMAScript プロセスの場合は、スクリプトへのパスを指定します。

### ペイロード {#payload}

ペイロードは、ワークフローインスタンスの処理対象となるエンティティです。ペイロードは、ワークフローインスタンスが開始されるコンテキストによって暗黙的に選択されます。

例えば、ワークフローが AEM ページ「*P*」に適用された場合は、ワークフローが進むたびに「*P*」が手順から手順に引き渡され、各手順で必要に応じて「*P*」に対して何らかの処理がおこなわれます。

最も多いのは、ペイロードがリポジトリ内の JCR ノード（例えば AEM ページまたはアセット）である場合です。JCR ノードのペイロードは、JCR パスまたは JCR 識別子（UUID）のいずれかの文字列として渡されます。ペイロードは、JCR プロパティ（JCR パスとして渡されます）、URL、バイナリオブジェクト、汎用 Java オブジェクトのいずれかである場合もあります。ペイロードに対して動作するプロセスの個々の手順は、通常、特定のタイプのペイロードを想定しているか、ペイロードタイプに応じて異なる動作をします。次の各プロセスでは、想定するペイロードタイプ（存在する場合）を記述しています。

### 引数 {#arguments}

一部のワークフロープロセスは引数を受け取ります。引数は、ワークフローステップを設定するときに管理者が指定します。

引数は、ワークフローエディターの&#x200B;**プロパティ**&#x200B;ウィンドウの「**プロセスの引数**」プロパティに単一文字列として入力します。次の各プロセスでは、引数文字列の形式を単純な EBNF 文法で記述しています。次のように、引数の文字列は 1 つまたは複数のコンマ区切りのペアで構成されています。各ペアは、2 つのコロンで区切られた名前（文字列）と値で構成されます。

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### タイムアウト {#timeout}

このタイムアウト期間が経過すると、ワークフローステップは動作しなくなります。タイムアウトを適用するワークフロープロセスもありますが、タイムアウトを適用せず、無視するワークフロープロセスもあります。

### 権限 {#permissions}

`WorkflowProcess` に渡されたセッションは、ワークフロープロセスサービスのサービスユーザーをベースとしています。このユーザーは、リポジトリのルートで次の権限を持っています。

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

この権限セットが `WorkflowProcess` の実装に十分でない場合は、必要な権限を持つセッションを使用する必要があります。

これをおこなうには、必要な（ただし最小限の）権限のサブセットを持つよう作成されたサービスユーザーを使用する方法が推奨されます。

>[!CAUTION]
>
>AEM 6.2 より前のバージョンからアップグレードする場合は、実装の更新が必要になる場合があります。
>
>以前のバージョンでは、管理者セッションが `WorkflowProcess` 実装に渡されたので、特定の ACL を定義しなくてもリポジトリへのフルアクセスが可能でした。
>
>現在、権限は上述のように定義されています（[権限](#permissions)を参照）。実装を更新するために推奨される方法も同様です。
>
>コード変更が不可能な場合には、下位互換性を維持する目的で、短期的なソリューションも使用できます。
>
>* Web コンソール（`/system/console/configMgr`/）を使用して、**Adobe Granite ワークフロー設定サービス**&#x200B;を探します
>
>* **ワークフロープロセスのレガシーモード**&#x200B;を有効にします
>
>これにより、管理者セッションを `WorkflowProcess` 実装に渡すという古い動作に戻り、再びリポジトリ全体に無制限にアクセスできるようになります。

## ワークフロー制御プロセス {#workflow-control-processes}

次のプロセスは、コンテンツに対するアクションを実行しません。ワークフロー自体の動作を制御する役割を果たします。

### AbsoluteTimeAutoAdvancer（絶対時刻自動アドバンサー） {#absolutetimeautoadvancer-absolute-time-auto-advancer}

`AbsoluteTimeAutoAdvancer`（絶対時刻自動アドバンサー）プロセスは、**AutoAdvancer** と同じように動作します。ただし、指定された長さの時間が経過した後ではなく、指定された日時にタイムアウトする点が異なります。

* **Java クラス**：`com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **ペイロード**：なし.
* **引数**：なし.
* **タイムアウト**：設定された日時に達すると、プロセスはタイムアウトします。

### AutoAdvancer（自動アドバンサー） {#autoadvancer-auto-advancer}

`AutoAdvancer` プロセスは、ワークフローを次の手順に自動的に進めます。次に生じる可能性のある手順が複数ある場合（例えば OR 分岐がある場合）、このプロセスは、*デフォルトのルート*&#x200B;が指定されているときはそのルートに沿ってワークフローを進め、指定されていないときはワークフローを進めません。

* **Java クラス**：`com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **ペイロード**：なし.
* **引数**：なし.
* **タイムアウト**：設定された時間が経過すると、プロセスはタイムアウトします。

### ProcessAssembler（プロセスアセンブラー） {#processassembler-process-assembler}

`ProcessAssembler` プロセスは、ワークフローの単一の手順内で複数のサブプロセスを順番に実行します。`ProcessAssembler` を使用するには、ワークフロー内にこのタイプの手順を 1 つ作成し、実行するサブプロセスの名前と引数を示す引数を設定します。

* **Java クラス**：`com.day.cq.workflow.impl.process.ProcessAssembler`

* **ペイロード**：DAM アセット、AEM ページ、ペイロードなしのいずれか（サブプロセスの要件に応じて異なります）。
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

次は例です。

* アセットからメタデータを抽出します。
* 指定した 3 つのサイズの 3 つのサムネールを作成します。
* アセットが元々 GIF でも PNG でもない場合（この場合は JPEG が作成されない）、アセットから JPEG 画像を作成します。
* アセットの最終更新日を設定します。

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## 基本プロセス {#basic-processes}

次のプロセスは単純なタスクを実行するか、例として機能します。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>`/libs` のコンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。

### delete {#delete}

指定されたパスにある項目が削除されます。

* **ECMAScript パス**：`/libs/workflow/scripts/delete.ecma`

* **ペイロード**：JCR パス
* **引数**：なし
* **タイムアウト**：無視されます

### noop {#noop}

これはヌルプロセスです。処理は実行しませんが、デバッグメッセージをログに記録します。

* **ECMAScript パス**：`/libs/workflow/scripts/noop.ecma`

* **ペイロード**：なし
* **引数**：なし
* **タイムアウト**：無視されます。

### rule-false {#rule-false}

これは、`check()` メソッドで `false` を返す null プロセスです。

* **ECMAScript パス**：`/libs/workflow/scripts/rule-false.ecma`

* **ペイロード**：なし
* **引数**：なし
* **タイムアウト**：無視されます。

### sample {#sample}

これは、ECMAScript プロセスのサンプルです。

* **ECMAScript パス**：`/libs/workflow/scripts/sample.ecma`

* **ペイロード**：なし
* **引数**：なし
* **タイムアウト**：無視されます

### LockProcess {#lockprocess}

ワークフローのペイロードをロックします。

* **Java クラス：** `com.day.cq.workflow.impl.process.LockProcess`

* **ペイロード：** JCR_PATH と JCR_UUID
* **引数：**&#x200B;なし
* **タイムアウト：**&#x200B;無視されます。

次の状況下では、このステップは無効です。

* ペイロードが既にロックされている
* ペイロードノードに jcr:content 子ノードが含まれていない

### UnlockProcess {#unlockprocess}

ワークフローのペイロードをロック解除します。

* **Java クラス：** `com.day.cq.workflow.impl.process.UnlockProcess`

* **ペイロード：** JCR_PATH と JCR_UUID
* **引数：**&#x200B;なし
* **タイムアウト：**&#x200B;無視されます。

次の状況下では、このステップは無効です。

* ペイロードが既にロック解除されている
* ペイロードノードに jcr:content 子ノードが含まれていない

## バージョン管理プロセス {#versioning-processes}

以下のプロセスは、バージョン関連のタスクを実行します。

### CreateVersionProcess {#createversionprocess}

ワークフローペイロード（AEM ページまたは DAM アセット）の新しいバージョンを作成します。

* **Java クラス**：`com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **ペイロード**：ページまたは DAM アセットを参照する JCR パスまたは UUID。
* **引数**：なし
* **タイムアウト**：適用されます。
