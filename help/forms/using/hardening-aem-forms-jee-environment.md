---
title: JEE 上の AEM Forms 環境の堅牢化
seo-title: Hardening Your AEM Forms on JEE Environment
description: 企業のイントラネット内で動作する JEE 上の AEM Forms のセキュリティを強化するための、様々なセキュリティ強化設定について学びます。
seo-description: Learn a variety of security-hardening settings to enhance the security of AEM Forms on JEE running in a corporate intranet.
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
role: Admin
exl-id: 6fb260f9-d0f8-431e-8d4e-535b451e4124
source-git-commit: d2661ee6614261179b5e8d2d9ffb7c240ce676dc
workflow-type: tm+mt
source-wordcount: '7665'
ht-degree: 99%

---

# JEE 上の AEM Forms 環境の堅牢化 {#hardening-your-aem-forms-on-jee-environment}

企業のイントラネット内で動作する JEE 上の AEM Forms のセキュリティを強化するための、様々なセキュリティ強化設定について学びます。

この記事では、JEE 上の AEM Forms を実行するサーバーを保護するための推奨事項とベストプラクティスについて説明します。ここでは、オペレーティングシステムとアプリケーションサーバーのホストの堅牢化について包括的な説明はしません。企業のイントラネット内で運用している JEE 上の AEM Forms のセキュリティを強化するために行うことが望ましい、様々なセキュリティ堅牢化設定について説明します。なお、JEE 上の AEM Forms アプリケーションサーバーのセキュリティを確実に保つには、これだけでなく、セキュリティの監視、検出および応答の方策を実装することも必要です。

この記事では、インストールと設定の作業において、次の各段階で適用する堅牢化手法について説明します。

* **インストール前：**&#x200B;この手法は、JEE 上の AEM Forms をインストールする前に実行します。
* **インストール時：**&#x200B;この手法は、JEE 上の AEM Forms ソフトウェアをインストールする作業の一環として実行します。
* **インストール後：**&#x200B;この手法は、インストール終了後と、それ以降の定期的な管理作業として実行します。

JEE 上の AEM Forms は詳細なカスタマイズが可能で、様々な環境で動作します。推奨事項には、一部の組織のニーズに合わないものも含まれている可能性があります。

## インストール前 {#preinstallation}

JEE 上の AEM Forms をインストールする前には、ネットワーク層とオペレーティングシステムに対してセキュリティソリューションを適用することができます。ここでは、いくつかの問題と、この領域におけるセキュリティの脆弱性を減らすための推奨事項について説明します。

**UNIX および Linux へのインストールと設定**

JEE 上の AEM Forms のインストール作業や設定作業を実行するときは、ルートシェルを使用しないでください。デフォルトでは、ファイルは /opt ディレクトリの下にインストールされるので、インストールを実行するユーザーには /opt 以下のすべてのファイルの権限が必要です。または、各ユーザーには /user ディレクトリに対するすべてのファイル権限があらかじめ付与されているので、/user ディレクトリにインストールを実行することもできます。

**Windows へのインストールと設定**

自動オプションインストールを使用して JBoss に JEE 上の AEM Forms をインストールする場合、または PDF Generator をインストールする場合、Windows へのインストールは管理者として実行する必要があります。また、PDF Generator をネイティブアプリケーションサポートと共に Windows にインストールする場合は、Microsoft Office をインストールしたのと同じ Windows ユーザーとしてインストールを実行する必要があります。インストールの権限について詳しくは、お使いのアプリケーションサーバーに対応した* JEE 上の AEM Forms のインストールおよびデプロイ* ドキュメントを参照してください。

### ネットワーク層のセキュリティ {#network-layer-security}

ネットワークセキュリティの脆弱性は、インターネットまたはイントラネットに接続しているすべてのアプリケーションサーバーにとって、最も重大な脅威の 1 つです。ここでは、このような脆弱性に対してネットワーク上のホストを堅牢化する手順について説明します。具体的には、ネットワークのセグメント化、TCP/IP（Transmission Control Protocol/Internet Protocol）スタックの堅牢化、ホスト保護のためのファイアウォールの使用などの手順を取り上げます。

次の表では、ネットワークセキュリティの脆弱性を減らすための一般的なプロセスについて説明します。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>説明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>非武装地帯（DMZ）</p> </td> 
   <td><p>forms サーバーを非武装地帯（DMZ）にデプロイします。ファイアウォールの内側に配置された、JEE 上の AEM Forms を実行するアプリケーションサーバーに対して、少なくとも 2 つのレベルでセグメント化が必要です。Web サーバーを含む DMZ から外部ネットワークを分離します。同様に、外部ネットワークは内部ネットワークからも分離している必要があります。ファイアウォールを使用して、この分離した層を実装します。必要最小限のデータのみが許可されるように、各ネットワーク層を通過するトラフィックを分類して制御します。</p> </td> 
  </tr> 
  <tr> 
   <td><p>プライベート IP アドレス</p> </td> 
   <td><p>AEM Forms アプリケーションサーバーで、RFC 1918 プライベート IP アドレスと NAT（ネットワークアドレス変換）を使用します。プライベート IP アドレス（10.0.0.0/8、172.16.0.0/12 および 192.168.0.0/16）を割り当てることにより、インターネットを通じて、NAT を使用する内部ホストに対して攻撃者がトラフィックをルーティングできないようにします。</p> </td> 
  </tr> 
  <tr> 
   <td><p>ファイアウォール</p> </td> 
   <td><p>次の基準を使用して、ファイアウォールソリューションを選択します。</p> 
    <ul> 
     <li><p>単純なパケットフィルタリングソリューションではなく、プロキシサーバーまたは「<em>ステートフルインスペクション</em>」をサポートするファイアウォールを実装する。</p> </li> 
     <li><p><em>明示的に許可されたサービス以外はすべて拒否する</em>セキュリティパラダイムをサポートするファイアウォールを使用する。</p> </li> 
     <li><p>デュアルホームまたはマルチホームのファイアウォールソリューションを実装する。このアーキテクチャによって、最も高いセキュリティレベルが実現し、権限のないユーザーがファイアウォールセキュリティを迂回できないようにすることができます。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>データベースポート</p> </td> 
   <td><p>データベースのデフォルトのリスニングポート（MySQL - 3306、Oracle - 1521、MS SQL - 1433）は、使用しないでください。データベースポートの変更について詳しくは、データベースのドキュメントを参照してください。</p> <p>データベースポートを変更すると、JEE 上の AEM Forms の設定全体に影響します。デフォルトポートを変更した場合、JEE 上の AEM Forms のデータソースなど、設定の別の領域を変更内容に合わせて修正する必要があります。</p> <p>JEE 上の AEM Forms におけるデータソースの設定について詳しくは、<a href="/help/forms/using/introduction-aem-forms.md" target="_blank">AEM Forms ユーザーガイド</a>の「JEE 上の AEM Forms のインストールおよびアップグレード」または「アプリケーションサーバー用 JEE 上の AEM Forms へのアップグレード」を参照してください。</p> </td> 
  </tr> 
 </tbody> 
</table>

### オペレーティングシステムのセキュリティ {#operating-system-security}

次の表では、オペレーティングシステムに存在するセキュリティの脆弱性を最小にするために役立つ方法について説明します。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p></th> 
   <th><p>説明</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>セキュリティパッチ</p></td> 
   <td><p>ベンダーのセキュリティパッチとアップデートが迅速に適用されない場合、権限のないユーザーがアプリケーションサーバーにアクセスするリスクが高まります。実稼働サーバーにセキュリティパッチを適用する場合は、適用する前にテストしてください。</p><p>さらに、パッチを定期的にチェックしてインストールするためのポリシーとプロシージャを作成してください。</p></td> 
  </tr> 
  <tr> 
   <td><p>ウイルス対策ソフトウェア</p></td> 
   <td><p>ウイルススキャンプログラムは、署名をスキャンするか、異常な動作を監視することによって、感染ファイルを識別します。スキャンプログラムでは、ウイルスの署名をファイルに保管します。通常、このファイルはローカルハードドライブに格納されます。新しいウイルスは次から次へと出現するので、ウイルススキャンプログラムですべての最新のウイルスを識別できるように、このファイルを頻繁に更新する必要があります。</p></td> 
  </tr> 
  <tr> 
   <td><p>ネットワークタイムプロトコル（NTP）</p></td> 
   <td><p>フォレンジック分析のために、forms サーバーの時計は常に正確に設定されている必要があります。NTP を使用して、インターネットに直接接続しているすべてのシステムの時間を同期させてください。</p></td> 
  </tr> 
 </tbody> 
</table>

お使いのオペレーティングシステムのセキュリティ情報について詳しくは、 [オペレーティング・システムのセキュリティ情報](https://helpx.adobe.com/jp/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information).

## インストール {#installation}

ここでは、AEM Forms インストールプロセスで、セキュリティの脆弱性を減らすために使用できる方法について説明します。これらの方法では、状況によってはインストールプロセスのオプションを使用します。次の表では、各方法について解説します。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>説明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>権限</p> </td> 
   <td><p>ソフトウェアのインストールには、必要最小限の権限を使用してください。Administrators グループに属していないアカウントでコンピューターにログインします。Windows では、runas コマンドを使用して、管理者ユーザーとして JEE 上の AEM Forms インストーラーを実行することができます。UNIX および Linux システムでは、<code>sudo</code> などのコマンドを使用してソフトウェアをインストールします。 </p> </td> 
  </tr> 
  <tr> 
   <td><p>ソフトウェアソース</p> </td> 
   <td><p>信頼できないソースから JEE 上の AEM Forms をダウンロードまたは実行しないでください。</p> <p>悪意のあるプログラムには、データの盗難、改変、削除、サービス拒否などの様々な手段でセキュリティを侵害するコードが含まれています。必ず、Adobe DVD または信頼できるソースから入手した JEE 上の AEM Forms をインストールしてください。</p> </td> 
  </tr> 
  <tr> 
   <td><p>ディスクのパーティション</p> </td> 
   <td><p>JEE 上の AEM Forms は、専用のディスクパーティションに配置してください。ディスクのセグメント化とは、セキュリティを強化するために、サーバー上の特定のデータを個別の物理ディスクに保管するプロセスのことです。この方法でデータを整理すると、ディレクトリトラバーサル攻撃のリスクを軽減することができます。システムパーティションとは別に、JEE 上の AEM Forms コンテンツディレクトリをインストールするパーティションを作成することを検討してください。（Windows のシステムパーティションには system32 ディレクトリまたはブートパーティションが含まれています）。</p> </td> 
  </tr> 
  <tr> 
   <td><p>コンポーネント</p> </td> 
   <td><p>既存のサービスを評価し、不要なサービスを無効化またはアンインストールしてください。不要なコンポーネントやサービスをインストールしないでください。</p> <p>アプリケーションサーバーのデフォルトインストールには、サーバーの用途によっては必要のないサービスが含まれている可能性があります。攻撃のエントリポイントを最小限に抑えるために、デプロイメントに先立って、不要なサービスをすべて無効にする必要があります。例えば、JBoss では、META-INF/jboss-service.xml 記述子ファイル内の不要なサービスをコメントアウトします。</p> </td> 
  </tr> 
  <tr> 
   <td><p>クロスドメインポリシーファイル</p> </td> 
   <td><p>サーバー上に <code>crossdomain.xml</code> ファイルが存在すると、そのサーバーを直ちに弱化させる可能性があります。ドメインのリストに可能な限り制限をかけることをお勧めします。ガイド<em>（非推奨）</em>を使用する場合、開発環境から実稼働環境への移行中に使用される <code>crossdomain.xml</code> ファイルを配置しないでください。Web サービスで使用されるガイドの場合、ガイドを提供するサーバーと同じサーバー上にそのサービスがあれば、<code>crossdomain.xml</code> ファイルはまったく必要ありません。しかし、サービスが別のサーバー上にある場合や、クラスターが関係している場合は、<code>crossdomain.xml</code> ファイルが存在している必要があります。crossdomain.xml ファイルについて詳しくは、 <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a> を参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td><p>オペレーティングシステムのセキュリティ設定</p> </td> 
   <td><p>Solaris プラットフォームで 192 ビットまたは 256 ビット XML 暗号化を使用する必要がある場合、<code>pkcs11_softtoken.so</code> ではなく、必ず <code>pkcs11_softtoken_extra.so</code> をインストールしてください。</p> </td> 
  </tr> 
 </tbody> 
</table>

## インストール後の手順 {#post-installation-steps}

JEE 上の AEM Forms のインストールが完了したら、セキュリティ上の観点から、定期的に環境の保守を行うことが重要です。

次の節では、デプロイ済みの Forms サーバーを保護するための、各種の推奨タスクについて詳細に説明します。

### AEM Forms のセキュリティ {#aem-forms-security}

次の推奨設定は、管理 Web アプリケーションの外にある JEE 上の AEM Forms サーバーに適用されます。サーバーのセキュリティリスクを軽減するには、この設定を JEE 上の AEM Forms のインストール直後に適用してください。

**セキュリティパッチ**

ベンダーのセキュリティパッチとアップデートが迅速に適用されない場合、権限のないユーザーがアプリケーションサーバーにアクセスするリスクが高まります。実稼働サーバーにセキュリティパッチを適用する場合は、事前にテストを実施し、 アプリケーションの互換性と可用性を確認した上で適用してください。また、パッチのチェックとインストールを定期的に行うためのポリシーと手続きを定めてください。JEE 上の AEM Forms のアップデートは Enterprise 製品のダウンロードサイトにあります。

**サービスアカウント（Windows への JBoss 自動インストールのみ）**

JEE 上の AEM Forms は、デフォルトでは、LocalSystem アカウントを使用してサービスをインストールします。組み込み LocalSystem ユーザーアカウントは、高いレベルのアクセス権限を付与されており、Administrators グループに属しています。ワーカープロセス ID を LocalSystem ユーザーアカウントで実行した場合、そのワーカープロセスはシステム全体に対してフルアクセス権限を持ちます。

JEE 上の AEM Forms のデプロイ先のアプリケーションサーバーを実行するには、次の手順に従って、管理者以外の固有のアカウントを使用してください。

1. Microsoft 管理コンソール（MMC）で、forms サーバーサービスへのログインに使用するローカルユーザーを作成します。

   * 「**ユーザーはパスワードを変更できない**」オプションを選択します。
   * **所属するグループ**&#x200B;タブに、「ユーザー」グループが表示されていることを確認してください&#x200B;**。**

   >[!NOTE]
   >
   >PDF Generator 用のこの設定は変更できません。

1. **スタート**／**設定**／**管理ツール**／**サービス**&#x200B;を選択します。
1. JEE 上の AEM Forms 向けの JBoss をダブルクリックして、サービスを停止します。
1. 「**ログオン**」タブで、「**アカウント**」を選択し、作成したユーザーアカウントを参照して、アカウントのパスワードを入力します。
1. MMC で、「**ローカルセキュリティ設定**」を開き、**ローカルポリシー**／**ユーザー権利の割り当て**&#x200B;を選択します。
1. forms サーバーを実行しているユーザーアカウントに、次の権限を割り当てます。

   * ターミナルサービスを使ったログオンを拒否する
   * ローカルでログオンを拒否する
   * サービスとしてログオン（通常は既に設定済み）

1. 次のディレクトリの新しいユーザーアカウントに変更権限を付与します。
   * **グローバルドキュメントストレージ (GDS) ディレクトリ**：GDS ディレクトリの場所は、AEM Forms のインストールプロセス中に手動で設定します。インストール時に場所を指定しないと、`[JBoss root]/server/[type]/svcnative/DocumentStorage` にあるアプリケーションサーバーのインストールディレクトリの下にあるディレクトリがデフォルトの場所になります。
   * **CRX リポジトリディレクトリ**：デフォルトの場所は `[AEM-Forms-installation-location]\crx-repository` です。
   * **AEM Forms 一時ディレクトリ**：
      * （Windows）環境変数で設定されている TMP または TEMP パス
      * （AIX、Linux または Solaris）ログインユーザーのホームディレクトリ
UNIX 系のシステムでは、root 以外のユーザーは次のディレクトリを一時ディレクトリとして使用できます。
      * （Linux）/var/tmp or /usr/tmp
      * （AIX）/tmp or /usr/tmp
      * （Solaris）/var/tmp または /usr/tmp
1. 新しいユーザーアカウントに、次のディレクトリへの書き込み権限を付与します。
   * [JBoss ディレクトリ]\standalone\deployment
   * [JBoss ディレクトリ]\standalone\
   * [JBoss ディレクトリ]\bin\

   >[!NOTE]
   >
   >JBoss Application サーバーのデフォルトのインストール場所：
   >
   >* Windows：C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux：/opt/jboss/


1. アプリケーションサーバーを起動します。

**Configuration Manager ブートストラップサーブレットの無効化**

Configuration Manager は、アプリケーションサーバーにデプロイ済みのサーブレットを利用して、JEE 上の AEM Forms データベースのブートストラップを実行します。Configuration Manager は、設定が完了する前にこのサーブレットにアクセスするので、承認済みユーザーのみにアクセスを限定するセキュリティは施されていません。Configuration Manager を使用して JEE 上の AEM Forms の設定を完了した後は、このサーブレットを無効にしてください。

1. adobe-livecycle-[appserver].ear ファイルを解凍します。
1. META-INF/application.xml ファイルを開きます。
1. adobe-bootstrapper.war セクションを検索します。

   ```java
   <!-- bootstrapper start --> 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   <!-- bootstrapper end-->
   ```

1. AEM Forms サーバーを停止します。
1. adobe-bootstrapper.war および adobe-lcm-bootstrapper-redirectory. war モジュールを次のようにコメントアウトします。

   ```java
   <!-- bootstrapper start --> 
   <!-- 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   --> 
   <!-- bootstrapper end-->
   ```

1. META-INF/application.xml ファイルを保存して閉じます。
1. EAR ファイルの zip ファイルを作成し、アプリケーションサーバーに再デプロイします。
1. AEM Forms サーバーを起動します。
1. 以下の URL をブラウザーに入力して変更をテストし、URL が機能しないことを確認します。

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**Trust Store へのリモートアクセスのロックダウン**

Configuration Manager を使用して、Acrobat Reader DC Extensions の資格情報を JEE 上の AEM Forms Trust Store にアップロードできます。つまり、リモートプロトコル（SOAP および EJB）経由の Trust Store 資格情報サービスへのアクセスは、デフォルトで有効になっています。このアクセスは、Configuration Manager を使用して使用権限資格情報のアップロードを完了した後、または後で管理コンソールを使用して資格情報を管理することにした場合は、必要なくなります。

[サービスへの不要なリモートアクセスの無効化](https://helpx.adobe.com/jp/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services)の手順に従って、Trust Store の全サービスへのリモートアクセスを無効にすることができます。

**すべての不要な匿名アクセスの無効化**

一部の forms サーバーサービスには、匿名の呼び出しによって実行される操作があります。このようなサービスへの匿名アクセスが必要ない場合は、[サービスへの不要な匿名アクセスの無効化](https://helpx.adobe.com/jp/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services)の手順に従って、アクセスを無効にしてください。

#### デフォルトの管理者パスワードの変更 {#change-the-default-administrator-password}

JEE 上の AEM Forms をインストールすると、上級管理者ユーザーまたはログイン ID 管理者ユーザーのために、デフォルトパスワードが「*password*」であるデフォルトユーザーアカウントが 1 つ設定されます。このパスワードは、Configuration Manager を使用して直ちに変更してください。

1. Web ブラウザーに次の URL を入力します。

   ```java
   https://[host name]:[port]/adminui
   ```

   デフォルトのポート番号は次のいずれかです。

   **JBoss：** 8080

   **WebLogic Server：** 7001

   **WebSphere：** 9080

1. **ユーザー名**&#x200B;フィールドに `administrator` と入力し、**パスワード**&#x200B;フィールドに `password` と入力します。
1. **設定**／**User Management**／**ユーザーとグループ**&#x200B;をクリックします。
1. **検索**&#x200B;フィールドに `administrator` と入力し、**検索**&#x200B;をクリックします。
1. ユーザーの一覧で「**上級管理者**」 をクリックします。
1. ユーザーを編集ページで「**パスワードの変更**」をクリックします。
1. 新しいパスワードを指定し、「**保存**」をクリックします。

次の手順を実行することで CRX 管理者のデフォルトパスワードの変更もお勧めします。

1. デフォルトのユーザー名／パスワードを使用して、`https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` にログインします。
1. 検索フィールドに「管理者」と入力し、**移動**&#x200B;をクリックします。
1. 検索結果から「**管理者**」を選択し、ユーザーインターフェイスの右下で「**編集**」アイコンをクリックします。
1. 「**新しいパスワード**」フィールドに新しいパスワードを、「**パスワード**」フィールドに古いパスワードを指定します。
1. ユーザーインターフェイスの右下で「保存」アイコンをクリックします。

#### WSDL の生成の無効化 {#disable-wsdl-generation}

Web Service Definition Language（WSDL）の生成は、開発者が WSDL の生成を使用してクライアントアプリケーションを構築する開発環境でのみ有効にしてください。実稼働環境では WSDL の生成を無効化して、サービスの内部詳細が公開されないようにすることができます。

1. Web ブラウザーに次の URL を入力します。

   ```java
   https://[host name]:[port]/adminui
   ```

1. **設定／コアシステム設定／設定**&#x200B;をクリックします。
1. 「**WSDL を有効にする**」のチェックを外して「**OK**」をクリックします。

### アプリケーションサーバーのセキュリティ {#application-server-security}

次の表では、JEE 上の AEM Forms アプリケーションのインストール後に、アプリケーションサーバーを保護するために使用するいくつかの方法について説明します。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>説明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>アプリケーションサーバーの管理コンソール</p> </td> 
   <td><p>アプリケーションサーバーで JEE 上の AEM Forms のインストール、設定およびデプロイを完了したら、アプリケーションサーバーの管理コンソールへのアクセスを無効にする必要があります。詳しくは、アプリケーションサーバーのドキュメントを参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td><p>アプリケーションサーバーの cookie の設定</p> </td> 
   <td><p>アプリケーションの cookie は、アプリケーションサーバーが管理しています。アプリケーションをデプロイするときに、アプリケーションサーバーの管理者は cookie の環境設定をサーバー全体に対してまたは個別のアプリケーションに対して指定することができます。デフォルトでは、サーバーの設定が優先します。</p> <p>アプリケーションサーバーで生成されるすべてのセッション cookie に <code>HttpOnly</code> 属性が含まれている必要があります。例えば、JBoss アプリケーションサーバーを使用する場合、<code>WEB-INF/web.xml</code> ファイルで、SessionCookie 要素を <code>httpOnly="true"</code> に変更できます。</p> <p>cookie の送信には HTTPS のみを使用するように制限することもできます。このように設定すると、cookie が HTTP を経由して暗号化されずに送信されることはありません。アプリケーションサーバーの管理者は、サーバーの cookie 保護をグローバルに有効化する必要があります。例えば、JBoss アプリケーションサーバーを使用する場合、<code>server.xml</code> ファイルで、コネクタ要素を <code>secure=true</code> に変更できます。</p> <p>cookie の設定について詳しくは、アプリケーションサーバーのドキュメントを参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td><p>ディレクトリの参照</p> </td> 
   <td><p>存在しないページに対する要求、またはディレクトリ名に対する要求（最後がスラッシュ（/）で終わる要求文字列）が行われた場合、アプリケーションサーバーによってディレクトリの内容が返されないようにする必要があります。これが行われないようにするには、アプリケーションサーバーのディレクトリ参照を無効にします。管理コンソールアプリケーションおよびサーバーで実行している他のアプリケーションについても、ディレクトリ参照を無効にしてください。</p> <p>JBoss の場合、次の例に示すように、web.xml ファイルで <code>DefaultServlet</code> プロパティの初期化パラメーターの listings 値を <code>false</code> に設定します。</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;default&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;listings&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>WebSphere の場合、ibm-web-ext.xmi ファイルの <code>directoryBrowsingEnabled</code> プロパティを <code>false</code> に設定します。</p> <p>WebLogic の場合、次の例に示すように、weblogic.xml ファイルの index-directories プロパティを <code>false</code> に設定します。</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### データベースのセキュリティ {#database-security}

データベースの保護を行う場合、データベースのベンダーが挙げている対策を実装することを慎重に検討してください。データベースのユーザーには、JEE 上の AEM Forms でデータベースを使用するために必要な最小限の権限を付与するようにします。例えば、データベースの管理権限を持つアカウントは使用しないでください。

Oracle では、データベースアカウントで使用する必要がある権限は、CONNECT、RESOURCE および CREATE VIEW だけです。他のデータベースについての同様の要件については、「[JEE 上の AEM Forms のインストールの準備（シングルサーバー）](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64_jp)」を参照してください。

#### Windows 上での統合セキュリティの設定（JBoss 版） {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. 次の例に示すように、[JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} を変更して、`integratedSecurity=true` を接続 URL に追加します。

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. アプリケーションサーバーを実行しているコンピューターの Windows システムパスに sqljdbc_auth.dll ファイルを追加します。sqljdbc_auth.dll ファイルは、Microsoft SQL JDBC 6.2.1.0 ドライバーのインストールフォルダー内にあります。
1. JBoss Windows サービス（JBoss for JEE 上の AEM Forms）のログオンプロパティを、ローカルシステムから、JEE 上の AEM Forms データベースと最低限の権限を持つログインアカウントに変更します。Windows サービスとしてではなく、コマンドラインから JBoss を実行している場合、この手順を行う必要はありません。
1. SQL Server のセキュリティを「**混合**」モードから「**Windows 認証のみ**」に変更します。

#### Windows 上での SQL サーバーの統合セキュリティの設定（WebLogic 版） {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. Web ブラウザーの URL 行に次の URL を入力して、WebLogic Server 管理コンソールを起動します。

   ```java
   https://[host name]:7001/console
   ```

1. Change Center で、「**Lock &amp; Edit**」をクリックします。
1. 「ドメイン構造」で、*[base_domain]*／**サービス**／**JDBC**／**データソース** をクリックし、右側のパネルで「**IDP_DS**」をクリックします。
1. 次の画面の「**設定**」タブで「**接続プール**」タブをクリックし、「**プロパティ**」ボックスに `integratedSecurity=true` と入力します。
1. 「ドメイン構造」で、**[base_domain]**／**サービス**／**JDBC**／**データソース** をクリックし、右側のパネルで「**RM_DS**」をクリックします。
1. 次の画面の「**設定**」タブで「**接続プール**」タブをクリックし、「**プロパティ**」ボックスに `integratedSecurity=true` と入力します。
1. アプリケーションサーバーを実行しているコンピューターの Windows システムパスに sqljdbc_auth.dll ファイルを追加します。sqljdbc_auth.dll ファイルは、Microsoft SQL JDBC 6.2.1.0 ドライバーのインストールフォルダー内にあります。
1. SQL Server のセキュリティを「**混合**」モードから「**Windows 認証のみ**」に変更します。

#### Windows 上での統合セキュリティの設定（WebSphere 版） {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

WebSphere では、統合セキュリティを設定できるのは外部の SQL Server JDBC ドライバーを使用している場合のみです。WebSphere の埋め込みの SQL Server JDBC ドライバーを使用している場合は設定できません。

1. WebSphere Administrative Console にログインします。
1. ナビゲーションツリーで、**リソース**／**JDBC**／**データソース** をクリックし、右側のパネルで「**IDP_DS**」をクリックします。
1. 右側のパネルの「追加のプロパティ」で「**カスタムプロパティ**」をクリックし、「**新規**」をクリックします。
1. 「**名前**」ボックスに `integratedSecurity` と入力し、「**値**」ボックスに `true` と入力します。
1. ナビゲーションツリーで、**リソース**／**JDBC**／**データソース** をクリックし、右側のパネルで「**RM_DS**」をクリックします。
1. 右側のパネルの「追加のプロパティ」で「**カスタムプロパティ**」をクリックし、「**新規**」をクリックします。
1. 「**名前**」ボックスに `integratedSecurity` と入力し、「**値**」ボックスに `true` と入力します。
1. WebSphere がインストールされているコンピューター上で、Windows システムパス（C:¥Windows）に sqljdbc_auth.dll ファイルを追加します。sqljdbc_auth.dll ファイルは、Microsoft SQL JDBC 1.2 ドライバーのインストール先ディレクトリ（デフォルトは *[InstallDir]*¥sqljdbc_1.2¥enu¥auth¥x86）と同じ場所にあります。
1. **スタート**／**コントロールパネル**／**サービス**&#x200B;を選択し、WebSphere の Windows サービス（IBM WebSphere Application Server &lt;version> - &lt;node>）を右クリックして、「**プロパティ**」を選択します。
1. プロパティダイアログボックスで、「**ログオン**」タブをクリックします。
1. 「**アカウント**」を選択し、必要な情報を入力して、使用するログインアカウントを設定します。
1. SQL Server のセキュリティを「**混合**」モードから「**Windows 認証のみ**」に変更します。

### データベース内の機密性の高い情報の保護 {#protecting-access-to-sensitive-content-in-the-database}

AEM Forms データベーススキーマには、システム設定やビジネスプロセスに関する機密性の高い情報が含まれているので、ファイアウォールの内側に隠しておく必要があります。データベースは、forms サーバーと同じ信頼境界内にあると見なされる必要があります。情報の意図しない開示やビジネスデータの盗難を防ぐために、データベース管理者（DBA）は、権限のある管理者のみにアクセスを制限するようにデータベースを設定する必要があります。

追加の予防策として、データベースベンダー固有のツールを使用して、次のデータを含むテーブルの列を暗号化することを考慮してください。

* Rights Management ドキュメントキー
* Trust Store HSM PIN 暗号化キー
* ローカルユーザーパスワードハッシュ

ベンダー固有のツールについて詳しくは、 [データベースのセキュリティ情報](https://helpx.adobe.com/jp/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information).

### LDAP のセキュリティ {#ldap-security}

LDAP（Lightweight Directory Access Protocol）ディレクトリは、通常、エンタープライズユーザーおよびグループ情報のソースとして、またパスワード認証実行の手段として JEE 上の AEM Forms で使用されます。LDAP ディレクトリが SSL（Secure Socket Layer）を使用するように設定されていること、および JEE 上の AEM Forms が SSL ポートを使用して LDAP ディレクトリにアクセスするように設定されていることを確認してください。

#### LDAP のサービス拒否 {#ldap-denial-of-service}

LDAP を使用した最もよく行われる攻撃は、攻撃者が大量の認証エラーを故意に引き起こすというものです。この攻撃を受けると、LDAP ディレクトリサーバーは、すべての LDAP 依存のサービスからユーザーをロックアウトしなければならなくなります。

試行できる認証エラーの回数と、それに伴うロックアウト時間の値を設定すると、AEM Forms への認証でユーザーが繰り返しエラーになったときに、AEM Forms がロックアウトを実行します。管理コンソールでは、小さい値を選択します。認証エラーの許容回数を選択するときは、許容回数に達した後に、LDAP ディレクトリサーバーより前に AEM Forms がユーザーをロックアウトすることを理解することが重要です。

#### 自動アカウントロックの設定 {#set-automatic-account-locking}

1. 管理コンソールにログインします。
1. **設定**／**ユーザー管理**／**ドメイン管理**&#x200B;をクリックします。
1. 「自動アカウントロックの設定」で、「**連続する認証エラーの最大回数**」を 3 などの小さい値に設定します。
1. 「**保存**」をクリックします。

### 監査とログ {#auditing-and-logging}

アプリケーションの監査およびログ機能を適切に保護した状態で使用することで、セキュリティを確保し、他の異常なイベントを追跡して、それらのイベントを可能な限り迅速に検出することができます。アプリケーション内における監査とログの効果的な使用には、成功したログインと失敗したログインの追跡、キーレコードの作成と削除などのキーアプリケーションイベントの追跡などが挙げられます。

監査を使用して、各種の攻撃を検出することができます。具体的には、以下のものがあります。

* ブルートフォースパスワードアタック
* サービス拒否攻撃
* 敵意のある入力値と関連するクラスのスクリプト挿入攻撃

次の表では、サーバーの脆弱性を減らすために使用できる監査およびログの方法について説明します。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>説明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>ログファイル ACL</p> </td> 
   <td><p>JEE 上の AEM Forms ログファイルには、適切なアクセス制御リスト（ACL）を設定します。</p> <p>適切な資格情報を設定することで、攻撃者によってファイルが削除されないように防御します。</p> <p>ログファイルディレクトリのセキュリティ権限として、Administrators グループおよび SYSTEM グループのフルコントロール権限が必要です。AEM Forms ユーザーアカウントには、読み取りおよび書き込み権限のみが必要です。</p> </td> 
  </tr> 
  <tr> 
   <td><p>ログファイルの冗長性</p> </td> 
   <td><p>リソースに余裕があれば、攻撃者がアクセスできないように、Syslog、Tivoli、Microsoft Operations Manager（MOM）やその他のメカニズムを使用して、ログを別のサーバーにリアルタイムで送信してください。</p> <p>この方法でログを保護することで、改ざんを防ぐことができます。さらに、中央リポジトリにログを保管することで、対比と監視に役立ちます（例えば、複数の forms サーバーを使用している場合に、パスワードの照会先となる複数のコンピューターに対してパスワード推測攻撃が行われた場合など）。</p> </td> 
  </tr> 
 </tbody> 
</table>

### 管理者以外のユーザに対して、PDF Generatorの実行を許可する

管理者以外のユーザに対して、PDF Generatorの使用を許可することができます。通常は、管理者権限を持つユーザーのみがPDF Generatoを実行できます。管理者以外のユーザに対してPDF Generatorの実行を許可するには、次の手順を実行します。

1. PDFG_NON_ADMIN_ENABLED という名前の環境変数を作成します。

1. 変数の値を TRUE に設定します。

1. AEM Forms のインスタンスを再起動します。

## 社外からのアクセスを可能にするための JEE 上の AEM Forms の設定 {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

JEE 上の AEM Forms のインストールが完了したら、定期的に環境のセキュリティの保守を行うことが重要です。ここでは、JEE 上の AEM Forms 実稼働サーバーのセキュリティを維持するための推奨タスクについて説明します。

### Web アクセスのリバースプロキシの設定 {#setting-up-a-reverse-proxy-for-web-access}

「*リバースプロキシ*」は、1 セットの JEE 上の AEM Forms Web アプリケーションの URL を、外部ユーザーと内部ユーザーの両方から利用できるように設定するものです。この設定は、JEE 上の AEM Forms を実行するアプリケーションサーバーへのユーザーの直接接続を許可する方法よりも、高いセキュリティで保護されます。リバースプロキシは、JEE 上の AEM Forms を実行しているアプリケーションサーバーに対するすべての HTTP 要求を実行します。ユーザーは、リバースプロキシに対するネットワークアクセスしか持たないので、リバースプロキシでサポートされている URL 接続のみを試みることができます。

**リバースプロキシサーバーで使用する JEE 上の AEM Forms ルート URL**

次のアプリケーションルート URL は、各 JEE 上の AEM Forms Web アプリケーションのものです。リバースプロキシは、エンドユーザーに提供する Web アプリケーション機能の URL だけを公開するように設定する必要があります。

一部の URL は、エンドユーザーが使用する Web アプリケーションを示しています。Configuration Manager のその他の URL は、リバースプロキシ経由の外部ユーザーのアクセスを許可しないので、公開しないでください。

<table> 
 <thead> 
  <tr> 
   <th><p>ルート URL</p> </th> 
   <th><p>用途および関連する Web アプリケーション</p> </th> 
   <th><p>Web ベースのインターフェイス</p> </th> 
   <th><p>エンドユーザーアクセス</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>PDF ドキュメントに使用権限を適用する Acrobat Reader DC Extensions エンドユーザー Web アプリケーション</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>Rights Management エンドユーザー Web アプリケーション</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>Rights Management の Web サービス URL</p> </td> 
   <td><p>いいえ</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>PDF Generator 管理 Web アプリケーション</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace/*</p> </td> 
   <td><p>Workspace エンドユーザー Web アプリケーション</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>Workspace クライアントアプリケーションが必要とする Workspace サーブレットおよび Data Services</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>JEE 上の AEM Forms をブートストラップするサーブレット</p> </td> 
   <td><p>いいえ</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>forms サーバー Web サービスの情報ページ</p> </td> 
   <td><p>いいえ</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>すべての forms サーバーサービス用の Web サービス URL</p> </td> 
   <td><p>いいえ</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>Rights Management 管理 Web アプリケーション</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adminui/*</p> </td> 
   <td><p>管理コンソールのホームページ</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/TruststoreComponent/</p> <p>secured/*</p> </td> 
   <td><p>Trust Store Management 管理ページ</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>フォームのレンダリングのテストとデバッグを行う Forms IVS アプリケーション</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>Output サービスのテストとデバッグを行う Output IVS アプリケーション</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rmws/*</p> </td> 
   <td><p>Rights Management のための REST URL</p> </td> 
   <td><p>いいえ</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputAdmin/*</p> </td> 
   <td><p>Output 管理ページ</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>Forms Web アプリケーションファイル</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>サーブレット</p> </td> 
   <td><p>HTML 変換時に、JavaScript の取得に使用</p> </td> 
   <td><p>いいえ</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>Forms 管理ページ</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/repository/*</p> </td> 
   <td><p>WebDAV（デバッグ）アクセス用の URL</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/AACComponent/*</p> </td> 
   <td><p>アプリケーションおよびサービスユーザーインターフェイス</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/WorkspaceAdmin/*</p> </td> 
   <td><p>Workspace 管理ページ</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rest/*</p> </td> 
   <td><p>残りのサポートページ</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>JEE 上の AEM Forms Core 設定ページ</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/</p> </td> 
   <td><p>User Management 認証</p> </td> 
   <td><p>いいえ</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/*</p> </td> 
   <td><p>User Management 管理インターフェイス</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/DoumentManager/*</p> </td> 
   <td><p>HTTP ドキュメント対応の SOAP トランスポートまたは EJB トランスポート経由でリモートエンドポイント、SOAP WSDL エンドポイントおよび Java SDK にアクセスするときに、処理するドキュメントをアップロードおよびダウンロードする。</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
 </tbody> 
</table>

## クロスサイト要求偽造攻撃からの保護 {#protecting-from-cross-site-request-forgery-attacks}

クロスサイト要求偽造（CSRF）攻撃とは、ユーザーに対する web サイトの信頼を悪用して、ユーザーが許可していないコマンドを知らないうちに送信することです。この攻撃は、web ページ上に配置したリンクまたはスクリプトや、電子メールメッセージに含めた URL を介して、既にユーザーの認証が済んでいる別のサイトへのアクセスを達成するという形で行われます。

例えば、管理者は、他の web サイトを閲覧しながら管理コンソールにログインすることがあります。CSRF 攻撃者は、このような状況を狙って、閲覧されるサイトの web ページに含まれている HTML img タグの `src` 属性などに、攻撃対象 web サイト内のサーバー側スクリプトを参照する URL を記述しておきます。Web ブラウザーに備わっている Cookie ベースのセッション認証メカニズムにより、攻撃者の web サイトは正当なユーザーを装って、攻撃対象のサーバー側スクリプトに悪意ある要求を送信することができます。その他の例については、 [https://owasp.org/www-community/attacks/csrf#Examples](https://owasp.org/www-community/attacks/csrf#Examples) を参照してください。

CSRF に共通の特性を次に示します。

* ユーザーの ID を信頼したサイトに関与する。
* その ID に対するサイトの信頼を利用する。
* ユーザーのブラウザーをだましてターゲットサイトに HTTP 要求を送信させる。
* 副次的な悪影響のある HTTP 要求に関与する。

JEE 上の AEM Forms では、リファラーフィルター機能を使用して CSRF 攻撃を防ぎます。ここでは、次の用語を使用してリファラーフィルターメカニズムについて説明します。

* **許可されているリファラー：**&#x200B;リファラーは、リクエストをサーバーに送信するソースページのアドレスです。JSP ページまたはフォームの場合、リファラーは一般的にブラウザー履歴の前のページになります。画像のリファラーは、通常、画像が表示されるページです。許可されているリファラーリストにリファラーを追加すると、サーバーリソースにアクセスできるリファラーを識別できます。
* **許可されているリファラーの例外：**&#x200B;許可されているリファラーリストの特定のリファラーに対して、アクセス範囲を制限することができます。この制限を適用するには、そのリファラーのパスを、許可されているリファラーの例外リストに個別に追加します。許可されているリファラーの例外リストに含まれるパスから要求が発行された場合、AEM Forms サーバー上のリソースは呼び出されません。許可されているリファラーの例外リストは、特定のアプリケーションに対して定義できます。また、すべてのアプリケーションに適用される例外のグローバルリストを使用することもできます。
* **許可されている URI：**&#x200B;リファラーヘッダーを確認ぜずに提供されるリソースのリストです。例えば、サーバーの状態に変更を加えることのない、リソースのヘルプページをこのリストに追加できます。許可されている URI リストのリソースは、リファラーが何であっても、リファラーフィルターでブロックされることはありません。
* **ヌルリファラー：**&#x200B;関連付けられていない、または送信元が親 web ページではないサーバーリクエストは、ヌルリファラーからのリクエストと見なされます。例えば、新しいブラウザーウィンドウを開き、アドレスを入力して、Enter キーを押すと、サーバーには Null リファラーが送信されます。Web サーバーに HTTP リクエストを送信するデスクトップアプリケーション（.NET または SWING）も、Null リファラーをサーバーに送信します。

### リファラーフィルタリング {#referer-filtering}

ここでは、リファラーのフィルタリングプロセスについて説明します。

1. Forms サーバーが、呼び出しに使用される HTTP メソッドを確認します。

   1. POST の場合、Forms サーバーはリファラーのヘッダーのチェックを実行します。
   1. GET の場合、Forms サーバーはリファラーをチェックしません。ただし、*CSRF_CHECK_GETS*&#x200B;が true に設定されている場合は除きます。この場合、Forms サーバーはリファラーヘッダーを確認します。*CSRF_CHECK_GETS* は、アプリケーションの *web.xml* ファイル内に設定されます。

1. Forms サーバーが、リクエストされた URI が許可リストに存在するかどうかを確認します。

   1. URI が許可リストに登録されている場合、サーバーはリクエストを受け入れます。
   1. リクエストされた URI が許可リストに登録されていなかった場合、サーバーはリクエストのリファラーを取得します。

1. リクエスト内にリファラーがある場合、サーバーはそれが許可されているリファラーかどうかを確認します。許可されている場合は、リファラーの例外を確認します。

   1. 例外の場合、リクエストはブロックされます。
   1. 例外でない場合、要求はパスします。

1. リクエスト内にリファラーが指定されていない場合、サーバーは Null リファラーが許可されているかどうかを確認します。

   1. Null リファラーが許可されている場合は、リクエストが渡されます。
   1. Null リファラーが許可されていない場合、サーバーは要求された URI が Null リファラーの例外に相当するかどうかを確認し、適宜リクエストを処理します。

### リファラーフィルタリングの管理 {#managing-referer-filtering}

JEE 上の AEM Forms には、ご使用のサーバーのリソースへのアクセスを許可するリファラーを指定するためのリファラーフィルターが用意されています。デフォルトの場合、リファラーフィルターでは安全な HTTP メソッド（GET など）を使用したリクエストはフィルタリングされません。ただし、*CSRF_CHECK_GETS* が true にセットされている場合は除きます。許可されているリファラーのエントリにあるポート番号が 0 に設定されている場合、JEE 上の AEM Forms では、ポート番号とは関係なく、ホストからのリクエストがすべてリファラーと共に許可されます。ポート番号が指定されていない場合は、デフォルトのポート 80（HTTP）またはポート 443（HTTPS）からのリクエストのみが許可されます。許可されているリファラーリストのすべてのエントリが削除されると、リファラーフィルタリングは無効になります。

Document Services を最初にインストールすると、許可されているリファラーリストは、Document Services がインストールされたサーバーのアドレスで更新されます。サーバーのエントリには、サーバー名、IPv4 アドレス、IPv6 アドレス（IPv6 が有効の場合）、ループバックアドレス、localhost エントリなどがあります。許可されているリファラーのリストに追加された名前は、ホストのオペレーティングシステムから返されます。例えば、IP アドレスが 10.40.54.187 のサーバーには、次のエントリが含まれます。`https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`ホストのオペレーティングシステムから返された正規でない名前（IPv4 アドレス、IPv6 アドレスのない名前、または完全修飾のないドメイン名）については、許可リストは更新されません。許可されているリファラーリストを、ビジネス環境に合わせて変更します。実稼働環境に Forms サーバーをデプロイするとき、許可されているリファラーリストの内容がデフォルトのままになっていないことを確認してください。許可されているリファラー、リファラーの例外または URI を変更したら、必ずサーバーを再起動して、その変更を有効にします。

**許可されているリファラーリストの管理**

許可されているリファラーリストは、管理コンソールの User Management インターフェイスから管理できます。User Management インターフェイスを使用すると、リストを作成、編集または削除できます。許可されているリファラーのリストの操作について詳しくは、*管理ヘルプ*&#x200B;の[CSRF 攻撃の防止](/help/forms/using/admin-help/preventing-csrf-attacks.md)を参照してください。

**許可されているリファラーの例外および許可されている URI のリストの管理**

JEE 上の AEM Forms には、許可されているリファラーの例外と許可されている URI の各リストを管理するための API が用意されています。この API を使用すると、リストを取得、作成、編集または削除できます。使用可能な API のリストを次に示します。

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

API について詳しくは、*AEM Forms on JEE の API リファレンス* を参照してください。

許可されているリファラーの例外の&#x200B;***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION***&#x200B;リストは、グローバルレベルで使用します。つまり、すべてのアプリケーションに適用できる例外を定義します。このリストには、絶対パス（例：`/index.html`）または相対パス（例：`/sample/`）のいずれかの URI のみが記載されます。また、相対 URI の末尾に正規表現を追加することもできます（例：`/sample/(.)*`）。

***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** リストの ID は、`com.adobe.idp.um.api` 名前空間の `UMConstants` クラスで定数として定義されており、`adobe-usermanager-client.jar` にあります。この AEM Forms API を使用すると、リストを取得、作成、編集または削除できます。例えば、グローバルで許可されているリファラーの例外のリストを作成するには、次を使用します。

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

アプリケーション固有の例外については、***CSRF_ALLOWED_REFERER_EXCEPTIONS***&#x200B;リストを使用します。

**リファラーフィルターの無効化**

リファラーフィルターによって Forms サーバーへのアクセスが完全にブロックされ、許可されているリファラーリストを編集できない場合は、サーバー起動スクリプトを更新して、リファラーフィルタリングを無効にできます。

それには、起動スクリプトに`-Dlc.um.csrffilter.disabled=true`JAVA 引数を追加してから、サーバーを再起動してください。許可されているリファラーリストを適切に再設定したら、JAVA 引数は必ず削除してください。

**カスタム WAR ファイルのリファラーフィルタリング**

管理者は、ビジネス要件に合わせて JEE 上の AEM Forms を操作するためのカスタム WAR ファイルを用意している場合があります。カスタム WAR ファイルに対してリファラーフィルタリングを有効にするには、***adobe-usermanager-client.jar***&#x200B;を WAR のクラスパスに追加し、次のパラメーターを含むフィルターエントリを* web.xml* ファイルに追加してください。

**CSRF_CHECK_GETS** は、GET 要求でリファラーチェックを制御します。このパラメーターが定義されていない場合、デフォルト値は false に設定されます。このパラメーターは、GET 要求をフィルタリングする場合にのみ指定します。

**CSRF_ALLOWED_REFERER_EXCEPTIONS** は、許可されているリファラーの例外リストの ID です。このリファラーフィルターを使用すると、リスト ID で特定されたリスト内のリファラーからのリクエストでは、Forms サーバーのリソースを呼び出すことはできません。

**CSRF_ALLOWED_URIS_LIST_NAME** は、許可されている URI リストの ID です。リファラーフィルターは、リクエストのリファラーヘッダーの値に関係なく、リスト ID で特定されたリストのリソースに対するリクエストをブロックしません。

**CSRF_ALLOW_NULL_REFERER**&#x200B;は、リファラーが Null の場合または存在しない場合のリファラーフィルターの動作を制御します。このパラメーターが定義されていない場合、デフォルト値は false に設定されます。このパラメーターは、Null リファラーを許可する場合にのみ指定します。Null リファラーを許可すると、ある種のクロスサイト要求偽造攻撃を許可してしまう可能性があります。

**CSRF_NULL_REFERER_EXCEPTIONS** は、リファラーが Null の場合にリファラーチェックが行われない URI のリストです。このパラメーターは、*CSRF_ALLOW_NULL_REFERER* が false に設定されている場合にのみ有効です。リスト内で複数の URI を指定するときはコンマで区切ります。

*サンプル* WAR ファイルに対する ***web.xml*** ファイルのフィルターエントリの例を次に示します。

```java
<filter> 
       <filter-name> filter-name </filter-name> 
       <filter-class> com.adobe.idp.um.auth.filter.RemoteCSRFFilter </filter-class> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_ALLOW_NULL_REFERER </param-name> 
      <param-value> false </param-value> 
     </init-param> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_CHECK_GETS </param-name> 
      <param-value> true </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
       <param-name> CSRF_NULL_REFERER_EXCEPTIONS </param-name> 
       <param-value> /SAMPLE/login, /SAMPLE/logout  </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_REFERER_EXCEPTIONS </param-name> 
      <param-value> SAMPLE_ALLOWED_REF_EXP_ID </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_URIS_LIST_NAME </param-name> 
      <param-value> SAMPLE_ALLOWED_URI_LIST_ID     </param-value> 
     </init-param> 
</filter> 
    ........ 
    <filter-mapping> 
      <filter-name> filter-name </filter-name> 
      <url-pattern>/*</url-pattern> 
    </filter-mapping>
```

**トラブルシューティング**

適切なサーバー要求が CSRF フィルターによってブロックされる場合は、次のいずれかを試してみてください。

* 拒否されたリクエストにリファラーヘッダーがある場合は、許可されているリファラーリストにそのリファラーを追加することを慎重に検討します。信頼できるリファラーのみを追加します。
* 拒否されたリクエストにリファラーヘッダーがない場合は、リファラーヘッダーを含めるようにクライアントアプリケーションを変更します。
* クライアントがブラウザーで動作できる場合は、そのデプロイメントモデルを試してみます。
* 最後の手段として、許可されている URI リストにリソースを追加できます。ただし、これは推奨設定ではありません。

## ネットワーク設定の保護 {#secure-network-configuration}

ここでは、JEE 上の AEM Forms が必要とするプロトコルとポートについて説明し、保護されたネットワーク設定で JEE 上の AEM Forms をデプロイするための推奨事項を示します。

### JEE 上の AEM Forms で使用されるネットワークプロトコル {#network-protocols-used-by-aem-forms-on-jee}

前の節で説明したように、保護されたネットワークアーキテクチャを設定する場合、エンタープライズネットワーク内の JEE 上の AEM Forms と他のシステムのやり取りのために次のネットワークプロトコルが必要です。

<table> 
 <thead> 
  <tr> 
   <th><p>プロトコル</p> </th> 
   <th><p>使用方法</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>HTTP</p> </td> 
   <td> 
    <ul> 
     <li><p>Configuration Manager およびエンドユーザー Web アプリケーションをブラウザーに表示する</p> </li> 
     <li><p>すべての SOAP 接続</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>.NET アプリケーションなどの Web サービスクライアントアプリケーション</p> </li> 
     <li><p>Adobe Reader® は JEE 上の AEM Forms サーバー Web サービスとのやり取りに SOAP を使用する</p> </li> 
     <li><p>Adobe Flash® アプリケーションは Forms サーバー Web サービスとのやり取りに SOAP を使用する</p> </li> 
     <li><p>SOAP モードで使用された場合に JEE 上の AEM Forms SDK によって呼び出される</p> </li> 
     <li><p>Workbench 設計環境</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>Enterprise JavaBeans（EJB）モードで使用された場合に JEE 上の AEM Forms SDK によって呼び出される</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP/POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>サービスに対する電子メールベースの入力（電子メールエンドポイント）</p> </li> 
     <li><p>電子メールを使用したユーザータスク通知</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>UNC ファイル IO</p> </td> 
   <td><p>サービスに対する入力用の監視フォルダーを JEE 上の AEM Forms で監視する（監視フォルダーエンドポイント）</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>ディレクトリ内の組織ユーザーとグループ情報を同期する</p> </li> 
     <li><p>対話的にやり取りするユーザーに LDAP 認証を行う</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>JDBC サービスを使用したプロセスの実行時に、外部データベースに対するクエリーとプロシージャの呼び出しを行う</p> </li> 
     <li><p>JEE 上の AEM Forms リポジトリへの内部からのアクセス</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>任意の WebDAV クライアントによる JEE 上の AEM Forms デザイン時リポジトリ（フォーム、フラグメントなど）のリモート参照を有効にする</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>JEE 上の AEM Forms サーバーサービスがリモートエンドポイントとして設定されている Adobe Flash アプリケーション</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>JEE 上の AEM Forms は監視対象の MBeans を JMX を使用して公開する</p> </td> 
  </tr> 
 </tbody> 
</table>

### アプリケーションサーバーのポート {#ports-for-application-servers}

ここでは、サポートしている各種のアプリケーションサーバーのデフォルトポート（および代替設定の範囲）について説明します。これらのポートについては、JEE 上の AEM Forms を実行しているアプリケーションサーバーに接続するクライアントに対して許可するネットワーク機能に応じて、内側のファイアウォール上で有効と無効を切り替える必要があります。

>[!NOTE]
>
>デフォルトでは、サーバーは、adobe.com 名前空間内に複数の JMX MBeans を公開します。サーバーの正常性監視に有用な情報だけが公開されます。ただし、情報開示を防ぐには、信頼できないネットワーク内の呼び出し元によって JMX MBeans の参照と正常性評価基準へのアクセスが行われないようにする必要があります。

**JBoss ポート**

<table> 
 <thead> 
  <tr> 
   <th><p>目的</p> </th> 
   <th><p>ポート</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Web アプリケーションへのアクセス</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>HTTP/1.1 コネクタポート 8080</p> <p>AJP 1.3 コネクタポート 8009</p> <p>SSL/TLS コネクタポート 8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>CORBA サポート</p> </td> 
   <td><p>[JBossroot]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**WebLogic ポート**

<table> 
 <thead> 
  <tr> 
   <th><p>用途</p> </th> 
   <th><p>ポート</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Web アプリケーションへのアクセス</p> </td> 
   <td> 
    <ul> 
     <li><p>管理サーバーリスンポート：デフォルトは 7001</p> </li> 
     <li><p>管理サーバー SSL リスンポート：デフォルトは 7002</p> </li> 
     <li><p>管理対象サーバー用に設定されたポート：8001 など</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JEE 上の AEM Forms へのアクセスに必要とされない WebLogic 管理ポート</p> </td> 
   <td> 
    <ul> 
     <li><p>管理対象サーバーリスンポート：1 ～ 65534 の範囲で設定可能</p> </li> 
     <li><p>管理対象サーバー SSL リスンポート：1 ～ 65534 の範囲で設定可能</p> </li> 
     <li><p>ノードマネージャーリスンポート：デフォルトは 5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**WebSphere ポート**

JEE 上の AEM Forms で必要な WebSphere ポートについて詳しくは、「WebSphere Application Server UI のポート番号設定」を参照してください。

### SSL の設定 {#configuring-ssl}

[JEE 上の AEM Forms の物理アーキテクチャ](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture)で取り上げている物理アーキテクチャについては、使用するすべての接続に SSL を設定する必要があります。特に すべての SOAP 接続は、ネットワーク上にユーザー資格情報が漏洩されないように、すべて SSL 経由で行う必要があります。

JBoss、WebLogic、WebSphere で SSL を設定する手順については、 [管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_64_jp).

AEM Forms サーバー用に設定された JVM（Java 仮想マシン）に証明書を読み込む手順については、[AEM Forms Workbench ヘルプ](http://www.adobe.com/go/learn_aemforms_workbench_65_jp)の「相互認証」の節を参照してください。 

### SSL リダイレクトの設定 {#configuring-ssl-redirect}

SSL をサポートするようにアプリケーションサーバーを設定した後、 アプリケーションおよびサービスに対するすべての HTTP トラフィックは、SSL ポートを使用するように強制されます。

WebSphere または WebLogic で SSL リダイレクトを設定するには、使用しているアプリケーションサーバーのドキュメントを参照してください。

1. コマンドプロンプトを開き、/JBOSS_HOME/standalone/configuration ディレクトリに移動して、次のコマンドを実行してください。

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. JBOSS_HOME/standalone/configuration/standalone.xml ファイルを編集用に開きます。

   &lt;subsystem xmlns=&quot;urn:jboss:domain:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;> 要素の後に、次の詳細を追加します。

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. https コネクタ要素に次のコードを追加します。

   ```xml
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   standalone.xml ファイルを保存して閉じます。

## Windows 固有のセキュリティに関する推奨事項 {#windows-specific-security-recommendations}

ここでは、JEE 上の AEM Forms の実行に使用する場合の Windows 固有のセキュリティ推奨事項について説明します。

### JBoss サービスアカウント {#jboss-service-accounts}

JEE 上の AEM Forms 自動インストールは、デフォルトで、ローカルシステムアカウントを使用してサービスアカウントを設定します。組み込みのローカルシステムユーザーアカウントは、高いレベルのアクセス権限を付与されており、Administrators グループに属しています。ワーカープロセス ID をローカルシステムユーザーアカウントで実行した場合、ワーカープロセスはシステム全体に対してフルアクセス権限を持ちます。

#### 管理者以外のアカウントでのアプリケーションサーバーの実行 {#run-the-application-server-using-a-non-administrative-account}

1. Microsoft 管理コンソール（MMC）で、forms サーバーサービスへのログインに使用するローカルユーザーを作成します。

   * 「**ユーザーはパスワードを変更できない**」オプションを選択します。
   * **所属するグループ**&#x200B;タブに、「ユーザー」グループが表示されていることを確認してください。

1. **設定**／**管理ツール**／**サービス**&#x200B;を選択します。
1. アプリケーションサーバーサービスをダブルクリックし、サービスを停止します。
1. 「**ログオン**」タブで、「**アカウント**」を選択し、作成したユーザーアカウントを参照して、アカウントのパスワードを入力します。
1. ローカルセキュリティ設定ウィンドウの「ユーザー権利の割り当て」で、forms サーバーを実行しているユーザーアカウントに次の権限を付与します。

   * ターミナルサービスを使ったログオンを拒否する
   * locallyxx でのログオンを拒否する
   * サービスとしてログオン（通常は既に設定済み）

1. 次のディレクトリの新しいユーザーアカウントに変更権限を付与します。
   * **グローバルドキュメントストレージ (GDS) ディレクトリ**：GDS ディレクトリの場所は、AEM Forms のインストールプロセス中に手動で設定します。インストール時に場所を指定しないと、`[JBoss root]/server/[type]/svcnative/DocumentStorage` にあるアプリケーションサーバーのインストールディレクトリの下にあるディレクトリがデフォルトの場所になります。
   * **CRX リポジトリディレクトリ**：デフォルトの場所は `[AEM-Forms-installation-location]\crx-repository` です。
   * **AEM Forms 一時ディレクトリ**：
      * （Windows）環境変数で設定されている TMP または TEMP パス
      * （AIX、Linux または Solaris）ログインユーザーのホームディレクトリ
UNIX 系のシステムでは、root 以外のユーザーは次のディレクトリを一時ディレクトリとして使用できます。
      * （Linux）/var/tmp or /usr/tmp
      * （AIX）/tmp or /usr/tmp
      * （Solaris）/var/tmp または /usr/tmp
1. 新しいユーザーアカウントに、次のディレクトリへの書き込み権限を付与します。
   * [JBoss ディレクトリ]\standalone\deployment
   * [JBoss ディレクトリ]\standalone\
   * [JBoss ディレクトリ]\bin\

   >[!NOTE]
   >
   >JBoss Application サーバーのデフォルトのインストール場所：
   >
   >* Windows：C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux：/opt/jboss/。


1. アプリケーションサーバーサービスを起動します。

### ファイルシステムのセキュリティ {#file-system-security}

JEE 上の AEM Forms は、次の方法でファイルシステムを利用します。

* ドキュメントの入力と出力を処理する際に使用する一時ファイルを格納する
* インストールしたソリューションコンポーネントのサポートに使用されるファイルをグローバルアーカイブストアに格納する
* ファイルシステムフォルダーからサービスへの入力として使用されるドロップファイルを監視フォルダーに格納する

forms サーバーサービスのドキュメントを送受信する方法として監視フォルダーを使用する場合、ファイルシステムのセキュリティを確保するために一層の予防策を講じる必要があります。ユーザーが監視フォルダーにコンテンツをドロップした場合、コンテンツは監視フォルダーを通じて公開されます。この場合、サービスは実際のエンドユーザーを認証していません。代わりに、フォルダーレベルに設定されている ACL と共有レベルセキュリティに応じて、サービスを呼び出して実行することのできるユーザーを決定しています。

## JBoss 固有のセキュリティに関する推奨事項 {#jboss-specific-security-recommendations}

ここでは、JEE 上の AEM Forms を実行する際に使用される JBoss 7.0.6 に特有のアプリケーションサーバー設定の推奨事項について説明します。

### JBoss 管理コンソールおよび JMX コンソールの無効化 {#disable-jboss-management-console-and-jmx-console}

JBoss 管理コンソールと JMX コンソールへのアクセスは、自動インストールオプションを使用して JBoss に JEE 上の AEM Forms をインストールしたときに設定されます。独自の JBoss Application Server を使用している場合は、JBoss 管理コンソールおよび JMX 監視コンソールへのアクセスが保護されていることを確認してください。JMX 監視コンソールへのアクセスは、jmx-invoker-service.xml という JBoss 設定ファイルで設定されています。

### ディレクトリ参照の無効化 {#disable-directory-browsing}

管理コンソールにログインした後に、URL を変更することにより、コンソールのディレクトリ一覧を参照することができます。例えば、URL を次のいずれかの URL に変更すると、ディレクトリ一覧が表示される場合があります。

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## WebLogic 固有のセキュリティに関する推奨事項 {#weblogic-specific-security-recommendations}

ここでは、JEE 上の AEM Forms の実行時に WebLogic 9.1 を保護するためのアプリケーションサーバー設定の推奨事項について説明します。

### ディレクトリ参照の無効化 {#disable_directory_browsing-1}

weblogic.xml ファイルの index-directories プロパティを `false` に設定します。次に例を示します。

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### WebLogic SSL ポートの有効化 {#enable-weblogic-ssl-port}

デフォルトでは、WebLogic はデフォルト SSL リスンポート 7002 を有効にしません。SSL を設定する前に、WebLogic Server 管理コンソールでこのポートを有効にしてください。

## WebSphere 固有のセキュリティに関する推奨事項 {#websphere-specific-security-recommendations}

ここでは、JEE 上の AEM Forms の実行時に WebSphere を保護するためのアプリケーションサーバー設定の推奨事項について説明します。

### ディレクトリ参照の無効化 {#disable_directory_browsing-2}

ibm-web-ext.xml ファイルの `directoryBrowsingEnabled` プロパティを `false` に設定します。

### WebSphere 管理セキュリティの有効化 {#enable-websphere-administrative-security}

1. WebSphere Administrative Console にログインします。
1. ナビゲーションツリーで、**セキュリティ**／**Global Security** に移動します。
1. 「**Enable administrative security**」を選択します。
1. 「**Enable application security**」および「**Use Java 2 security**」の選択を解除します。
1. 「**OK**」または「**Apply**」をクリックします。
1. 「**Messages**」ボックスで、「**Save directly to the master configuration**」をクリックします。
