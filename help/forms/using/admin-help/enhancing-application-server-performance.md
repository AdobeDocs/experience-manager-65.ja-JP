---
title: アプリケーションサーバーのパフォーマンスの強化
seo-title: アプリケーションサーバーのパフォーマンスの強化
description: このドキュメントでは、AEM Forms アプリケーションサーバーのパフォーマンスを向上させるために設定できるオプション設定について説明します。
seo-description: このドキュメントでは、AEM Forms アプリケーションサーバーのパフォーマンスを向上させるために設定できるオプション設定について説明します。
uuid: 88d2f96a-3b59-410d-8160-20581d27acad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fad65765-d56d-4a9f-82d5-bcceb1758953
translation-type: tm+mt
source-git-commit: a26bc4e4ea10370dd2fc3403500004b9e378c418

---


# アプリケーションサーバーのパフォーマンスの強化{#enhancing-application-server-performance}

ここでは、AEM Forms アプリケーションサーバーのパフォーマンスを向上させるために設定できるオプション設定について説明します。

## アプリケーションサーバーのデータソースの設定 {#configuring-application-server-data-sources}

AEM Forms は、AEM Forms リポジトリをデータソースとして使用します。AEM Forms リポジトリにはアプリケーションアセットが格納されます。また実行時に、サービスは、自動化されたビジネスプロセスの実行の一環として、リポジトリからアセットを取得できます。

実行中の AEM Forms モジュールの数や、アプリケーションにアクセスしている同時ユーザーの数によっては、これらのデータソースへのアクセス負荷が大きくなる場合があります。データソースへのアクセスは、接続プールを使用して最適化できます。「接続プール」**&#x200B;は、アプリケーションやサーバーオブジェクトがデータベースへのアクセスを必要とするたびに生じる、新しいデータベース接続の作成に伴うオーバーヘッドを回避するために使用される技術です。通常、接続プールは Web ベースのアプリケーションおよびエンタープライズアプリケーションで使用されます。また、アプリケーションサーバーによって処理されるのが一般的ですが、必ずしもそれだけに限定されません。

接続を使い切らないように接続プールのパラメーターを適切に設定することが重要です。接続が足りなくなった場合、アプリケーションのパフォーマンスが低下する可能性があります。

接続プールを適切に設定するには、アプリケーションサーバー管理者がピーク時間帯に接続プールを監視することが重要になります。監視によって、アプリケーションやユーザーがいつでも十分な数の接続を使用できるようになります。ほとんどのアプリケーションサーバーには監視用のツールが組み込まれています。

WebLogic Server 管理コンソールでは、ドメイン内の JDBC データソースインスタンスごとに様々な統計値を監視できます。詳しくは WebLogic のドキュメントを参照してください。

アプリケーションサーバー管理者は、適切な接続プールの設定を決める際に、それらの情報をデータベース管理者に伝えてください。データベース管理者がこの情報を必要とするのは、データベース接続の数はデータソース用の接続プール内の接続数に等しくなるためです。そして、以下に示すアプリケーションサーバーおよびデータソースの種類に応じて、接続プールを設定する手順を実行してください。

### Oracle および MySQL に対する WebLogic の接続プールの設定 {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. 「Domain Structure」で、Services／JDBC／Data Sources をクリックし、右側のウィンドウの「IDP_DS」をクリックします。
1. 次の画面で、「Configuration」タブ／Connection Pool をクリックして、以下のボックスに値を入力します。

   * 「Initial Capacity」
   * 「Maximum Capacity」
   * 「Capacity Increment」
   * 「Statement Cache Size」

1. 「Save」をクリックし、「Activate Changes」をクリックします。
1. WebLogic 管理対象サーバーを再起動します。

### SQLServer に対する WebLogic の接続プールの設定 {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. 「Change Center」で、「Lock &amp; Edit」をクリックします。
1. 「Domain Structure」で、Services／JDBC／Data Sources をクリックし、右側のウィンドウの「EDC_DS」をクリックします。
1. 次の画面で、「Configuration」タブ／Connection Pool をクリックして、以下のボックスに値を入力します。

   * 「Initial Capacity」
   * 「Maximum Capacity」
   * 「Capacity Increment」
   * 「Statement Cache Size」

1. 「Save」をクリックし、「Activate Changes」をクリックします。
1. WebLogic 管理対象サーバーを再起動します。

### DB2 に対する WebSphere の接続プールの設定 {#configure-connection-pool-settings-for-websphere-for-db2}

1. ナビゲーションツリーで、Resources／JDBC／JDBC Providers をクリックします。右側のウィンドウで、作成したデータソース（DB2 Universal JDBC Driver Provider または LiveCycle - db2 - IDP_DS）を選択します。
1. 「Additional Properties」で「Data Sources」をクリックし、「IDP_DS」を選択します。
1. 次の画面の「Additional Properties」で「Connection Pool Properties」をクリックし、「Maximum connections」ボックスと「Minimum Connections」ボックスに値を入力します。
1. 「OK」または「Apply」をクリックし、「Save Directly To Master Configuration」をクリックします。

### Oracle に対する WebSphere の接続プールの設定 {#configure-connection-pool-settings-for-websphere-for-oracle}

1. ナビゲーションツリーで、Resources／JDBC／JDBC Providers をクリックします。右側のウィンドウで、作成した Oracle JDBC Driver データソースをクリックします。
1. 「Additional Properties」で「Data Sources」をクリックし、「IDP_DS」を選択します。
1. 次の画面の「Additional Properties」で「Connection Pool Properties」をクリックし、「Maximum connections」ボックスと「Minimum Connections」ボックスに値を入力します。
1. 「OK」または「Apply」をクリックし、「Save Directly To Master Configuration」をクリックします。

### SQL Server に対する WebSphere の接続プールの設定 {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. ナビゲーションツリーで、Resources／JDBC／JDBC Providers をクリックし、右側のウィンドウで、作成した User-Defined JDBC Driver データソースをクリックします。
1. 「Additional Properties」で「Data Sources」をクリックし、「IDP_DS」を選択します。
1. 次の画面の「Additional Properties」で「Connection Pool Properties」をクリックし、「Maximum Connections」ボックスと「Minimum Connections」ボックスに値を入力します。
1. 「OK」または「Apply」をクリックし、「Save Directly To Master Configuration」をクリックします。

## インラインドキュメントの最適化と JVM メモリに対する影響 {#optimizing-inline-documents-and-impact-on-jvm-memory}

比較的小さいサイズのドキュメントを処理することが多い場合は、ドキュメント転送速度と記憶領域に関するパフォーマンスを向上させることができます。それには、AEM Forms 製品に対して以下の設定を適用します。

* AEM Forms におけるデフォルトのドキュメントの最大インラインサイズを、ほとんどのドキュメントのサイズよりも大きい値に増やします。
* 大きいファイルを処理する場合は、高速ディスクシステムまたは RAM ディスクにあるストレージディレクトリを指定します。

最大インラインサイズとストレージディレクトリ（AEM Forms の一時ファイルディレクトリと GDS ディレクトリ）は、管理コンソールで設定します。

### ドキュメントサイズと最大インラインサイズ {#document-size-and-maximum-inline-size}

AEM Forms に送信して処理するドキュメントのサイズがデフォルトのドキュメント最大インラインサイズ以下の場合、ドキュメントはサーバーにインラインで保存され、Adobe Document オブジェクトとしてシリアライズされます。ドキュメントをインラインで格納することで、パフォーマンスを大幅に向上させることができます。ただし、forms ワークフローを使用している場合は、管理のためにコンテンツもデータベースに保存されることがあります。このため、最大インラインサイズを増やすと、データベースサイズに影響する場合があります。

最大インラインサイズよりも大きいサイズのドキュメントはローカルファイルシステムに格納されます。サーバーとの間で転送される Adobe Document オブジェクトがそのファイルへの唯一のポインターとなります。

ドキュメントコンテンツがインライン化される（つまり、最大インラインサイズ未満である）と、コンテンツはドキュメントのシリアライズペイロードの一部としてデータベースに保存されます。このため、最大インラインサイズを増やすと、データベースサイズに影響する場合があります。

**最大インラインサイズの変更**

1. 管理コンソールで、設定／コアシステム設定／設定をクリックします。
1. 「デフォルトのドキュメント最大インラインサイズ」ボックスに値を入力し、「OK」をクリックします。

   >[!NOTE]
   >
   >JEE上のAEM Forms環境ではDocument Max Inline Sizeプロパティの値が同じである必要があり、JEE上のAEM FormsをバンドルしてOSGi上のAEM Forms環境に含める場合は同じである必要があります。 この手順では、JEE 環境上の AEM Forms の値のみを更新し、OSGi バンドル上の AEM Forms に含まれる JEE 環境上の AEM Forms の値は更新していません。

1. 次のシステムプロパティでアプリケーションサーバーを再起動します。

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >上記のシステムプロパティは、JEE 環境上の AEM Forms と、OSGi バンドル上の AEM Forms に含まれる JEE 環境上の AEM Forms に対して設定された「ドキュメント最大インラインサイズ」プロパティの値を上書きします。

>[!NOTE]
>
>デフォルトの最大インラインサイズは 65536 バイトです。

### JVM 最大ヒープサイズ {#jvm-maximum-heap-size}

最大インラインサイズを増やすと、シリアライズされたドキュメントを保存するために多くのメモリが必要になります。このため、通常は JVM 最大ヒープサイズも増やす必要があります。

大量のドキュメントを処理している負荷の高いシステムでは、JVM ヒープメモリがすぐにいっぱいになることがあります。OutOfMemoryError を防ぐために、インラインドキュメントのサイズと稼働中に通常実行されるドキュメントの数を掛けた値を求めて、JVM 最大ヒープサイズにその分を上乗せしてください。

JVM 最大ヒープサイズの増加量 = （インラインドキュメントサイズ） x （処理するドキュメントの平均数）

**JVM 最大ヒープサイズの計算**

この例では、現在の JVM 最大ヒープが 512 MB、最大インラインサイズは 64 KB に設定されています。サーバーの設定は、100 個のジョブが同時に実行されていて、各ジョブに 9 個の入力ファイルと 1 個の結果ファイルがある（ジョブあたり合計 10 個のファイルがあり、100 個のジョブを同時に処理する）シナリオに対応できるように指定する必要があります。ファイルのサイズはすべて 512 KB 未満です。

すべてのファイルをインラインで格納するには、最大インラインサイズを少なくとも 512 KB に設定する必要があります。

JVM 最大ヒープサイズの必要な増加量は、次の式で算出します。

（512 KB）x（100）=51200 KB（50 MB）

JVM 最大ヒープサイズは、50 MB 単位で増やす必要があり、合計 562 MB まで増やすことができます。

**ヒープフラグメンテーションについて**

ヒープフラグメンテーションの傾向があるシステムで、インラインドキュメントのサイズに大きな値を設定すると、OutOfMemoryError が発生する可能性が高くなります。ドキュメントをインラインで格納するには、JVM ヒープメモリに十分な連続スペースを確保する必要があります。一部のオペレーティングシステム、JVM およびガベージコレクションアルゴリズムでは、ヒープフラグメントが発生しがちです。フラグメンテーションにより、連続するヒープ領域の量が減少し、合計空き容量が十分にある場合でも OutOfMemoryError が発生することがあります。

例えば、アプリケーションサーバーでの以前の処理により JVM ヒープがフラグメントされた状態になっている場合、ガベージコレクタはヒープを十分に圧縮することができず、空き領域の大きなブロックを確保することができません。最大インラインサイズの増加に伴って JVM 最大ヒープサイズを調整した場合でも、OutOfMemoryError が発生することがあります。

ヒープフラグメンテーションに対応するには、インラインドキュメントのサイズを合計ヒープサイズの 0.1 ％以下に設定する必要があります。例えば、JVM 最大ヒープサイズが 512 MB の場合は、最大インラインサイズを 512 KB（512 MB x 0.001 = 0.512 MB）に設定できます。

## WebSphere Application Server の強化 {#websphere-application-server-enhancements}

ここでは、WebSphere Application Server 環境に固有の設定について説明します。

### JVM に割り当てられる最大メモリサイズの増加 {#increasing-the-maximum-memory-allocated-to-the-jvm}

Configuration Manager を実行しているとき、またはコマンドラインユーティリティ *ejbdeploy* を使用して Enterprise JavaBeans（EJB）デプロイコードを生成しようとしているときに、OutOfMemory エラーが発生した場合は、JVM に割り当てるメモリを増やします。

1. Edit the ejbdeploy script in the *[appserver root]*/deploytool/itp/ directory:

   * (Windows) `ejbdeploy.bat`
   * (Linux and UNIX) `ejbdeploy.sh`

1. Find the `-Xmx256M` parameter and change it to a higher value, such as `-Xmx1024M`.
1. ファイルを保存します。
1. `ejbdeploy` コマンドを実行するか、または Configuration Manager を使用して再デプロイします。

## LDAP を使用した Windows Server 2003 のパフォーマンスの向上 {#improving-windows-server-2003-performance-with-ldap}

ここでは、Microsoft Windows Server 2003 オペレーティングシステム環境に固有の設定について説明します。

検索のための接続で接続プールを使用すると、必要なポート数を 50 ％減らすことができます。これは、接続で常に特定のドメインの同じ証明書が使用され、コンテキストと関連オブジェクトが明示的に閉じられるためです。

### 接続プールを使用するための Windows Server の設定 {#configure-your-windows-server-for-connection-pooling}

1. スタート／ファイル名を指定して実行をクリックし、「名前」ボックスに `regedit` と入力して「OK」をクリックし、レジストリエディターを起動します。
1. レジストリキーに移動します。 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. レジストリエディターの右側のウィンドウで、TcpTimedWaitDelay という値の名前を探します。値の名前が表示されない場合は、メニューバーから編集／新規／DWORD 値を選択して名前を追加します。
1. 「名前」ボックスにフラグメント名として「`TcpTimedWaitDelay`

   >[!NOTE]
   >
   >If you do not see a flashing cursor and `New Value #` inside the box, right-click inside the right panel, select Rename and, in the Name box, type `TcpTimedWaitDelay`*.*

1. MaxUserPort、MaxHashTableSize および MaxFreeTcbs の値について、手順 4 を繰り返します。
1. 右側のウィンドウ内をダブルクリックし、TcpTimedWaitDelay 値を設定します。「表記」で「10 進」を選択し、「値のデータ」ボックスに `30` と入力します。
1. 右側のウィンドウ内をダブルクリックし、MaxUserPort 値を設定します。「表記」で「10 進」を選択し、「値のデータ」ボックスに `65534` と入力します。
1. 右側のウィンドウ内をダブルクリックし、MaxHashTableSize 値を設定します。「表記」で「10 進」を選択し、「値のデータ」ボックスに `65536` と入力します。
1. 右側のウィンドウ内をダブルクリックし、MaxFreeTcbs 値を設定します。「表記」で「10 進」を選択し、「値のデータ」ボックスに `16000` と入力します。

>[!NOTE]
>
>レジストリエディターまたは別の方法を使用してレジストリを誤って変更すると、重大な問題が発生する場合があります。これらの問題を解決するために、オペレーティングシステムの再インストールが必要になる場合があります。レジストリの変更はユーザーの責任で行ってください。

