---
title: カスタムスタンドアロンインストール
description: スタンドアロン AEM インスタンスのインストール時に使用可能なオプションについて説明します。
content-type: reference
topic-tags: deploying
exl-id: d6484bb7-8123-4f42-96e8-aa441b1093f3
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 3effd4fa686ac89421ffe74e52bf34830ddd776c
workflow-type: ht
source-wordcount: '1614'
ht-degree: 100%

---

# カスタムスタンドアロンインストール{#custom-standalone-install}

この節では、スタンドアロン AEM インスタンスのインストール時に使用可能なオプションについて説明します。AEM 6 を新規インストールした後のバックエンドストレージタイプの選択について詳しくは、[ストレージ要素](/help/sites-deploying/storage-elements-in-aem-6.md)も参照してください。

## ファイル名の変更によるポート番号の変更 {#changing-the-port-number-by-renaming-the-file}

AEM のデフォルトのポートは 4502 です。このポートが使用できない場合や、既に使用中の場合は、最初に有効なポート番号（4502、8080、8081、8082、8083、8084、8085、8888、9362、`<*random*>`）を使用するようにクイックスタートによって自動的に設定されます。

ファイル名にポート番号が含まれるようにクイックスタート jar ファイルの名前を変更して（例：`cq5-publish-p4503.jar`、`cq5-author-p6754.jar`）、ポート番号を設定することもできます。

クイックスタート jar ファイル名を変更する際に従わなければならない様々なルールがあります。

* ファイル名を変更する場合は、先頭を `cq;` にする必要があります。例えば、`cq5-publish-p4503.jar` のように指定します。

* ポート番号の直前には接頭辞として -p を付けることをお勧めします。例えば、cq5-publish-p4503.jar または cq5-author-p6754.jar のように指定します&#x200B;*。*

>[!NOTE]
>
>これは、ポート番号の抽出に使用される以下のルールについて心配する必要がないようにするためです。
>
>* ポート番号は 4 桁または 5 桁にする
>* ダッシュの後にこれらの数字を指定する
>* ファイル名にその他の数字が含まれる場合は、ポート番号の直前に接頭辞として `-p` を付ける
>* ファイル名の先頭の接頭辞「cq5」は無視される
>

>[!NOTE]
>
>start コマンドで `-port` オプションを使用してポート番号を変更することもできます。

### Java 11 に関する考慮事項 {#java-considerations}

Oracle Java 11（または一般にバージョン 8 より新しい Java）を実行している場合は、AEM の起動時にコマンドラインにさらにスイッチを追加する必要があります。

* 関連するリフレクションアクセス警告メッセージが `stdout.log` に出力されないように、次の - `-add-opens` スイッチを追加する必要があります。

```shell
--add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

* さらに、パフォーマンスの潜在的な問題を軽減するために、`-XX:+UseParallelGC` スイッチを利用する必要があります。

以下は、Java 11 で AEM を起動するときに指定する追加の JVM パラメータのサンプルです。

```shell
-XX:+UseParallelGC --add-opens=java.desktop/com.sun.imageio.plugins.jpeg=ALL-UNNAMED --add-opens=java.base/sun.net.www.protocol.jrt=ALL-UNNAMED --add-opens=java.naming/javax.naming.spi=ALL-UNNAMED --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/jdk.internal.loader=ALL-UNNAMED --add-opens=java.base/java.net=ALL-UNNAMED -Dnashorn.args=--no-deprecation-warning
```

最後に、AEM 6.3 からアップグレードしたインスタンスを実行する場合は、**で次のプロパティが** true`sling.properties` に設定されていることを確認します。

* `felix.bootdelegation.implicit`

## 実行モード {#run-modes}

**実行モード**&#x200B;を使用すると、特定の目的に合わせて AEM インスタンスを調整できます。例えば、オーサーまたはパブリッシュ、テスト、開発、イントラネットなどです。これらのモードを使用すると、サンプルコンテンツの使用を制御できます。サンプルコンテンツは、クイックスタートの構築前に定義され、パッケージや設定などを含めることができます。これは、インストールをサンプルコンテンツなしで無駄のない状態に保つ場合に、実稼動の準備が整ったインストールで特に役立ちます。詳しくは、次を参照してください。

* [実行モード](/help/sites-deploying/configure-runmodes.md)

## ファイルインストールプロバイダーの追加 {#adding-a-file-install-provider}

デフォルトでは、`crx-quickstart/install` フォルダーのファイルが監視されます。
このフォルダーは存在しませんが、実行時に作成できます。

このディレクトリに追加されたバンドル、設定またはコンテンツパッケージは自動的に選択およびインストールされます。削除された場合は、アンインストールされます。
これは、バンドル、コンテンツパッケージまたは設定をリポジトリに追加するためのもう 1 つの方法です。

この方法は次に示すいくつかのユースケースで特に有効です。

* 開発時に、ファイルシステムへの項目の追加が容易になります。
* 問題が発生した場合は、web コンソールとリポジトリにアクセスできません。その際に、このディレクトリにバンドルを追加してインストールできます。
* クイックスタートを起動する前に `crx-quickstart/install` フォルダーを作成して、そこにパッケージを追加できます。

## Windows サービスとしての Adobe Experience Manager のインストールと起動 {#installing-and-starting-adobe-experience-manager-as-a-windows-service}

>[!NOTE]
>
>管理者としてログオンしている間に次の手順を実行するか、またはコンテキストメニューの「**管理者として実行**」オプションを使用して手順を開始／実行してください。
>
>管理者権限を持つユーザーとしてログオンしただけでは&#x200B;**不十分**&#x200B;です。管理者としてログオンしていない状態でこれらの手順の完了すると、「**アクセスが拒否されました**」というエラーが表示されます。

AEM を Windows サービスとしてインストールして起動するには：

1. crx-quickstart\opt\helpers\instsrv.bat ファイルをテキストエディターで開きます。
1. 64 ビット Windows Server を設定する場合は、オペレーティングシステムに応じて次のいずれかのコマンドを使用して、prunsrv のインスタンスをすべて置き換えます。

   * prunsrv_amd64
   * prunsrv_ia64

   このコマンドは、32 ビット Java ではなく 64 ビット Java で Windows サービスデーモンを起動する適切なスクリプトを呼び出します。

1. プロセスが複数のプロセスに分岐しないようにするには、PermGen JVM パラメーターを増やします。 `set jvm_options` コマンドを探して、値を次のように設定します。

   `set jvm_options=-Xmx1792m`

1. コマンドプロンプトを開き、現在のディレクトリを AEM インストールの crx-quickstart/opt/helpers フォルダーに変更し、次のコマンドを入力してサービスを作成します。

   `instsrv.bat cq5`

   サービスが作成されたことを確認するには、管理ツールコントロールパネルで「サービス」を開くか、コマンドプロンプトで「`start services.msc`」と入力します。リストに cq5 サービスが表示されます。

1. 次のいずれかの方法でサービスを起動します。

   * コントロールパネルの「サービス」で、「cq5」をクリックして、「開始」をクリックします。

   ![chlimage_1-11](assets/chlimage_1-11.png)

   * コマンドラインで、&quot;net start cq5&quot; と入力します。

   ![chlimage_1-12](assets/chlimage_1-12.png)

1. Windows は、サービスが実行中であることを示します。AEMが起動し、prunsrv 実行可能ファイルがタスクマネージャーに表示されます。 AEM を使用開始するには、web ブラウザーで、AEM（例：`https://localhost:4502`）に移動します。 

   ![chlimage_1-13](assets/chlimage_1-13.png)

>[!NOTE]
>
>instsrv.bat ファイル内のプロパティ値は、Windows サービスの作成時に使用されます。instsrv.bat 内のプロパティ値を編集する場合は、サービスをアンインストールしてから再インストールする必要があります。

>[!NOTE]
>
>AEM をサービスとしてインストールする場合は、Configuration Manager から、`com.adobe.xmp.worker.files.ncomm.XMPFilesNComm` でログディレクトリの絶対パスを指定する必要があります。

サービスをアンインストールするには、コントロールパネルの「**サービス**」で「**停止**」をクリックするか、コマンドラインでフォルダーに移動して、「`instsrv.bat -uninstall cq5`」と入力します。「`net start`」と入力すると、コントロールパネルの「**サービス**」のリストまたはコマンドライン内のリストからサービスが削除されます。

## 一時的な作業ディレクトリの場所の再定義 {#redefining-the-location-of-the-temporary-work-directory}

Java マシンの一時フォルダーのデフォルトの場所は `/tmp` です。AEM でも、パッケージの構築時などにこのフォルダーを使用します。

一時フォルダーの場所を変更する場合（ディレクトリの空き容量を増やす必要がある場合など）は、JVM パラメーターを追加して * `<new-tmp-path>`* を定義します。

`-Djava.io.tmpdir="/<*new-tmp-path*>"`

定義先は次のいずれかです。

* サーバー起動コマンドライン
* serverctl または start スクリプトの CQ_JVM_OPTS 環境パラメーター

## クイックスタートファイルから使用可能なその他のオプション {#further-options-available-from-the-quickstart-file}

「–help」 オプションを使用して表示するクイックスタートのヘルプファイルには、その他のオプションと名前変更の規則が記述されています。ヘルプにアクセスするには、次のように入力します。

* `java -jar cq-quickstart-6.5.0.jar -help`

>[!CAUTION]
>
>これらのオプションは、AEM 6.5（6.5.0.0）のオリジナルのリリース以降で有効です。SP の新しいリリースでは変更が可能です。

```shell
Loading quickstart properties: default
Loading quickstart properties: instance
Setting properties from filename '/Users/Desktop/AEM/cq-quickstart-6.5.0.jar'
--------------------------------------------------------------------------------
Adobe Experience Manager Quickstart (build 20190328)                            
--------------------------------------------------------------------------------
Usage:                                                                          
 Use these options on the Quickstart command line.                              
--------------------------------------------------------------------------------

-help (--help,-h)
         Show this help message                                                 
-quickstart.server.port (-p,-port) <port>
         Set server port number                                                 
-contextpath (-c,-org.apache.felix.http.context_path) <contextpath>
         Set context path                                                       
-debug <port>
         Enable Java Debugging on port number; forces forking                   
-gui 
         Show GUI if running on a terminal                                      
-nobrowser (-quickstart.nobrowser)
         Do not open browser at startup                                         
-unpack
         Unpack installation files only, do not start the server (implies       
         -verbose)                                                              
-v (-verbose)
         Do not redirect stdout/stderr to files and do not close stdin          
-nofork
         Do not fork the JVM, even if not running on a console                  
-fork
         Force forking the JVM if running on a console, using recommended       
         default memory settings for the forked JVM.                            
-forkargs <args> [<args> ...]
         Additional arguments for the forked JVM, defaults to '-Xmx1024m        
         -XX:MaxPermSize=256m '.  Use -- to specify values starting with -,     
         example: '-forkargs -- -server'                                        
-a (--interface) <interface>
         Optional IP address (interface) to bind to                             
-pt <string>
         Process type (main/fork) - do not use directly, used when forking a    
         process                                                                
-r <string> [<string> [<string> [<string> [<string> [<string> [<string> [<string> [<string> [<string>]]]]]]]]]
         Runmode(s) - Use this to define the run mode(s)                        
-b <string>
         Base folder - defines the path under which the quickstart work folder  
         is created                                                             
-low-mem-action <string>
         Low memory action - what to do if memory is insufficient at startup    
-use-control-port
         Start a control port                                                   
-nointeractive
         Start with no interactivity                                            
-ll <level>
         Define launchpad log level (1 = error...4 = debug)                     
-n   
         Do not install shutdown hook                                           
-D<property>=<value>
         Additional framework properties.                                       
-listener-port <listener-port>
         Set listener port number                                               
-x <string>
         Run a Quickstart extension.                                            
  Options for executing Quickstart extensions:
                                                                                
    -xargs <arg> [<arg> ...]
         Construct an arguments list for a Quickstart extension (for example, -xargs -- 
         -arg1 val1 -arg2 val2).                                                
--------------------------------------------------------------------------------
Quickstart filename options                                                     
--------------------------------------------------------------------------------
Usage:                                                                          
 Rename the jar file, including one of the patterns shown below, to set the     
corresponding option. Command-line options have priority on these filename      
patterns.                                                                       
--------------------------------------------------------------------------------

-NNNN
         Include -NNNN.jar or -pNNNN in the renamed jar filename to run on port 
         NNNN, for example: quickstart-8085.jar                                 
-nobrowser
         Include -nobrowser in the renamed jar filename to avoid opening the    
         browser at startup, example: quickstart-nobrowser-8085.jar             
-publish
         Include -publish in the renamed jar filename to run in "publish" mode, 
         example: cq-publish-7502.jar                                           
-dynamicmedia
         Include -dynamicmedia in the renamed jar filename to run in            
         "dynamicmedia" mode, example: quickstart-dynamicmedia-4502.jar         
-dynamicmedia_scene7
         Include -dynamicmedia_scene7 in the renamed jar filename to run in     
         "dynamicmedia_scene7" mode, example:                                   
         quickstart-dynamicmedia_scene7-p4502.jar                               
--------------------------------------------------------------------------------
The license.properties file
--------------------------------------------------------------------------------
  The license.properties file stores licensing information, created from the    
  licensing form displayed on first startup and stored in the folder from where 
  Quickstart is run.                                                            
--------------------------------------------------------------------------------
Log files
--------------------------------------------------------------------------------
  Once Quickstart has been unpacked and started, log files can be found under   
  /Users/aemdocs/CQInstallationKits/AEM-65150-L8/crx-quickstart/logs.           
--------------------------------------------------------------------------------
```

## Amazon EC2 環境への AEM のインストール {#installing-aem-in-the-amazon-ec-environment}

Amazon Elastic Compute Cloud（EC2）インスタンスに AEM をインストールする場合は、EC2 インスタンスに作成者と発行の両方をインストールすると、[AEM マネージャーのインスタンスのインストール](#installinginstancesofaemmanager)の手順に従って、作成者インスタンスが正しくインストールされます。ただし、発行インスタンスは作成者インスタンスになります。

EC2 環境にパブリッシュインスタンスをインストールする前に、次の手順を実行してください。

1. インスタンスを初めて起動する前に、パブリッシュインスタンスの jar ファイルを展開します。ファイルを展開するには、次のコマンドを使用します。

   ```xml
   java -jar quickstart.jar -unpack
   ```

   >[!NOTE]
   >
   >インスタンスを初めて起動した&#x200B;**後**&#x200B;にモードを変更する場合は、実行モードを変更できません。

1. 次のコマンドを実行してインスタンスを起動します。

   ```xml
   java -jar quickstart.jar -r publish
   ```

   >[!CAUTION]
   >
   >上記のコマンドを実行してインスタンスを展開した後は、最初にそのインスタンスを実行してください。そうしないと、quickstart.properties ファイルが生成されません。このファイルが生成されない場合は、以降の AEM のアップグレードが失敗します。

1. **bin** フォルダー内の **start** スクリプトを開いて、次のセクションを確認します。

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='author'
   fi
   ```

1. 実行モードを&#x200B;**パブリッシュ**&#x200B;に変更して、ファイルを保存します。

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='publish'
   fi
   ```

1. インスタンスを停止し、**start** スクリプトを実行して再起動します。

## インストールの確認 {#verifying-the-installation}

次のリンクを使用して、インストールが機能していることを確認できます（すべての例では、インスタンスが localhost のポート 8080 で実行されていること、および CRX が /crx に、Launchpad が / の下にインストールされていることを前提としています）。

* `https://localhost:8080/crx/de`
CRXDE Lite コンソール

* `https://localhost:8080/system/console`
Web コンソール

## インストール後のアクション {#actions-after-installation}

AEM WCM の様々な設定を行うことができますが、インストール直後には、実行が必要な特定のアクションや、少なくとも確認が必要な項目があります。

* システムのセキュリティを確保するために必要なタスクについて、[セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。
* AEM WCM と共にインストールされたデフォルトのユーザーとグループのリストを確認します。また、他のアカウントに対してアクションを実行するかどうかを確認します。詳しくは、[ユーザー管理とセキュリティ](/help/sites-administering/security.md)を参照してください。

## CRXDE Lite および web コンソールへのアクセス {#accessing-crxde-lite-and-the-web-console}

AEM WCM を起動したら、次の場所にアクセスできます。

* [CRXDE Lite](#accessing-crxde-lite) - リポジトリにアクセスして管理するために使用
* [Web コンソール](#accessing-the-web-console) - OSGi バンドル（OSGi コンソールとも呼ばれる）の管理や設定のために使用

### CRXDE Lite へのアクセス {#accessing-crxde-lite}

CRXDE Lite を開くには、スタートアップスクリーンから **CRXDE Lite** を選択するか、ブラウザーを使用して以下に移動します

```
 https://<<i>host</i>>:<<i>port</i>>/crx/de/index.jsp
```

次に例を示します。`https://localhost:4502/crx/de/index.jsp`

![installcq_crxdelite](assets/installcq_crxdelite.png)

#### Web コンソールへのアクセス {#accessing-the-web-console}

Adobe CQ web コンソールにアクセスするには、ようこそ画面から **OSGi コンソール**&#x200B;を選択するか、ブラウザーを使用して以下に移動します

```
 https://<host>:<port>/system/console
```

例：
`https://localhost:4502/system/console`
またはバンドルページの
`https://localhost:4502/system/console/bundles`

![chlimage_1-14](assets/chlimage_1-14.png)

詳しくは、[Web コンソールでの OSGi 設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)を参照してください。

## トラブルシューティング {#troubleshooting}

インストール時に発生する可能性のある問題の対処方法について詳しくは、以下を参照してください。

* [トラブルシューティング](/help/sites-deploying/troubleshooting.md)

## Adobe Experience Manager のアンインストール {#uninstalling-adobe-experience-manager}

AEM は単一のディレクトリにインストールされるので、アンインストールユーティリティは必要ありません。インストールディレクトリ全体を削除するだけでアンインストールできます。ただし、AEM のアンインストール方法は、その目的および使用している永続ストレージによって変わります。

例えば、デフォルトの TarPM インストールなど、永続ストレージがインストールディレクトリに埋め込まれている場合、フォルダーを削除するとデータも削除されます。

>[!NOTE]
>
>アドビでは、AEM を削除する前にリポジトリをバックアップすることを強くお勧めします。&lt;cq-installation-directory> 全体を削除すると、リポジトリも削除されます。削除する前にリポジトリのデータを保管する場合は、&lt;cq-installation-directory>/crx-quickstart/repository フォルダーを他の場所に移動またはコピーしてから、その他のフォルダーを削除するようにしてください。

例えば、データベースサーバーなど、AEM のインストールが外部ストレージを使用している場合、フォルダーを削除してもデータは自動的には削除されませんが、ストレージ設定が削除されるので、JCR コンテンツの復元は困難になります。
