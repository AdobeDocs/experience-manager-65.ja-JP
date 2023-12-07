---
title: アプリケーションサーバーのパフォーマンスの強化
description: このドキュメントでは、AEM forms アプリケーションサーバーのパフォーマンスを向上させるために設定できるオプション設定について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6e2f3d4c-2ead-45b3-98e7-32cacc7e2985
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 13%

---

# アプリケーションサーバーのパフォーマンスの強化{#enhancing-application-server-performance}

ここでは、AEM forms アプリケーションサーバーのパフォーマンスを向上させるために設定できるオプション設定について説明します。

## アプリケーションサーバーのデータソースの設定 {#configuring-application-server-data-sources}

AEM forms では、AEM forms リポジトリをデータソースとして使用します。 AEM forms リポジトリにはアプリケーションアセットが格納されます。また、サービスは、自動化されたビジネスプロセスの完了の一環として、実行時にリポジトリからアセットを取得することができます。

実行しているAEM forms モジュールの数と、アプリケーションにアクセスする同時ユーザーの数によっては、データソースへのアクセスが大きくなる場合があります。 接続プールを使用して、データソースへのアクセスを最適化できます。 「*接続プール*」は、アプリケーションやサーバーオブジェクトがデータベースへのアクセスを必要とするたびに生じる、新しいデータベース接続の作成に伴うオーバーヘッドを回避するために使用される技術です。接続プールは、通常、Web ベースおよびエンタープライズアプリケーションで使用され、通常はアプリケーションサーバーで処理されますが、これらに限定されません。

接続が不足したり、アプリケーションのパフォーマンスが低下したりする可能性があるので、接続プールのパラメーターを適切に設定することが重要です。

接続プールの設定を適切に構成するには、アプリケーションサーバー管理者が 1 日のピーク時に接続プールを監視することが重要です。 監視により、アプリケーションとユーザーが常に十分な接続を利用できるようになります。 ほとんどのアプリケーションサーバーには監視ツールが含まれています。

WebLogic Server 管理コンソールを使用して、ドメイン内の JDBC データソースインスタンスごとに様々な統計を監視できます。 詳しくは、WebLogic のドキュメントを参照してください。

アプリケーション・サーバー管理者が正しい接続プール設定を決定した場合、そのユーザーはこの情報をデータベース管理者に伝える必要があります。 データベース管理者は、データベース接続の数がデータソースの接続プール内の接続数と等しいので、この情報を必要とします。 次に、以下に示すように、アプリケーションサーバーとデータソースの種類の接続プールを設定する手順を実行します。

### 接続と MySQL に関する WebLogic のOracleプール設定 {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. 「Domain Structure」で、 Services / JDBC / Data Sources をクリックし、右側のウィンドウで「IDP_DS」をクリックします。
1. 次の画面で、「 Configuration 」>「 Connection Pool 」タブをクリックし、次のボックスに値を入力します。

   * 初期容量
   * 最大容量
   * 処理能力増分
   * 文のキャッシュサイズ

1. 「保存」をクリックし、「変更をアクティベート」をクリックします。
1. WebLogic 管理対象サーバーを再起動します。

### SQLServer に対する WebLogic の接続プール設定の構成 {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. Change Center で、「Lock &amp; Edit」をクリックします。
1. 「Domain Structure」で、 Services / JDBC / Data Sources をクリックし、右側のウィンドウで「EDC_DS」をクリックします。
1. 次の画面で、「 Configuration 」>「 Connection Pool 」タブをクリックし、次のボックスに値を入力します。

   * 初期容量
   * 最大容量
   * 処理能力増分
   * 文のキャッシュサイズ

1. 「保存」をクリックし、「変更をアクティベート」をクリックします。
1. WebLogic 管理対象サーバーを再起動します。

### DB2 用の WebSphere の接続プール設定の指定 {#configure-connection-pool-settings-for-websphere-for-db2}

1. ナビゲーションツリーで、 Resources / JDBC / JDBC Providers をクリックします。 右側のウィンドウで、作成したデータソース (DB2 Universal JDBC Driver Provider またはLiveCycle- db2 - IDP_DS) をクリックします。
1. 「Additional Properties」で「 Data Sources 」をクリックし、「 IDP_DS 」を選択します。
1. 次の画面の「Additional Properties」で、「Connection Pool Properties」をクリックし、「Maximum Connections」ボックスと「Minimum Connections」ボックスに値を入力します。
1. [OK] または [ 適用 ] をクリックし、[ 直接マスター構成に保存 ] をクリックします。

### oracle用の WebSphere の接続プールの設定 {#configure-connection-pool-settings-for-websphere-for-oracle}

1. ナビゲーションツリーで、 Resources / JDBC / JDBC Providers をクリックします。 右側のウィンドウで、作成したOracleJDBC Driver データソースをクリックします。
1. 「Additional Properties」で「 Data Sources 」をクリックし、「 IDP_DS 」を選択します。
1. 次の画面の「Additional Properties」で、「Connection Pool Properties」をクリックし、「Maximum Connections」ボックスと「Minimum Connections」ボックスに値を入力します。
1. [OK] または [ 適用 ] をクリックし、[ 直接マスター構成に保存 ] をクリックします。

### WebSphere の接続プールの設定（SqlServer 用） {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. ナビゲーションツリーで、 Resources / JDBC / JDBC Providers をクリックし、右側のウィンドウで、作成した User-Defined JDBC Driver データソースをクリックします。
1. 「Additional Properties」で「 Data Sources 」をクリックし、「 IDP_DS 」を選択します。
1. 次の画面の「Additional Properties」で「Connection Pool Properties」をクリックし、「Maximum Connections」ボックスと「Minimum Connections」ボックスに値を入力します。
1. [OK] または [ 適用 ] をクリックし、[ 直接マスター構成に保存 ] をクリックします。

## インラインドキュメントの最適化と JVM メモリへの影響 {#optimizing-inline-documents-and-impact-on-jvm-memory}

比較的小さいサイズのドキュメントを処理する場合は、ドキュメント転送速度とストレージスペースに関連するパフォーマンスを向上させることができます。 これをおこなうには、次のAEM forms 製品設定を実装します。

* ほとんどのドキュメントのサイズより大きくなるように、AEM forms のデフォルトのドキュメントの最大インラインサイズを増やします。
* 大きなファイルを処理する場合は、高速ディスクシステムまたは RAM ディスク上のストレージディレクトリを指定します。

最大インラインサイズとストレージディレクトリ (AEM forms の一時ファイルディレクトリと GDS ディレクトリ ) は、管理コンソールで設定します。

### ドキュメントサイズと最大インラインサイズ {#document-size-and-maximum-inline-size}

AEM forms で処理用に送信されるドキュメントがデフォルトのドキュメント最大インラインサイズ以下の場合、ドキュメントはAdobeにインラインで保存され、ドキュメントはサーバーのドキュメントオブジェクトとしてシリアライズされます。 ドキュメントをインラインで保存すると、パフォーマンスが大幅に向上する場合があります。 ただし、Forms ワークフローを使用している場合は、追跡のためにコンテンツをデータベースに保存することもできます。 したがって、最大インラインサイズを増やすと、データベースサイズに影響を与える場合があります。

最大インラインサイズより大きいドキュメントは、ローカルファイルシステムに保存されます。 Adobeとサーバーの間で転送されるサーバードキュメントオブジェクトは、そのファイルへのポインタに過ぎません。

ドキュメントコンテンツがインライン化される（つまり、最大インラインサイズより小さい）と、コンテンツはドキュメントのシリアル化ペイロードの一部としてデータベースに保存されます。 したがって、最大インラインサイズを増やすと、データベースサイズに影響を与える可能性があります。

**最大インラインサイズの変更**

1. 管理コンソールで、設定／コアシステム設定／設定をクリックします。
1. 「デフォルトのドキュメント最大インラインサイズ」ボックスに値を入力し、「OK」をクリックします。

   >[!NOTE]
   >
   >ドキュメント最大インラインサイズプロパティの値は、JEE 環境上の AEM Forms と、JEE 環境上の OSGi バンドルを含む AEM Forms 上の AEM Forms と同一である必要があります。この手順では、JEE 環境上のAEM Formsに対してのみ値を更新し、JEE 環境に含まれる OSGi バンドル上のAEM Formsに対しては値を更新しません。

1. 次のシステムプロパティを使用して、アプリケーションサーバーを再起動します。

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >上記のシステムプロパティは、JEE 環境上のAEM Formsと、OSGi バンドル上のAEM Formsに JEE 環境に含まれているAEM Formsに設定された「ドキュメント最大インラインサイズ」プロパティの値を上書きします。

>[!NOTE]
>
>デフォルトの最大インラインサイズは65536バイトです。

### JVM 最大ヒープサイズ {#jvm-maximum-heap-size}

最大インラインサイズを増やすと、シリアル化されたドキュメントの保存に必要なメモリが増えます。 したがって、通常は JVM 最大ヒープサイズも増やす必要があります。

多くのドキュメントを処理している負荷の高いシステムは、JVM ヒープメモリを急速に飽和させる可能性があります。 OutOfMemoryError を回避するには、JVM 最大ヒープサイズを、インラインドキュメントのサイズと、特定の時点で通常実行されるドキュメント数を掛けた値に増やします。

JVM 最大ヒープサイズの増加= （インラインドキュメントのサイズ） x （処理されたドキュメントの平均数）

**JVM 最大ヒープサイズの計算**

この例では、現在の JVM 最大ヒープが 512 MB に設定され、最大インラインサイズは 64 KB です。 サーバーは、10 個のジョブが同時に実行され、各ジョブに 9 個の入力ファイルと 1 個の結果ファイル（合計 10 個のジョブあたりのファイルと 100 個のファイルが同時に処理される）があるシナリオに対して設定する必要があります。 すべてのファイルのサイズは 512 KB 未満です。

すべてのファイルをインラインで保存するには、最大インラインサイズを 512 KB 以上に設定します。

JVM の最大ヒープサイズの必要な増加は、次の式を使用して計算されます。

(512 KB) x (100) = 51200 KB(50 MB)

JVM の最大ヒープサイズは 50 MB 増やす必要があり、合計 562 MB です。

**ヒープフラグメント化の検討**

インラインドキュメントのサイズを大きな値に設定すると、ヒープフラグメンテーションが発生しやすいシステムで OutOfMemoryError が発生するリスクが高くなります。 ドキュメントをインラインで保存するには、JVM ヒープメモリに十分な連続スペースが必要です。 一部のオペレーティングシステム、JVM、およびガベージコレクションアルゴリズムでは、ヒープフラグメント化が発生しやすくなっています。 フラグメンテーションは、連続したヒープ領域の量を減らし、十分な合計空き領域が存在する場合でも OutOfMemoryError を引き起こす可能性があります。

例えば、アプリケーションサーバー上の以前の操作は、JVM ヒープを断片化された状態に残し、ガベージコレクターは、ヒープを十分にコンパクト化して空き領域の大きなブロックを取り戻すことができません。 最大インラインサイズの増加に合わせて JVM 最大ヒープサイズが調整された場合でも、OutOfMemoryError が発生する可能性があります。

ヒープの断片化を考慮するには、インラインドキュメントのサイズを合計ヒープサイズの 0.1%より大きく設定しないでください。 例えば、JVM の最大ヒープサイズが 512 MB の場合、最大インラインサイズは 512 MB x 0.001 = 0.512 MB、または 512 KB になります。

## WebSphere Application Server の機能強化 {#websphere-application-server-enhancements}

この節では、WebSphere Application Server 環境に固有の設定について説明します。

### JVM に割り当てられる最大メモリの増加 {#increasing-the-maximum-memory-allocated-to-the-jvm}

Configuration Manager を実行している場合、またはコマンドラインユーティリティを使用して Enterprise JavaBeans(EJB) の配備コードを生成しようとしている場合 *ejbdeploy* OutOfMemory エラーが発生した場合は、JVM に割り当てるメモリ量を増やします。

1. *[appserver root]*/deploytool/itp/ ディレクトリの ejbdeploy スクリプトを編集します。

   * Windows：`ejbdeploy.bat`
   * Linux および UNIX：`ejbdeploy.sh`

1. `-Xmx256M` パラメーターを検索して、値を現在のものより高い値に変更します（`-Xmx1024M` など）。
1. ファイルを保存します。
1. `ejbdeploy` コマンドを実行するか、Configuration Manager を使用して再デプロイします。

## LDAP を使用した Windows Server 2003 のパフォーマンスの向上 {#improving-windows-server-2003-performance-with-ldap}

このコンテンツでは、Microsoft Windows Server 2003 オペレーティングシステム環境に固有の設定について説明します。

検索接続で接続プールを使用すると、必要なポート数が 50 %減少する可能性があります。 これは、接続が常に特定のドメインに同じ資格情報を使用し、コンテキストと関連オブジェクトが明示的に閉じられるからです。

### 接続プーリング用に Windows Server を構成する {#configure-your-windows-server-for-connection-pooling}

1. スタート／ファイル名を指定して実行をクリックし、「名前」ボックスに `regedit` と入力して「OK」をクリックし、レジストリエディターを起動します。
1. レジストリキー `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters` に移動します。
1. レジストリエディターの右側のウィンドウで、 TcpTimedWaitDelay 値の名前を探します。 名前が表示されない場合は、メニューバーから編集/新規/DWORD 値を選択して名前を追加します。
1. 「名前」ボックスに `TcpTimedWaitDelay` と入力します。

   >[!NOTE]
   >
   >点滅するカーソルと `New Value #` がボックス内に表示されない場合は、右側のパネル内を右クリックし、「名前の変更」を選択して、「名前」ボックスに `TcpTimedWaitDelay`*と入力します。*

1. MaxUserPort、MaxHashTableSize、MaxFreeTcbs の値に対して、手順 4 を繰り返します。
1. 右側のウィンドウ内をダブルクリックして、TcpTimedWaitDelay 値を設定します。 「表記」で「10 進」を選択し、「値のデータ」ボックスに `30` と入力します。
1. 右側のウィンドウ内をダブルクリックし、MaxUserPort 値を設定します。「表記」で「10 進」を選択し、「値のデータ」ボックスに `65534` と入力します。
1. 右側のウィンドウ内をダブルクリックし、MaxHashTableSize 値を設定します。「表記」で「10 進」を選択し、「値のデータ」ボックスに `65536` と入力します。
1. 右側のウィンドウ内をダブルクリックし、MaxFreeTcbs 値を設定します。「表記」で「10 進」を選択し、「値のデータ」ボックスに `16000` と入力します。

>[!NOTE]
>
>レジストリエディターを使用したり、別の方法を使用したりしてレジストリを正しく変更しない場合、重大な問題が発生する可能性があります。 この問題が発生した場合は、オペレーティングシステムを再インストールする必要があります。 レジストリを自分の責任で変更します。
