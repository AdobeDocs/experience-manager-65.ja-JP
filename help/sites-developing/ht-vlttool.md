---
title: VLT ツールを使用する方法
seo-title: VLT ツールを使用する方法
description: Jackrabbit FileVault ツール（VLT）は、Jackrabbit／AEM インスタンスのコンテンツをファイルシステムにマップするためのツールで、The Apache Foundation によって開発されました
seo-description: Jackrabbit FileVault ツール（VLT）は、Jackrabbit／AEM インスタンスのコンテンツをファイルシステムにマップするためのツールで、The Apache Foundation によって開発されました
uuid: 579e7785-8b50-4366-b562-8e79b6451464
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a76425e9-fd3b-4c73-80f9-0ebabb8fd94f
translation-type: tm+mt
source-git-commit: 2da3da1a36f074593e276ddd15ed8331239ab70f
workflow-type: tm+mt
source-wordcount: '2748'
ht-degree: 81%

---


# How to Use the VLT Tool {#how-to-use-the-vlt-tool}

Jackrabbit FileVault ツール（VLT）は、Jackrabbit／AEM インスタンスのコンテンツをファイルシステムにマップするためのツールで、[The Apache Foundation](https://www.apache.org/) によって開発されました。VLT ツールの機能はソース管理システムクライアント（Subversion（SVN）クライアントなど）に似ており、通常のチェックイン、チェックアウト、管理操作をおこなうことができるほか、プロジェクトのコンテンツを柔軟に表現するための設定オプションも用意されています。

VLT ツールはコマンドラインから実行します。このドキュメントでは、ツールの使い方（導入方法、ヘルプの表示方法、すべての[コマンド](#vlt-commands)と使用可能な[オプション](#vlt-global-options)のリストを含む）について説明します。

## 概念およびアーキテクチャ {#concepts-and-architecture}

Filevaultツールの概念と構造の概要については、 [Apache Jackrabbit Filevaultの公式ドキュメント](https://jackrabbit.apache.org/filevault/overview.html)[の「Filevaultの概要と](https://jackrabbit.apache.org/filevault/vaultfs.html) Vault FS [](https://jackrabbit.apache.org/filevault/index.html) 」ページを参照してください。

## VLT の導入 {#getting-started-with-vlt}

VLT の使用を開始するには、次の手順を実行する必要があります。

1. VLT をインストールして、環境変数を更新し、グローバルに無視されている subversion ファイルを更新します。
1. AEM リポジトリをセットアップします（セットアップが完了していない場合）。
1. AEM リポジトリをチェックアウトします。
1. リポジトリとの同期をおこないます。
1. 同期が正しくおこなわれたかどうかをテストします。

### Installing the VLT Tool {#installing-the-vlt-tool}

VLT ツールを使用するには、まず VLT ツールをインストールする必要があります。このツールは追加のツールなので、デフォルトではインストールされません。 また、システムの環境変数を設定する必要があります。

1. FileVaultアーカイブファイルを [Mavenアーティファクトリポジトリからダウンロードします。](https://repo1.maven.org/maven2/org/apache/jackrabbit/vault/vault-cli/)
   >[!NOTE]
   >
   >VLTツールのソースはGitHubで [利用できます。](https://github.com/apache/jackrabbit-filevault)
1. アーカイブを解凍します。
1. Add `<archive-dir>/vault-cli-<version>/bin` to your environment `PATH` so that the command files `vlt` or `vlt.bat` are accessed as appropriate. 次に例を示します。

   `<aem-installation-dir>/crx-quickstart/opt/helpers/vault-cli-3.1.16/bin>`

1. Open a command line shell and execute `vlt --help`. 出力が次のヘルプ画面のようになっていることを確認します。

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
* lines of files checked out on Linux/Unix end with a `LF`
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

### Checking Out the Repository {#checking-out-the-repository}

ソース管理システムを使用してリポジトリをチェックアウトします。例えば svn では、次のように入力します（URI とパスはお使いのリポジトリのものに置き換えてください）。

```shell
svn co https://svn.server.com/repos/myproject
```

### Synchronizing with the Repository {#synchronizing-with-the-repository}

filevault とリポジトリを同期する必要があります。次の手順を実行します。

1. In the command line, navigate to `content/jcr_root`.
1. 次のように入力してリポジトリをチェックアウトします（**4502** をお使いのポート番号に置き換えて、お使いの admin パスワードを使用してください）。

   ```shell
   vlt --credentials admin:admin co --force http://localhost:4502/crx
   ```

   >[!NOTE]
   >
   >The credentials have to be specified only once upon your initial checkout. They will then be stored in your home directory inside `.vault/auth.xml`.

### Testing Whether the Synchronization Worked {#testing-whether-the-synchronization-worked}

リポジトリのチェックアウトと同期が完了したら、すべてが適切に機能しているかどうかをテストする必要があります。このテストを簡単におこなうには、**.jsp** ファイルを編集して、変更のコミット後にその変更が反映されているかどうかを確認します。

同期をテストするには：

1. `.../jcr_content/libs/foundation/components/text` に移動します。
1. Edit something in `text.jsp`.
1. See the modified files by typing `vlt st`
1. See the changes by typing `vlt diff text.jsp`
1. 変更をコミット： `vlt ci test.jsp`.
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

特定のコマンドに関するヘルプを表示するには、help コマンドの後にそのコマンドの名前を入力します。次に例を示します。

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

VLT で実行される一般的なタスクの一部を以下に示します。各コマンドについて詳しくは、個々の[コマンド](#vlt-commands)を参照してください。

### Checking Out a Subtree {#checking-out-a-subtree}

If you only want to check out a subtree of the repository for example, `/apps/geometrixx`, you can do so by typing the following:

```shell
vlt co http://localhost:4502/crx/-/jcr:root/apps/geometrixx geo
```

Doing this creates a new export root `geo` with a `META-INF` and `jcr_root` directory and puts all files below `/apps/geometrixx` in `geo/jcr_root`.

### Performing a Filtered Checkout {#performing-a-filtered-checkout}

既存のワークスペースフィルターがあり、チェックアウトにそのフィルターを使用する場合は、最初に `META-INF/vault` ディレクトリを作成して、そこにフィルターを配置するか、またはコマンドラインで次のようにフィルターを指定します。

```shell
$ vlt co --filter filter.xml http://localhost:4502/crx/-/jcr:root geo
```

サンプルのフィルターを次に示します。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/etc/designs/geometrixx" />
    <filter root="/apps/geometrixx"/>
</workspaceFilter>
```

### Using Import/Export Instead of .vlt Control {#using-import-export-instead-of-vlt-control}

コントロールファイルを使用せずに、JCR リポジトリとローカルファイルシステムとの間でコンテンツの読み込みと書き出しをおこなうことができます。

To import and export content without using `.vlt` control:

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

すべてのコマンドで使用可能な VLT のオプションのリストを次に示します。使用可能なその他のオプションについては、個々のコマンドを参照してください。

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
| `--log-level <level>` | ログレベル（例：log4j）を示します |
| `-h (--help) <command>` | 特定のコマンドのヘルプを出力します |

## VLT のコマンド {#vlt-commands}

次の表は、使用可能な VLT のすべてのコマンドを示しています。構文、使用可能なオプションおよび例について詳しくは、個々のコマンドを参照してください。

|  |  |  |
|--- |--- |--- |
| コマンド | コマンドの略称 | 説明 |
| `export` |  | コントロールファイルを使用せずに JCR リポジトリ（vault ファイルシステム）からローカルファイルシステムに書き出します。 |
| `import` |  | ローカルファイルシステムを JCR リポジトリ（vault ファイルシステム）に読み込みます。 |
| `checkout` | `co` | Vault ファイルシステムをチェックアウトします。最初の JCR リポジトリをローカルファイルシステムにチェックアウトする場合にこのコマンドを使用します（注意：最初に subversion でリポジトリをチェックアウトする必要があります）。 |
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

### export {#export}

&lt;uri> でマウントされた Vault ファイルシステムをローカルファイルシステム（&lt;local-path>）に書き出します。サブツリーのみを書き出すには、オプションの &lt;jcr-path> を指定できます。

#### 構文 {#syntax}

```shell
export -v|-t <arg>|-p <uri> <jcr-path> <local-path>
```

#### Options {#options}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細出力 |
| `-t (--type) <arg>` | 書き出しのタイプ（platform または jar）を指定します。 |
| `-p (--prune-missing)` | 見つからないローカルファイルを削除する必要がある場合に指定します。 |
| `<uri>` | マウントポイントの URI |
| `<jcrPath>` | JCR パス |
| `<localPath>` | ローカルパス |

#### 例 {#examples}

```shell
vlt export http://localhost:4502/crx /apps/geometrixx myproject
```

### import {#import}

Imports the local file system (starting at `<local-path>` to the vault file system at `<uri>`. You can specify a `<jcr-path>` as import root. If `--sync` is specified, the imported files are automatically put under vault control.

#### 構文 {#syntax-1}

```shell
import -v|-s <uri> <local-path> <jcr-path>
```

#### Options {#options-1}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細出力 |
| `-s (-- sync)` | ローカルファイルの vault を管理します。 |
| `<uri>` | マウントポイントの URI |
| `<jcrPath>` | JCR パス |
| `<localPath>` | ローカルパス |

#### 例 {#examples-1}

```shell
vlt import http://localhost:4502/crx . /
```

### Checkout (co) {#checkout-co}

JCR リポジトリから &lt;uri> で始まるローカルファイルシステムおよび &lt;local-path> で始まるローカルファイルシステムへの最初のチェックアウトを順に実行します。&lt;jcrPath> 引数を追加して、リモートツリーのサブディレクトリをチェックアウトすることもできます。META-INF ディレクトリにコピーするワークスペースフィルターを指定できます。

#### 構文 {#syntax-2}

```shell
checkout --force|-v|-q|-f <file> <uri> <jcrPath> <localPath>  
```

#### Options {#options-2}

|  |  |
|--- |--- |
| `--force` | ローカルファイルが既に存在する場合は、チェックアウトを実行してそのファイルを強制的に上書きします |
| `-v (--verbose)` | 詳細出力 |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `-f (--filter) <file>` | 自動フィルターを指定します（定義されていない場合） |
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

### analyze {#analyze}

パッケージを分析します。

#### 構文 {#syntax-3}

```shell
analyze -l <format>|-v|-q <localPaths1> [<localPaths2> ...]
```

#### Options {#options-3}

|  |  |
|--- |--- |
| `-l (--linkFormat) <format>` | printf format for hotfix links (name,id), for example `[CQ520_HF_%s|%s]` |
| `-v (--verbose)` | 詳細出力 |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `<localPaths> [<localPaths> ...]` | ローカルパス |

### ステータス {#status}

作業用コピーファイルとディレクトリのステータスを出力します。

If `--show-update` is specified, each file is checked against the remote version. 2 番目の文字は、更新操作によって実行されるアクションを指定します。

#### 構文 {#syntax-4}

```shell
status -v|-q|-u|-N <file1> [<file2> ...]
```

#### Options {#options-4}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細出力 |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `-u (--show-update)` | 更新情報を表示します |
| `-N (--non-recursive)` | 単一のディレクトリで処理が実行されます |
| `<file> [<file> ...]` | ステータスを表示するファイルまたはディレクトリ |

### 更新 {#update}

リポジトリから作業用コピーに変更をコピーします。

#### 構文 {#syntax-5}

```shell
update -v|-q|--force|-N <file1> [<file2> ...]
```

#### Options {#options-5}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細出力 |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `--force` | ローカルファイルを強制的に上書きします |
| `-N (--non-recursive)` | 単一のディレクトリで処理が実行されます |
| `<file> [<file> ...]` | 更新するファイルまたはディレクトリ |

### 情報 {#info}

ローカルファイルに関する情報を表示します。

#### 構文 {#syntax-6}

```shell
info -v|-q|-R <file1> [<file2> ...]
```

#### Options {#options-6}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細出力 |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `-R (--recursive)` | 処理を再帰的に実行します |
| `<file> [<file> ...]` | 情報を表示するファイルまたはディレクトリ |

### commit {#commit}

作業用コピーからリポジトリに変更を送信します。

#### 構文 {#syntax-7}

```shell
commit -v|-q|--force|-N <file1> [<file2> ...]
```

#### Options {#options-7}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細出力 |
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

#### Options {#options-8}

|  |  |
|--- |--- |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `-R (--recursive)` | 処理を再帰的に実行します |
| `<file> [<file> ...]` | コミットするファイルまたはディレクトリ |

### resolved {#resolved}

作業用コピーファイルまたはディレクトリの&#x200B;**競合**&#x200B;状態を削除します。

>[!NOTE]
>
>このコマンドは意味的に競合を解決したり、競合のマーカーを削除したりするのではなく、単に競合に関連するアーティファクトファイルを削除して、PATH を再びコミットできるようにします。

#### 構文 {#syntax-9}

```shell
resolved -q|-R|--force <file1> [<file2> ...]  
```

#### Options {#options-9}

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

#### Options {#options-10}

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

#### Options {#options-11}

|  |  |
|--- |--- |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `-R (--recursive)` | 処理を再帰的に実行します |
| `<file> [<file> ...]` | プロパティの出力元のファイルまたはディレクトリ |

### propset {#propset}

ファイルまたはディレクトリのプロパティの値を設定します。

>[!NOTE]
>
>VLTは、次の特別なバージョン付きプロパティを認識します。
>
>`vlt:mime-type`
>
>ファイルの MIME タイプ。ファイルを結合するかどうかを判断するために使用します。「text/」で始まる MIME タイプ（または MIME タイプが存在しない場合）はテキストとして扱われます。それ以外の MIME タイプはバイナリとして扱われます。

#### 構文 {#syntax-12}

```shell
propset -q|-R <propname> <propval> <file1> [<file2> ...]
```

#### Options {#options-12}

|  |  |
|--- |--- |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `-R (--recursive)` | 処理を再帰的に実行します |
| `<propname>` | プロパティ名 |
| `<propval>` | プロパティ値 |
| `<file> [<file> ...]` | プロパティを設定するファイルまたはディレクトリ |

### Add {#add}

ファイルとディレクトリのバージョンを管理し、それらをリポジトリに追加するスケジュールを設定します。ファイルとディレクトリは次回のコミット時に追加されます。

#### 構文 {#syntax-13}

```shell
add -v|-q|-N|--force <file1> [<file2> ...]
```

#### Options {#options-13}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細出力 |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `-N (--non-recursive)` | 単一のディレクトリで処理が実行されます |
| `--force` | 操作を強制的に実行します |
| `<file> [<file> ...]` | 追加するローカルファイルまたはディレクトリ |

### 削除 {#delete}

ファイルとディレクトリのバージョン管理を削除します。

#### 構文 {#syntax-14}

```shell
delete -v|-q|--force <file1> [<file2> ...]
```

#### Options {#options-14}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細出力 |
| `-q (--quiet)` | 出力を最小限に抑えます |
| `--force` | 操作を強制的に実行します |
| `<file> [<file> ...]` | 削除するローカルファイルまたはディレクトリ |

### diff {#diff}

2 つのパスの差分を表示します。

#### 構文 {#syntax-15}

```shell
diff -N <file1> [<file2> ...]
```

#### Options {#options-15}

|  |  |
|--- |--- |
| `-N (--non-recursive)` | 単一のディレクトリで処理が実行されます |
| `<file> [<file> ...]` | 差分を表示するファイルまたはディレクトリ |

### コンソール {#console}

インタラクティブコンソールを実行します。

#### 構文 {#syntax-16}

```shell
console -F <file>
```

#### Options {#options-16}

|  |  |
|--- |--- |
| `-F (--console-settings) <file>` | コンソール設定ファイルを指定します。デフォルトのファイルは console.properties です。 |

### rcp {#rcp}

ノードツリーをリモートリポジトリ間でコピーします。`<src>` はソースノードを指し、親ノードが存在する必要がある宛先パスを `<dst>` 指定します。 rcp は、データをストリーミングすることでノードを処理します。

#### 構文 {#syntax-17}

```shell
rcp -q|-r|-b <size>|-t <seconds>|-u|-n|-e <arg1> [<arg2> ...] <src> <dst>
```

#### Options {#options-17}

|  |  |
|--- |--- |
| `-q (--quiet)` | 出力を最小限に抑えます。 |
| `-r (--recursive)` | 処理を再帰的に実行します。 |
| `-b (--batchSize) <size>` | 中間保存前に処理されるノード数。 |
| `-t (--throttle) <seconds>` | 中間保存の後に待機する秒数。 |
| `-u (--update)` | 既存のノードを上書き／削除します。 |
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
>The `--exclude` options need to be followed by another option before the `<src>` and `<dst>` arguments. 次に例を示します。
>
>`vlt rcp -e ".*\.txt" -r`

### sync {#sync}

vault 同期サービスを制御できるようにします。引数を指定しない場合、このコマンドは現在の作業ディレクトリの同期の管理を試行します。vlt チェックアウト内で実行される場合は、それぞれのフィルターとホストを使用して同期を設定します。vlt チェックアウト外で実行される場合は、現在のフォルダーを同期用に登録します（ディレクトリが空の場合のみ）。

#### 構文 {#syntax-18}

```shell
sync -v|--force|-u <uri> <command> <localPath>
```

#### Options {#options-18}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細出力。 |
| `--force` | 特定のコマンドを強制的に実行します。 |
| `-u (--uri) <uri>` | 同期ホストの URI を指定します。 |
| `<command>` | 実行する sync コマンド。 |
| `<localPath>` | 同期するローカルフォルダー。 |

### ステータスコード {#status-codes}

VLT で使用するステータスコードは次のとおりです。

* （空白文字）：変更なし
* A：追加済み
* C：競合
* D：削除済み
* I：無視
* M：変更済み
* R：置換済み
* ?：項目がバージョン管理されていない
* !：項目が見つからない（svn 以外のコマンドによって削除済み）か不完全である
* ~：バージョン管理された項目が別の種類の項目によって遮断されている

## Setting Up FileVault Sync {#setting-up-filevault-sync}

vault 同期サービスは、リポジトリのコンテンツをローカルファイルシステム表現と同期する（またはその逆の同期をおこなう）場合に使用します。そのためには、リポジトリの変更をリッスンし、ファイルシステムのコンテンツを定期的にスキャンする OSGi サービスをインストールします。このサービスでは、vault と同じシリアル化形式を使用して、リポジトリのコンテンツをディスクにマップします。

>[!NOTE]
>
>vault 同期サービスは開発ツールであり、本番システムでの使用は推奨されません。また、このサービスはローカルファイルシステムとの同期のみ可能であり、リモート開発には使用できません。

### vlt を使用したサービスのインストール {#installing-the-service-using-vlt}

`vlt sync install` コマンドを使用すると、vault 同期サービスのバンドルおよび設定を自動的にインストールできます。

The bundle is installed below `/libs/crx/vault/install` and the config node is created at `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`. 最初はサービスが有効になっていますが、同期のルートは設定されていません。

次の例では、特定の uri によってアクセス可能な CRX インスタンスに同期サービスをインストールします。

```shell
$ vlt --credentials admin:admin sync --uri http://localhost:4502/crx install
```

### サービスのステータスの表示 {#displaying-the-service-status}

The `status` command can be used to display information about the running sync service. ``

```shell
$ vlt sync status --uri http://localhost:4502/crx
Connecting via JCR remoting to http://localhost:4502/crx/server
Listing sync status for http://localhost:4502/crx/server/-/jcr:root
- Sync service is enabled.
- No sync directories configured.
```

>[!NOTE]
>
>The `status` command does not fetch any live data from the service but rather reads the configuration at `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`.

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

* `vault.sync.fscheckinterval`:ファイル・システムで変更をスキャンする頻度（秒）。 デフォルト値は 5 秒です。
* `vault.sync.enabled`：サービスを有効または無効にする一般的なフラグ。

>[!NOTE]
>
>このサービスは、Web コンソールまたはリポジトリ内の `sling:OsgiConfig` ノード（名前：`com.day.jcr.sync.impl.VaultSyncServiceImpl`）で設定できます。
>
>AEM と連携する場合は、いくつかの方法でこのようなサービスの設定を管理できます。詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

#### 同期フォルダーの設定 {#sync-folder-configuration}

各同期フォルダー内の次の 3 つのファイルに設定とステータスが格納されます。

* `.vlt-sync-config.properties`:設定ファイル。

* `.vlt-sync.log`:同期中に実行された操作に関する情報を含むログファイルです。
* `.vlt-sync-filter.xml`:リポジトリのどの部分が同期されるかを定義するフィルター。 The format of this file is decribed by the [Performing a filtered checkout](#performing-a-filtered-checkout) section.

The `.vlt-sync-config.properties` file allows you to configure the following properties:

**disabled** 同期のオン/オフを切り替えます。 デフォルトでは、このパラメーターは false に設定されており、同期が許可されます。

**sync-once** 空でない場合は、次のスキャンで指定された方向のフォルダが同期され、パラメータがクリアされます。 次の 2 つの値がサポートされています。

* `JCR2FS`：JCR リポジトリ内のコンテンツをすべて書き出して、ローカルディスクに書き込みます。
* `FS2JCR`：ディスクから JCR リポジトリにすべてのコンテンツを読み込みます。

**sync-log** ：ログファイル名を定義します。 デフォルト値は .vlt-sync.log です。

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

1. Edit the `.vlt-sync-config.properties` hidden file and configure sync to synchronize the content of your repository:

   ```xml
   sync-once=JCR2FS
   ```

   >[!NOTE]
   >
   >この手順では、フィルター条件に従ってリポジトリ全体をダウンロードします。

1. Check the log file `.vlt-sync.log` to see the progress:

   ```xml
   ***
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/GeoProduct.java
   ***
   ```

これで、ローカルフォルダーがリポジトリと同期されます。この同期は双方向なので、リポジトリからの変更はローカルの同期フォルダーに適用されます。逆の場合も同様です。

>[!NOTE]
>
>VLT 同期機能でサポートされるのはシンプルなファイルとフォルダーのみです。vault でシリアル化された特殊なファイル（.content.xml、dialog.xml など）は検出されても無視されます。そのため、デフォルトの vlt チェックアウトで vault 同期を使用できます。
