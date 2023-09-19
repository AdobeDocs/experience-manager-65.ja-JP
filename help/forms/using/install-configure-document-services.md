---
title: ドキュメントサービスのインストールと設定
seo-title: Installing and configuring document services
description: AEM Forms ドキュメントサービスをインストールして、PDF ドキュメントを作成、アセンブル、配布、アーカイブし、デジタル署名を追加してドキュメントへのアクセスを制限し、Barcoded Forms をデコードしましょう。
seo-description: Install AEM Forms document services to create, assemble, distribute, archive PDF documents, add digital signatures to limit access to documents, and decode barcoded forms.
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
role: Admin
exl-id: 5d48e987-16c2-434b-8039-c82181d2e028
source-git-commit: f41962faa0567ed99c1e2ab189e81fb978781af3
workflow-type: tm+mt
source-wordcount: '5515'
ht-degree: 78%

---


# ドキュメントサービスのインストールと設定 {#installing-and-configuring-document-services}

AEM Forms は、PDF ドキュメントの作成、アセンブル、配布、アーカイブや、ドキュメントへのアクセスを制限するためのデジタル署名の追加、Barcoded Forms のデコードなど、様々なドキュメントレベルの操作を実現する一連の OSGi サービスを提供します。これらのサービスは、AEM Formsアドオンパッケージに含まれています。 これらのサービスをまとめて、ドキュメントサービスと呼びます。 使用可能なドキュメントサービスとその主な機能のリストを次に示します。

* **Assembler サービス：** PDF ドキュメントや XDP ドキュメントの結合、並べ替えおよび拡張と、PDF ドキュメントに関する情報の取得を実行できます。PDF ドキュメントを PDF/A 規格に変換して検証することもできます。また、PDF フォーム、XML フォームを PDF/A-1b、PDF/A-2b および PDFA/A-3b に変換することもできます。詳しくは、[Assembler サービス](/help/forms/using/assembler-service.md)を参照してください。

* **ConvertPDF サービス：** PDF ドキュメントを PostScript ファイルまたは画像ファイル（JPEG、JPEG 2000、PNG および TIFF）に変換します。詳しくは、[ConvertPDF サービス](/help/forms/using/using-convertpdf-service.md)を参照してください。

* **Barcoded Forms サービス：**&#x200B;バーコードの電子画像からデータを抽出します。このサービスは、入力として 1 つまたは複数のバーコードを含んだ TIFF ファイルや PDF ファイルを受け取り、バーコードデータを抽出します。詳しくは、[Barcoded Forms サービス](/help/forms/using/using-barcoded-forms-service.md)を参照してください。

* **DocAssurance サービス：**&#x200B;ドキュメントの暗号化と復号、使用権限の追加による Adobe Reader の機能拡張、ドキュメントへのデジタル署名の追加を実行できます。DocAssurance サービスには、3 つのサービス（署名、暗号化、Reader 拡張機能）があります。詳しくは、[DocAssurance サービス](/help/forms/using/overview-aem-document-services.md)を参照してください。

* **Encryption サービス：**&#x200B;ドキュメントの暗号化と復号を実行できます。ドキュメントが暗号化されると、その内容が読み取れなくなります。 許可されたユーザーは、ドキュメントを復号化して、コンテンツにアクセスできます。 詳しくは、[Encryption サービス](/help/forms/using/overview-aem-document-services.md#encryption-service)を参照してください。

* **Forms サービス：**&#x200B;通常 Forms Designer で作成されたフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャを行うクライアントアプリケーションを作成できます。Forms サービスは、作成したあらゆるフォームデザインを PDF ドキュメントとして処理します。詳しくは、[ Forms サービス](/help/forms/using/forms-service.md)を参照してください。

* **Output サービス：** PDF、レーザープリンター形式、ラベルプリンター形式など、様々な形式のドキュメントを作成します。レーザープリンター形式には、PostScript と Printer Control Language（PCL）があります。詳しくは、[Output サービス](/help/forms/using/output-service.md)を参照してください。

* **PDF Generator サービス：**&#x200B;ネイティブファイル形式を PDF に変換する API を提供します。また、PDF を他のファイル形式に変換し、PDF ドキュメントのサイズを最適化します。詳しくは、[PDF Generator サービス](aem-document-services-programmatically.md#pdfgeneratorservice)を参照してください。

* **Reader Extension サービス：**&#x200B;使用権限を追加して Adobe Reader の機能を拡張することで、組織内でインタラクティブな PDF ドキュメントを容易に共有できます。このサービスにより、PDF ドキュメントを Adobe Reader で開いた場合には使用できない機能（ドキュメントへのコメントの追加、フォームへの入力、ドキュメントの保存など）が有効になります。詳しくは、[Reader Extension サービス](/help/forms/using/overview-aem-document-services.md#reader-extension-service)を参照してください。

* **Signature サービス：** AEM サーバーでデジタル署名とドキュメントを処理できます。例えば、通常、Signature サービスは次の状況で使用されます。

   * AEMサーバーは、AcrobatまたはAdobe Readerを使用して開くユーザーにフォームが送信される前に、フォームを認証します。
   * AEMサーバーは、AcrobatまたはAdobe Readerを使用してフォームに追加された署名を検証します。
   * AEMサーバーは公証人に代わってフォームに署名します。

  Signature サービスは、Trust Store に保存されている証明書と秘密鍵証明書にアクセスします。 詳しくは、[Signature サービス](/help/forms/using/aem-document-services-programmatically.md)を参照してください。

AEM Forms は強力なエンタープライズクラスのプラットフォームであり、ドキュメントサービスは AEM Forms の機能の 1 つです。機能の完全な一覧については、「[AEM Forms の概要](/help/forms/using/introduction-aem-forms.md)」を参照してください。

## デプロイメントトポロジ {#deployment-topology}

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。通常、AEM Forms Document Services を実行するには、1 つのAEMインスタンス（オーサーまたはパブリッシュ）のみが必要です。 AEM Forms Document Services を実行するには、次のトポロジを使用することをお勧めします。 トポロジについて詳しくは、「[AEM Forms のアーキテクチャとデプロイメントトポロジ](/help/forms/using/aem-forms-architecture-deployment.md)」を参照してください。

![AEM Forms のアーキテクチャとデプロイメントトポロジ](do-not-localize/document-services.png)

>[!NOTE]
>
>AEM Formsでは、1 台のサーバーからすべての機能を設定して実行できますが、容量計画、ロードバランシングを実行し、実稼動環境で特定の機能用に専用のサーバーを設定する必要があります。 例えば、PDF Generatorサービスを使用して 1 日に数千ページ、複数のアダプティブフォームを変換してデータを取得する環境の場合、PDF Generatorサービスとアダプティブフォーム機能用に別々のAEM Formsサーバーを設定します。 これにより、パフォーマンスが最適化され、各サーバーを個別にスケーリングできるようになります。

## システム要件 {#system-requirements}

AEM Forms Document Services のインストールと設定を開始する前に、次の点を確認してください。

* ハードウェアとソフトウェアのインフラが正しく設定されていること。サポート対象のハードウェアとソフトウェアの一覧について詳しくは、「[技術要件](/help/sites-deploying/technical-requirements.md)」を参照してください。

* AEM インスタンスのインストールパスに空白が含まれていないこと。
* AEM インスタンスが稼働していること。AEM の用語では、「インスタンス」とは、サーバー上でオーサーモードまたはパブリッシュモードで実行されている AEM のコピーのことです。通常、AEM Forms Document Services を実行するには、1 つのAEMインスタンス（オーサーまたはパブリッシュ）のみ必要です。

   * **オーサー**：コンテンツの作成、アップロードおよび編集や web サイトの管理に使用される AEM インスタンス。公開の準備が整ったコンテンツは、パブリッシュインスタンスにレプリケートされます。
   * **公開**：公開されたコンテンツをインターネットや内部ネットワークを介して公開するAEMインスタンス。

* メモリ要件が満たされていること。AEM Forms アドオンパッケージでは、次が必要です。

   * Microsoft® Windows ベースのインストールの場合、15 GB の一時的な空きスペースが必要です。
   * Unix ベースのインストールの場合、6 GB の一時的な空きスペースが必要です。

* PDF Generator を使用して Microsoft® Windows や Linux® で変換を実行するには、必要なクライアントソフトウェアをインストールする必要があります。

   * **Microsoft® Windows**：[Microsoft® Office](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p) または [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) をインストールします
   * **Linux®**：[Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p) をインストールします

>[!NOTE]
>
>* Microsoft® Windows では、PDF Generator は、WebKit、Acrobat WebCapture、および PhantomJS の変換ルートをサポートし、HTML ファイルを PDF ドキュメントに変換します。
>* UNIX ベースのオペレーティングシステムでは、PDF Generator は、WebKit および PhantomJS の変換ルートをサポートし、HTML ファイルを PDF ドキュメントに変換します。
>

### UNIX ベースのオペレーティングシステムの追加要件 {#extrarequirements}

Unix ベースのオペレーティングシステムを使用する場合は、それぞれのオペレーティングシステムのインストールメディアから、次の 32 ビットパッケージをインストールしてください。
<table>
 <tbody>
  <tr>
   <td>
    <ul>
     <li>expat</li>
    </ul> </td>
   <td>
    <ul>
     <li>libxcb</li>
    </ul> </td>
   <td>
    <ul>
     <li>freetype</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXau</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>libSM</li>
    </ul> </td>
   <td>
    <ul>
     <li>zlib</li>
    </ul> </td>
   <td>
    <ul>
     <li>libICE</li>
    </ul> </td>
   <td>
    <ul>
     <li>libuuid</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>glibc</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXext</li>
    </ul> </td>
   <td>
    <ul>
     <li>nss-softokn-freebl</li>
    </ul> </td>
   <td>
    <ul>
     <li>fontconfig</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>libX11</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXrender</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXrandr</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXinerama</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

* **(PDF Generatorのみ**) 32 ビット版の libcurl、libcrypto および libssl ライブラリをインストールし、以下のシンボリックリンクを作成します。 シンボリックリンクは、それぞれのライブラリの最新バージョンを指すようにします。

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **（PDF Generator のみ）** PDF Generator サービスは、HTML ファイルを PDF ドキュメントに変換するため、WebKit および PhantomJS の各ルートをサポートしています。PhantomJS ルートの変換を有効にするには、以下に示す 64 ビットライブラリをインストールします。 一般に、これらのライブラリは既にインストールされています。 不足しているライブラリがあれば、手動でインストールします。

   * linux-gate.so.1
   * libz.so.1
   * libfontconfig.so.1
   * libfreetype.so.6
   * libdl.so.2
   * librt.so.1
   * libpthread.so.0
   * libstdc++.so.6
   * libm.so.6
   * libgcc_s.so.1
   * libc.so.6
   * ld-linux.so.2
   * libexpat.so.1

## プリインストール設定 {#preinstallationconfigurations}

プリインストール設定の節に記載されている設定は、PDF Generatorサービスにのみ適用されます。 インストールサービスを設定していない場合は、PDF Generator前の設定の節をスキップできます。

### Adobe Acrobat とサードパーティ製アプリケーションのインストール {#install-adobe-acrobat-and-third-party-applications}

PDF Generator サービスを使用して、Microsoft® Word、Microsoft® Excel、Microsoft® PowerPoint、OpenOffice、WordPerfect X7、Adobe Acrobat などのネイティブファイル形式を PDF ドキュメントに変換する場合は、これらのアプリケーションを AEM Forms サーバーにインストールしてください。

>[!NOTE]
>
>* AEM Forms Server がオフラインまたはセキュア環境にあり、インターネットを使用して Adobe Acrobat をアクティブ化できない場合は、[オフラインアクティベーション](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=jp)を参照して、そのような場合に Adobe Acrobat のインスタンスをアクティブ化する手順を確認してください。
>* Adobe Acrobat、Microsoft® Word、Excel および PowerPoint は、Microsoft® Windows でのみ使用できます。UNIX ベースのオペレーティングシステムを使用している場合は、OpenOffice をインストールして、リッチテキストファイルやサポートされている Microsoft® Office ファイルを PDF ドキュメントに変換します。
>* PDF Generator サービスを使用できるすべてのユーザーに対して、Adobe Acrobat およびサードパーティソフトウェアのインストール後に表示されるすべてのダイアログボックスを閉じます。
>* インストールされているすべてのソフトウェアを少なくとも 1 回起動します。PDF Generator サービスを使用するように設定されているすべてのユーザーに対して、すべてのダイアログボックスを解除します。
>* [Adobe Acrobat シリアル番号の有効期限を確認](https://helpx.adobe.com/jp/enterprise/kb/volume-license-expiration-check.html)してライセンスを更新する日付を設定するか、有効期限に基づいて[シリアル番号を移行](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number)します。

Acrobat をインストールしてから、Microsoft® Word を開きます。「**Acrobat**」タブで「**PDFを作成**」をクリックし、マシン上にある .doc または .docx のファイルを PDF ドキュメントに変換します。変換が成功すれば、AEM Forms が PDF Generator サービスで Acrobat を使用する準備が整います。

### 環境変数の設定 {#setup-environment-variables}

32 ビットおよび 64 ビットの Java Development Kit、サードパーティアプリケーション、Adobe Acrobatの環境変数を設定します。 環境変数には、対応するアプリケーションを起動する際に使用する実行ファイルの絶対パスを含める必要があります。以下の表に、いくつかのアプリケーション用の環境変数を例示します。

<table>
 <tbody>
  <tr>
   <td><p><strong>アプリケーション</strong></p> </td>
   <td><p><strong>環境変数</strong></p> </td>
   <td><p><strong>例</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>JDK（64 ビット）</strong></p> </td>
   <td><p>JAVA_HOME</p> </td>
   <td><p>C:\Program Files\Java\jdk1.8.0_74</p> </td>
  </tr>
  <tr>
   <td><p><strong>Adobe Acrobat</strong></p> </td>
   <td><p>Acrobat_PATH</p> </td>
   <td><p>C:\Programファイル (x86)\Adobe\Acrobat 2015\Acrobat\Acrobat.exe</p> </td>
  </tr>
  <tr>
   <td><p><strong>メモ帳</strong></p> </td>
   <td><p>Notepad_PATH</p> </td>
   <td><p>C:\WINDOWS\notepad.exe<br /> <strong></strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>OpenOffice</strong></p> </td>
   <td><p>OpenOffice_PATH</p> </td>
   <td><p>C:¥Program Files (x86)¥OpenOffice.org4</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* すべての環境変数とそれぞれのパスでは、大文字と小文字が区別されます。
>* JAVA_HOME およびAcrobat_PATH（Windows のみ）は必須の環境変数です。
>* 環境変数 OpenOffice_PATH は、実行ファイルではなく、インストールフォルダーのパスに設定します。
>* Word、PowerPoint、Excel、Project などの Microsoft® Office アプリケーション、または AutoCAD については、環境変数を設定する必要はありません。これらのアプリケーションがサーバーにインストールされている場合、GeneratePDFサービスは自動的にこれらのアプリケーションを開始します。
>* UNIX ベースのプラットフォームでは、OpenOffice を/root としてインストールします。 OpenOffice がルートとしてインストールされていない場合、PDF Generatorサービスは OpenOffice ドキュメントをPDFドキュメントに変換できません。 OpenOffice を非 root ユーザーとしてインストールして実行する必要がある場合は、非 root ユーザーに sudo 権限を与えます。
>* UNIX ベースのプラットフォームで OpenOffice を使用している場合は、以下のコマンドを実行して PATH 変数を設定します。
>
>  `export OpenOffice_PATH=/opt/openoffice.org4`

### （IBM® WebSphere® のみ）IBM® SSL ソケットプロバイダーの設定 {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

以下の手順を実行して、IBM® SSL ソケットプロバイダーを設定します。

1. java.security ファイルのコピーを作成します。ファイルのデフォルトの場所は次のとおりです。`[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`
1. コピーした java.security ファイルを開いて編集します。
1. デフォルトの SSL ソケットファクトリとして、デフォルトの IBM® WebSphere® ファクトリではなく JSSE2 ファクトリを使用するように変更します。

   **デフォルトの内容：**

   ```shell
   #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   #WebSphere socket factories (in cryptosf.jar)
   ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

   **変更後の内容：**

   ```shell
   ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   
   #WebSphere socket factories (in cryptosf.jar)
   #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

1. AEM Forms サーバーが更新した java.security ファイルを使用できるようにするには、AEM Forms サーバーの開始時に次の java 引数を追加します。

   `-Djava.security.properties= [path of newly created Java.security file].`

### （Windows のみ）Microsoft Office® のファイル制限機能の設定 {#configure-the-file-block-settings-for-microsoft-office}

Microsoft® Office のセキュリティセンターの設定を変更して、PDF Generator サービスが古いバージョンの Microsoft® Office で作成されたファイルを変換できるようにします。

1. Microsoft® Office のアプリケーションを開きます。例えば、Microsoft® Word などです。「**[!UICONTROL ファイル]**」／「**[!UICONTROL オプション]**」に移動します。オプションのダイアログボックスが表示されます。

1. クリック **[!UICONTROL Trust Center]**&#x200B;をクリックし、 **[!UICONTROL Trust Center の設定]**.
1. Adobe Analytics の **[!UICONTROL Trust Center の設定]**&#x200B;をクリックし、 **[!UICONTROL ファイルブロック設定]**.
1. PDF Generator サービスで PDF ドキュメントへの変換を許可するファイルタイプについて、「**[!UICONTROL ファイルタイプ]**」リストで「**[!UICONTROL 開く]**」チェックボックスをオフにします。

### （Windows のみ）プロセスレベルのトークンを置き換える権限の付与 {#grant-the-replace-a-process-level-token-privilege}

アプリケーションサーバーの起動に使用するユーザーアカウントには、 **プロセスレベルトークンの置換** 権限 ローカルシステムアカウントには **プロセスレベルトークンの置換** デフォルトで権限を持っています。 Local Administrators グループのユーザーと共に実行するサーバーに対しては、明示的に権限を付与する必要があります。 次の手順を実行して権限を付与します。

1. Microsoft® Windows のグループポリシーエディターを開きます。グループポリシーエディターを開くには、「**[!UICONTROL スタート]**」をクリックしてスタートの検索ボックスに **gpedit.msc** と入力し、「**[!UICONTROL グループポリシーエディター]**」をクリックします。
1. に移動します。 **[!UICONTROL ローカルコンピューターポリシー]** > **[!UICONTROL コンピュータの構成]** > **[!UICONTROL Windows 設定]** > **[!UICONTROL セキュリティ設定]** > **[!UICONTROL ローカルポリシー]** > **[!UICONTROL ユーザー権限の割り当て]** をクリックし、 **[!UICONTROL プロセスレベルトークンの置換]** ポリシーを作成し、 Administrators グループを含めます。
1. 「プロセスレベルトークンの置き換え」エントリにユーザーを追加します。

### （Windows のみ）管理者以外のユーザーに対する PDF Generator サービスの有効化 {#enable-the-pdf-generator-service-for-non-administrators}

管理者以外のユーザーが PDF Generator サービスを使用できるようにすることができます。通常は、管理者権限を持つユーザーのみがこのサービスを実行できます。

1. PDFG_NON_ADMIN_ENABLED 環境変数を作成します。
1. 環境変数の値を TRUE に設定します。
1. AEM Forms のインスタンスを再起動します。

### （Windows のみ）ユーザーアカウント制御（UAC）の無効化 {#disable-user-account-control-uac}

1. システム構成ユーティリティにアクセスするには、**[!UICONTROL スタート／ファイル名を指定して実行]**&#x200B;を選択し、**[!UICONTROL MSCONFIG]** と入力します。
1. 「**[!UICONTROL ツール]**」タブをクリックし、スクロールして「**[!UICONTROL UAC 設定を変更]**」を選択します。「**[!UICONTROL 起動]**」をクリックして新しいウィンドウでコマンドを実行します。
1. スライダーを「通知しない」レベルに設定します。完了したら、コマンドウィンドウを閉じ、システム構成ウィンドウを閉じます。
1. レジストリ設定で UAC が 0（ゼロ）に設定されていることを検証します。検証するには、以下の手順を実行します。

   1. Microsoft® は、レジストリを変更する前にバックアップをとっておくことを推奨しています。詳しい手順については、「[Windows でのレジストリのバックアップと復元方法](https://support.microsoft.com/ja-jp/help/322756)」を参照してください。
   1. Microsoft® Windows のレジストリエディターを開きます。レジストリエディターを開くには、「スタート／ファイル名を指定して実行」に移動し、「regedit」と入力して「OK」をクリックします。
   1. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\` に移動します。EnableLUA の値が 0（ゼロ）に設定されていることを確認します。
   1. **EnableLUA** の値が 0（ゼロ）に設定されていることを確認します。値が 0 でない場合は、値を 0 に変更します。 レジストリエディターを終了します。

1. コンピューターを再起動します。

### （Windows のみ）エラーレポートサービスの無効化 {#disable-error-reporting-service}

Windows Server で PDF Generator サービスを使用してドキュメントを PDF に変換しているとき、実行ファイルに問題が見つかったためファイルを閉じる必要があると Windows Server で報告される場合があります。ただし、バックグラウンドで継続されるので、PDFの変換には影響しません。

エラーを受け取らないようにするには、Windows エラーレポートを無効にします。 エラーレポート機能を無効にする手順について詳しくは、[https://technet.microsoft.com/ja-jp/library/cc754364.aspx](https://technet.microsoft.com/ja-jp/library/cc754364.aspx) を参照してください。

### （Windows のみ）HTML から PDF への変換の設定 {#configure-html-to-pdf-conversion}

PDF Generator サービスは、HTML ファイルを PDF ドキュメントに変換するため、WebKit、WebCapture および PhantomJS の各ルートまたはメソッドを提供しています。Windows で WebKit および Acrobat WebCapture ルートの変換を有効にするには、Unicode フォントを %windir%\fonts ディレクトリにコピーします。

>[!NOTE]
>
>新しいフォントをフォントフォルダーにインストールしたときは、AEM Forms インスタンスを再起動してください。

### （UNIX ベースのプラットフォームのみ）HTML から PDF への変換用の追加設定  {#extra-configurations-for-html-to-pdf-conversion}

UNIX ベースのプラットフォームでは、PDF Generatorサービスは、HTMLファイルをPDFドキュメントに変換する WebKit および PhantomJS ルートをサポートします。 HTMLからPDFへの変換を有効にするには、目的の変換ルートに適した次の設定を実行します。

### （UNIX ベースのプラットフォームのみ）Unicode フォントのサポートの有効化（WebKit のみ） {#enable-support-for-unicode-fonts-webkit-only}

Unicode フォントを、使用しているシステムに応じて、次のいずれかのディレクトリにコピーします。

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType（Solaris™）

>[!NOTE]
>
>* Red Hat® Enterprise Linux® 6.x 以降で courier フォントは使用できません。courier フォントをインストールするには、 font-ibm-type1-1.0.3.zip アーカイブをダウンロードします。 /usr/share/fonts にあるアーカイブを抽出します。 /usr/share/X11/fonts から/usr/share/fonts へのシンボリックリンクを作成します。
>* Html2PdfSvc/bin ディレクトリと/usr/share/fonts ディレクトリから、すべての.lst フォントキャッシュファイルを削除します。
>* /usr/lib/X11/fonts ディレクトリと/usr/share/fonts ディレクトリが存在することを確認します。 ディレクトリが存在しない場合は、ln コマンドを使用して/usr/share/X11/fonts から/usr/lib/X11/fonts へのシンボリックリンクを作成し、/usr/share/fonts から/usr/share/X11/fonts への別のシンボリックリンクを作成します。 また、courier フォントが/usr/lib/X11/fonts で使用可能であることを確認してください。
>* すべてのフォント（Unicode および非 Unicode）が /usr/share/fonts または /usr/share/X11/fonts ディレクトリで使用できることを確認してください。
>* PDF Generator サービスを非 root ユーザーとして実行する場合は、すべてのフォントディレクトリへの読み取りおよび書き込みアクセス権を非 root ユーザーに与えます。
>* 新しいフォントをフォントフォルダーにインストールしたときは、AEM Forms インスタンスを再起動してください。
>

## AEM Forms アドオンパッケージのインストール {#install-aem-forms-add-on-package}

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。このパッケージには、AEM Forms Document Services およびその他のAEM Forms機能が含まれています。 次の手順を実行してパッケージをインストールします。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適したパッケージの名前をタップし、「**[!UICONTROL EULA 利用規約に同意する]**」を選択して、「**[!UICONTROL ダウンロード]**」をタップします。
1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja)を開き、「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択して「**[!UICONTROL インストール]**」をクリックします。

   [AEM Forms リリース](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)の記事に記載されている直接リンクからパッケージをダウンロードすることもできます。

1. パッケージのインストールが完了したら、AEM インスタンスを再起動します。**その際、すぐにサーバーを停止しないでください。** AEM Forms サーバーを停止する前に、ServiceEvent REGISTERED メッセージと ServiceEvent UNREGISTERED メッセージが `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log ファイルに表示されなくなり、ログファイルが安定した状態になるまで待ちます。

## インストール後の設定 {#post-installation-configurations}

### RSA/BouncyCastle ライブラリ用のブート委任の設定  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. AEM インスタンスを停止します。[AEM インストールディレクトリ]¥crx-quickstart¥conf フォルダーに移動します。sling.properties ファイルを開いて編集します。

   `[AEM installation directory]\crx-quickstart\bin\start.bat` を使用して AEM インスタンスを起動する場合は、`[AEM_root]\crx-quickstart\` にある sling.properties 編集します。

1. 次のプロパティを sling.properties ファイルに追加します。

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. （AIX® のみ）以下のプロパティを sling.properties ファイルに追加します。

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. ファイルを保存して閉じます。

### フォントマネージャーサービスの設定  {#configuring-the-font-manager-service}

1. 管理者として「[AEM Configuration Manager](http://localhost:4502/system/console/configMgr)」にログインします。
1. **[!UICONTROL CQ-DAM-Handler-Gibson Font Managers]** サービスを探して開きます。システムフォント、Adobe サーバーフォント、カスタマーフォントの各ディレクトリのパスを指定します。「**[!UICONTROL 保存]**」をクリックします。

   >[!NOTE]
   >
   >アドビ システムズ社以外が提供しているフォントを使用するユーザーの権利は、それらのフォントを所有する会社が提供する使用許諾契約書に拘束されるもので、アドビソフトウェアを使用するための使用許諾契約書は適用されません。アドビ以外が提供しているフォントをアドビのソフトウェアで使用する前に、適用されるすべてのアドビ以外の使用許諾契約書に準拠していることを確認してください。特に、サーバー環境でフォントを使用する際は注意が必要です。
   >新しいフォントをフォントフォルダーにインストールしたときは、AEM Forms インスタンスを再起動してください。
   >

### PDF Generator サービスを実行するためのローカルユーザーアカウントの設定  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

PDF Generator サービスを実行するには、ローカルユーザーのアカウントが必要です。ローカルユーザーを作成する手順については、「[Windows のユーザー アカウントを作成する](https://support.microsoft.com/ja-jp/help/13951/windows-create-user-account)」または「UNIX ベースのプラットフォームでユーザーアカウントを作成する」を参照してください。

1. [AEM Forms PDF Generator の設定](http://localhost:4502/libs/fd/pdfg/config/ui.html)ページを開きます。

1. 「**[!UICONTROL ユーザーアカウント]**」タブでローカルユーザーのアカウントの認証情報を入力し、「**[!UICONTROL 送信]**」をクリックします。Microsoft® Windows のプロンプトが表示されたら、ユーザーにアクセスを許可します。正常に追加されると、設定されたユーザーが「**[!UICONTROL ユーザーアカウント]**」タブの「**[!UICONTROL ユーザーアカウント]**」セクションに表示されます。

### タイムアウトの設定 {#configure-the-time-out-settings}

1. [AEM Configuration Manager](http://localhost:4502/system/console/configMgr) で、**[!UICONTROL Jacorb ORB Provider]** サービスを開きます。

   次のプロパティを「**[!UICONTROL Custom Properties.name]**」フィールドに追加し、「**[!UICONTROL 保存]**」をクリックします。これで、保留中の応答タイムアウト（「CORBA クライアントのタイムアウト」とも呼ばれます）が 600 秒に設定されます。

   `jacorb.connection.client.pending_reply_timeout=600000`

1. AEM オーサーインスタンスにログインし、**[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL ツール]**／**[!UICONTROL Forms]**／**[!UICONTROL PDF Generator を設定]**&#x200B;に移動します。デフォルトの URL は <http://localhost:4502/libs/fd/pdfg/config/ui.html> です。

   を開きます。 **[!UICONTROL 一般設定]** 「 」タブをタブに移動し、環境に応じて次のフィールドの値を変更します。

<table>
 <tbody>
  <tr>
   <td>フィールド</td>
   <td>説明</td>
   <td>デフォルト値</td>
  </tr>
  <tr>
   <td>サーバーコンバージョンタイムアウト</td>
   <td>PDFG 変換は、サーバー変換タイムアウトで定義された秒数の間アクティブになります</td>
   <td>270 秒<br /> </td>
  </tr>
  <tr>
   <td>PDFG クリーンアップスキャン秒</td>
   <td>変換後の操作の実行に必要な秒数。<br /> </td>
   <td>3600 秒</td>
  </tr>
  <tr>
   <td>ジョブ有効期限秒</td>
   <td>変換サービスがPDF Generatorを実行できる期間。 「Job Expiration Seconds」の値が「PDFG Cleanup Scan Seconds」の値よりも大きいことを確認してください。</td>
   <td>7200 秒</td>
  </tr>
 </tbody>
</table>

### （Windows のみ）PDF Generator サービス用 Acrobat の設定 {#configure-acrobat-for-the-pdf-generator-service}

Microsoft® Windows では、PDF Generator サービスは Adobe Acrobat を使用して、サポートしているファイル形式を PDF ドキュメントに変換します。以下の手順を実行して、Adobe Acrobat を PDF Generator サービスに設定します。

1. Acrobat を開き、「**[!UICONTROL 編集]**」／「**[!UICONTROL 環境設定]**」／「**[!UICONTROL Updater]**」を選択します。「アップデートの有無をチェック」で「**[!UICONTROL アップデートを自動的にインストール]**」のチェックを解除し、「**[!UICONTROL OK]**」をクリックします。Acrobat を終了します。
1. システム上の PDF ドキュメントをダブルクリックします。Acrobatを初めて起動すると、ログイン、ようこそ画面、EULA のダイアログボックスが表示されます。 [PDF Generator] を使用するように設定されているすべてのユーザに対して、これらのダイアログボックスを閉じます。
1. PDF Generator ユーティリティのバッチファイルを実行して、Adobe Acrobat を PDF Generator サービス用に設定します。

   1. [AEM パッケージマネージャー](http://localhost:4502/crx/packmgr/index.jsp)を開き、`adobe-aemfd-pdfg-common-pkg-[version].zip` ファイルをパッケージマネージャーからダウンロードします。
   1. ダウンロードした.zip ファイルを解凍します。 管理者権限でコマンドプロンプトを開きます。
   1. `[extracted-zip-file]\jcr_root\etc\packages\day\cq60\fd\adobe-aemds-common-pkg-[version]\jcr_root\etc\packages\day\cq60\fd\` に移動します。
   1. `adobe-aemfd-pdfg-common-pkg-[version]` を解凍します。
   1. `[downloaded-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]` ディレクトリに移動します。次のバッチファイルを実行します。

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat が PDF Generator サービスを実行するように設定されます。

1. [System Readiness Tool（SRT）](#SRT)を実行して、Acrobat のインストールを検証します。

### （Windows のみ）HTML から PDF への変換のためのプライマリルートの設定 {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

PDF Generator サービスは、HTML ファイルを PDF ドキュメントに変換する複数のルート（Webkit、Acrobat WebCapture（Windows のみ）および PhantomJS）を提供します。Adobeは PhantomJS ルートを使用することをお勧めします。動的コンテンツを処理する機能を持ち、32 ビットライブラリに依存しないか、追加のフォントが必要ないからです。 また、PhantomJS ルートは、変換を実行するために sudo または root アクセスを必要としません。

HTMLからPDFへの変換のデフォルトの主ルートは Webkit です。 変換ルートを変更するには：

1. AEM オーサーインスタンスで、「**[!UICONTROL ツール]**」／「**[!UICONTROL フォーム]**」／「**[!UICONTROL PDF Generator を設定]**」に移動します。

1. 「**[!UICONTROL 一般的な設定]**」タブで、「**[!UICONTROL HTML を PDF へ変換するプライマリルート]**」ドロップダウンから希望の変換ルートを選択します。

### グローバル Trust Store の初期化 {#intialize-global-trust-store}

Trust Store の管理を使用すると、電子署名と証明書認証の検証のために、サーバーで信頼する証明書の読み込み、編集、削除を行うことができます。 任意の数の証明書を読み込み、書き出すことができます。 証明書が読み込まれたら、信頼設定と Trust Store の種類を編集できます。 Trust Store を初期化するには、以下の手順を実行します。

1. AEM Forms インスタンスに管理者としてログインします。
1. **[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL Trust Store]** に移動します。
1. 「**[!UICONTROL Trust Store を作成]**」をクリックします。パスワードを設定して「**[!UICONTROL 保存]**」をタップします。

### 証明書拡張およびReaderサービス用の証明書を設定する {#set-up-certificates-for-reader-extension-and-encryption-service}

DocAssurance サービスは PDF ドキュメントに使用権限を適用できます。PDF ドキュメントに使用権限を適用するには、証明書を設定します。

証明書を設定する前に、次が揃っていることを確認します。

* 証明書ファイル (.pfx)。

* 証明書と共に提供された秘密鍵のパスワード。

* 秘密鍵のエイリアス。Java keytool コマンドを実行し、秘密鍵エイリアスを表示します。
  `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* キーストアファイルのパスワード。 アドビの Reader Extensions 証明書を使用している場合、Keystore ファイルのパスワードは常に秘密鍵のパスワードと同一です。

証明書を設定するには、以下の手順を実行します。

1. AEM オーサーインスタンスに管理者としてログインします。「**[!UICONTROL ツール]**」／「**[!UICONTROL セキュリティ]**」／「**[!UICONTROL ユーザー]**」に移動します。
1. ユーザーアカウントの&#x200B;**[!UICONTROL 名前]**&#x200B;フィールドをクリックします。**[!UICONTROL ユーザー設定を編集]**&#x200B;ページが開きます。AEM オーサーインスタンスでは、証明書は KeyStore にあります。KeyStore をまだ作成していない場合は、「**[!UICONTROL KeyStore を作成]**」をクリックして、KeyStore の新しいパスワードを設定します。KeyStore がサーバーに既にある場合は、この手順をスキップします。アドビの Reader Extensions 証明書を使用している場合、Keystore ファイルのパスワードは常に秘密鍵のパスワードと同一です。
1. **[!UICONTROL ユーザー設定を編集]** ページで「**[!UICONTROL キーストア]**」タブを選択します。「**[!UICONTROL 秘密鍵をキーストアファイルから追加]**」オプションを展開し、エイリアスを指定します。エイリアスは Reader Extensions の操作を実行する際に使用されます。
1. 証明書ファイルをアップロードするには、「**[!UICONTROL キーストアファイルを選択]**」をクリックし、&lt;filename>.pfx ファイルをアップロードします。

   **[!UICONTROL キーストアのパスワード]**、**[!UICONTROL 秘密鍵のパスワード]**、証明書に関連付けられている&#x200B;**[!UICONTROL 秘密鍵エイリアス]**&#x200B;を、各フィールドに追加します。「**[!UICONTROL 送信]**」をクリックします。

   >[!NOTE]
   >
   >実稼働環境では、評価用の資格情報を実稼働用の資格情報に置き換えます。期限切れの資格情報または評価用の資格情報を更新する前に、Reader Extensions の古い資格情報を削除してください。

1. **[!UICONTROL ユーザー設定を編集]** ページで「**[!UICONTROL 保存して閉じる]**」をクリックします。

### AES-256 を有効にする {#enable-aes}

PDFファイルに AES 256 暗号化を使用するには、Java Cryptography Extension(JCE)Unlimited Strength Jurisdiction Policy ファイルを取得してインストールします。 jre/lib/security フォルダーの local_policy.jar ファイルと US_export_policy.jar ファイルを置き換えます。 例えば、Sun JDK を使用している場合、ダウンロードしたファイルを `[JAVA_HOME]/jre/lib/security` フォルダーにコピーします。

Assembler サービスは、Reader拡張サービス、Signature サービス、Formsサービス、Output サービスに依存します。 次の手順を実行して、必要なサービスが起動および実行されていることを確認します。

1. 管理者として URL `https://'[server]:[port]'/system/console/bundles` にログインします。
1. 次のサービスを検索し、サービスが起動および実行されていることを確認します。

<table>
 <tbody>
  <tr>
   <th>サービス名</th>
   <th>バンドル名</th>
  </tr>
  <tr>
   <td>署名サービス</td>
   <td>adobe-aemfd-signatures</td>
  </tr>
  <tr>
   <td>Reader Extensions サービス</td>
   <td>com.adobe.aemfd.adobe-aemfd-readerextensions<br /> </td>
  </tr>
  <tr>
   <td>Forms サービス</td>
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector<br /> </td>
  </tr>
  <tr>
   <td>Output サービス</td>
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector</td>
  </tr>
 </tbody>
</table>

## 既知の問題とトラブルシューティング {#known-issues-and-troubleshooting}

* zip 形式の入力ファイルにファイル名が 2 バイト文字のHTMLファイルが含まれている場合、HTMLからPDFへの変換は失敗します。 この問題を回避するには、HTML・ファイルに名前を付ける際に 2 バイト文字を使用しないでください。

* UNIX ベースのオペレーティング・システムで、次の手順を実行して、見つからないライブラリを検索します。

1. `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/` に移動します。

1. 次のコマンドを実行して、PhantomJS が HTML から PDF への変換に必要とするすべてのライブラリを一覧表示します。

   `ldd phantomjs`

   次のコマンドを実行して、不足しているライブラリを一覧表示します。

   `ldd phantomjs | grep not`

1. 不足しているライブラリを手動でインストールします。

## System Readiness Tool（SRT） {#SRT}

[System Readiness ツール](#srt-configuration)は、PDF Generator 変換を実行するようにマシンが正しく設定されているかどうかを確認します。ツールは、指定されたパスでレポートを生成します。ツールを実行するには：

1. コマンドプロンプトを開き、`[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools` フォルダーに移動します。

1. コマンドプロンプトから次のコマンドを実行します。

   `java -jar forms-srt-[version].jar [Path_of_reports_folder] en`

   このコマンドは、レポートを生成し、 srt_config.yaml ファイルも作成します。SRT ツールのオプションを設定する場合に使用できます。 SRT ツールのオプションを設定するオプションです。

   >[!NOTE]
   >
   >* pdfgen.api ファイルが Acrobat プラグインフォルダーで使用できないことが System Readiness ツールから報告された場合は、pdfgen.api ファイルを `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]\plugins\x86_win32` ディレクトリから `[Acrobat_root]\Acrobat\plug_ins` ディレクトリにコピーします。

1. `[Path_of_reports_folder]` に移動します。SystemReadinessTool.html ファイルを開きます。レポートを検証して前述の問題を修正します。

### SRT ツールのオプションの設定 {#srt-configuration}

srt_config.yaml ファイルを使用して、SRT ツールの様々な設定を行うことができます。 ファイルの形式は次のとおりです。

```shell
   # =================================================================
   # SRT Configuration
   # =================================================================
   #Note - follow correct format to avoid parsing failures
   #for example, <param name>:<space><param value> 
   #locale: (mandatory field)Locale to be used for SRT. Supported locales [en/fr/de/ja].
   locale: en
   
   #aemTempDir: AEM Temp direcotry
   aemTempDir:
   
   #users: provide PDFG converting users list
   #users:
   # - user1
   # - user2
   users:
   
   #profile: select profile to run specific checks. Choose from [LCM], more will be added soon 
   profile:
   
   #outputDir: directory where output files will be saved
   outputDir:
```

* **Locale：**&#x200B;これは必須パラメーターです。英語（en）、ドイツ語（de）、フランス語（fr）、日本語（ja）をサポートしています。 デフォルト値は en です。OSGi 上の AEM Forms で実行される PDF Generator サービスには影響しません。
* **aemTempDir：**&#x200B;これはオプションのパラメーターです。Adobe Experience Manager の一時的な保存場所を指定します。
* **users：**&#x200B;これはオプションのパラメーターです。ユーザーを指定して、そのユーザーが PDF Generator の実行に必要なディレクトリに対する必要な権限と読み取り／書き込みアクセス権を持っているかどうかを確認できます。 ユーザーが指定されていない場合、ユーザー固有のチェックはスキップされ、失敗としてレポートに表示されます。
* **outputDir：** SRT レポートを保存する場所を指定します。 デフォルトの場所は、SRT ツールの現在の作業ディレクトリです。

## トラブルシューティング

SRT ツールが報告する問題をすべて修正した後でも問題が発生した場合は、次のチェックを実行します。

次のチェックを実行する前に、[System Readiness ツール](#SRT)がエラーを報告していないことを確認します。

+++ Adobe Acrobat

* Microsoft® Office（32 ビット）と Adobe Acrobat の[サポート対象バージョン](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)のみがインストールされ、ダイアログを開く操作がキャンセルされていることを確認します。
* Adobe Acrobat アップデートサービスが無効になっていることを確認します。
* [Acrobat_for_PDFG_Configuration.bat](#configure-acrobat-for-the-pdf-generator-service) バッチファイルが管理者権限で実行されたことを確認します。
* PDF Generator ユーザーが PDF 設定 UI に追加されていることを確認します。
* [プロセスレベルトークンの置き換え](#grant-the-replace-a-process-level-token-privilege)権限が PDF Generator ユーザーに追加されていることを確認します。
* Acrobat PDFMaker Office COM Addin が Microsoft Office アプリケーションで有効になっていることを確認します。

+++

+++OpenOffice

**Microsoft® Windows**

* Microsoft Office 32 ビット[サポート対象バージョン](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)のインストールが完了していること、およびすべてのアプリケーションでダイアログを開くことがキャンセルされていることを確認します。
* PDF Generator ユーザーが PDF 設定 UI に追加されていることを確認します。
* PDF Generator ユーザーが管理グループのメンバーであり、[プロセスレベルトークンの置き換え](#grant-the-replace-a-process-level-token-privilege)権限がそのユーザーに対して設定されていることを確認します。
* ユーザーが PDF Generator UI で設定されており、次のアクションを実行していることを確認します。
   1. Microsoft® Windows に、PDF Generator ユーザーでログインします。
   1. Microsoft® Office または OpenOffice アプリケーションを開き、すべてのダイアログをキャンセルします。
   1. AdobePDF をデフォルトのプリンターとして設定します。
   1. Acrobat を PDF ファイルのデフォルトプログラムに設定します。
   1. Microsoft Office アプリケーションのファイル／印刷および Acrobat リボンを使用して手動変換を実行し、すべてのダイアログをキャンセルします。
   1. winword.exe、powerpoint.exe、excel.exe など、変換に関連するすべてのプロセスを終了します。
   1. AEM Forms サーバーを再起動します。

**Linux®**

* OpenOffice の[サポート対象バージョン](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)をインストールします。AEM Formsは、32 ビットバージョンと 64 ビットバージョンの両方をサポートしています。  インストール後、すべての OpenOffice アプリケーションを開き、すべてのダイアログウィンドウをキャンセルして、アプリケーションを閉じます。 アプリケーションを再度開き、OpenOffice アプリケーションを開く際にダイアログボックスが表示されないことを確認します。

* 環境変数 `OpenOffice_PATH` を作成し、[コンソール](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/)または dt（デバイスツリー）プロファイルに設定されている OpenOffice のインストール先を指すように設定します。
* OpenOffice のインストールに問題がある場合は、OpenOffice のインストールに必要な [32 ビットライブラリ](#extrarequirements)が利用可能であることを確認します。

+++

+++HTML から PDF への変換に関する問題

* フォントディレクトリが PDF Generator の設定 UI に追加されていることを確認します。

**Linux および Solaris（PhantomJS 変換ルート）**

* Webkit ベースの HTMLToPDF 変換に 32 ビットライブラリ（libicudata.so.42）が使用可能であり、64 ビット（libicudata.so.42）が PhantomJS ベースの HTMLToPDF 変換に使用可能であることを確認します。

* 次のコマンドを実行して、phantomjs に不足しているライブラリを一覧表示します。

  ```
  ldd phantomjs | grep not
  ```

**Linux® および Solaris™（WebKit 変換ルート）**

* `/usr/lib/X11/fonts` および `/usr/share/fonts` ディレクトリが存在することを確認します。ディレクトリが存在しない場合は、`/usr/share/X11/fonts` から `/usr/lib/X11/fonts` にシンボリックリンクを作成し、別のシンボリックリンクを `/usr/share/fonts` から `/usr/share/X11/fonts`.に作成します。

  ```
  ln -s /usr/share/fonts /usr/share/X11/fonts
  
  ln -s /usr/share/X11/fonts /usr/lib/X11/fonts
  ```

* IBM のフォントが usr/share/fonts の下にコピーされていることを確認します。
* GHOST 脆弱性が修正済みの glibc がマシン上で利用可能であることを確認します。デフォルトのパッケージマネージャーを使用して、glibc の最新バージョンにアップデートします。これには GHOST 脆弱性の修正も含まれます。
* 最新バージョンの 32 ビット lib curl、libcrypto、libssl ライブラリがシステムにインストールされていることを確認します。また、それぞれのライブラリの最新版（32 ビット）を指すシンボリックリンク `/usr/lib/libcurl.so`（AIX® では libcurl.a）、`/usr/lib/libcrypto.so`（AIX® では libcrypto.a）および `/usr/lib/libssl.so`（AIX® では libssl.a）も作成します。

* 以下の手順を実行して、IBM® SSL ソケットプロバイダーを設定します。
   1. java.security ファイルを `<WAS_Installed_JAVA>\jre\lib\security` から AEM Forms Server 上の任意の場所にコピーします。デフォルトの場所は `<WAS_Installed>\Appserver\java_[version]\jre\lib\security`.です。

   1. コピー先の java.security ファイルを編集し、デフォルトの SSL Socket factories を JSSE2 factories に変更します（WebSphere® の代わりに JSSE2 factories を使用します）。

      次のデフォルトの JSSE socket factories を変更します。

      ```
      #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

      以下に置き換えます。

      ```
      ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

+++

+++ PDF Generator（PDFG）ユーザーを追加できない

* Microsoft® Visual C++ 2012 x86 および Microsoft® Visual C++ 2013 x86（32 ビット）の再頒布可能パッケージが Windows にインストールされていることを確認します。

+++

+++自動化テストの失敗

* Microsoft® Office および OpenOffice の場合は、（各ユーザーと同様に）1 つ以上の変換を手動で実行し、変換時にダイアログがポップアップ表示されないようにします。ダイアログが表示された場合は、ダイアログを閉じます。自動変換時に、このようなダイアログが表示されないようにします。

* OSGi 環境の AEM Forms で自動処理を実行する前に、テストパッケージがインストールされ、アクティブになっていることを確認します。

+++

+++複数ユーザー変換の失敗

* 特定のユーザーが変換に失敗したかどうかを確認するには、サーバーログを確認します。（プロセスエクスプローラは、異なるユーザーの実行中のプロセスを確認するのに役立ちます）

* PDF Generator 用に設定したユーザーに、ローカルの管理者権限が付与されていることを確認します。

* PDF Generator ユーザーに、LC 一時ユーザーと PDFG 一時ユーザーに対する読み取り、書き込み、実行の権限があることを確認します。

* Microsoft® Office および OpenOffice の場合は、（各ユーザーと同様に）1 つ以上の変換を手動で実行し、変換時にダイアログがポップアップ表示されないようにします。ダイアログが表示された場合は、ダイアログを閉じます。自動変換時に、このようなダイアログが表示されないようにします。

* サンプル変換を実行します。

+++

+++ AEM Forms Server にインストールされた Adobe Acrobat のライセンスの有効期限

* Adobe Acrobat の既存のライセンスを持っていて、そのライセンスが期限切れの場合、[最新バージョンの Adobe Application Manager をダウンロード](https://helpx.adobe.com/jp/creative-suite/kb/aam-troubleshoot-download-install.html)し、シリアル番号を移行します。[シリアル番号の移行](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number)前に以下のことを行います。

   * 次のコマンドを使用して prov.xml を生成し、[シリアル番号の移行](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number)の記事で提供されているコマンドの代わりに、prov.xml ファイルを使用して既存のインストールを再シリアル化します。

         ```
         
         adobe_prtk --tool=VolumeSerialize --generate --serial=&lt;serialnum> [--leid=&lt;LEID>] [--regsuppress=ss] [--eulasuppress] [--locales=limited list of locales in xx_XX format or ALL>] [--provfile=&lt;Absolute path to prov.xml>]
         
         ```
     
   * パッケージをボリュームシリアライズします（prov.xml ファイルと新しいシリアルを使用して既存のインストールを再シリアライズします）。PRTK インストールフォルダーから次のコマンドを管理者として実行し、クライアントマシンにデプロイされたパッケージをシリアライズしてアクティベートします。

         ```
         adobe_prtk --tool=VolumeSerialize --provfile=C:\prov.xml –stream
         
         ```
     
* 大規模インストールの場合は、[Acrobat Customization Wizard](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/index.html) をクリックして、以前のバージョンの Reader と Acrobat を削除します。インストーラーをカスタマイズし、組織のすべてのマシンにデプロイします。

+++

+++ AEM Forms サーバーはオフラインまたはセキュアな環境にあり、インターネットを使用して Acrobat をアクティブ化できません。

* アドビ製品の初回起動から 7 日以内にオンラインにアクセスして、オンラインでのアクティベーションと登録を完了したり、インターネット対応デバイスと製品のシリアル番号を使用してこのプロセスを完了したりできます。手順について詳しくは、[オフラインアクティベーション](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=jp)を参照してください。

+++

+++ Windows Server 上で Word または Excel ファイルを PDF に変換できない

ユーザーが Word ファイルまたは Excel ファイルを Microsoft Windows Server 上で PDF に変換しようとすると、次のエラーが発生します。

*プライマリコンバーターからのエラーメッセージ：
ALC-PDG-015-003-システムは入力ファイルを開けません。 ファイルを再度送信するか、システム管理者に問い合わせてください。*

この問題を解決するには、[Word ファイルまたは Excel ファイルを Windows Server 上で PDF に変換できません](/help/forms/using/disable-uac-for-pdfgconfiguration.md)を参照してください。


## 次の手順 {#next-steps}

作業中のAEM Forms Document Services 環境がある。 ドキュメントサービスは、以下で使用できます。  

* [OSGi 上の Forms 中心のワークフロー](/help/forms/using/aem-forms-workflow.md)
* [監視フォルダー](/help/forms/using/watched-folder-in-aem-forms.md)
* [ドキュメントサービス API](/help/forms/using/aem-document-services-programmatically.md)
