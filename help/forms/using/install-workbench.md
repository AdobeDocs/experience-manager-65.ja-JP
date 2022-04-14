---
title: Workbench のインストール
seo-title: Install workbench
description: Workbench をインストールします。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
role: Admin
exl-id: d530dbb9-f95e-4329-9665-37faf8f7931b
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: ht
source-wordcount: '2244'
ht-degree: 100%

---

# Workbench のインストール {#install-workbench}

このドキュメントでは、AEM Forms Workbench のインストールと設定の手順を示します。このインストールプログラムは Forms Designer もインストールします。

## このドキュメントの対象読者 {#who-should-read-this-doc}

このドキュメントは、インストール、設定、管理または Workbench のデプロイを担当している管理者または開発者を対象としています。また、アップグレードした AEM Forms プロセスをサポートするためにシステムを構成するのに必要な情報も含まれています。このドキュメントで扱う内容は、Microsoft® Windows® オペレーティングシステムに関する十分な知識がある読者を想定しています。

## 追加情報 {#additional-information}

次の表に、AEM Forms の学習およびこの使用を開始する際に役立つ情報を示します。
<table>
 <tbody>
  <tr>
   <td><p><strong>情報</strong></p> </td>
   <td><p><strong>参照先</strong></p> </td>
  </tr>
  <tr>
   <td><p>Workbench の手順に関する情報</p> </td>
   <td><p><a href="https://helpx.adobe.com/jp/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">Workbench ヘルプ</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>AEM Forms および AEM Forms を他の Adobe 製品と統合するための方法に関する一般的な情報</p> </td>
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65_jp">AEM Forms の概要</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>AEM Forms 用のすべてのドキュメント</p> </td>
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65_jp">AEM Forms のドキュメント</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>現在のバージョンに関するパッチアップデート、テクニカルノート、および追加情報</p> </td>
   <td><p>アドビの販売代理店にお問い合わせください。</a><br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM Forms の Flex Workspace は非推奨（廃止予定）となりました。AEM Forms のリリースで使用できます。

## インストールの準備 {#before-you-install}

### Workbench のインストールの概要 {#workbench-installation-overview}

Workbench は、開発者およびフォーム作成者が自動化されたビジネスプロセスおよびフォームを作成するための統合開発環境（IDE）です。また、Workbench はそれらのプロセスおよびフォームで使用するリソースやサービスを管理するためにも使用されます。

次の図に、以下を含む Workbench のインストールについて示します。
* Workbench を使用した Process Design
* Designer を使用した Form Design

>[!NOTE]
>
>AEM Forms サーバーでは個別のインストールプログラムが必要です。詳しくは、JEE インストールドキュメントで AEM Forms を参照してください。

![default-render-form](assets/installing-workbench.png)

## システムの前提条件 {#system-prerequisites}

この節では、ハードウェアとソフトウェアの要件およびサポートされているプラットフォームの概要を説明します。

### ハードウェアおよびソフトウェアの最小要件 {#minimum-hardware-software-requirements}

**Workbench**
最小要件を次に示します。
インストール用のディスク容量：
* 680 MB（Workbench のみの場合）.
* 2.15 GB（Workbench 、Designer およびサンプルアセンブリを 1 つのドライブにフルインストールした場合）.
* 一時インストールディレクトリ用に 400 MB（ユーザーの ¥temp ディレクトリに 200 MB、Windows 一時ディレクトリに 200 MB）.

>[!NOTE]
>
>これらの場所がすべて 1 つのドライブ上にある場合は、インストール時に 1.5 GB の空き容量が必要です。一時ディレクトリにコピーされるファイルは、インストールが完了すると削除されます。

* ハードウェア要件： Intel® Pentium® 4 または AMD の同等の 1 GHz プロセッサー.
* Java™ ランタイム環境（JRE）7.0 アップデート 51 または 7.0 の以降のアップデート。
* 1024 X 768 ピクセル以上のモニター解像度、16 ビットカラー以上.
* AEM Forms サーバーに対する TCP/IPv4 または TCP/IPv6 ネットワーク接続。
* Visual C++ 再頒布可能ランタイムパッケージ 2012 32 ビットをインストールします。
* Visual C++ 再頒布可能ランタイムパッケージ 2013 32 ビットをインストールします。

>[!NOTE]
>
>Workbench をインストールするには、管理者権限が必要です。管理者以外のアカウントを使用してインストールする場合は、適切なアカウントの資格情報が求められます。

### サポートされているプラットフォーム {#supported-platforms}

Workbench でサポートされているプラットフォームの完全なリストについては、[AEM Forms でサポートされているプラットフォーム](http://adobe.com/go/learn_aemforms_supportedplatforms_65_jp)を参照してください。

## Designer のインストールに関する考慮事項 {#designer-installation-considerations}

Workbench のインストールには、対応する Designer（英語版のみ）がデフォルトで含まれています。Workbench インストールアプリケーションがコンピューター上で既存バージョンの Designer を検出した場合、インストールが終了することがあります。この場合、続行するには現在のバージョンの Designer を削除する必要があります。次の表に、発生する可能性のある Designer のすべてのインストールシナリオと、Workbench をインストールするときに行う必要のあるすべてのアクションを一覧で示します。

<table>
 <tbody>
  <tr>
   <td><p><strong>現在インストールされている Designer のバージョン</strong></p> </td>
   <td><p><strong>必要なアクション</strong></p> </td>
  </tr>
  <tr>
   <td><p>Acrobat Pro または Acrobat Pro Extended（Designer が付属）</p> </td>
   <td><p>なし.<br />Workbench のインストールで、Acrobat Pro または Acrobat Pro Extended と共にインストールされた Designer のインスタンスがコンピューター上で検出されます。<br />
Workbench 6.4 用 Designer 6.4.x や Workbench 6.5 用 Designer 6.5.0.x など、異なるバージョンの Designer は同じシステム上で共存できます。Acrobat 10 Pro または Acrobat 10 Pro Extended などと一緒にインストールされた Designer のバージョンをアンインストールする必要はありません。
<br /></p> </td>
  </tr>
  <tr>
   <td><p>Designer（スタンドアロン）</p> </td>
   <td><p>なし. <br />Workbench に付属する Designer のバージョンは英語版のみです。<br />Workbench インストーラーでは、新しいバージョンの Designer は再インストールされません。代わりに、Workbench インストーラーにバンドルされている更新バージョンにパッチが適用されます。これにより、ローカライズバージョンの Designer を Workbench 内で使用することができます。<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Windows 10 で Designer（スタンドアロン）をアンインストールするには： {#uninstall-designer-standalone-windows10}

1. **コントロールパネル／プログラム／プログラムと機能**&#x200B;に移動します。
1. 「現在インストールされているプログラム」リストで、「**Adobe Designer**」を選択します。
1. 「**アンインストール**」をクリックしてから、「**はい**」をクリックします。

## Workbench のインストール {#installing-workbench}

この章では、Workbench をインストールする方法について説明します。

### Workbench のインストールと実行 {#installing-and-running-workbench}

Workbench をインストールする前に、Workbench の実行に必要なソフトウェアとハードウェアが使用環境に含まれていることを確認してください（**インストールの前に**&#x200B;の節を参照してください）。

**Workbench をインストールして実行するには：**

1. 次のいずれかのタスクを実行します。
   * インストールメディアの ¥workbench ディレクトリに移動して、run_windows_installer.bat ファイルをダブルクリックします。
   * Workbench をファイルシステムにダウンロードして解凍します。ダウンロード後、¥workbench ディレクトリに移動して run_windows_installer.bat ファイルをダブルクリックします。

   >[!IMPORTANT]
   >
   >Workbench インストーラーは、ローカルドライブからのみ実行できます。リモートサイトから実行することはできません。

   >[!NOTE]
   >
   >「Java 仮想マシンを作成できませんでした」というエラーが表示された場合は、_JAVA_OPTIONS という名前の環境変数を -Xmx512M という値で作成し、インストーラーを実行します。

1. はじめに画面で「次へ」をクリックします。
1. 使用許諾契約書を読み、「使用許諾契約書の条件に同意します」を選択して、「次へ」をクリックします。
1. （オプション）フォームを作成および変更するツールが必要な場合は、「Adobe Designer のインストール」を選択します。

   >[!NOTE]
   >
   >Acrobat 10 と共にインストールされた Designer を引き続き使用するには、このオプションの選択を解除したままにします。

1. 表示されるデフォルトのディレクトリをそのまま使用するか、「選択」をクリックして Workbench のインストール先ディレクトリを選択し、「次へ」をクリックします。

   >[!NOTE]
   >
   >インストールディレクトリのパスには、#（ポンド）および $（ドル）文字を含めることはできません。

1. インストール前の概要を確認して、「インストール」をクリックします。インストールプログラムによりインストールの進行状況が表示されます。
1. インストールの概要を確認します。「Adobe AEM forms Workbench の起動」を選択して Workbench を起動し、「次へ」をクリックします。
1. リリースノートを確認して「完了」をクリックします。
1. コンピューターに以下のアイテムがインストールされました。
   * **Workbench**：スタートメニューにショートカットフォルダーを保存するよう選択した場合にこのメニューから Workbench を起動するには、すべてのプログラム／AEM Forms／Workbench を選択します。詳しくは、<a href="https://helpx.adobe.com/jp/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">Workbenchの使用</a>ドキュメントを参照してください。
   * **Designer**：Designer は Workbench 内部からアクセスできます。詳しくは、<a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf">Designer ヘルプ</a>のはじめにのトピックを参照してください。
   * **AEM Forms SDK**：SDK 使用方法の詳細については、<a href="http://www.adobe.com/go/learn_aemforms_programming_65">AEM Forms によるプログラミング</a>を参照してください。

## プロセスのアップグレード {#upgrading-processes}

JEE 上の AEM Forms プロセスは、アップグレードウィザードを使用して AEM Forms アプリケーションにアップグレードできます。詳しくは、Workbench ヘルプの既存のアーティファクトのアップグレードドキュメントを参照してください。

### サーバーの設定およびログイン {#configuring-and-logging-server}

Workbench を使用するには、通常は別のコンピューターで AEM Forms のインスタンスを実行させる必要があります。AEM Forms にログインにするには、ユーザー名とパスワードおよびこのサーバーの場所に関する詳細情報が必要です。

>[!NOTE]
>
>EMC Documentum または IBM FileNet リポジトリプロバイダーを使用するように AEM Forms を設定している場合、AEM Forms 管理コンソール でデフォルトとして設定されている以外のリポジトリにログインするには、ユーザー名を username@Repository と指定します。

### タイムアウトの設定 {#configuring-timeout-settings}

デフォルトでは、Workbench は動作状況に関係なく 2 時間後にタイムアウトになります。タイムアウトの設定を編集するには、<a href="https://docs.adobe.com/content/help/jp/experience-manager-65/forms/administrator-help/configure-user-management/configure-advanced-system-attributes.html">管理コンソールヘルプ</a> の「User Management の設定」の「詳細なシステム属性の設定」を参照してください。

### HTTPS 経由で接続するための Workbench の設定 {#configuring-workbench-to-connect-over-HTTPS}

HTTPS 経由で Workbench を AEM Forms サーバーに接続するには、公開鍵を発行した認証局（CA）が信頼できることを Workbench が認識する必要があります。この証明書が信頼できるソースに由来すると認識されない場合、[Workbench_HOME]/workbench/jre/lib/security ディレクトリにある cacert ファイルを更新する必要があります。

>[!NOTE]
>
>[Workbench_HOME] は、Workbench をインストールしたディレクトリを表します。デフォルトの場所は C:¥Program Files (x86)¥Adobe Experience Manager forms Workbench です。

HTTPS には、証明書で指定されている名前を使用して接続してください。この名前は通常、完全修飾ホスト名です。

**cacert ファイルを更新するには**：
1. Secure Sockets Layer（SSL）証明書のコピーがあることを確認します。SSLサーバーを設定した管理者に問い合わせるか、または Web ブラウザーを使用して証明書を書き出します。

   >[!NOTE]
   >
   >証明書を書き出すには、web ブラウザーを開いて管理コンソールにログインし、ブラウザーに証明書をインストールします。次にブラウザーから一時的な保存場所（または直接 [Workbench_HOME]/workbench/jre/lib/security ディレクトリ）に証明書を書き出します。

1. 証明書を [Workbench_HOME]/workbench/jre/lib/security ディレクトリにコピーします。

1. コマンドプロンプトウィンドウを開き、[Workbench_HOME]/workbench/jre/bin に移動して、次のコマンドを入力します。
   `keytool -import -storepass changeit -file [Workbench_HOME]\workbench\jre\lib\security\ssl_cert_for_certname.cer -keystore [Workbench_HOME]\workbench\jre\lib\security\cacerts -alias example`ここで、
   * changeit：cacerts キーストアのデフォルトのパスワードです。
   * certname：手順 1 で選択した証明書です。
   * example：証明書用に選択したエイリアスです。この値は変更できます。

1. 証明書を信頼するように求めるプロンプトが表示されたら、「Yes」と入力し、Enter キーを押します。次に、keytool が cacerts ファイルを [Workbench_HOME]/workbench/jre/lib/securit ディレクトリに読み込みます。

1. Workbench を閉じて再起動し、変更を適用します。

### 動的に生成されるテンプレート用のキャッシュ設定の指定 {#configuring-cache-settings-for-dynamically-generated-templates}

アプリケーションで、XFA コンテンツを自動的に更新することによって固有のテンプレートをすばやく生成する場合は、キャッシュ操作の以下の側面を考慮する必要があります。実際には、各トランザクションで新しい固有のテンプレートが使用されています。

Forms Generator または Output が、特定のフォームテンプレートのキャッシュ内のエントリを検索または更新する場合は、以下の複数のキー値を使用して、アクセスする特定のキャッシュエントリを探します。

* **テンプレートファイルの名前**：キャッシュされているフォームの固有のプライマリ識別子として使用される、テンプレートの場所およびファイル名です。
* **タイムスタンプ**：テンプレートファイルには、フォームの最終更新時間の確定に使用するタイムスタンプが含まれています。
* **テンプレートの UUID**：各テンプレートには、Designer により、フォームとそのバージョンに応じて固有の識別子（UUID）が挿入されます。埋め込まれた UUID は、フォームが更新されるびに更新されます。例えば、XDP テンプレートには次の内容が表示されます。

   `<?xml version="1.0" encoding="UTF-8"?>`
   `<?xfa generator="AdobeAEM formsDesignerES_V8.2" APIVersion="2.6.7185.0"?><xdp:xdp xmlns:xdp=http://ns.adobe.com/xdp/ timeStamp="2008-07-29T21:22:12Z" uuid="823e538f-ff6c-4961-b759-f7626978a223"><template xmlns="http://www.xfa.org/schema/xfa-template/2.6/">`

* **レンダリングオプション**：キャッシュの内容は、固有のレンダリングオプションのセットごとにレンダリングフォームキャッシュ内に個別に保存されます。


Forms サービスは、ファイル名またはリポジトリの場所を参照するか、メモリ内で XML オブジェクトとしての値を使用することによって、テンプレートを受け取ります。
* **参照によって渡されるテンプレート**：コンテンツルートおよびファイル名を使用します。この方法を使用して、固有のテンプレートが、要求ごとに異なるファイル名で渡されると、ディスクキャッシュは無制限に増えて再利用できなくなります。これを防ぐには、固有のテンプレートは同じファイル名を使用して渡し、すべての要求で同じキャッシュが更新されるようにします。
* **値によって渡されるテンプレート**：theinDataDoc パラメーターを使用して、データと共に渡されるテンプレートのバイトを使用します。この方法を使用して、固有のテンプレートが、異なる UUID を指定して渡されると、ディスクキャッシュは無制限に増えて再利用できなくなります。これを防ぐには、すべてのテンプレートから UUID 属性を削除し、テンプレートのキャッシュが作成されないようにします。または、Null 以外の同一の UUID を渡すと、キャッシュオブジェクトは作成されますがすべての要求で同じキャッシュが更新されるようになります。

キャッシュが無制限に増えないようにするために、新しい AEM Forms API（renderHTMLForm2 および renderPDFForm2）を使用して動的に生成されるテンプレートのレンダリングについて、次の要因を考慮します。

新しい API を使用する場合、テンプレートはドキュメントオブジェクトとして渡され、パッシブにするかしないかに基づいて Forms サービス内で処理されます。

UUID およびコンテンツルートがキャッシュのキーとして機能するパッシブにしたドキュメントの場合は、以下の側面を考慮します。
* UUID が含まれないパッシブにした入力テンプレートに対しては、キャッシュは作成されません。
* UUID とコンテンツルートが同一の、パッシブにした複数の入力テンプレートが渡される場合は、同じキャッシュが上書きされます。

ファイル名およびコンテンツルートがキャッシュのキーとして機能する、パッシブにしていないドキュメントの場合は、以下の側面を考慮します。
* パッシブにしていない入力テンプレートの場合、キャッシュは、ドキュメントの生成元となったコンテンツルートとファイル名に依存します。コンテンツルートとテンプレートのファイル名が同じ要求についてのみ、同じキャッシュが使用されます。動的に生成されたテンプレートが Forms サービスに渡されるとき、以下のベストプラクティスによってにキャッシュが無制限に増えないようになります。
   * UUID を削除するか、動的に生成されたすべてのテンプレートで同一の UUID を渡します。
   * テンプレートのバイト、またはディスク上の同じファイル名からドキュメントを生成します。

### Workbench のアンインストール {#uninstalling-workbench}

コントロールパネルのプログラムの追加と削除機能を使用して、アンインストーラーを起動します。Workbench および Designer アプリケーションには、個別のアンインストールプログラムがあります。

## AEM Forms XDC Editor の設定 {#configuring-aem-forms-xdc-editor}

XDC Editor を使用すると、ネットワークプリンターの管理者は XML Forms Architecture Device Configuration（XDC）ファイルの作成および変更ができます。XDC ファイルには、プリンターの機能が記述されます。例えば、プリンター言語、用紙サイズとトレイ位置との関係付けなどが記述されます。

ネットワークプリンターの管理者が XDC Editor を使用する前に、サンプルの XDC ファイルを配置し直して、『XDC Editor を使用したデバイスプロファイルの作成』を確認してください。

**サンプルの XDC ファイルを入手するには**：
1. AEM Forms サーバーで、[AEM Forms root]\sdk\samples\Output\IVS から XDC フォルダーを探します。
1. このフォルダーの内容を、Workbench または Eclipse システムからアクセス可能なディレクトリにコピーします。

**XDC Editor のヘルプを入手するには**：
1. AEM Forms ドキュメントの web サイトへ移動します。
1. 「**開発**」タブをクリックし、「XDC Editor を使用したデバイスプロファイルの作成」へ移動します。xdc_editor_help_web.zip ファイルをダウンロードし、「お読みください」ファイル内の手順に従ってヘルプファイルをインストールします。
