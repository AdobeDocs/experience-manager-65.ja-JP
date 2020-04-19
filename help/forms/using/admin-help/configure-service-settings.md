---
title: サービス設定の指定
seo-title: サービス設定の指定
description: サービス設定の指定方法について説明します。
seo-description: サービス設定の指定方法について説明します。
uuid: e95425a4-62f6-473e-b21b-d081c432e02d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 2fab4b0c-e5db-47cd-b85a-4ff5ad6eb178
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# サービス設定の指定 {#configure-service-settings}

サービスの管理ページを使用して、AEM Forms に含まれる各サービスの設定を行うことができます。使用できる設定は、指定されているサービスによって異なります。

1. 管理コンソールで、サービス／アプリケーションおよびサービス／サービスの管理をクリックします。
1. 変更するサービスを停止しておきます（[サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)を参照してください）。
1. 設定するサービスの名前をクリックします。
1. サービスに「設定」タブがある場合は、このタブを使用してサービスの設定を変更します。詳しくは、以下のリンクを参照してください。

   >[!NOTE]
   >
   >サービスの管理ページに表示されるすべてのサービスに「設定」タブがあるわけではありません。作成したプロセスについて、Workbench でプロセスに設定パラメーターを追加した場合にのみ「設定」タブが表示されます（[Workbench ヘルプ](https://www.adobe.com/go/learn_aemforms_workbench_63)の「設定パラメーター」を参照）。


1. 「セキュリティ」タブをクリックして、サービスのセキュリティ設定を指定します。[サービスのセキュリティ設定の変更](configure-service-settings.md#modifying-security-settings-for-a-service)を参照してください。
1. サービスに「エンドポイント」タブがある場合は、このタブを使用してエンドポイント設定を変更します。[エンドポイントの管理](/help/forms/using/admin-help/adding-enabling-modifying-or-removing.md)を参照してください。
1. 「プーリング」タブをクリックして、プーリング設定を指定します。[サービスのプーリングの設定](configure-service-settings.md#configuring-pooling-for-a-service)を参照してください。
1. 「保存」をクリックして変更を保存するか、「キャンセル」をクリックして変更を破棄します。
1. サービス名の横にあるチェックボックスを選択し、「開始」をクリックしてサービスを再起動します。

## Audit Workflow サービスの設定 {#audit-workflow-service-settings}

Workbench には、実行時に処理されるプロセスインスタンスを記録し、記録を再生してプロセスの動作を観察できる機能が用意されています（[Workbench ヘルプ](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照）。forms サーバーのファイルシステム上のスペースを確保するために、保存するプロセス記録データの量を制限できます。Audit Workflow Service サービス（`AuditWorkflowService`）の次のプロパティを設定できます。

**maxNumberOfRecordingInstances:** 保存される記録の最大数。 保存の最大数に達すると、新しいレコードが作成されるときに最も古いレコードがファイルシステムから削除されます。このプロパティは、多数のレコードを作成する可能性が高いので、古いレコードを自動的に削除する場合に便利です。デフォルト値は 50 です。

**MaxNumberOfRecordingEntries:** 各記録に保存できるデータエントリの最大数です。 データエントリはプロセスの操作に関する情報です。一部のエントリは操作の実行ごとに保存されます。例えば、操作が開始されたかどうか、操作が完了したかどうか、操作を発生させるルートが完了したかどうか、などです。このプロパティは、プロセスに操作の実行が多数含まれる場合（例えば、永久ループが発生した場合など）に便利です。デフォルト値は 50 です。

## Barcoded Forms サービスの設定 {#barcoded-forms-service-settings}

The barcoded forms service `(BarcodedFormsService)` extracts barcode data from scanned images. このサービスは、バーコードフォーム（TIFF または PDF）を入力として受け取り、バーコードでエンコードされたデータのマシン表現を抽出します。

Barcoded Forms サービスでは、以下の設定を使用できます。

**Read Left:** 選択すると、バーコード画像が右から左に水平方向にスキャンされます。

**右読み：** 選択すると、バーコード画像が左から右に水平方向にスキャンされます。

**読み上げ：** 選択すると、バーコード画像が下から上に縦方向にスキャンされます。

**読み取り：** 選択すると、バーコード画像が上から下に縦方向にスキャンされます。

>[!NOTE]
>
>デフォルトでは、すべてのオプションが選択されています。フォームで適用されていないことが確実なバーコードの表示方法のみ、オプションを選択解除します。

**Base File Path:** 「Run XML File Job」操作と「Run Flat File Job」操作のバッチ入力および出力ファイルのパラメーターが解決される相対パス。 クラスター構成では、ベースファイルパスは、すべてのクラスターノードが読み取り/書き込みアクセス権を持つ共有ファイルシステムの場所である必要があります。

**データソース名：** バッチ処理ジョブの状態と履歴の情報を維持するために使用するデータソースの名前。 指定したデータソースは、グローバル(XA)トランザクションをサポートしている必要があります。

## Central Migration Bridge サービス（非推奨）の設定 {#central-migration-bridge-service-settings}

Central Migration Bridge サービス（`CentralMigrationBridge`）は Adobe Central Pro Output Server（Central）機能の一部を呼び出します（JFMERGE、JFTRANS、XMLIMPORT コマンドなど）。Central Migration Bridge サービスの操作により、AEM forms では以下の Central アセットを再使用できます。

* テンプレートデザイン(&amp;A;ast;.ifd)
* 出力テンプレート(&amp;ast;.mdf)
* データファイル（&amp;A;ast;.datファイル）
* プリアンブルファイル（&amp;ast;.preファイル）
* データ定義ファイル(&amp;A;ast;.tdf)

Central Migration Bridge サービスでは、以下の設定を使用できます。

**Central Install Directory:** Adobe Central 5.7がインストールされているディレクトリ。

## Content Repository Connector for EMC Documentum サービスの設定 {#content-repository-connector-for-emc-documentum-service-settings}

Content Repository Connector for EMC Documentum サービス（`EMCDocumentumContentRepositoryConnector`）を使用すると、Documentum リポジトリに保存されているコンテンツをインタラクティブに操作するプロセスを作成できます。

Content Repository Connector for EMC Documentum サービスでは、以下の設定を使用できます。

**Asset Link Object Default Path:** Documentumリポジトリ内の、アセットリンクオブジェクトを保存するためのパスのデフォルト部分。 実際のパスは、デフォルトパスと、AEM forms リポジトリのフォームテンプレートの位置で構成されます。

For example, if the default path is set to `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`, and the form template is stored in a folder `/Docbase/forms/`, the Asset Link object is stored at the following location:

`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects/Docbase/forms/`

The default value of this setting is `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`.

## Content Repository Connector for IBM FileNet サービスの設定 {#content-repository-connector-for-ibm-filenet-service-settings}

Content Repository Connector for IBM FileNet を使用すると、IBM FileNet リポジトリに保存されているコンテンツをインタラクティブに操作するプロセスを作成できます。

Content Repository Connector for IBM FileNet サービスでは、以下の設定を使用できます。

**Asset Link Object Default Path:** IBM FileNetリポジトリ内で、アセットリンクオブジェクトを保存するためのパスのデフォルト部分。 実際のパスは、デフォルトパスと、AEM forms リポジトリのフォームテンプレートの位置で構成されます。

For example, if the default path is set to `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`, and the form template is stored in a folder `/Docbase/forms/`, the Asset Link object is stored at the following location:

`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects/Docbase/forms/`

The default value of this setting is `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`.

## Convert PDF サービスの設定 {#convert-pdf-service-settings}

Convert PDF サービス（`ConvertPdfService`）は、PDF ドキュメントを PostScript および様々な画像形式（JPEG、JPEG 2000、PNG および TIFF）に変換します。PDF ドキュメントの PostScript への変換は、PostScript プリンターでの無人のサーバーベース印刷に便利です。PDF ドキュメントをサポートしていないコンテンツ管理システムでドキュメントをアーカイブする場合、PDF ドキュメントをマルチページ TIFF ファイルに変換するのが現実的です。

Convert PDF サービスでは、以下の設定を使用できます。

**トランザクションタイプ：** トランザクションコンテキストを操作に適用する方法を指定します。

**必須：** トランザクションコンテキストが存在する場合は、そのコンテキストをサポートします。それ以外の場合は、新しいトランザクションコンテキストが作成されます。 これがデフォルト値です。

**新規作成が必要：** 常に新しいトランザクションコンテキストを作成します。 アクティブなトランザクションコンテキストが存在する場合は、休止されます。

**トランザクションタイムアウト（秒）:** 操作をラップしているトランザクションがロールバックされるまでに、基になるトランザクションプロバイダーが待機する秒数。 既存のトランザクションコンテキストが適用されている場合、この値は無視されます。デフォルト値は 180 です。

**Threshold Resolution For Smoothing (in dpi):** テキスト、ラインアート、画像に対して「スムージングを適用」オプションを選択した場合に、これらの要素にスムージング（アンチエイリアス）を適用する画像解像度。

**テキストにスムージングを適用：** テキストのアンチエイリアスを制御します。 テキストのスムージングを無効にしてテキストをよりシャープにし、画面の拡大時に読みやすくするには、このチェックボックスをオフにします。

**ラインアートにスムージングを適用：** 直線の急な角度を削除するスムージングを適用します。

**画像にスムージングを適用：** 画像の急な変化を最小限に抑えるスムージングを適用します。

## Distiller サービスの設定 {#distiller-service-settings}

Distiller サービス（`DistillerService`）は、ネットワークを介して PostScript、Encapsulated PostScript（EPS）および PRN ファイルを PDF ファイルに変換できます。

Distiller サービスでは、以下の設定を使用できます。

**Adobe PDF設定：** 次の事前設定が、生成されるPDFに適用されます。

* 高品質印刷
* オーバーサイズページ
* PDFA 1b 2005 CMYK
* PDFA1b 2005 RGB
* PDFX1a 2001
* PDFX3 2002
* プレス品質
* 最小ファイルサイズ
* 標準

新しい設定を作成するには、PDF Generator ユーザーインターフェイスを使用します。

**セキュリティ設定：** 生成されたPDFドキュメントに適用される事前設定済みのセキュリティ設定。 デフォルト値は「セキュリティなし」です。PDF Generator を使用してセキュリティ設定を作成してから、ここに設定を入力する必要があります。

**プールサイズ：** プールの初期サイズ。 Distiller サービスがデプロイされると、サービス実装インスタンスが何個作成され、呼び出し要求を待機している空きプールに割り当てられるかが、この数値を使用して特定されます。そうすると、サービスコンテナでは、サービスインスタンスを初期化する必要なく、呼び出し要求に直ちに応答できます。

## Document Management サービスの設定 {#document-management-service-settings}

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES（非推奨）は LiveCycle と共にインストールされるコンテンツ管理システムです。Content Services では、ユーザーは人間中心のプロセスを設計、管理、監視および最適化することができます。Content Services（非推奨）のサポートは 2014 年 12 月 31 日をもって終了しています。[製品のライフサイクルに関するドキュメント](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)を参照してください。Content Services（非推奨）の設定について詳しくは、『[Content Services の管理](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf)』を参照してください。

Document Management サービス（`DocumentManagementService`）を使用すると、プロセスで Content Services（非推奨）のコンテンツ管理機能を使用できます。Document Management 操作には、コンテンツ管理システムのスペースとコンテンツを保守するために必要な基本的なタスクがあります。例えば、コンテンツのコピー、削除、移動、取得、および保存、スペースと関連付けの作成、コンテンツ属性の取得および設定などのタスクです。

Document Management サービスでは、以下の設定を使用できます。

**ストアスキーム：** コンテンツを保存する場所のスキーム。 デフォルト値はワークスペースです。

**HTTPポート：** Content Services（非推奨）へのアクセスに使用するポートです。 デフォルト値は 8080 です。

## Email サービスの設定 {#email-service-settings}

電子メールは通常、自動化されたプロセスの一部として、コンテンツの配布やステータス情報の提供に使用されます。Email サービス（`EmailService`）によって、プロセスでは電子メールメッセージを POP3 または IMAP サーバーから受信したり、SMTP サーバーに送信したりすることができます。

例えば、Email サービスを使用して、PDF フォームが添付された電子メールメッセージが送信されます。Email サービスは SMTP サーバーに接続され、添付ファイル付きの電子メールメッセージが送信されます。PDF フォームは、受信者がフォームの入力を完了すると「送信」をクリックできるように設計されています。「送信」をクリックすると、フォームは指定された電子メールサーバーに添付ファイルとして返されます。Email サービスは返された電子メールメッセージを取得して、完成したフォームをプロセスデータフォーム変数に格納します。

Email サービスでは、以下の設定を使用できます。

**SMTP Host:** 電子メールの送信に使用するSMTPサーバーのIPアドレスまたはURLです。

**SMTP Port Number:** SMTPサーバーへの接続に使用するポートです。

**SMTP Authenticate:** SMTPサーバーへの接続にユーザー認証が必要な場合に選択します。

**SMTP User:** SMTPサーバーへのログインに使用するユーザーアカウントのユーザー名です。

**SMTP Password:** SMTPユーザーアカウントに関連付けられているパスワードです。

**SMTP Transport Security:** SMTPサーバーへの接続に使用するセキュリティプロトコル：

* プロトコルを使用しない場合は「None」を選択します（データはクリアテキストで送信されます）
* Secure Sockets Layer プロトコルを使用する場合は「SSL」を選択します。
* Transport Layer Security を使用する場合は「TLS」を選択します。

**POP3/IMAP Host:** 電子メールの送信に使用するPOP3またはIMAPサーバーのIPアドレスまたはURLです。

**POP3/IMAP Username:** POP3またはIMAPサーバーへのログインに使用するユーザーアカウントのユーザー名です。

**POP3/IMAP Password:** POP3またはIMAPユーザーアカウントに関連付けられているパスワードです。

**POP3/IMAP Port Number:** POP3またはIMAPサーバーへの接続に使用するポートです。

**POP3/IMAP:** 電子メールの送受信に使用するプロトコルです。

**Receive Transport Security:** SMTPサーバーへの接続に使用するセキュリティプロトコル：

* プロトコルを使用しない場合は「None」を選択します（データはクリアテキストで送信されます）。
* Secure Sockets Layer プロトコルを使用する場合は「SSL」を選択します。
* Transport Layer Security を使用する場合は「TLS」を選択します。

## Encryption サービスの設定 {#encryption-service-settings}

Encryption サービス（`EncryptionService`）は、ドキュメントの暗号化および復号化を有効にします。ドキュメントを暗号化すると、その内容は判読できなくなります。許可されたユーザーはドキュメントを復号化して、コンテンツにアクセスできます。PDF ドキュメントがパスワードで暗号化されている場合、ユーザーは開くためのパスワードを指定しないと、Adobe Reader または Adobe Acrobat でドキュメントを表示できません。同じように、PDF ドキュメントが証明書で暗号化されている場合も、ユーザーが PDF ドキュメントを復号化するには、その PDF ドキュメントの暗号化に使用された証明書（秘密鍵）に対応した公開鍵が必要です。

Encryption サービスでは、以下の設定を使用できます。

**接続するデフォルトのLDAPサーバー：** ドキュメント暗号化の証明書を取得するために使用するLDAPサーバーのホスト名。

**接続するデフォルトのLDAPポート：** LDAPサーバーのポート番号。

**Default LDAP User Name:** LDAPサーバーで認証が必要な場合は、LDAPサーバーへの接続に使用するユーザー名を指定します。

**Default LDAP Password:** LDAPサーバーで認証が必要な場合は、LDAPサーバーへの接続に使用するユーザー名に対応するパスワードを指定します。

>[!NOTE]
>
>接続が SSL（LDAPS を使用）で保護されている場合は、単純な認証（ユーザー名とパスワード）のみを使用します。

**互換性モード：**

## FTP サービスの設定 {#ftp-service-settings}

 サービス（`FTP`FTP）を使用すると、プロセスで FTP サーバーをインタラクティブに操作できます。FTP サービスの操作によって、FTP サーバーからのファイルの取得、FTP サーバーへのファイルの配置、および FTP サーバーからのファイルの削除を行うことができます。例えば、プロセスから生成されたレポートなどのドキュメントを、配布のために FTP サーバーに保存することができます。また、プロセスにおける前の手順に基づいて、外部システムでファイルを生成することができます。プロセスの後続の手順では、ファイルを離れた場所に転送することができます。

FTP サービスでは、以下の設定を使用できます。

**デフォルトホスト：** FTPサーバーのIPアドレスまたはURL。

**デフォルトのポート：** FTPサーバーへの接続に使用するポート。 デフォルト値は 21 です。

**デフォルトのユーザー名：** FTPサーバーへのアクセスに使用できるユーザーアカウントの名前。 このサービスで要求される FTP 操作を実行するには、ユーザーアカウントに十分な権限が備わっている必要があります。

**デフォルトのパスワード：** FTPサーバーでの認証用に指定したユーザー名と共に使用するパスワードです。

## GeneratePDF サービスの設定 {#generate-pdf-service-settings}

Generate PDF サービス（`GeneratePDFService`）は、様々な種類の形式のファイルを PDF ドキュメントに変換し、PDF ドキュメントを様々な種類のファイル形式に変換します。

Generate PDF サービスでは、以下の設定を使用できます。

**Adobe PDF設定：** 変換ジョブに適用する、事前設定済みのAdobe PDF設定の名前です（これらの設定がAPI呼び出しパラメーターの一部として指定されていない場合）。 Adobe PDF 設定は、管理コンソールで、サービス／PDF Generator／Adobe PDF 設定をクリックして指定します。これらの設定は、PDFMaker ベースの変換の場合にのみ適用可能です。

**セキュリティ設定：** 変換ジョブに適用する事前設定済みのセキュリティ設定の名前（API呼び出しパラメーターの一部としてこれらの設定が指定されていない場合）。 セキュリティ設定は、管理コンソールで、サービス／PDF Generator／セキュリティ設定をクリックして指定します。

**ファイルタイプ設定：** 変換ジョブに適用するために事前設定されたファイルタイプ設定の名前（これらの設定がAPI呼び出しパラメーターの一部として指定されていない場合）。 ファイルタイプの設定は、管理コンソールで、サービス／PDF Generator／ファイルタイプごとの設定をクリックして指定します。

**Use Acrobat WebCapture（Windowsのみ）:** この設定がtrueの場合、Generate PDFサービスはAcrobat X Proを使用して、すべてのHTMLからPDFへの変換を行います。 これにより、HTML から生成される PDF ファイルの品質は改善されますが、パフォーマンスはやや低下します。デフォルト値は false です。

**Use Acrobat Image Conversion（Windowsのみ）:** この設定がtrueの場合、Generate PDFサービスはAcrobat X Proを使用して、すべての画像からPDFへの変換を行います。 この設定は、デフォルトの Pure Java 変換メカニズムで入力画像の大部分を正常に変換できない場合にのみ有用です。デフォルト値は false です。

**AcrobatベースのAutoCAD変換を有効にする（Windowsのみ）:** この設定がtrueの場合、Generate PDFサービスはAcrobat X Proを使用して、すべてのDWGからPDFへの変換を行います。 この設定が有用であるのは、AutoCAD がサーバーにインストールされていない場合や、AutoCAD 変換メカニズムではファイルを正常に変換できない場合のみです。

**式名に使用できない特殊文字を探す正規文字（Windowsのみ）:** ユーザーの名前に文字が含まれる場合に、「PDFの書き出し」および「PDFの最適化」操作の妨げとなる文字を指定します。

**ImageToPDF Pool Size:** Generate PDFサービスのデフォルト(Pure Java)の画像からPDFへのコンバーターのプールサイズです。 この設定により、Generate PDF サービスで実行できる画像から PDF への最大同時変換が制御されます。この設定のデフォルト値（シングルプロセッサーシステムの場合に推奨）は 3 です。マルチプロセッサーシステムでは、この値を増やすことができます。

**HTML to PDF Pool Size:** Generate PDFサービスのHTMLからPDFへのコンバーターのプールサイズです。 この設定により、Generate PDF サービスで実行できる HTML から PDF への最大同時変換が制御されます。この設定のデフォルト値（シングルプロセッサーシステムの場合に推奨）は 3 です。マルチプロセッサーシステムでは、この値を増やすことができます。

**OCR Pool Size:** PDF GeneratorがOCRに使用するPaperCaptureServiceのプールサイズです。 この設定のデフォルト値（シングルプロセッサーシステムの場合に推奨）は 3 です。マルチプロセッサーシステムでは、この値を増やすことができます。この設定は Windows システムでのみ有効です。

**Fallback Font Family For HTML To PDF Conversions:** 元のHTMLで使用されていたフォントがAEM formsドキュメントで使用できない場合にPDFサーバーで使用するフォントファミリーの名前。 変換対象の HTML ページで使用されているフォントが使用不可能なフォントである場合、ここでフォントファミリーを指定します。例えば、特定の地域の言語で作成されたページには、利用不可能なフォントが使用されていることがあります。

**ネイティブ変換の再試行ロジック** ：最初の変換に失敗した場合に、PDF生成再試行が制御されます。

**No retry**

最初の変換に失敗した場合、PDF 変換を再試行しません。

**Retry**

タイムアウトのしきい値に達したかどうかに関係なく、PDF 変換を再試行します。最初の試行までのデフォルトのタイムアウト時間は、270 秒です。

**Retry if time permits**

最初の変換に費やした時間が指定したタイムアウト時間より短かった場合に、PDF 変換を再試行します。例えば、タイムアウト時間が 270 秒で最初の変換に 200 秒を費やした場合、PDF Generator は変換を再試行します。最初の変換自体が 270 秒を費やした場合、変換は再試行されません。

## Guides ES4 Utilities サービスの設定 {#guides-es4-utilities-service-settings}

ガイドを作成すると、一部のリソース（ガイドの定義など）がガイドに埋め込まれます。リソースは、ローカルまたは AEM Forms サーバーに保存されているアプリケーションアセットへの参照として存在する場合もあります。ガイドにデータは含まれません。また、送信場所および入力の値は、すべての外部環境に適していません。

ほとんどの場合、デフォルトのガイドレンダリングサービスは、Workspace や他の外部環境に使用するガイドを準備するために適しています（Workbench のサービスビューでは、デフォルトのサービスは Guides (system)/Processes/Render Guide - 1.0 です）。Guide Utilities サービス（`GuidesUtility`）を使用すると、必要に応じてガイドをレンダリングするカスタマイズプロセスを作成できます。

Guide Utilities 操作を使用すると、以下のガイドレンダリングタスクをプロセスに追加できます。

* データをガイドの設定に使用できるかどうかを決定する
* ガイドデータを埋め込むか、リンクに変換する
* 参照されたコンテンツを、外部からアクセスできる URL に変換する
* HTML ドキュメントまたは他のラッパーの値を、外部からアクセスできる URL に置換または変換する
* 送信場所を設定する
* 入力値を指定する
* 参照されるコンテンツを表すパラメーターを作成する
* 別の設定を使用できる場合、別の設定を指定する

Guide Utilities サービスのデフォルト値はほとんどの使用例をサポートしています。ただし、必要に応じて以下の値を変更できます。

**publicPaths:** このオプションは非推奨です。 AEM Forms ではこのオプションを使用しないでください。

**pathInfoExpiryInSeconds:** クライアントからのパス情報の要求が期限切れになるまでの間隔。 初期設定は 1 です。

**collateralExpiryInSeconds:** クライアントからのコラテラルの要求が期限切れになるまでの間隔。 初期設定は 315576000 です。

**mismatchExpiryInSeconds:** eTag（エンティティタグ）が一致しない場合に、クライアントからのコラテラルの要求が期限切れになるまでの間隔。 （eTag は HTTP 応答ヘッダーです）。初期設定は 1 です。

**guideContext:** ガイドWebアプリケーションのコンテキストルートです。 ガイド Web アプリケーションを使用して値セットとマッチングします。デフォルトは /Guides/ です。

**secureRandomAlgorithm:** キーと識別子を生成する際に使用するアルゴリズムです。 この値は、SecureRandom Java クラスの getInstance メソッドに渡されます。デフォルトは SHA1PRNG です。

**idBytes:** キー識別子に使用するランダムバイト数。 初期設定は 6 です。

**macAlgorithm:** コラテラルURLの検証に使用するMAC（メッセージ認証コード）アルゴリズムです。 このメソッドは、Mac クラスの getInstance メソッドに渡されます。デフォルトは HmacSHA1 です。

**macRefreshIntervalInMinutes:** キーがアクティブな時間。 キーがアクティブになってこの時間が経過すると、新しいキーが生成されます。新しいキーがアクティブキーになります。以前のアクティブキーは、10% の更新間隔で保持されます。この動作によって、古いキーを使用して生成された URL は、キーが切り替わっても引き続き機能します。初期設定は 144000 です。

**macOverlapIntervalInMinutes:** 新しいキーが生成された後、前のキーが有効なままになる時間。 デフォルトは 1440 分（1 日）です。

**macKeySeed:** 保護されたURLを生成するためのシード値です。 これがオプションの場合は、キーは更新されません。異なるサーバーに同じシードを設定すると、これらのサーバーは互換性のある保護された URL を生成します。この値は、ロードバランサーの背後で複数の forms サーバーを使用している場合に便利です。文字と数字をランダムに組み合わせた文字列をシードとして入力してください。

### サーバークラスターでの Guides の使用 {#using-guides-in-a-server-cluster}

スティッキーセッションを使用しないサーバークラスターでのガイドのレンダリングは、NullPointerException が発生して失敗します。Guides 要求では、デフォルトで、要求を生成するサーバーに固有の保護された URL が利用されます。スティッキーセッションを使用するクラスターでは、要求がクラスター内のノードに届いた後、そのセッションまたはユーザー向けの後続するすべての要求がそのサーバーだけにルーティングされるので、順調に処理が進みます。スティッキーセッションを使用しないクラスターでは、後続する要求がクラスター内のどのサーバーにも届く可能性があります。要求が届いたサーバーが元のサーバーと異なる場合、保護された URL を解決できません。

スティッキーセッションを使用しないサーバークラスターで Guides を使用する場合は、GuidesUtility サービスの macKeySeed 値を設定した上で、クラスターを停止して再起動します。

macKeySeed 値は、保護された URL の生成に使用される乱数ジェネレーターのシード値です。この値を設定すると、各クラスターノードで乱数ジェネレーターが同様に初期化され、同じ保護された URL にアクセスできるようになります。このシード値には任意の乱数文字列を使用できます。

保護された URL を更新する必要がある場合は、macKeySeed 値を変更します。保護された URL の更新方法はセキュリティポリシーによって異なり、サーバーのマスタールートパスワードを変更するための更新ポリシーに類似しています。macSeedValue は、保護された URL に対するマスターパスワードと言えます。保護された URL の生成および取得で使用する新しい一意の乱数生成に、この値が使用されるからです。

macSeedValue が読み取られるのはシステム起動時だけなので、クラスターを再起動する必要があります。すべてのノードを再起動して、この値を読み取らせる必要があります。シード値を使用して内部的な乱数を初期化するために、各ノードがそれぞれ独立してこの値を使用するからです。

## JDBC サービスの設定 {#jdbc-service-settings}

JDBC サービス（`JdbcService`）を使用すると、プロセスにおいてデータベースとインタラクティブにやり取りを行えます。

JDBC サービスでは、以下の設定を使用できます。

**datasourceName:** データベースサーバーへの接続に使用するデータソースのJNDI名を表すstring値です。 データソースは、forms サーバーをホストするアプリケーションサーバー上に定義する必要があります。デフォルト値は AEM forms データベース用のデータソースの JNDI 名です。

## JMS サービスの設定 {#jms-service-settings}

 サービス（`JMS`JMS）を使用すると、ポイントツーポイントメッセージングとパブリッシュ／サブスクライブメッセージングの両方を実装する Java Messaging System（JMS）プロバイダーをインタラクティブに操作できます。

サービスを JMS プロバイダーおよび関連付けられている JNDI サービスと接続し、これらをインタラクティブに操作できるように、JMS サービスをデフォルトのプロパティを使用して設定します。サービスプロパティの値は、JBoss Application Server に基づいてデフォルト値に設定されています。別のアプリケーションサーバーを使用して AEM Forms をホストしている場合は、これらの値を変更してください。

JMS サービスでは、以下の設定を使用できます。

**プロバイダURL:** JNDIサービスプロバイダーのURL。 デフォルト値は、JBoss Application Server に基づいています。以下の URL は、AEM Forms によってサポートされるアプリケーションサーバーのデフォルト値です。

**JBoss:** `<server name>:1099`

**WebLogic:** `<server name>:7001`

**WebSphere:** `<server name>:2809`

**JNDI Username:** キューおよびトピック名の検索に使用されるJNDIサービスプロバイダーでの認証に使用するアカウントのユーザー名。 デフォルト値は「guest」です。

**JNDI Password:** 「JNDI Username」に指定されたユーザー名に関連付けられるパスワード。 デフォルト値は「guest」です。

**Initial Context Factory:** 初期コンテキストファクトリとして使用するJavaクラス。 JMS サービスではこのクラスが使用され、初期コンテキストが作成されます。初期コンテキストはトピックおよびキューの名前の解決の開始点になります。デフォルト値は、JBoss の JMS サービスの初期コンテキストファクトリです。以下のクラスは、AEM Forms によってサポートされるアプリケーションサーバーの初期コンテキストファクトリです。

**JBoss:** org.jnp.interfaces.NamingContextFactory

**WebLogic:** weblogic.jndi.WLInitialContextFactory

**WebSphere:** com.ibm.websphere.naming.WsnInitialContextFactory

**Connection Username:** 「Connection Username」に指定したユーザー名に関連付けられているパスワードです。 デフォルト値は「guest」です。

**接続パスワード：** 「Connection Username」に指定したユーザー名に関連付けられているパスワードです。 デフォルト値は「guest」です。

**その他のプロパティ：** JNDIサービスプロバイダーに渡すことのできるプロパティ名と値のペア。 これらのプロパティは、使用しているプロバイダーの実装と設定によって異なります。

The property name and value pairs are separated by semi-colons **;**. 例えば、以下のテキストでは、name1 と name2 という 2 つのプロパティ名にそれぞれ value1 と value2 の値が割り当てられています。

`name1=value1;name2=value2`

## LDAP サービスの設定 {#ldap-service-settings}

LDAP サービス（`LDAPService`）では、LDAP ディレクトリに対してクエリーを実行するための操作を提供します。LDAP ディレクトリは、通常、組織内のユーザー、グループおよびサービスについての情報を保存するために使用されます。

LDAP サービスでは、以下の設定を使用できます。

**Initial Context Factory:** コンテキストファクトリとして使用するJavaクラスです。 このクラスは、LDAP サーバーへの接続の作成に使用されます。デフォルト値は、ほとんどの LDAP サーバーに適切な「com.sun.jndi.ldap.LdapCtxFactory」です。

**プロバイダURL:** LDAPサービスへの接続に使用するURL。 The format of the value is `ldap://server name:port`

*server name* は、LDAP サーバーをホストするコンピューターの名前です。

*port* は、LDAP サービスによって使用される通信ポートです。デフォルト値は、LDAP 接続に使用される標準ポートの 389 です。

**ユーザー名：** LDAPサーバーへのログインに使用するユーザーアカウントのユーザー名。 ユーザーアカウントには、サーバーに接続して LDAP ディレクトリの情報を読み取るための権限が必要です。

Depending on the LDAP server, the user name could be a simple user name such as `myname` or a DN, such as `cn=myname,cn=users,dc=myorg`.

**パスワード：** 「ユーザー名」設定に指定したユーザー名に対応するパスワードです。

**その他のプロパティ：** LDAPサーバーに指定できるその他のプロパティと対応する値を表すstring値。 値は次の形式で入力します。

`property=value;property=value;...`

## Microsoft SharePoint Configuration サービスの設定 {#microsoft-sharepoint-configuration-service-settings}

The Microsoft SharePoint configuration service `(MSSharePointConfigService)`lets you specify credentials for the AEM forms user that has impersonation permissions. 他のユーザーとしての権限については、「[Connector for Microsoft SharePoint の設定](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html)」を参照してください。

Microsoft SharePoint Configuration サービスでは、以下の設定を使用できます。

* 仮装権限を持つユーザーのユーザー名
* 上記ユーザーのパスワード

**SSL(HTTPS)を有効にする：**

**有効期間：** このプロビジョニングプロファイルが有効で、クライアント上でキャッシュされる時間（秒）。 デフォルト値は86400（24時間）です。 クライアントアプリケーションがサーバーと同期し、指定時間が経過すると、クライアントアプリケーションはサーバーから新しいプロビジョニングプロファイルを要求します。

**暗号化：** モバイルデバイスに保存されたデータを暗号化するかどうかを指定します。

**Forms Application:** モバイルクライアントアプリケーションでForms機能を有効にします。 このオプションを選択すると、ユーザーはフォームを開いて、モバイルデバイスからプロセスを開始できます。

**タスクアプリ：** モバイルクライアントタスクでアプリケーション機能を有効にします。 このオプションを選択すると、ユーザーはモバイルデバイスからタスクリストにアクセスし、タスクを完了できます。

**Content Services Application:** モバイルクライアントアプリケーションでContent Services機能を有効にします。 この機能はiOSでのみ使用できます。 このオプションを選択すると、iPhoneおよびiPadのユーザーは、組織のWebDAVサーバーに保存されているファイルにアクセスできます。

**オフラインサポート：** サーバーに接続していない場合（例えば、セルの範囲を超えている場合や機内モードの場合）でも、モバイルクライアントアプリケーションを引き続き使用できます。 また、ユーザーは、モバイルデバイスでオフラインサポート設定を有効にする必要があります。 この機能は、AndroidおよびiOSデバイスで使用できます。 デフォルトでは、この機能はオフです。

>[!NOTE]
>
>オフラインサポートが有効になっていて、無効にした場合、ユーザーのプロビジョニングプロファイルは、オンラインになるとすぐに更新されます。 ユーザーがオフラインで作業している場合、保留中のタスクはすべてタスクリストに戻され、保留中のフォーム、タスク、検証エラーを含むフォームを含むキュー内のすべての項目がキューから削除されます。

**Android:** Androidデバイスからサーバーへの接続を許可します。

**Apple iOS:** iPhoneおよびiPadからサーバーへの接続を許可します。

**AIR:** Adobe AIR®ベースのアプリケーションを実行しているデバイスからサーバーに接続できるようにします。

**BlackBerry:** BlackBerryデバイスからサーバーへの接続を許可します。

**Android Microsoft Exchange ActiveSyncが必要：** AndroidデバイスにMicrosoft Exchange ActiveSyncポリシーマネージャー(EAS)をインストールし、アクティブにする必要があるかどうかを指定します。 このオプションを選択した場合、EASはAndroidデバイスに適用される必要があります。 このオプションを選択しない場合、他の要件は引き続き適用されますが、チェックは実行されません。

**AndroidのPINの最小長：** Androidデバイスには、PINまたはパスワードがこの長さ以上になるようにグローバル設定が必要です。 指定した長さのPINを持つだけでは不十分です。 PINの長さは、後でPINを削除または短縮できないように、システムによって適用される必要があります。 デフォルト値は 4 です。

**ワイプ前のAndroidの最大パスワード再試行数：** Androidデバイスには、指定された回数の無効なパスワードの試行後にシステムを消去するグローバル設定があります。 このグローバル設定は有効で、ここで指定した値以下です。 デフォルト値は 5 です。

**削除時のAndroidワイプ：** Androidデバイスでポリシー違反が発生した場合の動作を指定します。 このオプションを選択すると、アカウントが削除されます。 このオプションを選択しない場合、保存されているアカウントのパスワードとキャッシュされたデータが削除されます。 ユーザーがポリシー違反を修正するまで、同期は試行されません。

## Output サービスの設定 {#output-service-settings}

The Output service `(OutputService)`enables you to merge XML form data with a form design created in AEM forms Designer to create a document output stream in one of the following formats:

* PDF または PDF/A ドキュメント出力ストリーム
* Adobe PostScript 出力ストリーム
* Printer Control Language（PCL）出力ストリーム
* Zebra Programming Language（ZPL）出力ストリーム

出力ストリームは、ネットワークプリンター、ローカルプリンターまたはディスクファイルに送信できます。Output サービスをプロセスの一部として使用すると、出力ストリームを添付ファイルとして電子メールの受信者に送信することもできます。

Output サービスでは、以下の設定を使用できます。

**トランザクションタイプ：** トランザクションコンテキストを操作に適用する方法を指定します。

**必須：** 既にトランザクションコンテキストが存在する場合、それ以外の場合は、新しいトランザクションコンテキストが作成されます。 これがデフォルト値です。

**新規作成が必要：** 常に新しいトランザクションコンテキストを作成します。 アクティブなトランザクションコンテキストが存在する場合は、休止されます。

**トランザクションタイムアウト（秒）:** 操作をラップしているトランザクションがロールバックされるまで、基になるトランザクションプロバイダーが待機する秒数。 既存のトランザクションコンテキストが適用されている場合、この値は無視されます。

大型のデータファイルを処理する場合、またはビジー状態のサーバー上で操作する場合、状況によっては Output のサービスタイムアウトを長くする必要があります。タイムアウト値を変更するには、ハードウェアサーバーに十分なメモリがあり、Java Application Server ヒープがそのメモリを使用できることを確認します。デフォルト値は `180` です。

## PDFG Config サービスの設定 {#pdfg-config-service-settings}

PDFG Config サービス（`PDFGConfigService`）では、以下の設定を使用できます。

**User Job Options Directory:** Acrobat Pro Extendedにアクセス可能なジョブオプションファイルをCサービスが書き込むファイルシステムフォルダーのパスです。 The default value is [user.home]/Application Data/Adobe/Adobe PDF/Settings.

**PS Startup Directory:** Adobe Acrobat Distillerで必要な起動ファイルが保存されるファイルシステムフォルダーのパスです。 The default value is [user.home]/Application Data/Adobe/Adobe PDF/Distiller/Startup.

**PS Startup File:** Adobe Acrobat Distillerで必要な起動ファイルの名前。 デフォルト値は「example.ps」です。

**Server Conversion Timeout:** Generate PDFサービスおよびDistillerサービスの最大ジョブ変換タイムアウト（秒）です。 この設定により、config.xml ファイルおよび PDF Generator の管理コンソールページで指定できる最大変換タイムアウトが制限されます。デフォルト値は 270 です。

**Server Global Timeout:** PDF変換の実行時に、formsサーバーはタイムアウトの制限を考慮します。 この問題を解決するには、タイムアウトの値を設定します。

**Job Options Prefix:** ジョブオプションファイルに短い文字列を追加するためにGenerate PDFサービスで使用されるプレフィックスです。このファイルは、Acrobat Distillerで一時的に使用するために作成されます。 デフォルト値は「pdfg」です。

**Non Unicode Apps:** Unicodeに対応していないことがわかっているアプリケーション名のコンマ区切りリスト。 このリストには複数のアプリケーションの名前が事前に入力されており、それらのアプリケーションのサポートが PDF Generator で事前設定されています。Unicode に対応していない他のサードパーティアプリケーションでの PDF 変換へのサポートを追加する場合は、それらをこのリストに追加する必要があります。デフォルト値は「Autocad,Excel,PowerPoint,Project,Publisher,Visio,Word,WordPerfect」です。

**サーバースレッドプール数：** スパイダリング（メインページからアクセス可能なリンクページの変換）を伴うHTMLからPDFへの変換要求を処理するために、Generate PDFサービスが内部的に使用するスレッドプールのサイズを制御します。 デフォルト値は 20 です。

**PDFG Cleanup Scan Seconds:** 詳しくは、「Job Expirations Seconds」の節を参照してください。

**Job Expiration Seconds:** Generate PDFサービスは、入力ファイルが変換されるとすぐに削除します。 「PDFG Cleanup Scan Seconds」および「Job Expiration Seconds」によって決まる期間、出力ファイルを一時的に保存します。

「Job Expiration Seconds」設定では、どのくらい古いファイルまたは空のフォルダーを削除できるかを指定します。「PDFG Cleanup Scan Seconds」設定では、削除できるファイルの一時フォルダーをクリーンアップスレッドによってスキャンする頻度を指定します。

例えば、「Job Expiration Seconds」を 100 に設定し、「PDFG Cleanup Scan Seconds」を 200 に設定すると、クリーンアップスレッドは 200 秒ごとに実行され、100 秒以上古いファイルは削除されます。

「PDFG Cleanup Scan Seconds」のデフォルト値は `43200`（12 時間）です。「Job Expiration Seconds」のデフォルト値は `86400`（24 時間）です。

**デフォルトロケール：** Generate PDFサービスがデプロイされているサーバーのデフォルトのロケール（国+言語）を上書きするために使用します。 このパラメーターを指定しない場合、デフォルトのロケールは、サービスがデプロイされているオペレーティングシステムから判別されます。このパラメーターでは、API に返されるエラーメッセージの言語が制御されます。

## forms ワークフロー Data Services サービスの設定 {#forms-workflow-data-services-service-settings}

以下のサービスは Data Services を拡張し、Workspace でサーバーとの通信に使用されるアセンブラを公開します。アドビサポートからの指示がない限り、これらのサービスの設定オプションは変更しないでください。これらのサービスは、直接的なアクセスでの使用は意図されていません。

* `ProcessManagementLcdsAttachmentService`
* `ProcessManagementLcdsPropertyService`
* `ProcessManagementLcdsTaskService`

## Remoting サービスの設定 {#remoting-service-settings}

ほとんどのサービスは、AEM Forms Remoting（AEM Forms では廃止されています）でアクセスできるように設定されています。AEM Forms Remoting について詳しくは、「[AEM Forms によるプログラミング](https://adobe.com/go/learn_aemforms_programming_63)」を参照してください。

Remoting サービスでは、以下の設定を使用できます。

**Flexクライアント認証方法：** 呼び出されたサービスがセキュリティが有効な場合に、呼び出された操作で匿名呼び出しがサポートされず、クライアントが無効または無効な資格情報を渡すときに、サーバーがクライアントに返す応答のタイプを決定します。 「カスタム」または「基本」から選択します。デフォルト値は「基本」です。

**Allow Serialization Of Non-Serializable Classes:** ほとんどのAEM formsエンドポイントでは、呼び出しにSerializableクラスのみを使用できます。 それより前のバージョンでは、Remoting エンドポイントで Flex ベースのクライアントからの呼び出しに Serializable 以外のクラスを使用できました。APS11-15 で説明されているセキュリティ脆弱性を防止するため、この変更が行われました。Flex の Remoting エンドポイントで Serializable 以外のクラスを引き続き使用する場合は、このチェックボックスをオンにします。

## Repository サービスの設定 {#repository-service-settings}

Repository サービス（`RepositoryService`）は、リソースを保存および管理するためのサービスを AEM Forms に提供します。アプリケーションを作成するときは、アセットをファイルシステムではなくリポジトリにデプロイできます。アセットには、XML 形式、PDF 形式（Acrobat 形式を含む）、フォームのフラグメント、画像、プロファイル、ポリシー、SWF ファイル、DDX ファイル、XML スキーマ、WSDL ファイルおよびテストデータなど、任意のタイプのコラテラルが含まれます。

AEM Forms に含まれるデフォルトのリポジトリ、またはサードパーティのリポジトリ（EMC Documentum Content Server、IBM FileNet Content Manager または IBM Content Manager）を使用できます。

Repository Provider サービスは、プロバイダーサービスへのインターフェイスとして動作するサービス委任機能です。この機能を使用すると共通の API に接続できるので、ストレージ機能がどのプロバイダーサービスに実装されているのかを意識する必要はありません。RepositoryProvider サービスは、Repository サービスリソース用のデータベースストレージを備えています。

Repository サービスでは、以下の設定を使用できます。

**Provider Service:** サービスプロバイダーとして使用するストレージの名前。 デフォルト値は「RepositoryProviderService」です。

## Signature サービスの設定 {#signature-service-settings}

Signature サービス（`SignatureService`）を使用して、組織は配布および受信する PDF ドキュメントのセキュリティとプライバシーを保護できます。このサービスでは、電子署名と認証を使用して、ドキュメントが変更されないようにします。ドキュメントが変更されると、署名が破損します。セキュリティ機能がドキュメント自体に適用されるので、ドキュメントは、ファイアウォールの外でやり取りされるときでも、オフラインでダウンロードされるときでも、組織に返送されるときでも、そのライフサイクル全体でセキュリティ保護され、管理されます。

Signature サービスでは、以下の設定を使用できます。

**Name Of The Remote HSM SPI Service:** このオプションは、HSMがリモートコンピューターにインストールされている場合に使用します。 AEM Forms が 64 ビット Windows にインストールされていて、署名に HSM デバイスを使用する場合は、このオプションを指定します。

**Url Of The Remote HSM Web Service:** AEM Formsが64ビットWindowsにインストールされ、署名にHSMデバイスを使用する場合は、このオプションを指定します。

**Certification To Include Form Load Changes:** このオプションを選択すると、XFAテンプレートに加えてXFAフォーム状態が認証されます。 このオプションを有効にすると、パフォーマンスに悪影響を及ぼす可能性があります。デフォルト値は true です。

**ドキュメントJavaScriptスクリプトを実行：** 署名操作中にドキュメントJavaScriptスクリプトを実行するかどうかを指定します。 デフォルト値は false です。

**Acrobat 9互換のドキュメントを処理します。** Acrobat 9の互換性を有効にするかどうかを指定します。 例えば、このオプションを選択すると、「Visible Certification in Dynamic PDFs」が有効になります。デフォルト値は false です。

**Embed Revocation Info While Signing:** PDF署名時に失効情報を埋め込むかどうかを指定します。ドキュメント デフォルト値は false です。

**Embed Revocation Info While Certifying:** PDF認証時に失効情報を埋め込むかどうかを指定します。ドキュメント デフォルト値は false です。

**Enforce Embedding of Revocation Info For All Certificates署名中/認証中：** すべての証明書の有効な失効情報が埋め込まれていない場合に、署名または証明書の操作が失敗するかどうかを指定します。 証明書に CRL または OCSP 情報が含まれていない場合、失効情報が取得されなくても、証明書は有効と見なされることにご留意ください。デフォルト値は false です。

**Revocation Check Order:** 証明書失効リスト(CRL)とオンライン証明書ステータスプロトコル(OCSP)の両方のメカニズムを通じて確認できる場合の失効確認の順序を指定します。 デフォルト値は「OCSPFirst」です。

**Maximum Size Of Revocation Archival Info:** 失効アーカイブ情報の最大サイズ(KB)。 AEM Forms では、制限を超えない範囲で、できるだけ多くの失効情報が格納されます。デフォルト値は 10 KB です。

**Support Signatures Created From PreRelease Builds Of Adobe Products:** このオプションを選択すると、アドビ製品のプレリリース版を使用して作成された署名が正しく検証されます。 デフォルト値は false です。

**Verification Time Option:** 署名者の証明書の検証時刻を指定します。 デフォルト値は Secure Time Else Current Time です。

**Use Revocation Information Archived in Signature duringValidation:** 署名と共にアーカイブされた失効情報を失効確認に使用するかどうかを指定します。 デフォルト値は true です。

**Use Validation Information Stored Inthe Information Stored In The Signatures For Validation Of Signatures:** このオプションを選択すると、ドキュメントに埋め込まれた検証情報（失効情報やタイムスタンプ情報を含む）が署名の検証に使用されます。 デフォルト値は true です。

**ネストされた検証セッションの最大数：** ネスト可能な検証セッションの最大数。 AEM Forms では、この値を使用して、OCSP または CRL の証明書が正確に設定されていない状態で OCSP または CRL 署名者の証明書を検証する際に無限ループが発生しないようにします。デフォルト値は 10 です。

**Maximum Clock Skew for Verification:** 検証時間の後に署名時間を設定できる最大時間（分単位）です。 Clock Skew がこの値より大きい場合、署名は無効になります。デフォルト値は 65 分です。

**Certificate Lifetime Cache:** オンラインまたは他の方法で取得した、証明書がキャッシュに存続する時間。 デフォルト値は「1」日です。

### トランスポートオプション {#transport-options}

**Proxy Host:** プロキシホストのURL。 値が有効な場合のみ使用されます。デフォルト値はありません。

**プロキシポート：** プロキシポート。 0～65535 の範囲で有効なポート番号を入力します。デフォルト値は 80 です。

**Proxy Login Username:** プロキシログインユーザー名。 プロキシホストとプロキシポートの値が有効な場合のみ使用されます。デフォルト値はありません。

**Proxy Login Password:** プロキシログインパスワード。 プロキシホスト、プロキシポート、プロキシのログインユーザー名の値が有効な場合のみ使用されます。デフォルト値はありません。

**ダウンロードの最大数：** 1回の接続で受信できるデータの最大量（MB単位）。 最小値は 1 MB、最大値は 1024 MB です。デフォルト値は 16 MB です。

**接続タイムアウト：** 新しい接続が確立されるまでの最大待機時間（秒単位）です。 最小値は「1」、最大値は「300」です。デフォルト値は 5 です。

**Socket Time Out:** （データ転送を待機している間に）ソケットがタイムアウトになるまでの待機時間（秒単位）。 最小値は「1」、最大値は「3600」です。デフォルト値は 30 です。

### パス検証オプション {#path-validation-options}

**Require Explicit Policy:** 署名者の証明書のトラストアンカーに関連付けられている証明書ポリシーの少なくとも1つに対して、パスが有効である必要があるかどうかを指定します。 デフォルト値は false です。

**Inhibit ANY Policy:** ポリシーオブジェクト識別子(OID)が証明書に含まれる場合にそれを処理するかどうかを指定します。 デフォルト値は false です。

**Inhibit Policy Mapping:** 証明書パスでポリシーマッピングを許可するかどうかを指定します。 デフォルト値は false です。

**Check All Paths:** すべてのパスを検証するか、最初の有効なパスが見つかった後に検証を停止するかを指定します。 「true」または「false」を選択します。デフォルト値は false です。

**LDAP Server:** パス検証用の証明書の検索に使用するLDAPサーバー。 デフォルト値はありません。

**証明書AIAのURIを追跡：** 証明書AIAのUniform Resource Identifier(URI)をパス検出中に処理するかどうかを指定します。 デフォルト値は false です。

**CA証明書に必要な基本制約拡張：** 認証局(CA)の基本制約証明書拡張がCAの証明書に必要かどうかを指定します。 初期のドイツ語のルート証明書の一部（7 以前）は、RFC 3280 に準拠していないので、基本制約拡張が含まれていません。該当するドイツ語ルートに連結した EE 証明書を持つユーザーが存在することがわかっている場合は、このチェックボックスの選択を解除します。デフォルト値は true です。

**Require Valid Certificate Signature During Chain Building:** チェーンビルダーで、チェーンの構築に使用される証明書に有効な署名が必要かどうかを指定します。 このチェックボックスを選択すると、証明書に無効な RSA 署名が含まれている場合、チェーンビルダーではチェーンが構築されません。チェーン CA > ICA > EE で、ICA 上の CA の署名が無効な場合について考えます。この設定が「true」の場合、チェーン構築は ICA で停止し、CA はチェーンに含まれません。この設定が「false」の場合は、完全な 3 つの証明書のチェーンが生成されます。この設定は、DSA 署名には影響しません。デフォルト値は false です。

### タイムスタンププロバイダーのオプション {#timestamp-provider-options}

**TSP Server URL:** デフォルトのタイムスタンププロバイダーのURLです。 値が有効な場合のみ使用されます。デフォルト値はありません。

**TSP Server Username:** タイムスタンププロバイダーで必要な場合のユーザー名。 URL 値が有効な場合のみ使用されます。デフォルト値はありません。

**TSP Server Password:** タイムスタンププロバイダーで必要な場合に、上記のユーザー名のパスワード。 URL およびユーザー名の値が有効な場合のみ使用されます。デフォルト値はありません。

**Request Hash Algorithm:** タイムスタンププロバイダーの要求を作成する際に使用するハッシュアルゴリズムを指定します。 デフォルト値は SHA1 です。

**Revocation Check Style:** 監視失効ステータスからタイムスタンププロバイダーの証明書の信頼ステータスを判断するために使用する失効確認スタイルを指定します。 デフォルト値は BestEffort です。

**Send Nonce:** タイムスタンププロバイダーの要求でnonceを送信するかどうかを指定します。 nonce には、タイムスタンプまたは Web ページ訪問カウンターを使用することも、ファイルの不正な再生または複製を制限または防止するための特別なマーカーを使用することもできます。デフォルト値は true です。

**Use Expired Timestamps During Validation:** このオプションを選択すると、有効期限切れのタイムスタンプを使用して、署名の検証時間を取得できます。 デフォルト値は true です。

**TSP Response Size:** TSP応答の推定サイズ（バイト単位）。 この値は、設定済みのタイムスタンププロバイダーから返されるタイムスタンプの最大サイズに一致する必要があります。確信がない限り、この値を変更しないでください。最小値は「60B」、最大値は「10240B」です。デフォルト値は 4096 バイトです。

**タイムスタンプのサーバーエクステンションを無視**: **タイムスタンプのサーバーエクステンションを無視**&#x200B;オプションを選択し、AEM Forms サーバーが特定のタイムスタンプサーバーに接続することを阻止します。このオプションを選択することで、AEM Forms とタイムスタンプサーバー間のコネクションタイムアウトによるプロセスの失敗を防ぐことができます。

### 証明書失効リストのオプション {#certificate-revocation-list-options}

**Consult Local URI First:** 「ローカルURI」または「CRL参照」で指定されたCRLの場所を、失効確認のために証明書内で指定された場所よりも優先するかどうかを指定します。 デフォルト値は false です。

**Local URI for CRL Lookup:** ローカルCRLプロバイダーのURL。 「ローカル URI を最初に参照」設定が「true」に設定されている場合にこの値が参照されます。デフォルト値はありません。

**Revocation Check Style:** 監視失効ステータスからCRLプロバイダーの証明書の信頼ステータスを判断するために使用する失効確認スタイルを指定します。 デフォルト値は BestEffort です。

**LDAP Server for CRL Lookup:** CRLの取得に使用するLDAPサーバー(www.ldap.com)。 CRL に対する DN ベースのクエリーはすべてこのサーバーに送信されます。デフォルト値はありません。

**オンラインにする：** CRLを取得するためにオンラインにするかどうかを指定します。 「false」の場合、キャッシュされている CRL（ローカルディスク上または署名と共に埋め込まれているもの）のみが対象になります。デフォルト値は true です。

**Ignore Validity Dates:** 応答のthisUpdateおよびnextUpdateの時間を無視するかどうかを指定します。これらの時間は、応答の有効性に悪影響を及ぼすのを防ぎます。 デフォルト値は false です。

**Require AKI extension in CRL:** 認証機関キー識別子拡張をCRLに含める必要があるかどうかを指定します。 デフォルト値は false です。

### オンライン証明書ステータスプロトコルのオプション {#online-certificate-status-protocol-options}

**OCSP Server URL:** デフォルトのOCSPサーバーのURL。 この URL で指定された OCSP サーバーを使用するかどうかは、「参照 URL オプション」の設定によって決まります。デフォルト値はありません。

**Url To Consult Option:** ステータスリストの実行に使用するOCSPサーバーのサーバーと順序を制御します。 デフォルト値は UseAIAInCert です。

**Revocation Check Style:** OCSPサーバーの証明書の検証時に使用する失効確認スタイルを指定します。 デフォルト値は CheckIfAvailable です。

**Send Nonce:** OCSP要求でnonceを送信するかどうかを指定します。 nonce には、タイムスタンプまたは Web ページ訪問カウンターを使用することも、ファイルの不正な再生または複製を制限または防止するための特別なマーカーを使用することもできます。デフォルト値は true です。

**Max Clock Skew Time:** 応答時間とローカル時間の間の最大許容Skew（分単位）。 最小値は「0」、最大値は「2147483647m」です。デフォルト値は「5m」です。

**Response Freshness Time:** 事前に生成されたOCSP応答が有効と見なされる最大時間（分単位）です。 最小値は「1m」、最大値は「2147483647」です。デフォルト値は 525600（1 年）です。

**Sign OCSP Request:** OCSP要求に署名を必要とするかどうかを指定します。 デフォルト値は false です。

**Request Signer Credential Alias:** 署名が有効な場合にOCSP要求への署名に使用する秘密鍵証明書エイリアスを指定します。 OCSP 要求の署名が有効な場合にのみ使用されます。デフォルト値はありません。

**オンラインにする：** 失効確認を行うためにオンラインにするかどうかを指定します。 デフォルト値は true です。

**応答のthisUpdateおよびnextUpdateの時間を無視する：** 応答のthisUpdateおよびnextUpdateの時間を無視するかどうかを指定します。これらの時間は、応答の有効性に悪影響を及ぼすのを防ぎます。 デフォルト値は false です。

**Allow OCSPNoCheck extension:** OCSPNoCheck拡張が応答署名証明書で許可されるかどうかを指定します。 デフォルト値は true です。

**Require OCSP ISIS-MTT CertHash Extension:** 証明書の公開鍵ハッシュ拡張をOCSP応答に含める必要があるかどうかを指定します。 デフォルト値は false です。

### デバッグ用のエラー処理オプション {#error-handling-options-for-debugging}

**次のAPI呼び出し時に証明書キャッシュをクリア：** 次のSignatureサービス操作が呼び出されたときに証明書キャッシュをクリアするかどうかを指定します。 次の Signature サービス操作が呼び出されると、このオプションは「false」に戻ります。デフォルト値は false です。

**Purge CRL Cache on next API call:** 次のSignatureサービス操作が呼び出されたときにCRLキャッシュをクリアするかどうかを指定します。 次の Signature サービス操作が呼び出されると、このオプションは「false」に戻ります。デフォルト値は false です。

**Purge OCSP Cache on next API call:** 次のSignatureサービス操作が呼び出されたときにOCSPキャッシュをクリアするかどうかを指定します。 次の Signature サービス操作が呼び出されると、このオプションは「false」に戻ります。デフォルト値は false です。

## Watched Folder サービスの設定 {#watched-folder-service-settings}

Watched Folder サービス（`WatchedFolder`）では、すべての監視フォルダーエンドポイントに共通する属性を設定します。また、監視フォルダーエンドポイントのデフォルト値も指定します（[監視フォルダーエンドポイントの設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints)を参照）。このサービスは、外部クライアントアプリケーションによって呼び出されることも、Workbench で作成されたプロセスで使用されることもありません。

Watched Folder サービスでは、以下の設定を使用できます。

**Cron式:** Cron式。入力ディレクトリのポーリングをスケジュールするためにQuartzで使用されます。

**繰り返し回数：** 入力ディレクトリがポーリングされた回数。 エンドポイントの設定でこの値を指定しない場合は、デフォルトの繰り返し回数が使用されます。-1 を指定すると、ディレクトリは無限にスキャンされます。デフォルト値は -1 です。

**繰り返し間隔：** 各ポーリング間のデフォルトの秒数。 監視フォルダーエンドポイント設定にデフォルト値が指定されていない場合、繰り返し間隔としてこの値が使用されます。デフォルト値は 5 です。詳しくは、「バッチサイズ」設定の説明を参照してください。

**非同期：** 呼び出しの種類を非同期型または同期型として識別します。 一過性および同期型のプロセスは、同期型でのみ呼び出すことができます。デフォルト値は「asynchronous」です。

**Wait Time:** 入力フォルダーからファイルが取得されるまでの時間のデフォルト値（秒）です。 待機時間に指定されている時間より古いファイルまたはフォルダーが、処理対象として取得されます。デフォルト値は 0 です。

**バッチサイズ：** 1回のスキャンで処理されるファイルまたはフォルダーの数のデフォルト値です。 デフォルト値は 2 です。

「繰り返し間隔」設定と「バッチサイズ」設定では、監視フォルダーがスキャンごとに何個のファイルを取得するかを指定します。監視フォルダーは、Quartz スレッドプールを使用して入力フォルダーをスキャンします。スレッドプールは他のサービスと共有されます。スキャンの間隔が小さいと、スレッドによって入力フォルダーが頻繁にスキャンされます。ファイルが頻繁に監視フォルダーに配置される場合は、スキャンの間隔を小さくします。ファイルが頻繁には配置されない場合は、他のサービスがスレッドを使用できるように、スキャンの間隔を大きくします。

配置されるファイル数が多い場合は、バッチサイズを大きくします。例えば、監視フォルダーエンドポイントによって呼び出されるサービスが 1 分間に 700 個のファイルを処理でき、これと同じ速度でユーザーが入力フォルダーにファイルを配置するとします。このとき、「バッチサイズ 」を 350 に、「繰り返し間隔 」を 30 秒に設定すると、過度に頻繁に監視フォルダーをスキャンするコストを発生させることなく、監視フォルダーのパフォーマンス向上につなげることができます。

ファイルが監視フォルダーに配置されると監視フォルダーはファイルを入力内に一覧化するので、スキャンが毎秒行われているとパフォーマンスが低下する可能性があります。スキャンの間隔を大きくすると、パフォーマンスが向上する可能性があります。配置されるファイルの量が少ない場合は、それに従って「バッチサイズ 」と「繰り返し間隔 」を調整します。例えば、毎秒 10 個のファイルが配置される場合は、「繰り返し間隔 」を 1 秒に、「バッチサイズ 」を 10 に設定します。

クラスターの設定では、監視フォルダーエンドポイントのバッチサイズが複数のクラスターノードに対して調整されません。例えば、 ノードクラスターに対してバッチサイズが `2`2 に設定され、「ジョブ数を制限」オプションが選択されている場合、各ノードで 2 つのファイルが同時に処理されるのではなく、両方のノードでまとめて 2 つのバッチによりファイルが処理されます。

**重複ファイル名を上書き：** 監視フォルダーが重複ー結果のファイル名を上書きするかどうか、および同じ名前の保存済みドキュメントーを上書きするかどうかを指定するブール値の文字列です。

**フォルダを保存：** 保存フォルダーのデフォルト値です。 このフォルダーは、入力が正常に処理された場合にソースファイルをコピーするために使用されます。何も指定しないか、結果フォルダー設定で説明されているファイルパターンを使用して相対パスまたは絶対パスを指定できます。

**失敗フォルダ：** 失敗ファイルがコピーされるフォルダーの名前。 何も指定しないか、結果フォルダー設定で説明されているファイルパターンを使用して相対パスまたは絶対パスを指定できます。

**結果フォルダ：** 結果フォルダーのデフォルト名です。 このフォルダーに結果ファイルがコピーされます。何も指定しないか、相対パスまたは絶対パスを次のファイルパターンを使用して指定できます。

* %F = ファイル名プレフィックス
* %E = ファイル拡張子
* %Y = 年（4 桁表記）
* %y = 年（下 2 桁）
* %M = 月
* %D = 日（1～31）
* %d = 日（通日）
* %H = 時（24 時間）
* %h = 時（12 時間）
* %m = 分
* %s = 秒
* %l = ミリ秒
* %R = 乱数（0～9）
* %P = プロセス ID またはジョブ ID

For example, if it is 8 PM on July 17, 2009 and you specify `C:/Test/WF0/failure/%Y/%M/%D/%H/`, the result folder is `C:/Test/WF0/failure/2009/07/17/20`.

絶対パスではなく相対パスを指定すると、監視フォルダーの中に作成されます。ファイルパターンについて詳しくは、[ファイルパターンについて](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)を参照してください。

>[!NOTE]
>
>結果フォルダーのサイズを小さくすればするほど、監視フォルダーのパフォーマンスが向上します。例えば、監視フォルダーの推定負荷が 1 時間に 1000 個のファイルである場合、1 時間ごとに新しいサブフォルダーが作成されるように `result/%Y%M%D%H` のようなパターンを使用します。これよりも負荷が小さい場合（例えば、1 日に 1000 個のファイル）、`result/%Y%M%D` のようなパターンを使用することもできます。

**Stage Folder:** 監視フォルダー内のステージフォルダーのデフォルト名です。

**Input Folder:** 監視フォルダー内の入力フォルダーのデフォルト名です。

**失敗時に保存：** trueの場合、元のファイルは失敗時に失敗フォルダーに保持されます。

**スロットル：** このオプションを選択すると、AEM formsで同時に処理できる監視フォルダーのジョブ数が制限されます。 「バッチサイズ」の値によって、ジョブの最大数が決まります（ジョブ数の制限についてを参照）。

## Web Service サービスの設定 {#web-service-service-settings}

Web Service サービス（`WebService`）を使用すると、プロセスにおいて Web サービスの操作を呼び出すことができます。

Web Service サービスを使用すると、プロセスにおいて Web サービスの操作を呼び出すことができます。例えば、サービスプロバイダーの公開されている Web サービスを呼び出して、担当者やアカウントの詳細などの情報を保存および取得するためにプロセスを統合することができます。Web Service サービスは、指定された Web サービスを呼び出し、その各パラメーターの値を渡します。次に、操作からの戻り値を、プロセス内の指定された変数内に保存します。

Web Service サービスは、SOAP メッセージを送受信して Web サービスとやり取りします。また、このサービスは WS-Attachment プロトコルを使用した SOAP メッセージでの MIME、MTOM および SwaRef 添付ファイルの送信もサポートします。Web Service サービス操作は、SAP システムおよび .NET Web サービスと互換性があります。

Web Service サービスでは、以下の設定を使用できます。

**キーストア：** 認証に使用する秘密鍵が含まれているキーストアファイルのフルパスです。 forms サーバーからこのファイルにアクセスできる必要があります。

**Key Store Password:** キーストアファイルのパスワード。

**Key Store Type:** キーストアのタイプ。 forms サーバーを実行する JVM に設定されているデフォルトのキーストアの種類を使用する場合は、値を指定しません。それ以外の場合、以下のいずれかの値を指定します。

* jks
* pkcs12
* cms
* jceks

**Trust Store:** Webサービスサーバーの公開鍵を含むTrust Storeファイルのフルパスです。

**Trust Store Password:** truststoreファイルのパスワードです。

**Trust Storeの種類：** 信頼ストアの種類です。 forms サーバーを実行する JVM に設定されているデフォルトのキーストアの種類を使用する場合は、値を指定しません。それ以外の場合、以下のいずれかの値を指定します。

* jks
* pkcs12
* cms
* jceks

## XSLT Transformation サービスの設定 {#xslt-transformation-service-settings}

XSLT Transformation サービス（`XSLTService`）を使用すると、プロセスで XSLT（Extensible Stylesheet Language Transformations）を XML ドキュメントに適用できます。

XSLT Transformation サービスでは以下の設定を使用できます。

**ファクトリ名：** XSLT変換の実行に使用するJavaクラスの完全修飾名です。 値を指定しない場合は、forms サーバーを稼働する Java 仮想マシンに設定されたデフォルトのファクトリが使用されます。

## サービスのセキュリティ設定の変更 {#modifying-security-settings-for-a-service}

forms サーバーでは、各サービスのセキュリティ設定を指定できます。これにより、サービスごとにアクセス制御を細かく設定できます。

デフォルトのセキュリティプロファイルがインストールされ、このプロファイルはその後、システムの必要性に応じて設定できます。セキュリティプロファイルは、ユーザーレベルまたはグループレベルで作成され、ドメインに関連付けられます。

### サービスのセキュリティ設定の変更 {#modify-security-settings-for-a-service}

1. 管理コンソールで、サービス／アプリケーションおよびサービス／サービスの管理をクリックします。
1. サービスの管理ページで、設定するサービスをクリックします。
1. 「セキュリティ」タブをクリックします。
1. 「呼び出し元の認証が必要」リストで、「はい」または「いいえ」を選択して、サービスの呼び出しに秘密鍵証明書が必要かどうかを指定します。

   「はい」を選択する場合は、サービスの呼び出し元に認証が必要であり、その呼び出し元のユーザープリンシパルにはサービスを呼び出す権限が必要です。認証および権限がないと、呼び出しは拒否されます。

   「いいえ」を選択する場合は、サービスの呼び出し元は認証されていなくても構いません。認証チェックがないので、サービスの呼び出しは常に成功します。

1. 匿名アクセス用に 1 つ以上の操作にフラグが設定されているサービスの場合は、「匿名アクセスが許可されました」を選択または選択解除します。匿名アクセスが有効な場合、システムに存在するすべてのユーザーがサービスの操作を呼び出すことができます。匿名アクセスが無効に設定されている場合、ユーザーがサービスを呼び出して操作を実行するには、適切な権限が与えられている必要があります。このような権限は、ユーザーに直接与えられるか、ユーザーがその権限を持つグループに属していることによって間接的に与えられます。
1. 一部のサービスでは、操作を実行するユーザーアカウントが結果に影響を及ぼす場合があります。例えば、Content Services（非推奨）では、コンテンツを保存するユーザーはコンテンツの所有者になります。これは、以降にコンテンツにアクセスできるユーザーに影響があります。コンテンツを保存するプロセスを使用している場合、Document Management サービスの実行に使用されるユーザーについて考慮します。保存されるコンテンツの所有者がそのユーザーになるためです。

   操作を実行するサービスで使用する実行時 ID を指定するには、「実行ユーザーを指定」を選択して、関連するリストから任意のオプションを選択し、「保存」をクリックします。次のいずれかのオプションを選択します。

   **呼び出し元：**&#x200B;サービスを呼び出したユーザーと同じ ID を使用します。

   **システム：**&#x200B;フルコントロールでサービスを実行できる System ユーザーを使用します。

   **指定したユーザー：**&#x200B;ある特定のユーザーとしてサービスを実行できます。このオプションを選択する場合、「ユーザーを選択」をクリックすると、プリンシパルを選択ページが表示され、ユーザーを検索して選択することができます。

   「実行ユーザーを指定」を選択しない場合は、デフォルトの動作が使用されます。

   >[!NOTE]
   >
   >常に System ユーザーアカウントを使用して実行される xfaForm、Document Form、および Form 変数で使用されるサービスをレンダリングおよび送信します。

1. 「プリンシパルを追加」をクリックして、ユーザーおよびグループがこのサービスに対して持つ権限を指定します。
1. プリンシパルを選択画面に、User Management で設定したユーザーおよびグループが表示されます。目的のユーザーまたはグループが表示されない場合は、検索機能を使用して検索してください。ユーザーまたはグループの名前をクリックします。
1. 権限を追加画面で、このサービスに対して、ユーザーまたはグループに割り当てる権限を選択します。

   * **INVOKE_PERM：**&#x200B;サービスのすべての操作を呼び出します。
   * **MODIFY_CONFIG_PERM：**&#x200B;サービスの設定を変更します。
   * **SUPERVISOR_PERM：**&#x200B;サービスに対してプロセスから作成されたプロセスインスタンスデータを表示します。
   * **START_STOP_PERM：**&#x200B;サービスを開始および停止します。
   * **ADD_REMOVE_ENDPOINTS_PERM：**&#x200B;サービスのエンドポイントを追加、削除、変更します。
   * **CREATE_VERSION_PERM：**&#x200B;サービスの新しいバージョンを作成します。
   * **DELETE_VERSION_PERM：**&#x200B;サービスのバージョンを削除します。
   * **MODIFY_VERSION_PERM：**&#x200B;サービスのバージョンを変更します。
   * **READ_PERM：**&#x200B;サービスを表示します。
   * **PROCESS_OWNER_PERM：** AEM Forms の将来のバージョンで使用されます。この権限は使用しないでください。
   * **SERVICE_MANAGER_PERM：** AEM Forms の将来のバージョンで使用されます。この権限は使用しないでください。
   * **SERVICE_AGENT_PERM：** AEM Forms の将来のバージョンで使用されます。この権限は使用しないでください。

1. 「追加」をクリックします。

### セキュリティプロファイルからのプリンシパルの削除 {#remove-the-principal-from-a-security-profile}

1. サービスの管理ページで、設定するサービスを選択します。
1. 「**セキュリティ**」タブをクリックし、削除するセキュリティプロファイルを選択して、「**削除**」をクリックします。

## サービスのプーリングの設定 {#configuring-pooling-for-a-service}

各サービスでは、プーリング機能を利用して、受信する呼び出し要求を処理できます。サービスプールを使用すると、サービスインスタンスは一度に 1 つのスレッドで呼び出され、複数の呼び出し要求で再利用できるので、パフォーマンスが向上する場合があります。また、プーリングを使用して「非同期サービスインスタンスの最大数」オプションを指定することもでき、同時に処理される要求の数を制限することができます。

### プーリングの有効化 {#enable-pooling}

1. 管理コンソールで、サービス／アプリケーションおよびサービス／サービスの管理をクリックします。
1. サービスの管理ページで、設定するサービスをクリックします。
1. 「プーリング」タブをクリックします。
1. 「要求処理方法」リストで「すべての要求のプール済みインスタンス」を選択します。
1. 「サービスインスタンスの初期プールサイズ」ボックスに、プールの初期サイズを入力します。サービスがデプロイされると、サービス実装インスタンスが何個作成され、呼び出し要求を待機している空きプールに割り当てられるかが、この数値を使用して特定されます。これによって、サービスコンテナは、サービスインスタンスを初期化する必要なく、呼び出し要求に直ちに応答できます。
1. 「サービスインスタンスの最大プールサイズ」ボックスに、指定したサービスのプール内の最大インスタンス数を入力します。この設定によって、指定した時間に指定したサービスを実行できるスレッドの数が制御されます。デフォルト値は 0 で、プールサイズは無制限です。
1. 「非同期サービスインスタンスの最大数」ボックスに、指定した時間に非同期要求に対応できる、プールの最大インスタンス数を入力します。この設定によって、サービスで同時に処理できる要求の数を制限できます。
1. 「呼び出し待機のタイムアウト」ボックスに、サービスが呼び出し要求に対応可能になるまでの待機時間をミリ秒単位で入力します。この設定の値を指定しない場合、デフォルトは 0 で、待機時間はゼロです。
1. 「保存」をクリックします。

### プーリングの削除 {#remove-pooling}

1. 管理コンソールで、サービス／アプリケーションおよびサービス／サービスの管理をクリックします。
1. サービスの管理ページで、設定するサービスをクリックします。
1. 「プーリング」タブをクリックします。
1. 「要求処理方法」リストで「各要求の新しいインスタンス」または「すべての要求の単一インスタンス」のいずれかを選択します。

   **すべてのリクエストの単一インスタンス：** サービスインスタンスは、最初の要求がコンテナに到達したときに作成され、キャッシュされます。 その要求以降の要求はすべて、同じサービスインタンスを使用して処理されます。

   **各リクエストの新しいインスタンス：** 呼び出しを受け取るたびに、新しいサービスインスタンスが作成されます。

1. 「保存」をクリックします。

