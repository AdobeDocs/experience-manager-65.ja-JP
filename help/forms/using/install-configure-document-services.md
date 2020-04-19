---
title: ドキュメントサービスのインストールと設定
seo-title: ドキュメントサービスのインストールと設定
description: AEM Forms ドキュメントサービスをインストールして、PDF ドキュメントを作成、アセンブル、配布、アーカイブし、デジタル署名を追加してドキュメントへのアクセスを制限し、バーコード化されたフォームをデコードしましょう。
seo-description: AEM Forms ドキュメントサービスをインストールして、PDF ドキュメントを作成、アセンブル、配布、アーカイブし、デジタル署名を追加してドキュメントへのアクセスを制限し、バーコード化されたフォームをデコードしましょう。
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
translation-type: tm+mt
source-git-commit: a6afa740fa7897ef2629ca7ba07d6a1e08113957

---


# ドキュメントサービスのインストールと設定 {#installing-and-configuring-document-services}

AEM Forms は、PDF ドキュメントの作成、アセンブル、配布、アーカイブ、ドキュメントへのアクセスを制限するためのデジタル署名の追加、バーコード化されたフォームのデコードなど、様々なドキュメントレベルの操作を実現する一連の OSGi サービスを提供します。これらのサービスは、AEM Forms のアドオンパッケージに含まれており、ドキュメントサービスと総称されます。利用可能なドキュメントサービスのリストとその主な機能は次のとおりです。

* **Assemblerサービス：** PDFドキュメントとXDP画像を組み合わせ、再配置および拡張し、PDF画像に関する情報を取得できます。ドキュメント PDF ドキュメントを PDF/A 標準に変換して検証します。また、PDF フォーム、XML フォームを PDF/A-1b、PDF/A-2b および PDFA/A-3b に変換します。For more information, see [Assembler Service](/help/forms/using/assembler-service.md).

* **Convert PDFサービス：** PDFドキュメントをPostScriptまたは画像ファイル（JPEG、JPEG 2000、PNGおよびTIFF）に変換できます。 For more information, see [ConvertPDF Service](/help/forms/using/using-convertpdf-service.md).

* **Barcoded Formsサービス：** バーコードの電子画像からデータを抽出できます。 このサービスでは、少なくとも 1 つのバーコードを含んだ TIFF ファイルおよび PDF ファイルを入力として受け取り、バーコードデータを抽出します。For more information, see [Barcoded Forms Service](/help/forms/using/using-barcoded-forms-service.md).

* **DocAssuranceサービス：** ドキュメントの暗号化と復号化、追加の使用権限でのAdobe Readerの機能拡張、ドキュメントへの電子署名の追加を行うことができます。 DocAssurance サービスには、3 つのサービス（Signature、Encryption および Reader Extention）があります。For more information, see [DocAssurance Service](/help/forms/using/overview-aem-document-services.md).

* **Encryptionサービス：** 暗号化と復号化をドキュメントします。 ドキュメントを暗号化すると、その内容は判読できなくなります。許可されたユーザーはドキュメントを解読して、コンテンツにアクセスできます。For more information, see [Encryption Service](/help/forms/using/overview-aem-document-services.md#encryption-service).

* **Formsサービス：** 通常はForms Designerで作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャクライアントアプリケーションを作成できます。 Formsサービスは、PDFフォームに作成したフォームデザインをすべてレンダリングします。ドキュメント For more information, see [Forms Service](/help/forms/using/forms-service.md).

* **Outputサービス：** PDF、レーザードキュメント形式、ラベルプリンター形式など、様々な形式のプリンターを作成できます。 レーザープリンター形式には、PostScript と Printer Control Language（PCL）があります。For more information, see [Output Service](/help/forms/using/output-service.md).

* **PDF Generatorサービス：** PDF Generatorサービスは、ネイティブファイル形式をPDFに変換するAPIを提供します。 また、PDF を他のファイル形式に変換し、PDF ドキュメントのサイズを最適化します。For more information, see [PDF Generator Service](aem-document-services-programmatically.md#pdfgeneratorservice).

* **Reader Extensionサービス：** 追加の使用権限でAdobe Readerの機能を拡張して、組織でインタラクティブPDFドキュメントを簡単に共有できるようにします。 このサービスにより、PDF ドキュメントを Adobe Reader で開いた場合には使用できない機能（ドキュメントへのコメントの追加、フォームへの入力、ドキュメントの保存など）がアクティブになります。For more information, see [Reader Extension Service](/help/forms/using/overview-aem-document-services.md#reader-extension-service).

* **Signatureサービス：** AEMサーバー上で電子署名やドキュメントを使用できます。 例えば、通常、Signature サービスは次のような状況で使用されます。

   * Acrobat または Adobe Reader でフォームを開くユーザーにフォームが送信される前に、AEM サーバーでフォームが認証される場合。
   * Acrobat または Adobe Reader を使用してフォームに追加された署名が、AEM サーバーで検証される場合。
   * AEM サーバーが公証人に代わってフォームに署名する場合。
   Signature サービスは、Trust Store に格納されている証明書および秘密鍵証明書にアクセスしますFor more information, see [Signature Service](/help/forms/using/aem-document-services-programmatically.md).

AEM Formsは強力なエンタープライズクラスのプラットフォームで、ドキュメントサービスはAEM Formsの機能の1つに過ぎません。 機能の完全な一覧については、「[AEM Forms の概要](/help/forms/using/introduction-aem-forms.md)」を参照してください。

## デプロイメントトポロジ {#deployment-topology}

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。通常、AEM Forms ドキュメントサービスを実行するには、1 つの AEM インスタンス（オーサーインスタンスまたはパブリッシュインスタンス）があれば十分です。AEM Forms ドキュメントサービスを実行するには、次のトポロジをお勧めします。トポロジについて詳しくは、「[AEM Forms のアーキテクチャとデプロイメントトポロジ](/help/forms/using/aem-forms-architecture-deployment.md)」を参照してください。

![AEM Forms のアーキテクチャとデプロイメントトポロジー](do-not-localize/document-services.png)

>[!NOTE]
>
>AEM Forms では、設定されたすべての機能を 1 台のサーバーで実行できますが、運用規模の計画、負荷分散、特定の機能を実行するための専用サーバーのセットアップを、実稼働環境で行う必要があります。例えば、PDF Generator サービスを使用して、1 日に数千のページと複数のアダプティブフォームをデータ取得用に変換する環境の場合、PDF Generator サービスとアダプティブフォームの機能を実行するための AEM Forms サーバーを個別にセットアップする必要があります。これにより、パフォーマンスが最適化され、各サーバーを個別にスケーリングできるようになります。

## システム要件 {#system-requirements}

AEM Forms ドキュメントサービスのインストールおよび設定に進む前に、次のことを確認する必要があります。

* ハードウェアおよびソフトウェアのインフラが正しいこと。サポート対象のハードウェアおよびソフトウェアの詳細な一覧については、「[技術的要件](/help/sites-deploying/technical-requirements.md)」を参照してください。

* AEM インスタンスのインストールパスに空白が含まれていないこと。
* AEM インスタンスが稼働していること。AEM の用語では、「インスタンス」は、サーバー上でオーサーモードまたはパブリッシュモードで実行されている AEM のコピーのことです。通常、AEM Forms ドキュメントサービスを実行するには、1 つの AEM インスタンス（オーサーインスタンスまたはパブリッシュインスタンス）があれば十分です。

   * **オーサー：**&#x200B;コンテンツを作成、アップロード、編集し、Web サイトを管理する AEM インスタンス。公開する準備ができたコンテンツは、パブリッシュインスタンスにレプリケートされます。
   * **パブリッシュ：**&#x200B;発行されたコンテンツをインターネットまたは社内ネットワークを通じて公開する AEM インスタンス。

* メモリ要件が満たされていること。AEM Forms アドオンパッケージには次の一時領域が必要となります。

   * Microsoft Windows ベースのインストールの場合、15 GB の一時的な空きスペースが必要です。
   * Unix ベースのインストールの場合、6 GB の一時的な空きスペースが必要です。

* PDF GeneratorでMicrosoft WindowsおよびLinux上で変換を実行するために必要なクライアントソフトウェアがインストールされています。

   * **Microsoft Windows**: [Microsoft](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)Officeまたは [Apache OpenOfficeのインストール](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux**:Apache OpenOfficeのイ [ンストール](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* Microsoft Windowsの場合、PDF Generatorは、HTMLファイルをPDFドキュメントに変換するためのWebKit、Acrobat WebCapture、PhantomJSの変換ルートをサポートします。
>* UNIXベースのオペレーティングシステムでは、PDF Generatorは、HTMLファイルをPDFドキュメントに変換するWebKitおよびPhantomJS変換ルートをサポートします。
>



### UNIXベースのオペレーティング・システムに関する追加要件 {#extrarequirements}

Unix ベースのオペレーティングシステムを使用する場合は、それぞれのオペレーティングシステムのインストールメディアから、次のパッケージをインストールしてください。

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

* **（PDF Generator のみ）** 32 ビット版の libcurl、libcrypto および libssl ライブラリをインストールし、以下のシンボリックリンクを作成します。シンボリックリンクは、以下のとおりそれぞれのライブラリの最新バージョンを指すようにします。

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **（PDF Generator のみ）** PDF Generator サービスは、HTML ファイルを PDF ドキュメントに変換するため、WebKit および PhantomJS の各ルートをサポートしています。PhantomJS ルートの変換を有効にするには、下記の 64 ビットライブラリをインストールします。通常、これらのライブラリは既にインストールされています。見つからないライブラリがある場合は、手動でインストールします。

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

「プリインストール設定」節に記載されている設定は、PDF Generator サービスにのみ適用されます。PDF Generator サービスを設定していない場合は、「プリインストール設定」節をスキップできます。

### Adobe Acrobat とサードパーティアプリケーションのインストール {#install-adobe-acrobat-and-third-party-applications}

PDF Generatorサービスを使用して、Microsoft Word、Microsoft Excel、Microsoft PowerPoint、OpenOffice、WordPerfect X7、Adobe Acrobatなどのネイティブファイル形式をPDFドキュメントに変換する場合は、これらのアプリケーションがAEM Formsサーバーにインストールされていることを確認します。

>[!NOTE]
>
>* Adobe Acrobat、Microsoft Word、Excel および Powerpoint は、Microsoft Windows でのみ使用できます。UNIX ベースのオペレーティングシステムを使用している場合は、OpenOffice をインストールすることで、リッチテキストファイルやサポートされている Microsoft Office ファイルを PDF ドキュメントに変換します。
>* PDF Generator サービスを使用できるすべてのユーザーに対して、Adobe Acrobat およびサードパーティソフトウェアのインストール後に表示されるすべてのダイアログボックスを閉じます。
>* インストールされているすべてのソフトウェアを少なくとも 1 回起動します。PDF Generatorサービスを使用するように設定されているすべてのユーザーのすべてのダイアログボックスを閉じます。
>



Acrobat をインストールしてから、Microsoft Word を開きます。「**Acrobat**」タブで「**PDFを作成**」をクリックし、マシン上にある .doc または .docx のファイルを PDF ドキュメントに変換します。変換が成功すれば、AEM Forms が PDF Generator サービスで Acrobat を使用する準備が整っています。

### 環境変数の設定 {#setup-environment-variables}

32 ビットおよび 64 ビットの Java Development Kit、サードパーティアプリケーション、Adobe Acrobat の環境変数を設定します。環境変数には、対応するアプリケーションの開始に使用される実行可能ファイルの絶対パスを含める必要があります。例えば、次の表は、いくつかのアプリケーションのリスト環境変数を示しています。

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>アプリケーション</strong></p> </td> 
   <td><p><strong>環境変数</strong></p> </td> 
   <td><p><strong>例</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>JDK (64-bit)</strong></p> </td> 
   <td><p>JAVA_HOME</p> </td> 
   <td><p>C:¥Program Files¥Java¥jdk1.8.0_74</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>JDK (32-bit)</strong></p> </td> 
   <td><p>JAVA_HOME_32</p> </td> 
   <td><p>C:¥Program Files (x86)¥Java¥jdk1.8.0_74</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>Adobe Acrobat</strong></p> </td> 
   <td><p>Acrobat_PATH</p> </td> 
   <td><p>C:\Program Files (x86)\Adobe\Acrobat 2015\Acrobat\Acrobat.exe</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>メモ帳</strong></p> </td> 
   <td><p>Notepad_PATH</p> </td> 
   <td><p>C:¥WINDOWS¥notepad.exe<br /> <strong></strong></p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>OpenOffice</strong></p> </td> 
   <td><p>OpenOffice_PATH</p> </td> 
   <td><p>C:¥Program Files (x86)¥OpenOffice.org 4</p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>* すべての環境変数とそれぞれのパスでは、大文字と小文字が区別されます。
>* JAVA_HOME、JAVA_HOME_32およびAcrobat_PATH（Windowsのみ）は必須の環境変数です。
>* 環境変数 OpenOffice_PATH は、実行ファイルではなく、インストールフォルダーのパスに設定します。
>* Word、PowerPoint、Excel、ProjectなどのMicrosoft OfficeアプリケーションやAutoCAD用の環境変数は設定しないでください。 これらのアプリケーションがサーバーにインストールされている場合は、Generate PDF サービスが自動的にこれらのアプリケーションを起動します。
>* UNIX ベースのプラットフォームでは、OpenOffice を /root としてインストールします。OpenOffice が root としてインストールされていないと、PDF Generator サービスは OpenOffice ドキュメントを PDF ドキュメントに変換できません。OpenOffice を非 root ユーザーとしてインストールして実行する必要がある場合は、非 root ユーザーに sudo 権限を与えます。
>* UNIXベースのプラットフォームでOpenOfficeを使用している場合は、次のコマンドを実行してパス変数を設定します。\
   >  `export OpenOffice_PATH=/opt/openoffice.org4`
>



### （IBM WebSphere のみ）IBM SSL ソケットプロバイダーの設定{#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

次の手順を実行して、IBM SSLソケットプロバイダーを設定します。

1. java.security ファイルのコピーを作成します。ファイルのデフォルトの場所はです `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`。
1. コピーした java.security ファイルを開いて編集します。
1. デフォルトの SSL ソケットファクトリを、デフォルトの IBM WebSphere ファクトリではなく JSSE2 ファクトリを使用するように変更します。

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

### （Windowsのみ）インクと手書きサービスのインストールの構成 {#configure-install-ink-and-handwriting-service}

Microsoft Windows Server を実行している場合、インクおよび手書きサービスを設定します。サービスを使うには、Microsoft Office のインキング機能を使用する Microsoft PowerPoint ファイルを開くことが必要です。

1. サーバーマネージャーを開きます。クイック起動バーの&#x200B;**[!UICONTROL サーバーマネージャー]**&#x200B;アイコンをクリックします。
1. Click **[!UICONTROL Add Features]** in the **[!UICONTROL Features]** menu. Select the **[!UICONTROL Ink and Handwriting Services]** check box.
1. 「**[!UICONTROL インクおよび手書きサービス]**」が&#x200B;**[!UICONTROL 機能の選択]**&#x200B;ダイアログボックスで選択されます。「**[!UICONTROL インストール]**」をクリックするとサービスがインストールされます。

### (Windows Only) Configure the file block settings for Microsoft Office {#configure-the-file-block-settings-for-microsoft-office}

Microsoft Office のセキュリティセンターの設定を変更して、PDF Generator サービスが古いバージョンの Microsoft Office で作成されたファイルを変換できるようにします。

1. Microsoft Office のアプリケーションを開きます。例えば、Microsoft Word などです。**[!UICONTROL ファイル]**／**[!UICONTROL オプション]**&#x200B;に移動します。オプションダイアログボックスが表示されます。

1. 「**[!UICONTROL セキュリティ センター]**」をクリックし、「**[!UICONTROL セキュリティ センターの設定]**」をクリックします。
1. 「**[!UICONTROL セキュリティ センターの設定]**」で、「**[!UICONTROL ファイル制限機能の設定]**」をクリックします。
1. In the **[!UICONTROL File Type]** list, deselect **[!UICONTROL Open]** for the file type that the PDF Generator service should be allowed to convert to PDF documents.

### （Windowsのみ）「プロセスレベルトークンの置換」権限の付与 {#grant-the-replace-a-process-level-token-privilege}

アプリケーションサーバーを起動したユーザーアカウントは、「**プロセス レベル トークンの置き換え**」権限が必要です。ローカルシステムアカウントには、デフォルトで「**プロセス レベル トークンの置き換え**」権限があります。ローカル管理グループのユーザーが運用しているサーバーでは、権限は明示的に付与されなければなりません。次の手順を実行して権限を付与します：

1. Microsoft Windows のグループポリシーエディターを開きます。To open the Group Policy Editor, click **[!UICONTROL Start]**, type **gpedit.msc** in the Start Search box, and click **[!UICONTROL Group Policy Editor]**.
1. **[!UICONTROL ローカル コンピューター ポリシー]**／**[!UICONTROL コンピューターの構成]**／**[!UICONTROL Windows の設定]**／**[!UICONTROL セキュリティの設定]**／**[!UICONTROL ローカル ポリシー]**／**[!UICONTROL ユーザー権利の割り当て]**&#x200B;に移動して、**[!UICONTROL Administrators グループが含まれるように「プロセス レベル トークンの置き換え]**」ポリシーを編集します。
1. 「プロセス レベル トークンの置き換え」エントリにユーザーを追加します。

### (Windows Only) Enable the PDF Generator service for non-administrators {#enable-the-pdf-generator-service-for-non-administrators}

管理者以外のユーザーに対して、PDF Generator サービスの使用を許可することができます。通常は、管理者権限を持つユーザーのみがこのサービスを実行できます。

1. 環境変数PDFG_NON_ADMIN_ENABLEDを作成します。
1. 環境変数の値を TRUE に設定します。
1. AEM Forms のインスタンスを再起動します。

### （Windowsのみ）ユーザーアカウント制御(UAC)の無効化 {#disable-user-account-control-uac}

1. To access the System Configuration Utility, go to **[!UICONTROL Start > Run]** and then enter **[!UICONTROL MSCONFIG]**.
1. Click the **[!UICONTROL Tools]** tab and scroll down and select **[!UICONTROL Change UAC Settings]**. 「**[!UICONTROL 起動]**」をクリックして新しいウィンドウでコマンドを実行します。
1. スライダーを「通知しない」のレベルに設定します。完了したら、コマンドウィンドウを閉じ、システム構成ウィンドウを閉じます。
1. レジストリ設定で UAC が 0 に設定されていることを検証します。次の手順を実行して確認します。

   1. Microsoft は、レジストリを変更する前にバックアップをとっておくことを推奨しています。詳しい手順については、「[Windows でのレジストリのバックアップと復元方法](https://support.microsoft.com/ja-jp/help/322756)」を参照してください。
   1. Microsoft Windows のレジストリエディターを開きます。レジストリエディターを開くには、「スタート／ファイル名を指定して実行」に移動し、「regedit」と入力して「OK」をクリックします。
   1. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\` に移動します。EnableLUA の値が 0 に設定されていることを確認します。
   1. **EnableLUA** の値が 0 に設定されていることを確認します。値が 0 に設定されていない場合は、0 に変更します。レジストリエディターを終了します。

1. コンピューターを再起動します。

### （Windowsのみ）エラーレポートサービスの無効化 {#disable-error-reporting-service}

Windows Server上のPDF Generatorサービスを使用してドキュメントをPDFに変換する際、Windows Serverで、実行ファイルに問題が発生し、閉じる必要があると報告されることがあります。 ただし、PDF 変換はバックグラウンドで続行されるため、影響を与えません。

エラーを受信しないようにするために、Windows エラー報告を無効にすることができます。For more information on disabling error reporting, see [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

### （Windowsのみ）HTMLからPDFへの変換の設定 {#configure-html-to-pdf-conversion}

PDF Generatorサービスは、HTMLファイルをPDFドキュメントに変換するWebKit、WebCapture、PhantomJSのルートまたはメソッドを提供します。 Windows で WebKit および Acrobat WebCapture ルートの変換を有効にするには、Unicode フォントを %windir%¥fonts ディレクトリにコピーします。

>[!NOTE]
>
> フォントフォルダーに新しいフォントをインストールする場合は、必ずAEM Formsインスタンスを再起動します。


### （UNIXベースのプラットフォームのみ）HTMLからPDFへの変換の追加設定 {#extra-configurations-for-html-to-pdf-conversion}

UNIX ベースのプラットフォーム上の PDF Generator サービスは、HTML ファイルを PDF ドキュメントに変換するため、WebKit および PhantomJS の各ルートをサポートしています。HTML から PDF への変換を有効にするには、以下から目的の変換ルートに該当する設定を行います。

### （UNIXベースのプラットフォームのみ）Unicodeフォントのサポートを有効にする（WebKitのみ） {#enable-support-for-unicode-fonts-webkit-only}

Unicode フォントを、使用しているシステムに応じて、次のいずれかのディレクトリにコピーします。

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType（Solaris）

>[!NOTE]
>
>* RedHat Enterprise Linux 6.x 以降で courier フォントは使用できません。courier フォントをインストールするには、font-ibm-type1-1.0.3.zip アーカイブをダウンロードしてください。/usr/share/fonts でアーカイブを抽出します。/usr/share/X11/fonts から /usr/share/fonts へのシンボリックリンクを作成します。
>* Html2PdfSvc/bin と /usr/share/fonts のディレクトリから、.lstフォントのキャッシュをすべて削除します。
>* /usr/lib/X11/fonts および /usr/share/fonts ディレクトリが存在することを確認してください。このディレクトリが存在しない場合は、ln コマンドを使用して /usr/share/X11/fonts から /usr/lib/X11/fonts へのシンボリックリンク、さらに /usr/share/fonts から /usr/share/X11/fonts への別のシンボリックリンクを作成します。また、courier フォントが使用可能であることを /usr/lib/X11/fonts で確認してください。。
>* すべてのフォント（Unicode および非 Unicode）が /usr/share/fonts or /usr/share/X11/fonts ディレクトリで使用できることを確認してください。
>* PDF Generator サービスを非 root ユーザーとして実行する場合は、すべてのフォントディレクトリへの読み取りおよび書き込みアクセス権を非 root ユーザーに与えます。
>* フォントフォルダーに新しいフォントをインストールする場合は、必ずAEM Formsインスタンスを再起動します。
>



## AEM Forms アドオンパッケージのインストール {#install-aem-forms-add-on-package}

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。このパッケージには、AEM Forms ドキュメントサービスおよびその他の AEM Forms 機能が含まれています。次の手順を実行してパッケージをインストールします。

1. [AEM サーバー](http://localhost:4502)に管理者としてログインし、「[パッケージ共有](http://localhost:4502/crx/packageshare)」を開きます。パッケージ共有にログインするには、Adobe ID が必要です。

1. [AEM パッケージ共有](http://localhost:4502/crx/packageshare/login.html)で **[!UICONTROL AEM 6.4 Forms add-on packages]** を検索し、お使いのオペレーティングシステムに対応するパッケージをクリックして、「**[!UICONTROL ダウンロード]**」をクリックします。ライセンス使用許諾契約書を読んでから同意し、「**[!UICONTROL OK]**」をクリックします。ダウンロードが開始します。ダウンロードが完了したら、パッケージの横に「**[!UICONTROL ダウンロード済み]**」というテキストが表示されます。

   バージョン番号を使用してアドオンパッケージを検索することもできます。最新のパッケージのバージョン番号については、「[AEM Forms リリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)」の記事を参照してください。

1. ダウンロードが完了したら、「**[!UICONTROL ダウンロード済み]**」をクリックします。パッケージマネージャーに切り替わります。In the package manager, search the downloaded package, and click **[!UICONTROL Install]**.

   「[AEM Forms リリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)」記事に記載された直接リンクからパッケージを手動でダウンロードする場合は、パッケージマネージャーにログインし、「**[!UICONTROL パッケージをアップロード]**」をクリックし、ダウンロード済みパッケージを選択して「アップロード」をクリックします。After the package is uploaded, click package name, and click **[!UICONTROL Install]**.

1. パッケージのインストールが完了したら、AEM インスタンスを再起動するよう指示されます。**その際、すぐにサーバーを停止しないでください。** AEM Formsサーバーを停止する前に、ServiceEvent REGISTEREDおよびServiceEvent UNREGISTEREDメッセージが `[AEM-Installation-Directory]/crx-quickstart/logs/error`.logファイルに表示されなくなり、ログが安定するまで待ちます。

## インストール後の設定 {#post-installation-configurations}

### RSA/BouncyCastle ライブラリ用のブート委任の設定  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. AEM インスタンスを停止して [AEMのインストールディレクトリ\crx-quickstart\conf\ folderに移動]します。sling.propertiesファイルを開いて編集します。

   `[AEM installation directory]\crx-quickstart\bin\start.bat` を使用して AEM インスタンスを起動する場合は、`[AEM_root]\crx-quickstart\` フォルダー内の sling.properties ファイルを編集用として開きます。

1. 以下のプロパティを sling.properties ファイルに追加します。 

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. （AIXのみ）sling.properties追加ファイルの次のプロパティ。

   ```
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1.  ファイルを保存して閉じます。

### フォントマネージャーサービスの設定  {#configuring-the-font-manager-service}

1. Log in to [AEM Configuration Manager](http://localhost:4502/system/console/configMgr) as an administrator.
1. **[!UICONTROL CQ-DAM-Handler-Gibson Font Managersサービスを探して開きます]** 。 System Fonts、Adobe Server Fonts、Customer Fontsの各ディレクトリのパスを指定します。 「**[!UICONTROL 保存]**」をクリックします。

   >[!NOTE]
   >
   >アドビ システムズ社以外が提供しているフォントを使用するユーザーの権利は、それらのフォントを所有する会社が提供する使用許諾契約書に拘束されるもので、アドビソフトウェアを使用するための使用許諾契約書は適用されません。アドビ システムズ社以外が提供しているフォントをアドビソフトウェアで使用する前に、適用される、アドビ システムズ社以外の使用許諾契約書すべてに準拠していることを確認してください。特に、サーバー環境でフォントを使用する際は注意が必要です。
   > 新しいフォントをフォントフォルダーにインストールしたら、AEM Forms インスタンスを再起動してください。

### PDF Generator サービスを実行するためのローカルユーザーアカウントの設定  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

PDF Generator サービスを実行するには、ローカルユーザーのアカウントが必要です。For steps to create a local user, see [Create a user account in Windows](https://support.microsoft.com/ja-jp/help/13951/windows-create-user-account) or [create a user account in UNIX-based platforms](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/4/html/Step_by_Step_Guide/s1-starting-create-account.html).

1. Open the [AEM Forms PDF Generator Configuration](http://localhost:4502/libs/fd/pdfg/config/ui.html) page.

1. In the **[!UICONTROL User Accounts]** tab, provide credentials of a local user account, and click **[!UICONTROL Submit]**. Microsoft Windows のプロンプトが表示されたら、ユーザーにアクセスを許可します。When added successfully, the configured user is displayed under the **[!UICONTROL Your user accounts]** section in the **[!UICONTROL User Accounts]** tab.

### タイムアウトの設定 {#configure-the-time-out-settings}

1. [AEM Configuration Managerで](http://localhost:4502/system/console/configMgr)、 **[!UICONTROL Jacorb ORB Providerサービスを探して開きます]** 。

   次のプロパティを「**[!UICONTROL Custom Properties.name]**」フィールドに追加し、「**[!UICONTROL 保存]**」をクリックします。保留中の応答タイムアウト（CORBAクライアントのタイムアウト）を600秒に設定します。

   `jacorb.connection.client.pending_reply_timeout=600000`

1. Log in to the AEM author instance and navigate to **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Forms]** > **[!UICONTROL Configure PDF Generator]**. デフォルトのURLはhttp://localhost:4502/libs/fd/pdfg/config/ui.htmlです。

   「**[!UICONTROL 一般的な設定]**」タブを開いて、自分の環境に合わせて次のフィールドの値を変更します。

<table> 
 <tbody> 
  <tr> 
   <td>フィールド</td> 
   <td>説明</td> 
   <td>デフォルト値</td> 
  </tr> 
  <tr> 
   <td>Server Conversion Timeout</td> 
   <td>PDFG変換は、サーバー変換のタイムアウトで定義された秒数だけアクティブなままです</td> 
   <td>270 秒<br /> </td> 
  </tr> 
  <tr> 
   <td>PDFG Cleanup Scan Seconds</td> 
   <td>変換後操作を実行するために必要な秒数<br /> </td> 
   <td>3600 秒</td> 
  </tr> 
  <tr> 
   <td>Job Expiration Seconds</td> 
   <td>PDF Generator サービスが変換を実行できる期間。「Job Expiration Seconds」の値が「PDFG Cleanup Scan Seconds」の値より大きいことを確認します。</td> 
   <td>7200 秒</td> 
  </tr> 
 </tbody> 
</table>

### (Windows only) Configure Acrobat for the PDF Generator service {#configure-acrobat-for-the-pdf-generator-service}

Microsoft Windows では、PDF Generator サービスは Adobe Acrobat を使用して、サポートされているファイル形式を PDF ドキュメントに変換します。次の手順を実行して、PDF Generatorサービス用のAdobe Acrobatを設定します。

1. Acrobat を開き、**[!UICONTROL 編集]**／**[!UICONTROL 環境設定／]** Updater **[!UICONTROL を選択します]**。In Check for updates, deselect **[!UICONTROL Automatically install updates]**, and click **[!UICONTROL OK]**. Acrobat を終了します。
1. 重複上のPDFドキュメントをクリックします。 Acrobat の初回起動時に、ログインのダイアログボックス、スタートアップスクリーンおよび EULA が表示されます。PDF Generator を使用できるすべてのユーザーに対して、このダイアログボックスを閉じます。
1. PDF Generator ユーティリティバッチファイルを実行して、Adobe Acrobat を PDF Generator サービス用に設定します。

   1. [AEM Package Managerを開き](http://localhost:4502/crx/packmgr/index.jsp) 、パッケージマネージ `adobe-aemfd-pdfg-common-pkg-[version].zip` ャーからファイルをダウンロードします。
   1. ダウンロードした.zip ファイルを解凍します。管理者権限でコマンドプロンプトを開きます。
   1. Navigate to the `[extracted-zip-file]\jcr_root\etc\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\scripts` directory. 次のバッチファイルを実行します。

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat が PDF Generator サービスを実行するように設定されます。

1. System Readiness Tool（SRT）を実行して、Acrobat インストールを検証します。このツールは、PDF Generatorの変換を実行するように装置が適切に設定されているかどうかを確認し、指定されたパスでレポートを生成します。

   1. コマンドプロンプトを開きます。`[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\etc\fd\ pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\srt` フォルダーに移動し、コマンドプロンプトから次のコマンドを実行します。

      `cscript SystemReadinessTool.vbs [Path_of_reports_folder] en`

      >[!NOTE]
      >
      >If the System Readiness Tool reports that the pdfgen.api file is not available in the acrobat plug-ins folder then copy the pdfgen.api file from the `[extracted-adobe-aemfd-pdfg-common-pkg]\plugins\x86_win32` directory to the `[Acrobat_root]\Acrobat\plug_ins` directory.

   1. `[Path_of_reports_folder]` に移動します。SystemReadinessTool.htmlファイルを開きます。 レポートを検証して前述の問題を修正します。

### （Windowsのみ）HTMLからPDFへの変換のプライマリルートの設定 {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

PDF Generator サービスは、Webkit、Acrobat WebCapture（Windows のみ）および PhantomJS の、HTML ファイルを PDF ドキュメントに変換する複数のルートを提供します。PhantomJSルートの使用をお勧めします。これは、PhantomJSルートは、動的コンテンツを処理する機能を備えており、32ビットライブラリや32ビットJDKに依存しないか、追加のフォントが必要ないからです。 また、PhantomJS ルートでは、変換を実行するために sudo または root アクセスは必要ありません。

HTML から PDF への変換のデフォルトの主要ルートは WebKit です。変換ルートを変更するには：

1. AEM オーサーインスタンスで、**[!UICONTROL ツール]**／**[!UICONTROL フォーム]**／**[!UICONTROL PDF Generator を設定]**&#x200B;に移動します。

1. In the **[!UICONTROL General Configuration]** tab, select the preferred conversion route from the **[!UICONTROL Primary Route for HTML to PDF conversions]** drop-down.

### グローバルTrust Storeの初期化 {#intialize-global-trust-store}

Trust Store の管理では、電子署名の検証および証明書認証のために、サーバーで信頼される証明書の読み込み、編集および削除を行うことができます。証明書はいくつでも読み込みと書き出しを行うことができます。証明書が読み込まれたら、信頼設定および Trust Store の種類を編集できます。次の手順を実行してTrust Storeを初期化します。

1. AEM Forms インスタンスに管理者としてログインします。
1. ツール/ **[!UICONTROL セキュリ]** ティ **[!UICONTROL /]** Trust Storeに移 **[!UICONTROL 動します]**。
1. 「TrustStoreを作 **[!UICONTROL 成」をクリックしま]**&#x200B;す。 パスワードを設定し、「保存」をタ **[!UICONTROL ップしま]**&#x200B;す。

### Reader 拡張機能および Encription サービス用の証明書を設定します。{#set-up-certificates-for-reader-extension-and-encryption-service}

DocAssurance サービスは PDF ドキュメントに使用権限を適用できます。PDF証明書に使用権限を適用するには、ドキュメントを設定します。

証明書の設定前に、以下が揃っていることを確認します。

* 証明書ファイル（.pfx）。

* 証明書ファイルとともに提供する秘密鍵パスワード。

* 秘密鍵のエイリアス。 Java keytoolコマンドを実行して、秘密鍵エイリアスを表示できます。
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* キーストアファイルのパスワード。アドビの Reader Extensions 証明書を使用している場合、キーストアファイルのパスワードは常に秘密鍵のパスワードと同一です。

次の手順を実行して、証明書を設定します。

1. AEM オーサーインスタンスに管理者としてログインします。**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL ユーザー]**&#x200B;に移動します。
1. ユーザーアカウントの「**[!UICONTROL 名前]**」フィールドをクリックします。「**[!UICONTROL ユーザー設定を編集]**」ページが開きます。AEM オーサーインスタンスでは証明書がキーストアに存在します。キーストアをまだ作成していない場合は、「**[!UICONTROL キーストアを作成]**」をクリックし、キーストアの新しいパスワードを設定します。サーバーに既にキーストアが含まれている場合は、この手順をスキップします。  アドビの Reader Extensions 証明書を使用している場合、キーストアファイルのパスワードは常に秘密鍵のパスワードと同一です。
1. ユーザー設 **[!UICONTROL 定を編集ページで]** 、「キーストア」タブを **[!UICONTROL 選択します]** 。 Expand the **[!UICONTROL Add Private Key from Key Store file]** option and provide an alias. エイリアスは Reader Extensions の操作を実行する際に使用されます。
1. 証明書ファイルをアップロードするには、「**[!UICONTROL キーストアファイルを選択]**」をクリックし、&lt;filename>.pfx ファイルをアップロードします。

   **[!UICONTROL キーストアのパスワード]**、**[!UICONTROL 秘密鍵のパスワード]**、および証明書に関連付けられている&#x200B;**[!UICONTROL 秘密鍵エイリアス]**&#x200B;を、各フィールドに追加します。「**[!UICONTROL 送信]**」をクリックします。

   >[!NOTE]
   >
   >* 実稼働環境では、評価用の資格情報を実稼働用の資格情報に置き換えます。期限切れの証明書または評価用の証明書を更新する前に、古いReader Extensions証明書を削除してください。


1. ユーザ **[!UICONTROL 設定を編集ページで]** 、「保 **[!UICONTROL 存して閉じる]** 」をクリックします。

### AES-256 を有効にする {#enable-aes}

PDF ファイルに AES 256 暗号化を使用するには、Java Cryptography Extension（JCE）Unlimited Strength Jurisdiction Policy ファイルを入手し、インストールします。jre/lib/security フォルダーの local_policy.jar と US_export_policy.jar ファイルを置き換えます。For example, if you are using Sun JDK, copy the downloaded files to the `[JAVA_HOME]/jre/lib/security` folder.

Assembler サービスは、Reader Extensions サービス、Signature サービス、Forms サービス、Output サービスに依存します。次の手順を実行し、必要なサービスが起動および実行していることを確認します。

1. Log in to URL `https://'[server]:[port]'/system/console/bundles` as an administrator.
1. 次のサービスを検索し、サービスが起動および実行していることを確認します。

<table> 
 <tbody> 
  <tr> 
   <th>サービス名</th> 
   <th>バンドル名</th> 
  </tr> 
  <tr> 
   <td>Signature サービス</td> 
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

* 入力用 zip ファイルにファイル名が 2 バイト文字の HTML ファイルが含まれている場合、HTML から PDF への変換は失敗します。この問題を回避するには、HTML ファイルに名前を付けるときに 2 バイト文字を使用しないようにします。

* UNIX ベースのオペレーティングシステムでは、以下を実行して不足しているライブラリを見つけます。

1. `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/` に移動します。

1. PhantomJS が HTML から PDF への変換に必要とするすべてのライブラリを一覧表示するには、次のコマンドを実行します。

   `ldd phantomjs`

   不足しているライブラリを一覧表示するには、次のコマンドを実行します。

   `ldd phantomjs | grep not`

1. 不足しているライブラリを手動でインストールします。

## 次の手順 {#next-steps}

これで、AEM Forms ドキュメントサービスの動作環境が用意できました。次の方法でドキュメントサービスを使用できます。

* [OSGi 上の Forms 中心のワークフロー](/help/forms/using/aem-forms-workflow.md)
* [監視フォルダー](/help/forms/using/watched-folder-in-aem-forms.md)
* [Document services API](/help/forms/using/aem-document-services-programmatically.md)

