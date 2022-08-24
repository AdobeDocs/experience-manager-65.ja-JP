---
title: VLT ツールを使用する方法
seo-title: How to use the VLT Tool
description: Jackrabbit FileVault ツール（VLT）は、Jackrabbit／AEM インスタンスのコンテンツをファイルシステムにマップするためのツールで、The Apache Foundation によって開発されました
seo-description: The Jackrabbit FileVault tool (VLT) is developed by The Apache Foundation that maps the content of a Jackrabbit/AEM instance to your file system
uuid: 579e7785-8b50-4366-b562-8e79b6451464
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a76425e9-fd3b-4c73-80f9-0ebabb8fd94f
exl-id: efbba312-9fc8-4670-b8f1-d2a86162d075
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2718'
ht-degree: 100%

---

# VLT ツールの使用方法 {#how-to-use-the-vlt-tool}

Jackrabbit FileVault ツール（VLT）は、Jackrabbit／AEM インスタンスのコンテンツをファイルシステムにマップするためのツールで、[The Apache Foundation](https://www.apache.org/) によって開発されました。VLT ツールの機能はソース管理システムクライアント（Subversion（SVN）クライアントなど）に似ており、通常のチェックイン、チェックアウト、管理操作をおこなうことができるほか、プロジェクトのコンテンツを柔軟に表現するための設定オプションも用意されています。

VLT ツールはコマンドラインから実行します。このドキュメントでは、ツールの使い方（導入方法、ヘルプの表示方法、すべての[コマンド](#vlt-commands)と使用可能な[オプション](#vlt-global-options)のリストを含む）について説明します。

## 概念およびアーキテクチャ {#concepts-and-architecture}

Filevault ツールの概念と構造の完全な概要については、公式の [Apache Jackrabbit Filevault ドキュメント](https://jackrabbit.apache.org/filevault/index.html)の [Filevault の概要](https://jackrabbit.apache.org/filevault/overview.html)および [Vault FS](https://jackrabbit.apache.org/filevault/vaultfs.html) ページを参照してください。

## VLT の導入 {#getting-started-with-vlt}

VLT の使用を開始するには、次の手順を実行する必要があります。

1. VLT をインストールして、環境変数を更新し、グローバルに無視されている subversion ファイルを更新します。
1. AEM リポジトリをセットアップします（セットアップが完了していない場合）。
1. AEM リポジトリをチェックアウトします。
1. リポジトリとの同期をおこないます。
1. 同期が正しくおこなわれたかどうかをテストします。

### VLT ツールのインストール {#installing-the-vlt-tool}

VLT ツールを使用するには、まず VLT ツールをインストールする必要があります。追加のツールなので、デフォルトではインストールされません。また、システムの環境変数を設定する必要があります。

1. FileVault アーカイブファイルを [Maven アーティファクトリポジトリ](https://repo1.maven.org/maven2/org/apache/jackrabbit/vault/vault-cli/)からダウンロードします。
   >[!NOTE]
   >
   >VLT ツールのソースは [GitHub で入手](https://github.com/apache/jackrabbit-filevault)できます。
1. アーカイブを解凍します。
1. `<archive-dir>/vault-cli-<version>/bin` を環境の `PATH` に追加して、コマンドファイル `vlt` または `vlt.bat` に適宜アクセスできるようにします。次に例を示します。

   `<aem-installation-dir>/crx-quickstart/opt/helpers/vault-cli-3.1.16/bin>`

1. コマンドラインシェルを開き、`vlt --help` を実行します。出力が次のヘルプ画面に似ていることを確認します。

   ```shell
   vlt --help
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Usage:
     vlt [options] <command> [arg1 [arg2 [arg3] ..]]
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   
   Global options:
   
     -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
     -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
     --credentials <arg>      The default credentials to use
     --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
     --config <arg>           The JcrFs config to use
     -v (--verbose)           verbose output
     -q (--quiet)             print as little as possible
     --version                print the version information and exit
     --log-level <level>      the log4j log level
     -h (--help) <command>    print this help
   ```

インストールが完了したら、グローバルに無視されている subversion ファイルを更新する必要があります。svn 設定を編集して次の情報を追加します。

```xml
[miscellany]
### Set global-ignores to a set of whitespace-delimited globs
### which Subversion will ignore in its 'status' output, and
### while importing or adding files and directories.
global-ignores = .vlt
```

### 行末の文字の設定 {#configuring-the-end-of-line-character}

VLT は、次のルールに従って行末（EOF）を自動的に処理します。

* Windows でチェックアウトされたファイルの行は `CRLF` で終わる。
* Linux／Unix でチェックアウトされたファイルの行は `LF` で終わる。
* リポジトリにコミットされたファイルの行は `LF` で終わる。

VLT と SVN の設定を一致させるには、リポジトリに格納されたファイルの拡張子に対して `svn:eol-style` プロパティを `native` に設定する必要があります。svn 設定を編集して次の情報を追加します。

```xml
[auto-props]
*.css = svn:eol-style=native
*.cnd = svn:eol-style=native
*.java = svn:eol-style=native
*.js = svn:eol-style=native
*.json = svn:eol-style=native
*.xjson = svn:eol-style=native
*.jsp = svn:eol-style=native
*.txt = svn:eol-style=native
*.html = svn:eol-style=native
*.xml = svn:eol-style=native
*.properties = svn:eol-style=native
```

### リポジトリのチェックアウト {#checking-out-the-repository}

ソース管理システムを使用してリポジトリをチェックアウトします。例えば svn では、次のように入力します（URI とパスはお使いのリポジトリのものに置き換えてください）。

```shell
svn co https://svn.server.com/repos/myproject
```

### リポジトリとの同期 {#synchronizing-with-the-repository}

filevault とリポジトリを同期する必要があります。次の手順を実行します。

1. コマンドラインで、`content/jcr_root` に移動します。
1. 次のように入力してリポジトリをチェックアウトします（**4502** をお使いのポート番号に置き換えて、お使いの admin パスワードを使用してください）。

   ```shell
   vlt --credentials admin:admin co --force http://localhost:4502/crx
   ```

   >[!NOTE]
   >
   >資格情報は最初のチェックアウト時に 1 回だけ指定してください。これで、`.vault/auth.xml` 内のホームディレクトリに情報が格納されます。

### 同期が正しくおこなわれたかどうかのテスト {#testing-whether-the-synchronization-worked}

リポジトリのチェックアウトと同期が完了したら、すべてが適切に機能しているかどうかをテストする必要があります。このテストを簡単に行うには、**.jsp** ファイルを編集して、変更をコミットした後に変更が反映されているかどうかを確認します。

同期をテストするには：

1. `.../jcr_content/libs/foundation/components/text` に移動します。
1. `text.jsp` 内の項目を編集します。
1. `vlt st` を入力して、変更されたファイルを確認します。
1. `vlt diff text.jsp` を入力して、変更を確認します。
1. 変更 `vlt ci test.jsp` をコミットします。
1. テキストコンポーネントを含むページを再読み込みして、変更が反映されているかどうかを確認します。

## VLT ツールのヘルプの表示 {#getting-help-with-the-vlt-tool}

VLT ツールのインストールが完了したら、コマンドラインからヘルプファイルにアクセスできます。

```shell
vlt --help
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Usage:
  vlt [options] <command> [arg1 [arg2 [arg3] ..]]
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Global options:
  -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
  -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
  --credentials <arg>      The default credentials to use
  --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
  --config <arg>           The JcrFs config to use
  -v (--verbose)           verbose output
  -q (--quiet)             print as little as possible
  --version                print the version information and exit
  --log-level <level>      the log4j log level
  -h (--help) <command>    print this help
Commands:
  export                   Export the Vault filesystem
  import                   Import a Vault filesystem
  checkout (co)            Checkout a Vault file system
  status (st)              Print the status of working copy files and directories.
  update (up)              Bring changes from the repository into the working copy.
  info                     Displays information about a local file.
  commit (ci)              Send changes from your working copy to the repository.
  revert (rev)             Restore pristine working copy file (undo most local edits).
  resolved (res)           Remove 'conflicted' state on working copy files or directories.
  propget (pg)             Print the value of a property on files or directories.
  proplist (pl)            Print the properties on files or directories.
  propset (ps)             Set the value of a property on files or directories.
  add                      Put files and directories under version control.
  delete (del,rm)          Remove files and directories from version control.
  diff (di)                Display the differences between two paths.
  rcp                      Remote copy of repository content.
  sync                     Control vault sync service
  console                  Run an interactive console
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
```

特定のコマンドに関するヘルプを表示するには、help コマンドの後にそのコマンドの名前を入力します。次は例です。

```shell
vlt --help export
Usage:
 export -v|-t <arg>|-p <uri> <jcr-path> <local-path>

Description:
  Export the Vault filesystem mounted at <uri> to the local filesystem at <local-path>. An optional <jcr-path> can be specified in order to export just a sub tree.
  Example:
    vlt export http://localhost:4502/crx /apps/geometrixx myproject

Options:
  -v (--verbose)          verbose output
  -t (--type) <arg>       specifies the export type. either 'platform' or 'jar'.
  -p (--prune-missing)    specifies if missing local files should be deleted.
  <uri>                   mountpoint uri
  <jcr-path>              the jcr path
  <local-path>            the local path
```

## VLT で実行される一般的なタスク {#common-tasks-performed-in-vlt}

VLT で実行される一般的なタスクの一部を次に示します。各コマンドについて詳しくは、個々の[コマンド](#vlt-commands)を参照してください。

### サブツリーのチェックアウト {#checking-out-a-subtree}

リポジトリのサブツリー（例：`/apps/geometrixx`）のチェックアウトのみを行う場合は、次のように入力します。

```shell
vlt co http://localhost:4502/crx/-/jcr:root/apps/geometrixx geo
```

これにより、エクスポート用の新しいルート `geo` が `META-INF` と `jcr_root` ディレクトリで作成され、`/apps/geometrixx` の下のすべてのファイルが `geo/jcr_root` に配置されます。

### フィルターが適用されたチェックアウトの実行 {#performing-a-filtered-checkout}

既存のワークスペースフィルターがあり、チェックアウトにそのフィルターを使用する場合は、最初に `META-INF/vault` ディレクトリを作成してそこにフィルターを配置するか、またはコマンドラインで次のようにフィルターを指定します。

```shell
$ vlt co --filter filter.xml http://localhost:4502/crx/-/jcr:root geo
```

フィルターの例は次のとおりです。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/etc/designs/geometrixx" />
    <filter root="/apps/geometrixx"/>
</workspaceFilter>
```

### .vlt コントロールの代わりとしてのインポート／エクスポートの使用 {#using-import-export-instead-of-vlt-control}

コントロールファイルを使用せずに、JCR リポジトリとローカルファイルシステムとの間でコンテンツのインポートとエクスポートを行うことができます。

`.vlt` コントロールを使用せずにコンテンツのインポートとエクスポートを行うには：

1. 最初にリポジトリをセットアップします。

   ```shell
   $ cd /projects
   $ svn mkdir https://svn.server.com/repos/myproject
   $ svn co https://svn.server.com/repos/myproject
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx geometrixx
   $ cd geometrixx/
   $ svn add META-INF/ jcr_root/
   $ svn ci
   ```

1. リモートコピーを変更して JCR を更新します。

   ```shell
   $ cd /projects/geometrixx
   $ vlt -v import http://localhost:4502/crx . /
   ```

1. リモートコピーを変更してファイルサーバーを更新します。

   ```shell
   $ cd /projects/geometrixx
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx .
   $ svn st
   M      META-INF/vault/properties.xml
   M      jcr_root/apps/geometrixx/components/contentpage/.content.xml
   $ svn ci
   ```

## VLT の使用 {#using-vlt}

VLT でコマンドを実行するには、コマンドラインで次のように入力します。

```shell
vlt [options] <command> [arg1 [arg2 [arg3] ..]]  
```

以降の節で、オプションとコマンドについて詳しく説明します。

## VLT のグローバルオプション {#vlt-global-options}

すべてのコマンドで使用できる VLT のオプションのリストを次に示します。使用できるその他のオプションについては、個々のコマンドを参照してください。

|  |  |
|--- |--- |
| オプション | 説明 |
| `-Xjcrlog <arg>` | 拡張された JcrLog オプション |
| `-Xdavex <arg>` | 拡張された JCR のリモート処理のオプション |
| `--credentials <arg>` | 使用するデフォルトの資格情報 |
| `--config <arg>` | 使用する JcrFs 設定 |
| `-v (--verbose)` | 詳細出力 |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `--version` | バージョン情報を出力して VLT を終了します |
| `--log-level <level>` | ログレベル（例：log4j ログレベル）を示します。 |
| `-h (--help) <command>` | 特定のコマンドのヘルプを出力します |

## VLT のコマンド {#vlt-commands}

次の表は、使用可能なすべての VLT コマンドを示しています。構文、使用可能なオプションおよび例について詳しくは、個々のコマンドを参照してください。

|  |  |  |
|--- |--- |--- |
| コマンド | 短縮コマンド | 説明 |
| `export` |  | コントロールファイルを使用せずに JCR リポジトリ（vault ファイルシステム）からローカルファイルシステムにエクスポートします。 |
| `import` |  | ローカルファイルシステムを JCR リポジトリ（vault ファイルシステム）にインポートします。 |
| `checkout` | `co` | Vault ファイルシステムをチェックアウトします。最初の JCR リポジトリをローカルファイルシステムにチェックアウトする場合にこのコマンドを使用します（メモ：最初に subversion でリポジトリをチェックアウトする必要があります）。 |
| `analyze` |  | パッケージを分析します。 |
| `status` | `st` | 作業用コピーファイルとディレクトリのステータスを出力します。 |
| `update` | `up` | リポジトリから作業用コピーに変更を読み込みます。 |
| `info` |  | ローカルファイルに関する情報を表示します。 |
| `commit` | `ci` | 作業用コピーからリポジトリに変更を送信します。 |
| `revert` | `rev` | 作業用コピーファイルを元の状態に復元して、大部分のローカルの編集を元に戻します。 |
| `resolved` | `res` | 作業用コピーファイルまたはディレクトリの競合状態を削除します。 |
| `propget` | `pg` | ファイルまたはディレクトリのプロパティの値を出力します。 |
| `proplist` | `pl` | ファイルまたはディレクトリのプロパティを出力します。 |
| `propset` | `ps` | ファイルまたはディレクトリのプロパティの値を設定します。 |
| `add` |  | ファイルとディレクトリのバージョンを管理します。 |
| `delete` | `del` か `rm` のどちらかにする必要があります。 | ファイルとディレクトリのバージョン管理を削除します。 |
| `diff` | `di` | 2 つのパスの差分を表示します。 |
| `console` |  | インタラクティブコンソールを実行します。 |
| `rcp` |  | ノードツリーをリモートリポジトリ間でコピーします。 |
| `sync` |  | vault 同期サービスを制御できるようにします。 |

### エクスポート {#export}

&lt;uri> でマウントされた Vault ファイルシステムをローカルファイルシステム（&lt;local-path>）に書き出します。サブツリーのみをエクスポートするには、オプションの &lt;jcr-path> を指定できます。

#### 構文 {#syntax}

```shell
export -v|-t <arg>|-p <uri> <jcr-path> <local-path>
```

#### オプション {#options}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細出力 |
| `-t (--type) <arg>` | エクスポートのタイプ（platform または jar）を指定します。 |
| `-p (--prune-missing)` | 見つからないローカルファイルを削除する必要がある場合に指定します。 |
| `<uri>` | マウントポイントの URI |
| `<jcrPath>` | JCR パス |
| `<localPath>` | ローカルパス |

#### 例 {#examples}

```shell
vlt export http://localhost:4502/crx /apps/geometrixx myproject
```

### import {#import}

`<local-path>` で始まるローカルファイルシステムを vault ファイルシステム（`<uri>`）に読み込みます。`<jcr-path>` をインポートのルートとして指定できます。`--sync` が指定されている場合は、読み込むファイルは自動的に vault 管理下に置かれます。

#### 構文 {#syntax-1}

```shell
import -v|-s <uri> <local-path> <jcr-path>
```

#### オプション {#options-1}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細出力 |
| `-s (-- sync)` | ローカルファイルを vault 管理下に置きます |
| `<uri>` | マウントポイントの URI |
| `<jcrPath>` | JCR パス |
| `<localPath>` | ローカルパス |

#### 例 {#examples-1}

```shell
vlt import http://localhost:4502/crx . /
```

### checkout（co） {#checkout-co}

JCR リポジトリから &lt;uri> で始まるローカルファイルシステムおよび &lt;local-path> で始まるローカルファイルシステムへの最初のチェックアウトを順に実行します。&lt;jcrPath> 引数を追加して、リモートツリーのサブディレクトリをチェックアウトすることもできます。META-INF ディレクトリにコピーするワークスペースフィルターを指定できます。

#### 構文 {#syntax-2}

```shell
checkout --force|-v|-q|-f <file> <uri> <jcrPath> <localPath>  
```

#### オプション {#options-2}

|  |  |
|--- |--- |
| `--force` | ローカルファイルが既に存在する場合は、チェックアウトを実行してそのファイルを強制的に上書きします |
| `-v (--verbose)` | 詳細 Output |
| `-q (--quiet)` | 最小限に抑えた出力 |
| `-f (--filter) <file>` | 自動フィルターを指定（定義されていない場合） |
| `<uri>` | マウントポイントの URI |
| `<jcrPath>` | （オプション）リモートパス |
| `<localPath>` | （オプション）ローカルパス |

#### 例 {#examples-2}

JCR のリモート処理を使用する場合：

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/crx.default/jcr_root/
```

デフォルトのワークスペースを使用する場合：

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/-/jcr_root/
```

URI が不完全な場合は、展開されます。

```shell
vlt --credentials admin:admin co http://localhost:8080/crx
```

### 分析 {#analyze}

パッケージを分析します。

#### 構文 {#syntax-3}

```shell
analyze -l <format>|-v|-q <localPaths1> [<localPaths2> ...]
```

#### オプション {#options-3}

|  |  |
|--- |--- |
| `-l (--linkFormat) <format>` | ホットフィックスのリンクの出力形式（名前、ID）（例：`[CQ520_HF_%s|%s]`） |
| `-v (--verbose)` | 詳細 Output |
| `-q (--quiet)` | 最小限に抑えた出力 |
| `<localPaths> [<localPaths> ...]` | ローカルパス |

### ステータス {#status}

作業用コピーファイルとディレクトリのステータスを出力します。

`--show-update` が指定されている場合は、各ファイルがリモートのバージョンと照合されます。2 番目の文字は、更新操作によって実行されるアクションを指定します。

#### 構文 {#syntax-4}

```shell
status -v|-q|-u|-N <file1> [<file2> ...]
```

#### オプション {#options-4}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細 Output |
| `-q (--quiet)` | 最小限に抑えた出力 |
| `-u (--show-update)` | 更新情報を表示 |
| `-N (--non-recursive)` | 単一のディレクトリで動作 |
| `<file> [<file> ...]` | ステータスを表示するファイルまたはディレクトリ |

### アップデート {#update}

リポジトリから作業用コピーに変更をコピーします。

#### 構文 {#syntax-5}

```shell
update -v|-q|--force|-N <file1> [<file2> ...]
```

#### オプション {#options-5}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細 Output |
| `-q (--quiet)` | 最小限に抑えた出力 |
| `--force` | ローカルファイルの上書きを強制 |
| `-N (--non-recursive)` | 単一のディレクトリで動作 |
| `<file> [<file> ...]` | 更新するファイルまたはディレクトリ |

### 情報 {#info}

ローカルファイルに関する情報を表示します。

#### 構文 {#syntax-6}

```shell
info -v|-q|-R <file1> [<file2> ...]
```

#### オプション {#options-6}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細 Output |
| `-q (--quiet)` | 最小限に抑えた出力 |
| `-R (--recursive)` | 再帰的に動作 |
| `<file> [<file> ...]` | 情報を表示するファイルまたはディレクトリ |

### commit {#commit}

作業用コピーからリポジトリに変更を送信します。

#### 構文 {#syntax-7}

```shell
commit -v|-q|--force|-N <file1> [<file2> ...]
```

#### オプション {#options-7}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細 Output |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `--force` | リモートコピーが変更される場合でも、強制的にコミットします |
| `-N (--non-recursive)` | 単一のディレクトリで処理が実行されます |
| `<file> [<file> ...]` | コミットするファイルまたはディレクトリ |

### 元に戻す {#revert}

作業用コピーファイルを元の状態に復元して、大部分のローカルの編集を元に戻します。

#### 構文 {#syntax-8}

```shell
revert -q|-R <file1> [<file2> ...]
```

#### オプション {#options-8}

|  |  |
|--- |--- |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `-R (--recursive)` | 処理を再帰的に実行します |
| `<file> [<file> ...]` | コミットするファイルまたはディレクトリ |

### Resolved {#resolved}

作業用コピーファイルまたはディレクトリの&#x200B;**競合**&#x200B;状態を削除します。

>[!NOTE]
>
>このコマンドは意味的に競合を解決したり、競合のマーカーを削除したりするのではなく、単に競合に関連するアーティファクトファイルを削除して、PATH を再びコミットできるようにします。

#### 構文 {#syntax-9}

```shell
resolved -q|-R|--force <file1> [<file2> ...]  
```

#### オプション {#options-9}

|  |  |
|--- |--- |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `-R (--recursive)` | 処理を再帰的に実行します |
| `--force` | 競合のマーカーがある場合でも解決を実行します |
| `<file> [<file> ...]` | 解決するファイルまたはディレクトリ |

### propget {#propget}

ファイルまたはディレクトリのプロパティの値を出力します。

#### 構文 {#syntax-10}

```shell
propget -q|-R <propname> <file1> [<file2> ...]
```

#### オプション {#options-10}

|  |  |
|--- |--- |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `-R (--recursive)` | 処理を再帰的に実行します |
| `<propname>` | プロパティ名 |
| `<file> [<file> ...]` | プロパティの取得元のファイルまたはディレクトリ |

### proplist {#proplist}

ファイルまたはディレクトリのプロパティを出力します。

#### 構文 {#syntax-11}

```shell
proplist -q|-R <file1> [<file2> ...]
```

#### オプション {#options-11}

|  |  |
|--- |--- |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `-R (--recursive)` | 処理を再帰的に実行します |
| `<file> [<file> ...]` | プロパティの出力元のファイルまたはディレクトリ |

### propset {#propset}

ファイルまたはディレクトリのプロパティの値を設定します。

>[!NOTE]
>
>VLT は、バージョン管理された次の特殊なプロパティを認識します。 
>
>`vlt:mime-type`
>
>ファイルの MIME タイプ。ファイルを結合するかどうかを判断するために使用します。「text/」で始まる MIME タイプ（または MIME タイプが存在しない場合）はテキストとして扱われます。それ以外の MIME タイプはバイナリとして扱われます。

#### 構文 {#syntax-12}

```shell
propset -q|-R <propname> <propval> <file1> [<file2> ...]
```

#### オプション {#options-12}

|  |  |
|--- |--- |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `-R (--recursive)` | 処理を再帰的に実行します |
| `<propname>` | プロパティ名 |
| `<propval>` | プロパティ値 |
| `<file> [<file> ...]` | プロパティを設定するファイルまたはディレクトリ |

### add {#add}

ファイルとディレクトリのバージョンを管理し、それらをリポジトリに追加するスケジュールを設定します。これらは次回のコミット時に追加されます。

#### 構文 {#syntax-13}

```shell
add -v|-q|-N|--force <file1> [<file2> ...]
```

#### オプション {#options-13}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細 Output |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `-N (--non-recursive)` | 単一のディレクトリで処理を実行します |
| `--force` | 操作を強制的に実行します |
| `<file> [<file> ...]` | 追加するローカルファイルまたはディレクトリ |

### 削除 {#delete}

ファイルとディレクトリのバージョン管理を削除します。

#### 構文 {#syntax-14}

```shell
delete -v|-q|--force <file1> [<file2> ...]
```

#### オプション {#options-14}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細 Output |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `--force` | 操作を強制的に実行します |
| `<file> [<file> ...]` | 削除するローカルファイルまたはディレクトリ |

### diff {#diff}

2 つのパスの差分を表示します。

#### 構文 {#syntax-15}

```shell
diff -N <file1> [<file2> ...]
```

#### オプション {#options-15}

|  |  |
|--- |--- |
| `-N (--non-recursive)` | 単一のディレクトリで処理を実行します |
| `<file> [<file> ...]` | 差分を表示するファイルまたはディレクトリ |

### コンソール {#console}

インタラクティブコンソールを実行します。

#### 構文 {#syntax-16}

```shell
console -F <file>
```

#### オプション {#options-16}

|  |  |
|--- |--- |
| `-F (--console-settings) <file>` | コンソール設定ファイルを指定します。デフォルトのファイルは console.properties です。 |

### rcp {#rcp}

ノードツリーをリモートリポジトリ間でコピーします。`<src>`はコピー元のノードを指し、`<dst>`でコピー先のパスを指定します。親ノードが存在するパスである必要があります。rcp は、データをストリーミングすることでノードを処理します。

#### 構文 {#syntax-17}

```shell
rcp -q|-r|-b <size>|-t <seconds>|-u|-n|-e <arg1> [<arg2> ...] <src> <dst>
```

#### オプション {#options-17}

|  |  |
|--- |--- |
| `-q (--quiet)` | 出力を最小限に抑えます。 |
| `-r (--recursive)` | 再帰的に実行します。 |
| `-b (--batchSize) <size>` | 中間保存の前に処理するノードの数。 |
| `-t (--throttle) <seconds>` | 中間保存の後に待機する秒数。 |
| `-u (--update)` | 既存のノードを上書きまたは削除します。 |
| `-n (--newer)` | lastModified プロパティを更新に適用します。 |
| `-e (--exclude) <arg> [<arg> ...]` | 除外するコピー元のパスの正規表現。 |
| `<src>` | コピー元のツリーのリポジトリのアドレス。 |
| `<dst>` | コピー先のノードのリポジトリのアドレス。 |

#### 例 {#examples-3}

```shell
vlt rcp http://localhost:4502/crx/-/jcr:root/content  https://admin:admin@localhost:4503/crx/-/jcr:root/content_copy  
```

>[!NOTE]
>
>`--exclude` オプションの後には、`<src>` 引数と `<dst>` 引数の前に、別のオプションを指定する必要があります。次は例です。
>
>`vlt rcp -e ".*\.txt" -r`

### sync {#sync}

vault 同期サービスを制御できるようにします。引数を指定しない場合、このコマンドは現在の作業ディレクトリの同期の管理を試行します。vlt チェックアウト内で実行される場合は、それぞれのフィルターとホストを使用して同期を設定します。vlt チェックアウト外で実行される場合は、現在のフォルダーを同期用に登録します（ディレクトリが空の場合のみ）。

#### 構文 {#syntax-18}

```shell
sync -v|--force|-u <uri> <command> <localPath>
```

#### オプション {#options-18}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細 Output |
| `--force` | 特定のコマンドの実行を強制的に実行します。 |
| `-u (--uri) <uri>` | 同期ホストの URI を指定します。 |
| `<command>` | 実行する同期コマンド。 |
| `<localPath>` | 同期するローカルフォルダー。 |

### ステータスコード {#status-codes}

VLT で使用するステータスコードは次のとおりです。

* 「空白文字」：変更なし
* 「A」：追加
* 「C」：競合
* 「D」：削除
* 「I」：無視
* 「M」：変更
* 「R」：置換
* 「?」：項目がバージョン管理されていない
* 「!」：項目が見つからない（svn 以外のコマンドによって削除済み）または不完全
* 「~」：別の種類の項目によって妨害されたバージョン管理された項目アイテム

## FileVault 同期のセットアップ {#setting-up-filevault-sync}

vault 同期サービスは、リポジトリのコンテンツをローカルファイルシステム表現と同期する（またはその逆の同期をおこなう）場合に使用します。そのためには、リポジトリの変更をリッスンし、ファイルシステムのコンテンツを定期的にスキャンする OSGi サービスをインストールします。リポジトリのコンテンツをディスクにマッピングするために、Vault と同じシリアル化形式を使用します。

>[!NOTE]
>
>vault 同期サービスは開発ツールであり、本番システムでの使用は推奨されません。また、このサービスはローカルファイルシステムとの同期のみ可能であり、リモート開発には使用できません。

### vlt を使用したサービスのインストール {#installing-the-service-using-vlt}

`vlt sync install` コマンドを使用すると、Vault 同期サービスのバンドルおよび設定を自動的にインストールできます。

このバンドルは `/libs/crx/vault/install` の下にインストールされ、設定ノードは `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl` に作成されます。最初はサービスが有効になっていますが、同期のルートは設定されていません。

次の例では、特定の uri によってアクセス可能な CRX インスタンスに同期サービスをインストールします。

```shell
$ vlt --credentials admin:admin sync --uri http://localhost:4502/crx install
```

### サービスのステータスの表示 {#displaying-the-service-status}

`status` コマンドを使用すると、実行中の同期サービスに関する情報を表示できます。

```shell
$ vlt sync status --uri http://localhost:4502/crx
Connecting via JCR remoting to http://localhost:4502/crx/server
Listing sync status for http://localhost:4502/crx/server/-/jcr:root
- Sync service is enabled.
- No sync directories configured.
```

>[!NOTE]
>
>`status` コマンドは、このサービスからライブデータを取得するのではなく、`/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl` にある設定を読み取ります。

### 同期フォルダーの追加 {#adding-a-sync-folder}

`register` コマンドは、同期するフォルダーを設定に追加するために使用します。

```shell
$ vlt sync register
Connecting via JCR remoting to http://localhost:4502/crx/server
Added new sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>`register` コマンドは、`sync-once` を設定するまで同期をトリガーしません。

### 同期フォルダーの削除 {#removing-a-sync-folder}

`unregister` コマンドは、同期するフォルダーを設定から削除するために使用します。

```shell
$  vlt sync unregister
Connecting via JCR remoting to http://localhost:4502/crx/server
Removed sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>同期フォルダー自体を削除する前に、そのフォルダーの登録を解除する必要があります。

### 同期の設定 {#configuring-synchronization}

#### サービス設定 {#service-configuration}

実行中のサービスは以下のパラメーターを使用して設定できます。

* `vault.sync.syncroots`：同期のルートを定義する 1 つまたは複数のローカルファイルシステムのパス。

* `vault.sync.fscheckinterval`：ファイルシステムの変更をスキャンする頻度（秒）。デフォルト値は 5 秒です。
* `vault.sync.enabled`：サービスを有効または無効にする一般的なフラグ。

>[!NOTE]
>
>このサービスは、web コンソール、またはリポジトリ内の `sling:OsgiConfig` ノード（名前：`com.day.jcr.sync.impl.VaultSyncServiceImpl`）で設定できます。
>
>AEM と連携する場合は、いくつかの方法でこのようなサービスの設定を管理できます。詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

#### 同期フォルダーの設定 {#sync-folder-configuration}

各同期フォルダーにある次の 3 つのファイルに、設定とステータスが格納されます。

* `.vlt-sync-config.properties`：設定ファイル。

* `.vlt-sync.log`：同期中に実行された操作に関する情報を格納するログファイル。
* `.vlt-sync-filter.xml`：リポジトリのどの部分を同期するかを定義するフィルター。このファイルの形式については、[フィルターが適用されたチェックアウトの実行](#performing-a-filtered-checkout)を参照してください。

`.vlt-sync-config.properties` ファイルを使用すると、次のプロパティを設定できます。

**無効** 同期のオンとオフを切り替えます。デフォルトでは、このパラメーターは false に設定されており、同期が行われます。

**sync-once** 空でない場合は、次にスキャンするとき、指定した方向にフォルダーを同期し、パラメーターがクリアされます。次の 2 つの値をサポートしています。

* `JCR2FS`：JCR リポジトリ内のコンテンツをすべてエクスポートして、ローカルディスクに書き込みます。
* `FS2JCR`：ディスクから JCR リポジトリにすべてのコンテンツをインポートします。

**sync-log** ログのファイル名を定義します。デフォルト値は .vlt-sync.log です。

### 開発のための VLT 同期の使用 {#using-vlt-sync-for-development}

同期フォルダーに基づいて開発環境をセットアップするには、次の手順を実行します。

1. vlt コマンドラインを使用してリポジトリをチェックアウトします。

   ```shell
   $ vlt --credentials admin:admin co --force http://localhost:4502/crx dev
   ```

   >[!NOTE]
   >
   >フィルターを使用して、適切なパスだけをチェックアウトできます。詳しくは、[フィルターが適用されたチェックアウトの実行](#performing-a-filtered-checkout)を参照してください。

1. 作業用コピーのルートフォルダーに移動します。

   ```shell
   $ cd dev/jcr_root/
   ```

1. 同期サービスをリポジトリにインストールします。

   ```xml
   $ vlt sync install
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Preparing to install vault-sync-2.4.24.jar...
   Updated bundle: vault-sync-2.4.24.jar
   Created new config at /libs/crx/vault/config/com.day.jcr.sync.impl.VaultSyncServiceImpl
   ```

1. 同期サービスを初期化します。

   ```shell
   $ vlt sync
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Starting initialization of sync service in existing vlt checkout /Users/colligno/Applications/cq5/vltsync/sandbox/dev/jcr_root for http://localhost:4502/crx/server/-/jcr:root
   Added new sync directory: /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root
   
   The directory /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root is now enabled for syncing.
   You might perform a 'sync-once' by setting the
   appropriate flag in the /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/.vlt-sync-config.properties file.
   ```

1. `.vlt-sync-config.properties`隠しファイルを編集し、リポジトリのコンテンツを同期するように設定します。

   ```xml
   sync-once=JCR2FS
   ```

   >[!NOTE]
   >
   >この手順では、フィルター条件に従ってリポジトリ全体をダウンロードします。

1. ログファイル `.vlt-sync.log` で進行状況を確認します。

   ```xml
   ***
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/GeoProduct.java
   ***
   ```

これで、ローカルフォルダーがリポジトリと同期されました。この同期は双方向なので、リポジトリからの変更はローカルの同期フォルダーに適用され、その逆も同様です。

>[!NOTE]
>
>VLT 同期機能でサポートされるのはシンプルなファイルとフォルダーのみです。vault でシリアル化された特殊なファイル（.content.xml、dialog.xml など）は検出されても無視されます。そのため、デフォルトの vlt チェックアウトで vault 同期を使用できます。
