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
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '7665'
ht-degree: 41%

---

# JEE 上の AEM Forms 環境の堅牢化 {#hardening-your-aem-forms-on-jee-environment}

企業のイントラネット内で動作する JEE 上の AEM Forms のセキュリティを強化するための、様々なセキュリティ強化設定について学びます。

この記事では、JEE 上でAEM Formsを実行するサーバーを保護するための推奨事項とベストプラクティスについて説明します。 これは、オペレーティングシステムとアプリケーションサーバーに関する包括的なホスト堅牢化ドキュメントではありません。 企業のイントラネット内で運用している JEE 上の AEM Forms のセキュリティを強化するために行うことが望ましい、様々なセキュリティ堅牢化設定について説明します。ただし、JEE 上のAEM Formsアプリケーションサーバーのセキュリティを確保するには、セキュリティの監視、検出、および応答の手順も実装する必要があります。

この記事では、インストールおよび設定のライフサイクルの次の段階で適用する必要がある堅牢化方法について説明します。

* **プリインストール：** JEE にAEM Formsをインストールする前に、次の方法を使用します。
* **インストール時：**&#x200B;この手法は、JEE 上の AEM Forms ソフトウェアをインストールする作業の一環として実行します。
* **インストール後：** これらの手法は、インストール後、定期的に使用します。

JEE 上のAEM Formsは高度にカスタマイズ可能で、様々な環境で動作します。 レコメンデーションの一部は、組織のニーズに合わない可能性があります。

## プレインストール {#preinstallation}

JEE 上のAEM Formsをインストールする前に、ネットワークレイヤーとオペレーティングシステムにセキュリティソリューションを適用できます。 この節では、いくつかの問題と、これらの領域のセキュリティの脆弱性を減らすための推奨事項を説明します。

**UNIX および Linux でのインストールと設定**

JEE 上のAEM Formsをルートシェルを使用してインストールまたは設定しないでください。 デフォルトでは、ファイルは/opt ディレクトリにインストールされ、インストールを実行するユーザーは/opt の下のすべてのファイル権限が必要です。 または、すべてのファイル権限を持つ個々のユーザーの/user ディレクトリで、インストールを実行することもできます。

**Windows でのインストールと設定**

自動オプションを使用して JBoss に JEE 上のAEM Formsをインストールする場合、またはPDFジェネレーターをインストールする場合は、Windows でのインストールを管理者として実行する必要があります。 また、ネイティブPDFをサポートする Windows に Application Generator をインストールする場合は、Microsoft Office をインストールしたのと同じ Windows ユーザーとしてインストールを実行する必要があります。 インストールの権限について詳しくは、お使いのアプリケーションサーバーに対応した* JEE 上の AEM Forms のインストールおよびデプロイ* ドキュメントを参照してください。

### ネットワーク層のセキュリティ {#network-layer-security}

ネットワークセキュリティの脆弱性は、インターネットやイントラネットに接続するアプリケーションサーバーにとって、最初の脅威の 1 つです。 この節では、これらの脆弱性に対してネットワーク上のホストを強化するプロセスについて説明します。 これは、ネットワークのセグメント化、TCP/IP(Transmission Control Protocol/Internet Protocol) スタックの堅牢化、およびホスト保護のためのファイアウォールの使用に対応しています。

次の表に、ネットワークセキュリティの脆弱性を減らす一般的なプロセスを示します。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>説明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>非武装地帯 (DMZ)</p> </td> 
   <td><p>forms サーバーを非武装地帯 (DMZ) にデプロイします。 内側のファイアウォールの後ろに配置された、JEE 上のAEM Formsを実行するアプリケーションサーバーに対して、少なくとも 2 つのレベルでセグメント化が存在する必要があります。 Web サーバーを含む DMZ から外部ネットワークを分離します。その後、外部ネットワークを内部ネットワークから分離する必要があります。 ファイアウォールを使用して、分離の層を実装します。 各ネットワーク層を通過するトラフィックを分類および制御して、必要最小限のデータのみが許可されるようにします。</p> </td> 
  </tr> 
  <tr> 
   <td><p>プライベート IP アドレス</p> </td> 
   <td><p>AEM Forms アプリケーションサーバーで、RFC 1918 プライベート IP アドレスと NAT（ネットワークアドレス変換）を使用します。プライベート IP アドレス（10.0.0.0/8、172.16.0.0/12 および 192.168.0.0/16）を割り当てることにより、インターネットを通じて、NAT を使用する内部ホストに対して攻撃者がトラフィックをルーティングできないようにします。</p> </td> 
  </tr> 
  <tr> 
   <td><p>ファイアウォール</p> </td> 
   <td><p>次の条件を使用して、ファイアウォールソリューションを選択します。</p> 
    <ul> 
     <li><p>単純なパケットフィルタリングソリューションではなく、プロキシサーバーまたは「<em>ステートフルインスペクション</em>」をサポートするファイアウォールを実装する。</p> </li> 
     <li><p><em>明示的に許可されたサービス以外はすべて拒否する</em>セキュリティパラダイムをサポートするファイアウォールを使用する。</p> </li> 
     <li><p>デュアルホームまたはマルチホームのファイアウォールソリューションを実装します。 このアーキテクチャは、最高レベルのセキュリティを提供し、不正なユーザーがファイアウォールセキュリティをバイパスするのを防ぐのに役立ちます。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>データベースポート</p> </td> 
   <td><p>データベースにデフォルトのリスニングポート (MySQL - 3306、Oracle- 1521、MS SQL - 1433) を使用しないでください。 データベースポートの変更については、データベースのドキュメントを参照してください。</p> <p>異なるデータベースポートを使用すると、JEE 上のAEM Formsの設定全体に影響します。 デフォルトポートを変更する場合は、JEE 上のAEM Formsのデータソースなど、設定の他の領域で、対応する変更を行う必要があります。</p> <p>JEE 上の AEM Forms におけるデータソースの設定について詳しくは、<a href="/help/forms/using/introduction-aem-forms.md" target="_blank">AEM Forms ユーザーガイド</a>の「JEE 上の AEM Forms のインストールおよびアップグレード」または「アプリケーションサーバー用 JEE 上の AEM Forms へのアップグレード」を参照してください。</p> </td> 
  </tr> 
 </tbody> 
</table>

### オペレーティングシステムのセキュリティ {#operating-system-security}

次の表に、オペレーティングシステムで見つかるセキュリティの脆弱性を最小限に抑えるための潜在的なアプローチを示します。

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
   <td><p>ベンダーのセキュリティパッチとアップグレードが適時に適用されない場合、権限のないユーザーがアプリケーションサーバーにアクセスするリスクが高まります。 セキュリティパッチを本番サーバに適用する前に、テストを実施してください。</p><p>また、定期的にパッチをチェックしてインストールするポリシーと手順を作成します。</p></td> 
  </tr> 
  <tr> 
   <td><p>ウイルス対策ソフトウェア</p></td> 
   <td><p>ウイルススキャナは、署名をスキャンするか、異常な動作を監視することで、感染したファイルを識別できます。 スキャナーは、ウイルスの署名をファイルに保存します。このファイルは通常、ローカルのハードドライブに保存されます。 新しいウイルスは頻繁に発見されるので、ウイルススキャナーで最新のウイルスをすべて識別するには、このファイルを頻繁に更新する必要があります。</p></td> 
  </tr> 
  <tr> 
   <td><p>ネットワークタイムプロトコル (NTP)</p></td> 
   <td><p>フォレンジック分析の場合は、Forms サーバーの時間を正確に保ちます。 NTP を使用して、インターネットに直接接続されているすべてのシステムの時刻を同期します。</p></td> 
  </tr> 
 </tbody> 
</table>

オペレーティングシステムのその他のセキュリティ情報については、[オペレーティングシステムのセキュリティ情報](https://helpx.adobe.com/jp/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information)を参照してください。

## インストール {#installation}

この節では、AEM Formsのインストールプロセスでセキュリティの脆弱性を減らすために使用できる方法について説明します。 これらのテクニックでは、インストールプロセスの一部であるオプションを使用する場合があります。 次の表に、これらの方法を示します。

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
   <td><p>ソフトウェアのインストールには、必要最小限の権限を使用してください。Administrators グループに属さないアカウントを使用して、コンピュータにログインします。 Windows では、「実行名」コマンドを使用して、管理ユーザーとして JEE 上のAEM Formsインストーラーを実行できます。 UNIX および Linux システムでは、<code>sudo</code> などのコマンドを使用してソフトウェアをインストールします。 </p> </td> 
  </tr> 
  <tr> 
   <td><p>ソフトウェアソース</p> </td> 
   <td><p>信頼できないソースから JEE 上のAEM Formsをダウンロードまたは実行しないでください。</p> <p>悪意のあるプログラムには、データの盗難、変更と削除、サービス拒否など、セキュリティに違反するコードが含まれている場合があります。 JEE 上のAEM FormsをAdobeDVD から、または信頼できるソースからのみインストールします。</p> </td> 
  </tr> 
  <tr> 
   <td><p>ディスクパーティション</p> </td> 
   <td><p>JEE 上のAEM Formsを専用のディスクパーティションに配置します。 ディスクのセグメント化とは、セキュリティを強化するために、サーバ上の特定のデータを別の物理ディスクに保持するプロセスです。 この方法でデータを整理すると、ディレクトリトラバーサル攻撃のリスクが軽減されます。 JEE 上のAEM Formsコンテンツディレクトリをインストールできるシステムパーティションとは別のパーティションを作成することを計画します。 （Windows の場合、システムパーティションには system32 ディレクトリ、またはブートパーティションが含まれます）。</p> </td> 
  </tr> 
  <tr> 
   <td><p>コンポーネント</p> </td> 
   <td><p>既存のサービスを評価し、不要なサービスを無効にするかアンインストールします。 不要なコンポーネントやサービスをインストールしないでください。</p> <p>アプリケーションサーバーのデフォルトのインストールには、使用に不要なサービスが含まれている場合があります。 攻撃のエントリポイントを最小限に抑えるには、デプロイメント前に不要なサービスをすべて無効にする必要があります。 例えば、JBoss では、META-INF/jboss-service.xml記述子ファイル内の不要なサービスをコメントアウトできます。</p> </td> 
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

JEE 上のAEM Formsを正常にインストールした後は、セキュリティの観点から、定期的に環境を保守することが重要です。

次の節では、デプロイ済みの forms サーバーを保護するために推奨される様々なタスクについて詳しく説明します。

### AEM Formsセキュリティ {#aem-forms-security}

次の推奨設定は、管理 Web アプリケーションの外部にある JEE 上のAEM Formsサーバーに適用されます。 サーバーのセキュリティリスクを軽減するには、JEE 上のAEM Formsをインストールした直後にこれらの設定を適用します。

**セキュリティパッチ**

ベンダーのセキュリティパッチとアップグレードが適時に適用されない場合、権限のないユーザーがアプリケーションサーバーにアクセスするリスクが高まります。 セキュリティパッチを本番サーバに適用する前にテストし、アプリケーションの互換性と可用性を確保します。 また、定期的にパッチをチェックしてインストールするポリシーと手順を作成します。 JEE 上のAEM Formsのアップデートは、Enterprise 製品のダウンロードサイトにあります。

**サービスアカウント（Windows での JBoss 自動インストールのみ）**

JEE 上のAEM Formsは、デフォルトでは、LocalSystem アカウントを使用してサービスをインストールします。 組み込みの LocalSystem ユーザーアカウントは、高いレベルのアクセシビリティを持っています。これは管理者グループに属しています。 ワーカープロセス ID が LocalSystem ユーザーアカウントとして実行される場合、そのワーカープロセスはシステム全体に対するフルアクセス権を持ちます。

JEE 上のAEM Formsがデプロイされているアプリケーションサーバーを、特定の管理者以外のアカウントを使用して実行するには、次の手順に従います。

1. Microsoft管理コンソール (MMC) で、forms サーバーサービスのローカルユーザーを作成し、次のようにログインします。

   * 選択 **ユーザーはパスワードを変更できません**.
   * **所属するグループ**&#x200B;タブに、「ユーザー」グループが表示されていることを確認してください&#x200B;**。**

   >[!NOTE]
   >
   >この設定は、Generator に対して変更できません。PDF・ジェネレータ

1. 選択 **開始** > **設定** > **管理ツール** > **サービス**.
1. JEE 上のAEM Forms用の JBoss をダブルクリックして、サービスを停止します。
1. の **ログオン** タブ、選択 **このアカウント**&#x200B;作成したユーザーアカウントを参照し、そのアカウントのパスワードを入力します。
1. MMC で、を開きます。 **ローカルセキュリティ設定** を選択し、 **ローカルポリシー** > **ユーザー権限の割り当て**.
1. forms サーバーを実行しているユーザーアカウントに次の権限を割り当てます。

   * ターミナルサービスを通じてログオンを拒否する
   * ローカルでログオンを拒否
   * サービスとしてログオン（通常は既に設定済み）

1. 次のディレクトリの新しいユーザーアカウントに変更権限を付与します。
   * **グローバルドキュメントストレージ (GDS) ディレクトリ**：GDS ディレクトリの場所は、AEM Forms のインストールプロセス中に手動で設定します。インストール時に場所を指定しないと、`[JBoss root]/server/[type]/svcnative/DocumentStorage` にあるアプリケーションサーバーのインストールディレクトリの下にあるディレクトリがデフォルトの場所になります。
   * **CRX リポジトリディレクトリ**：デフォルトの場所は `[AEM-Forms-installation-location]\crx-repository` です。
   * **AEM Forms 一時ディレクトリ**：
      * （Windows）環境変数で設定されている TMP または TEMP パス
      * （AIX、Linux または Solaris）ログインユーザのホームディレクトリ UNIX ベースのシステムでは、root 以外のユーザは、次のディレクトリを一時ディレクトリとして使用できます。
      * (Linux) /var/tmp または/usr/tmp
      * (AIX) /tmp または/usr/tmp
      * (Solaris) /var/tmp または/usr/tmp
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

Configuration Manager は、アプリケーションサーバーにデプロイされたサーブレットを使用して、JEE 上のAEM Formsデータベースのブートストラップを実行します。 設定が完了する前に Configuration Manager がこのサーブレットにアクセスするので、権限を持つユーザーはアクセスできません。Configuration Manager を使用して JEE 上のAEM Formsを設定した後は、このサーブレットを無効にする必要があります。

1. adobe-livecycle-[appserver].ear ファイルを解凍します。
1. META-INF/application.xmlファイルを開きます。
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
1. adobe-bootstrapper.war および adobe-lcm-bootstrapper-redirectory をコメントアウトします。 war モジュールを次に示します。

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

1. META-INF/application.xmlファイルを保存して閉じます。
1. EAR ファイルを zip 形式で圧縮し、アプリケーションサーバーに再デプロイします。
1. AEM Forms サーバーを起動します。
1. 以下の URL をブラウザーに入力して変更をテストし、URL が機能しないことを確認します。

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**Trust Store へのリモートアクセスのロックダウン**

Configuration Manager を使用すると、Acrobat Reader DC Extensions の資格情報を JEE 上のAEM Forms Trust Store にアップロードできます。 つまり、リモートプロトコル（SOAP および EJB）を介した Trust Store 資格情報サービスへのアクセスがデフォルトで有効になっています。 このアクセスは、Configuration Manager を使用して使用権限資格情報のアップロードを完了した後、または後で管理コンソールを使用して資格情報を管理することにした場合は、必要なくなります。

の節の手順に従って、すべての Trust Store サービスへのリモートアクセスを無効にできます [サービスへの不要なリモートアクセスの無効化](https://helpx.adobe.com/jp/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services).

**不要な匿名アクセスをすべて無効にする**

一部の forms サーバーサービスには、匿名の呼び出し元によって呼び出される操作が含まれています。 これらのサービスへの匿名アクセスが不要な場合は、 [サービスへの不要な匿名アクセスの無効化](https://helpx.adobe.com/jp/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services).

#### デフォルトの管理者パスワードを変更します {#change-the-default-administrator-password}

JEE 上のAEM Formsをインストールすると、Super Administrator/login-id Administrator ユーザーに対して、デフォルトのパスワードが「 」のデフォルトユーザーアカウントが 1 つ設定されます。 *パスワード*. このパスワードは、Configuration Manager を使用して直ちに変更する必要があります。

1. Web ブラウザーに次の URL を入力します。

   ```java
   https://[host name]:[port]/adminui
   ```

   デフォルトのポート番号は次のいずれかです。

   **JBoss：** 8080

   **WebLogic Server:** 7001

   **WebSphere:** 9080。

1. **ユーザー名**&#x200B;フィールドに `administrator` と入力し、**パスワード**&#x200B;フィールドに `password` と入力します。
1. **設定**／**User Management**／**ユーザーとグループ**&#x200B;をクリックします。
1. **検索**&#x200B;フィールドに `administrator` と入力し、**検索**&#x200B;をクリックします。
1. クリック **上級管理者** を選択します。
1. クリック **パスワードを変更** をクリックします。
1. 新しいパスワードを指定し、 **保存**.

さらに、次の手順を実行して、CRX 管理者のデフォルトのパスワードを変更することをお勧めします。

1. デフォルトのユーザー名／パスワードを使用して、`https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` にログインします。
1. 検索フィールドに「管理者」と入力し、**移動**&#x200B;をクリックします。
1. 検索結果から「**管理者**」を選択し、ユーザーインターフェイスの右下で「**編集**」アイコンをクリックします。
1. 「**新しいパスワード**」フィールドに新しいパスワードを、「**パスワード**」フィールドに古いパスワードを指定します。
1. ユーザーインターフェイスの右下で「保存」アイコンをクリックします。

#### WSDL の生成を無効にする {#disable-wsdl-generation}

Web Service Definition Language(WSDL) の生成は、開発環境でのみ有効にする必要があります。開発環境では、開発者が WSDL の生成を使用してクライアントアプリケーションを構築します。 実稼働環境で WSDL の生成を無効にして、サービスの内部詳細が公開されないようにすることもできます。

1. Web ブラウザーに次の URL を入力します。

   ```java
   https://[host name]:[port]/adminui
   ```

1. クリック **設定/コアシステム設定/設定**.
1. 「**WSDL を有効にする**」のチェックを外して「**OK**」をクリックします。

### アプリケーションサーバーのセキュリティ {#application-server-security}

次の表に、JEE 上のAEM Formsアプリケーションのインストール後に、アプリケーションサーバーを保護するための方法を示します。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>説明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>アプリケーションサーバー管理コンソール</p> </td> 
   <td><p>アプリケーションサーバーに JEE 上のAEM Formsをインストール、設定およびデプロイした後は、アプリケーションサーバーの管理コンソールへのアクセスを無効にする必要があります。 詳しくは、アプリケーションサーバーのドキュメントを参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td><p>アプリケーションサーバーの cookie 設定</p> </td> 
   <td><p>アプリケーションの Cookie は、アプリケーションサーバーによって制御されます。 アプリケーションをデプロイする際、アプリケーションサーバー管理者は、サーバー全体またはアプリケーション固有の方法で cookie の環境設定を指定できます。 デフォルトでは、サーバー設定が優先されます。</p> <p>アプリケーションサーバーで生成されるすべてのセッション cookie に <code>HttpOnly</code> 属性が含まれている必要があります。例えば、JBoss アプリケーションサーバーを使用する場合、<code>WEB-INF/web.xml</code> ファイルで、SessionCookie 要素を <code>httpOnly="true"</code> に変更できます。</p> <p>HTTPS のみを使用して送信する Cookie を制限できます。 その結果、HTTP 経由では暗号化されずに送信されません。 アプリケーションサーバーの管理者は、サーバーに対して安全な cookie をグローバルに有効にする必要があります。 例えば、JBoss アプリケーションサーバーを使用する場合、<code>server.xml</code> ファイルで、コネクタ要素を <code>secure=true</code> に変更できます。</p> <p>cookie の設定について詳しくは、アプリケーションサーバーのドキュメントを参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td><p>ディレクトリの参照</p> </td> 
   <td><p>誰かが存在しないページを要求したり、ディレクタの名前を要求したりした場合 ( リクエスト文字列がスラッシュ (/) で終わる場合 )、アプリケーションサーバーはそのディレクトリの内容を返さないようにする必要があります。 これを防ぐには、アプリケーションサーバー上のディレクトリ参照を無効にします。 これは、管理コンソールアプリケーションと、サーバー上で実行されている他のアプリケーションに対しておこなう必要があります。</p> <p>JBoss の場合、次の例に示すように、web.xml ファイルで <code>DefaultServlet</code> プロパティの初期化パラメーターの listings 値を <code>false</code> に設定します。</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;デフォルト&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;リスト&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>WebSphere の場合、ibm-web-ext.xmi ファイルの <code>directoryBrowsingEnabled</code> プロパティを <code>false</code> に設定します。</p> <p>WebLogic の場合、次の例に示すように、weblogic.xml ファイルの index-directories プロパティを <code>false</code> に設定します。</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### データベースのセキュリティ {#database-security}

データベースを保護する場合は、データベースベンダーが説明した測定を実装する必要があります。 データベースユーザーには、JEE 上のAEM Formsで使用するために最低限必要なデータベース権限を付与する必要があります。 例えば、データベース管理者権限を持つアカウントを使用しないでください。

oracle時には、使用するデータベース・アカウントに必要な権限は、CONNECT、RESOURCE および CREATE VIEW のみです。 他のデータベースの同様の要件については、 [JEE 上のAEM Formsのインストールの準備（シングルサーバー）](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64_jp).

#### Windows 上での SQL Server の統合セキュリティの設定（JBoss 版） {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. 次の例に示すように、[JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} を変更して、`integratedSecurity=true` を接続 URL に追加します。

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. アプリケーションサーバーを実行しているコンピューターの Windows システムパスに sqljdbc_auth.dll ファイルを追加します。sqljdbc_auth.dll ファイルは、Microsoft SQL JDBC 6.2.1.0 ドライバーのインストールフォルダー内にあります。
1. AEM Formsデータベースを持ち、最小限の権限セットを持つログインアカウントに、「ログオン」の「JEE 上のAEM Formsサービス (JBoss for )」プロパティを変更します。 Windows サービスとしてではなくコマンドラインから JBoss を実行している場合は、この手順を実行する必要はありません。
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

#### Windows 上での SQL Server の統合セキュリティの設定（WebSphere 版） {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

WebSphere では、統合セキュリティを設定できるのは、WebSphere に埋め込まれた SQL Server JDBC ドライバーではなく、外部の SQL Server JDBC ドライバーを使用する場合のみです。

1. WebSphere Administrative Console にログインします。
1. ナビゲーションツリーで、**リソース**／**JDBC**／**データソース** をクリックし、右側のパネルで「**IDP_DS**」をクリックします。
1. 右側のパネルの「追加のプロパティ」で「**カスタムプロパティ**」をクリックし、「**新規**」をクリックします。
1. 「**名前**」ボックスに `integratedSecurity` と入力し、「**値**」ボックスに `true` と入力します。
1. ナビゲーションツリーで、**リソース**／**JDBC**／**データソース** をクリックし、右側のパネルで「**RM_DS**」をクリックします。
1. 右側のパネルの「追加のプロパティ」で「**カスタムプロパティ**」をクリックし、「**新規**」をクリックします。
1. 「**名前**」ボックスに `integratedSecurity` と入力し、「**値**」ボックスに `true` と入力します。
1. WebSphere がインストールされているコンピューター上で、Windows システムパス（C:¥Windows）に sqljdbc_auth.dll ファイルを追加します。sqljdbc_auth.dll ファイルは、Microsoft SQL JDBC 1.2 ドライバーのインストール先ディレクトリ（デフォルトは *[InstallDir]*¥sqljdbc_1.2¥enu¥auth¥x86）と同じ場所にあります。
1. 選択 **開始** > **Campaign コントロールパネル** > **サービス**、WebSphere(IBM WebSphere Application Server) の Windows サービスを右クリックします。 &lt;version> - &lt;node>) をクリックし、「 **プロパティ**.
1. プロパティダイアログボックスで、 **ログオン** タブをクリックします。
1. 選択 **このアカウント** をクリックし、使用するログインアカウントの設定に必要な情報を入力します。
1. 次の SQL Server のセキュリティを設定 **混在** ～に対する態度 **Windows 認証のみ**.

### データベース内の機密コンテンツへのアクセスの保護 {#protecting-access-to-sensitive-content-in-the-database}

AEM Formsデータベーススキーマには、システム設定とビジネスプロセスに関する機密情報が含まれているので、ファイアウォールの背後に隠しておく必要があります。 データベースは、forms サーバーと同じ信頼境界内にあると見なす必要があります。 情報の開示やビジネス・データの盗難を防ぐために、データベース管理者 (DBA) は、権限を持つ管理者のみがアクセスできるようにデータベースを構成する必要があります。

追加の予防策として、データベースベンダー固有のツールを使用して、以下のデータを含むテーブルの列を暗号化することを検討してください。

* Rights Managementドキュメントキー
* Trust Store HSM PIN 暗号化キー
* ローカルユーザーのパスワードハッシュ

ベンダー固有のツールについて詳しくは、[データベースのセキュリティ情報](https://helpx.adobe.com/jp/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information)を参照してください。

### LDAP セキュリティ {#ldap-security}

LDAP(Lightweight Directory Access Protocol) ディレクトリは、通常、JEE 上のAEM Formsでエンタープライズユーザーおよびグループ情報のソースとして使用され、パスワード認証を実行する手段として使用されます。 LDAP ディレクトリが Secure Socket Layer(SSL) を使用するように設定され、JEE 上のAEM Formsが SSL ポートを使用して LDAP ディレクトリにアクセスするように設定されていることを確認する必要があります。

#### LDAP のサービス拒否 {#ldap-denial-of-service}

LDAP を使用した一般的な攻撃では、攻撃者が複数回の認証に意図的に失敗します。 これにより、LDAP ディレクトリサーバーは、すべての LDAP 依存サービスからユーザーをロックアウトします。

AEM Formsへの認証にユーザーが繰り返し失敗した場合にAEM Formsが実装する、失敗の試行回数とそれ以降のロックアウト時間を設定できます。 管理コンソールでは、小さい値を選択します。失敗の試行回数を選択する場合は、すべての試行の後、AEM Formsが LDAP ディレクトリサーバーが実行する前にユーザーをロックアウトすることを理解しておくことが重要です。

#### 自動アカウントロックの設定 {#set-automatic-account-locking}

1. 管理コンソールにログインします。
1. クリック **設定** > **ユーザー管理** > **ドメイン管理**.
1. [ 自動アカウントロック設定 ] で、次の設定を行います。 **連続する認証失敗の最大数** を低い数（例： 3）に設定します。
1. 「**保存**」をクリックします。

### 監査とログ {#auditing-and-logging}

アプリケーションの監査とログの適切で安全な使用は、セキュリティや他の異常なイベントをできるだけ早く追跡し、検出するのに役立ちます。 アプリケーション内での監査とログの有効な使用には、成功したログインと失敗したログインの追跡、およびキーレコードの作成や削除などの主要なアプリケーションイベントが含まれます。

監査を使用して、次のような様々な種類の攻撃を検出できます。

* Brute Force パスワード攻撃
* サービス拒否攻撃
* 敵意のある入力および関連するクラスのスクリプティング攻撃のインジェクション

次の表は、サーバーの脆弱性を減らすために使用できる監査およびログの手法を示しています。

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
   <td><p>適切な JEE 上のAEM Formsファイルアクセス制御リスト (ACL) を設定します。</p> <p>適切な認証情報を設定すると、攻撃者がファイルを削除するのを防ぐことができます。</p> <p>ログファイルディレクトリのセキュリティアクセス許可は、管理者および SYSTEM グループに対するフルコントロールである必要があります。 AEM Formsユーザーアカウントには、読み取りおよび書き込み権限のみが必要です。</p> </td> 
  </tr> 
  <tr> 
   <td><p>ログファイルの冗長性</p> </td> 
   <td><p>リソースが許可されている場合は、Syslog、Tivoli、Microsoft Operations Manager(MOM) サーバ、または別のメカニズムを使用して、攻撃者がアクセスできない（書き込み専用）リアルタイムで別のサーバにログを送信します。</p> <p>この方法でログを保護すると、改ざんを防ぐことができます。 また、中央リポジトリにログを保存すると、相関関係と監視が容易になります（例えば、複数の Forms サーバーが使用中で、各コンピューターにパスワードを問い合わせる複数のコンピューターでパスワード推測攻撃が行われる場合）。</p> </td> 
  </tr> 
 </tbody> 
</table>

### 管理者以外のユーザーが Experience Generator を実行できるようにしますPDF

管理者以外のユーザーが Generator を使用できるようにします。PDF 通常、管理者権限を持つユーザーのみがPDFジェネレーターを使用できます。 管理者以外のユーザーが Adobe Generator を実行できるようにするには、次の手順をPDFします。

1. PDFG_NON_ADMIN_ENABLED という名前の環境変数を作成します。

1. 変数の値を TRUE に設定します。

1. AEM Forms のインスタンスを再起動します。

## JEE 上のAEM Formsを企業以外からのアクセスに設定する {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

JEE 上のAEM Formsを正常にインストールした後は、環境のセキュリティを定期的に維持することが重要です。 ここでは、JEE 上のAEM Forms実稼動サーバーのセキュリティを維持するために推奨されるタスクについて説明します。

### Web アクセス用のリバースプロキシの設定 {#setting-up-a-reverse-proxy-for-web-access}

A *リバースプロキシ* を使用して、外部ユーザーと内部ユーザーの両方が、JEE 上のAEM Forms Web アプリケーションの 1 つの URL セットを使用できるようにします。 この設定は、JEE 上のAEM Formsが実行されているアプリケーションサーバーへのユーザーの直接接続を許可するよりも、より安全です。 リバースプロキシは、JEE 上のAEM Formsを実行しているアプリケーションサーバーに対するすべての HTTP リクエストを実行します。 ユーザーは、リバースプロキシに対するネットワークアクセスのみを持ち、リバースプロキシでサポートされる URL 接続のみを試行できます。

**リバースプロキシサーバーで使用する JEE 上の AEM Forms ルート URL**

各 JEE 上のAEM Forms Web アプリケーションのアプリケーションルート URL を次に示します。 リバースプロキシは、エンドユーザーに提供する Web アプリケーション機能の URL を公開するようにのみ設定する必要があります。

特定の URL は、エンドユーザーに表示される Web アプリケーションとして強調表示されます。 リバースプロキシを介して外部ユーザーにアクセスするために、Configuration Manager のその他の URL を公開しないでください。

<table> 
 <thead> 
  <tr> 
   <th><p>ルート URL</p> </th> 
   <th><p>目的または関連する Web アプリケーション</p> </th> 
   <th><p>Web ベースのインターフェイス</p> </th> 
   <th><p>エンドユーザーアクセス</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>使用権限をPDFドキュメントに適用するAcrobat Reader DC Extensions エンドユーザー Web アプリケーション</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>Rights Managementエンドユーザー Web アプリケーション</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>Rights Managementの Web サービス URL</p> </td> 
   <td><p>いいえ</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>PDFジェネレーター管理 Web アプリケーション</p> </td> 
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
   <td><p>Workspace クライアントアプリケーションで必要な Workspace サーブレットとデータサービス</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>JEE 上のAEM Formsリポジトリをブートストラップするサーブレット</p> </td> 
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
   <td><p>すべての forms サーバーサービスの Web サービス URL</p> </td> 
   <td><p>いいえ</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>Rights Management管理 Web アプリケーション</p> </td> 
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
   <td><p>Trust Store 管理ページ</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>フォームのレンダリングのテストとデバッグを行うForms IVS アプリケーション</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>出力サービスのテストとデバッグを行うための Output IVS アプリケーション</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rmws/*</p> </td> 
   <td><p>Rights Managementの REST URL</p> </td> 
   <td><p>いいえ</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputAdmin/*</p> </td> 
   <td><p>出力管理ページ</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>Forms web アプリケーションファイル</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>サーブレット</p> </td> 
   <td><p>HTML変換中に JavaScript を取得するために使用</p> </td> 
   <td><p>いいえ</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>Forms管理ページ</p> </td> 
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
   <td><p>アプリケーションとサービスのユーザーインターフェイス</p> </td> 
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
   <td><p>Rest サポートページ</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>いいえ</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>JEE 上のAEM Forms Core 設定ページ</p> </td> 
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
   <td><p>/DocumentManager/*</p> </td> 
   <td><p>HTTP ドキュメントを有効にした SOAP トランスポートまたは EJB トランスポートを介してリモートエンドポイント、SOAP WSDL エンドポイント、および Java SDK にアクセスする際に処理されるドキュメントのアップロードとダウンロード。</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
 </tbody> 
</table>

## クロスサイトリクエストフォージェリ攻撃からの保護 {#protecting-from-cross-site-request-forgery-attacks}

クロスサイト要求偽造（CSRF）攻撃とは、ユーザーに対する web サイトの信頼を悪用して、ユーザーが許可していないコマンドを知らないうちに送信することです。この攻撃は、web ページ上に配置したリンクまたはスクリプトや、メールメッセージに含めた URL を介して、既にユーザーの認証が済んでいる別のサイトへのアクセスを達成するという形で行われます。

例えば、管理者は、他の web サイトを閲覧しながら管理コンソールにログインすることがあります。CSRF 攻撃者は、このような状況を狙って、閲覧されるサイトの web ページに含まれている HTML img タグの `src` 属性などに、攻撃対象 web サイト内のサーバー側スクリプトを参照する URL を記述しておきます。Web ブラウザーに備わっている Cookie ベースのセッション認証メカニズムにより、攻撃者の web サイトは正当なユーザーを装って、攻撃対象のサーバー側スクリプトに悪意ある要求を送信することができます。その他の例については、 [https://owasp.org/www-community/attacks/csrf#Examples](https://owasp.org/www-community/attacks/csrf#Examples) を参照してください。

CSRF に共通の特性は次のとおりです。

* ユーザーの ID に依存するサイトに関与する。
* その ID に対するサイトの信頼を活用する。
* ユーザーのブラウザーを騙して、ターゲットサイトに HTTP リクエストを送信させます。
* 副次的な影響を持つ HTTP 要求に関与する。

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
   1. 例外でない場合は、リクエストが渡されます。

1. リクエスト内にリファラーが指定されていない場合、サーバーは Null リファラーが許可されているかどうかを確認します。

   1. Null リファラーが許可されている場合は、リクエストが渡されます。
   1. Null リファラーが許可されていない場合、サーバーは要求された URI が Null リファラーの例外に相当するかどうかを確認し、適宜リクエストを処理します。

### リファラーフィルタリングの管理 {#managing-referer-filtering}

JEE 上の AEM Forms には、ご使用のサーバーのリソースへのアクセスを許可するリファラーを指定するためのリファラーフィルターが用意されています。デフォルトの場合、リファラーフィルターでは安全な HTTP メソッド（GET など）を使用したリクエストはフィルタリングされません。ただし、*CSRF_CHECK_GETS* が true にセットされている場合は除きます。許可されているリファラーのエントリにあるポート番号が 0 に設定されている場合、JEE 上の AEM Forms では、ポート番号とは関係なく、ホストからのリクエストがすべてリファラーと共に許可されます。ポート番号が指定されていない場合は、デフォルトのポート 80（HTTP）またはポート 443（HTTPS）からのリクエストのみが許可されます。許可されているリファラーリストのすべてのエントリが削除されると、リファラーフィルタリングは無効になります。

Document Services を最初にインストールすると、許可されているリファラーリストは、Document Services がインストールされたサーバーのアドレスで更新されます。サーバーのエントリには、サーバー名、IPv4 アドレス、IPv6 アドレス（IPv6 が有効の場合）、ループバックアドレス、localhost エントリなどがあります。許可されているリファラーのリストに追加された名前は、ホストのオペレーティングシステムから返されます。例えば、IP アドレスが 10.40.54.187 のサーバーには、次のエントリが含まれます。`https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`ホストのオペレーティングシステムから返された正規でない名前（IPv4 アドレス、IPv6 アドレスのない名前、または完全修飾のないドメイン名）については、許可リストは更新されません。許可されているリファラーリストを、ビジネス環境に合わせて変更します。実稼働環境に Forms サーバーをデプロイするとき、許可されているリファラーリストの内容がデフォルトのままになっていないことを確認してください。許可されているリファラー、リファラーの例外または URI を変更したら、必ずサーバーを再起動して、その変更を有効にします。

**許可されているリファラーリストの管理**

許可されているリファラーリストは、管理コンソールの User Management インターフェイスから管理できます。User Management インターフェイスを使用すると、リストを作成、編集または削除できます。許可されているリファラーのリストの操作について詳しくは、*管理ヘルプ*&#x200B;の[CSRF 攻撃の防止](/help/forms/using/admin-help/preventing-csrf-attacks.md)を参照してください。

**許可されているリファラーの例外および許可されている URI のリストの管理**

JEE 上の AEM Forms には、許可されているリファラーの例外と許可されている URI の各リストを管理するための API が用意されています。これらの API を使用して、リストを取得、作成、編集または削除できます。 使用可能な API のリストを以下に示します。

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

**CSRF_CHECK_GETS** は、GET 要求でリファラーチェックを制御します。このパラメーターが定義されていない場合、デフォルト値は false に設定されます。このパラメーターは、GETリクエストをフィルターする場合にのみ指定します。

**CSRF_ALLOWED_REFERER_EXCEPTIONS** は、許可されているリファラーの例外リストの ID です。このリファラーフィルターを使用すると、リスト ID で特定されたリスト内のリファラーからのリクエストでは、Forms サーバーのリソースを呼び出すことはできません。

**CSRF_ALLOWED_URIS_LIST_NAME** は、許可されている URI リストの ID です。リファラーフィルターは、リクエストのリファラーヘッダーの値に関係なく、リスト ID で特定されたリストのリソースに対するリクエストをブロックしません。

**CSRF_ALLOW_NULL_REFERER**&#x200B;は、リファラーが Null の場合または存在しない場合のリファラーフィルターの動作を制御します。このパラメーターが定義されていない場合、デフォルト値は false に設定されます。このパラメーターは、Null リファラーを許可する場合にのみ指定します。Null リファラーを許可すると、ある種のクロスサイト要求偽造攻撃を許可してしまう可能性があります。

**CSRF_NULL_REFERER_EXCEPTIONS** は、リファラーが Null の場合にリファラーチェックが行われない URI のリストです。このパラメーターは、 *CSRF_ALLOW_NULL_REFERER* が false に設定されている場合、 リスト内で複数の URI を使用する場合は、コンマで区切ります。

次に、 *web.xml* ファイルを ***サンプル*** WAR ファイル：

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

正当なサーバー要求が CSRF フィルターによってブロックされている場合は、次のいずれかを試します。

* 拒否されたリクエストにリファラーヘッダーがある場合は、許可されているリファラーリストにそのリファラーを追加することを慎重に検討します。信頼できるリファラーのみを追加します。
* 拒否されたリクエストにリファラーヘッダーがない場合は、リファラーヘッダーを含めるようにクライアントアプリケーションを変更します。
* クライアントがブラウザーで動作できる場合は、そのデプロイメントモデルを試してみてください。
* 最後の手段として、リソースを「許可されている URI 」リストに追加できます。 この設定は推奨されません。

## セキュアなネットワーク設定 {#secure-network-configuration}

この節では、JEE 上のAEM Formsで必要なプロトコルとポートについて説明し、安全なネットワーク設定で JEE 上のAEM Formsをデプロイする際の推奨事項を示します。

### JEE 上のAEM Formsで使用されるネットワークプロトコル {#network-protocols-used-by-aem-forms-on-jee}

前の節で説明したように、セキュアなネットワークアーキテクチャを設定する場合、JEE 上のAEM Formsとエンタープライズネットワーク内の他のシステムとの間のやり取りには、次のネットワークプロトコルが必要です。

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
     <li><p>ブラウザーに Configuration Manager とエンドユーザー Web アプリケーションが表示される</p> </li> 
     <li><p>すべての SOAP 接続</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>.NET アプリケーションなどの Web サービスクライアントアプリケーション</p> </li> 
     <li><p>Adobe Reader®は JEE 上のAEM Forms Web サービスに SOAP を使用</p> </li> 
     <li><p>AdobeFlash®アプリケーションは SOAP を forms サーバー Web サービスに使用します</p> </li> 
     <li><p>SOAP モードで使用された場合に JEE 上のAEM Forms SDK が呼び出される</p> </li> 
     <li><p>Workbench デザイン環境</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>Enterprise JavaBeans(EJB) モードで使用した場合に JEE 上のAEM Forms SDK が呼び出す</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP / POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>サービスへの電子メールベースの入力（電子メールエンドポイント）</p> </li> 
     <li><p>電子メールによるユーザータスク通知</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>UNC ファイル IO</p> </td> 
   <td><p>サービスへの入力用の監視フォルダーの JEE 上のAEM Forms監視（監視フォルダーエンドポイント）</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>ディレクトリ内の組織ユーザーとグループ情報の同期</p> </li> 
     <li><p>インタラクティブユーザーの LDAP 認証</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>JDBC サービスを使用したプロセスの実行中に外部データベースに対して実行されるクエリとプロシージャの呼び出し</p> </li> 
     <li><p>JEE 上のAEM Formsリポジトリへの内部アクセス</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>任意の WebDAV クライアントによる JEE 上のAEM Formsデザイン時リポジトリ（フォーム、フラグメントなど）のリモート参照を有効にします</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>AdobeFlashアプリケーション。JEE 上のAEM Formsサーバーサービスは、リモートエンドポイントを使用して設定されます。</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>JEE 上のAEM Formsは、JMX を使用した監視用に MBean を公開します</p> </td> 
  </tr> 
 </tbody> 
</table>

### アプリケーションサーバーのポート {#ports-for-application-servers}

このセクションでは、サポートされるアプリケーションサーバーの種類ごとに、デフォルトのポート（および代替構成範囲）について説明します。 JEE 上のAEM Formsを実行するアプリケーションサーバーに接続するクライアントに許可するネットワーク機能に応じて、これらのポートを内側のファイアウォールで有効または無効にする必要があります。

>[!NOTE]
>
>デフォルトでは、サーバーは複数の JMX MBean を adobe.com 名前空間の下に公開します。 サーバーの正常性監視に役立つ情報のみが公開されます。 ただし、情報開示を防ぐには、信頼できないネットワーク内の呼び出し元が JMX MBean を検索してヘルス指標にアクセスするのを防ぐ必要があります。

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
   <td><p>CORBA のサポート</p> </td> 
   <td><p>[JBoss root]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
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
     <li><p>管理サーバーのリスンポート：デフォルトは 7001 です。</p> </li> 
     <li><p>管理サーバー SSL リスンポート：デフォルトは 7002 です。</p> </li> 
     <li><p>管理対象サーバー用に構成されたポート（例：8001）</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JEE 上のAEM Formsへのアクセスに必要ない WebLogic 管理ポート</p> </td> 
   <td> 
    <ul> 
     <li><p>管理対象サーバーのリスンポート：1 ～ 65534の設定が可能</p> </li> 
     <li><p>管理対象サーバー SSL リスンポート：1 ～ 65534の設定が可能</p> </li> 
     <li><p>Node Manager リスンポート：デフォルトは 5556 です。</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**WebSphere ポート**

JEE 上の AEM Forms で必要な WebSphere ポートについて詳しくは、「WebSphere Application Server UI のポート番号設定」を参照してください。

### SSL の設定 {#configuring-ssl}

[JEE 上の AEM Forms の物理アーキテクチャ](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture)で取り上げている物理アーキテクチャについては、使用するすべての接続に SSL を設定する必要があります。特に すべての SOAP 接続は、ネットワーク上にユーザー資格情報が漏洩されないように、すべて SSL 経由で行う必要があります。

JBoss、WebLogic および WebSphere 上で SSL を設定する手順については、[管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_64_jp)の「SSL の設定」を参照してください。

AEM Forms サーバー用に設定された JVM（Java 仮想マシン）に証明書を読み込む手順については、[AEM Forms Workbench ヘルプ](https://www.adobe.com/go/learn_aemforms_workbench_65_jp)の「相互認証」の節を参照してください。 

### SSL リダイレクトの設定 {#configuring-ssl-redirect}

SSL をサポートするようにアプリケーションサーバーを設定した後、アプリケーションおよびサービスへのすべての HTTP トラフィックが、SSL ポートを使用するように強制されることを確認する必要があります。

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

この節では、JEE 上のAEM Formsを実行する際に使用する Windows に固有のセキュリティに関する推奨事項について説明します。

### JBoss Service アカウント {#jboss-service-accounts}

JEE 上のAEM Formsの自動インストールでは、デフォルトで、ローカルシステムアカウントを使用してサービスアカウントが設定されます。 組み込みのローカルシステムユーザーアカウントは、高いレベルのアクセシビリティを持っています。これは管理者グループに属しています。 ワーカープロセス ID がローカルシステムユーザーアカウントとして実行される場合、そのワーカープロセスはシステム全体に対するフルアクセス権を持ちます。

#### 管理者以外のアカウントを使用してアプリケーションサーバーを実行する {#run-the-application-server-using-a-non-administrative-account}

1. Microsoft管理コンソール (MMC) で、forms サーバーサービスのローカルユーザーを作成し、次のようにログインします。

   * 選択 **ユーザーはパスワードを変更できません**.
   * **所属するグループ**&#x200B;タブに、「ユーザー」グループが表示されていることを確認してください。

1. 選択 **設定** > **管理ツール** > **サービス**.
1. アプリケーションサーバーサービスをダブルクリックして、サービスを停止します。
1. の **ログオン** タブ、選択 **このアカウント**&#x200B;作成したユーザーアカウントを参照し、そのアカウントのパスワードを入力します。
1. 「ローカルセキュリティ設定」ウィンドウの「ユーザー権限の割り当て」で、forms サーバーを実行しているユーザーアカウントに次の権限を付与します。

   * ターミナルサービスを通じてログオンを拒否する
   * locallyxx でのログオンを拒否する
   * サービスとしてログオン（通常は既に設定済み）

1. 次のディレクトリの新しいユーザーアカウントに変更権限を付与します。
   * **グローバルドキュメントストレージ (GDS) ディレクトリ**：GDS ディレクトリの場所は、AEM Forms のインストールプロセス中に手動で設定します。インストール時に場所を指定しないと、`[JBoss root]/server/[type]/svcnative/DocumentStorage` にあるアプリケーションサーバーのインストールディレクトリの下にあるディレクトリがデフォルトの場所になります。
   * **CRX リポジトリディレクトリ**：デフォルトの場所は `[AEM-Forms-installation-location]\crx-repository` です。
   * **AEM Forms 一時ディレクトリ**：
      * （Windows）環境変数で設定されている TMP または TEMP パス
      * （AIX、Linux または Solaris）ログインユーザのホームディレクトリ UNIX ベースのシステムでは、root 以外のユーザは、次のディレクトリを一時ディレクトリとして使用できます。
      * (Linux) /var/tmp または/usr/tmp
      * (AIX) /tmp または/usr/tmp
      * (Solaris) /var/tmp または/usr/tmp
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


1. アプリケーションサーバーサービスを開始します。

### ファイルシステムのセキュリティ {#file-system-security}

JEE 上のAEM Formsでは、次の方法でファイルシステムを使用します。

* ドキュメントの入力および出力の処理中に使用される一時ファイルを格納します
* インストールされたソリューションコンポーネントをサポートするために使用されるファイルをグローバルアーカイブストアに格納します
* 監視フォルダーには、ファイルシステムフォルダーの場所からサービスへの入力として使用されるドロップファイルが格納されます

forms サーバーサービスでドキュメントを送受信する方法として監視フォルダーを使用する場合は、ファイルシステムのセキュリティに関して、さらに注意を払ってください。 ユーザーが監視フォルダーにコンテンツをドロップすると、そのコンテンツは監視フォルダーを通じて公開されます。 この場合、サービスは実際のエンドユーザーを認証しません。 代わりに、ACL と共有レベルのセキュリティをフォルダーレベルで設定し、サービスを効果的に呼び出せるユーザーを決定します。

## JBoss 固有のセキュリティに関する推奨事項 {#jboss-specific-security-recommendations}

ここでは、JEE 上の AEM Forms を実行する際に使用される JBoss 7.0.6 に特有のアプリケーションサーバー設定の推奨事項について説明します。

### JBoss 管理コンソールと JMX コンソールを無効にします {#disable-jboss-management-console-and-jmx-console}

JBoss 管理コンソールと JMX コンソールへのアクセスは、自動インストール方法を使用して JBoss に JEE にAEM Formsをインストールすると、既に設定されています（JMX 監視は無効になります）。 独自の JBoss Application Server を使用する場合は、JBoss 管理コンソールと JMX 監視コンソールへのアクセスが保護されていることを確認します。 JMX 監視コンソールへのアクセスは、jmx-invoker-service.xml という JBoss 設定ファイルで設定されます。

### ディレクトリ参照を無効にする {#disable-directory-browsing}

管理コンソールにログインした後で、URL を変更することで、コンソールのディレクトリリストを参照できます。 例えば、URL を次のいずれかの URL に変更すると、ディレクトリ一覧が表示される場合があります。

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## WebLogic 固有のセキュリティに関する推奨事項 {#weblogic-specific-security-recommendations}

ここでは、JEE 上でのAEM Formsの実行時に WebLogic 9.1 を保護するためのアプリケーションサーバー設定に関する推奨事項について説明します。

### ディレクトリ参照を無効にする {#disable_directory_browsing-1}

weblogic.xml ファイルの index-directories プロパティを `false` に設定します。次に例を示します。

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### WebLogic SSL ポートの有効化 {#enable-weblogic-ssl-port}

デフォルトでは、WebLogic はデフォルトの SSL リッスンポート (7002) を有効にしません。 SSL を設定する前に、WebLogic Server 管理コンソールでこのポートを有効にします。

## WebSphere 固有のセキュリティに関する推奨事項 {#websphere-specific-security-recommendations}

ここでは、JEE 上のAEM Formsを実行する WebSphere を保護するためのアプリケーションサーバー設定に関する推奨事項について説明します。

### ディレクトリ参照を無効にする {#disable_directory_browsing-2}

ibm-web-ext.xml ファイルの `directoryBrowsingEnabled` プロパティを `false` に設定します。

### WebSphere 管理セキュリティの有効化 {#enable-websphere-administrative-security}

1. WebSphere Administrative Console にログインします。
1. ナビゲーションツリーで、**セキュリティ**／**Global Security** に移動します。
1. 選択 **管理セキュリティの有効化**.
1. 両方を選択解除 **アプリケーションセキュリティの有効化** および **Java 2 セキュリティを使用**.
1. クリック **OK** または **適用**.
1. 内 **メッセージ** ボックス、 **マスター設定に直接保存**.
