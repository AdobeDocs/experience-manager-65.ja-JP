---
title: AEM Formsのバックアップの準備
seo-title: AEM Formsのバックアップの準備
description: 'null'
seo-description: 'null'
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Formsのバックアップの準備 {#preparing-aem-forms-for-backup}

## バックアップと復元サービスについて {#about-the-backup-and-restore-service}

バックアップと復元サービスを使用すると、AEM formsをバックアッ *プモードにし*、ホットバックアップを実行できます。 バックアップと復元サービスは、実際にはAEM Formsのバックアップを実行したり、システムを復元したりしません。 代わりに、サーバを一貫性のある信頼性の高いバックアップが可能な状態にし、サーバを引き続き実行できるようにします。 グローバルドキュメントストレージ(GDS)とformsサーバーに接続されているデータベースをバックアップするアクションは、ユーザーが行います。 GDSは、長期間有効なプロセス内で使用されるファイルの保存に使用されるディレクトリです。

バックアップモードは、バックアップ処理の実行中にGDS内のファイルが削除されないようにサーバーが開始する状態です。 代わりに、GDSディレクトリの下にサブディレクトリが作成され、保存バックアップモードの終了後に削除されるファイルの記録が維持されます。 ファイルは、システムの再起動後も維持され、数日または数年に及ぶ可能性があります。 これらのファイルは、formsサーバーの全体的な状態の重要な部分であり、PDFファイル、ポリシー、フォームテンプレートなどが含まれる場合があります。 これらのファイルのいずれかが失われたり破損した場合、formsサーバー上のプロセスが不安定になり、データが失われる可能性があります。

スナップショットバックアップの実行を選択できます。この場合、通常は一定期間バックアップモードに入り、バックアップアクティビティの完了後にバックアップモードを終了します。 GDSからファイルを削除して、ファイルのサイズが不必要に大きくならないようにするには、バックアップモードを終了する必要があります。 バックアップモードを明示的に終了するか、バックアップモードセッションで時間が経過するのを待つことができます。

また、サーバを永続的なバックアップモードのままにすることもできます。これは、ローリングバックアップや継続的なシステムカバーのバックアップ戦略に一般的です。 ローリングバックアップモードは、システムが常にバックアップモードで、前のセッションが解放されるとすぐに新しいバックアップモードセッションが開始されることを示します。 連続バックアップモードでは、2回のバックアップモードセッションの後にファイルがパージされ、参照されなくなります。

Backup and Restoreサービスを使用して、formsサーバーに接続されたGDSまたはデータベースのバックアップを実行するために作成した既存のアプリケーションまたは新しいアプリケーションを追加できます。

>[!NOTE]
>
>AEM Forms実装の他の側面と同様に、バックアップと回復戦略は、実稼働環境で使用する前に、開発環境またはステージング環境で開発およびテストし、データ損失を伴わずにソリューション全体が期待どおりに動作することを確認する必要があります。

バックアップと復元サービスを使用して、次のタスクを実行できます。

* バックアップモードに入ります。
* バックアップモードを終了します。

>[!NOTE]
>
>AEM Formsのバックアップを実行する際に考慮すべき事項について詳しくは、管理ヘルプを参照 [してください](https://www.adobe.com/go/learn_aemforms_admin_63)。

>[!NOTE]
>
>For more information about the Backup and Restore service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## formsサーバーでのバックアップモードの開始 {#entering-backup-mode-on-the-forms-server}

バックアップモードに切り替えて、formsサーバーのホットバックアップを許可します。 バックアップモードに入る際は、組織のバックアップ手順に基づいて次の情報を指定します。

* バックアップ・プロセスに役立つ可能性のあるバックアップ・モード・セッションを識別する一意のラベル。
* バックアップ手順が完了する時間。
* 連続バックアップモードにするかどうかを示すフラグ。ローリングバックアップを実行する場合にのみ役立ちます。

バックアップモードに入るアプリケーションを作成する前に、formsサーバーをバックアップモードにした後に使用するバックアップ手順を理解することをお勧めします。 AEM Formsのバックアップを実行する際に考慮すべき事項について詳しくは、管理ヘルプを参照 [してください](https://www.adobe.com/go/learn_aemforms_admin_63)。

>[!NOTE]
>
>For more information about the Backup and Restore service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

バックアップモードに入るアプリケーションを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. BackupServiceクライアントオブジェクトを作成します。
1. 一意のラベル、バックアップの実行時間、継続的なバックアップ・モードにするかどうかを決定します。
1. バックアップモードに入ります。
1. （オプション）サーバー上のバックアップモードセッションに関する情報を取得します。
1. GDS（グローバルデータストア）とデータベースのバックアップを実行します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 これらのファイルは、コードを正しくコンパイルし、Backup and Restore Service APIを使用するために、プロジェクトに組み込むことが重要です。

これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**BackupService Client APIオブジェクトの作成**

プログラムでバックアップモードを終了するには、Backup and Restore Service APIを使用するBackupServiceクライアントオブジェクトを作成します。

**一意のラベルを決定し、バックアップの実行時間を決定し、継続的なバックアップ・モードにするかどうかを決定**

バックアップモードに入る前に、一意のラベルを決定し、バックアップの実行に割り当てる時間を決定し、formsサーバーをバックアップモードにするかどうかを決定する必要があります。 これらの考慮事項は、組織が確立したバックアップ手順と統合する際に重要です。 (See [administration help](https://www.adobe.com/go/learn_aemforms_admin_63).)

**バックアップモードの開始**

組織のバックアップ手順と一致するパラメーターを使用して、バックアップモードに入ります。

**サーバー上のバックアップモードセッションに関する情報を取得します**

バックアップモードに入った後、セッションに関する情報を取得できます。 この情報は、バックアップ・プロシージャとの統合に使用できます。

**GDSとデータベースのバックアップの実行**

バックアップモードに正常に切り替えたら、グローバルドキュメントストレージ(GDS)とformsサーバーが接続されているデータベースのバックアップを実行できます。 この手順は、手動で実行することも、他のツールを実行してバックアップ手順を実行することもできるので、組織に固有です。

### Java APIを使用したバックアップモードの開始 {#enter-backup-mode-using-the-java-api}

バックアップと復元サービスAPIを使用してバックアップモードに入ります。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-backup-restore-client-sdk.jarなど、必要なクライアントJARファイルを含めます。 Javaクライアントアプリケーションを作成するには、プロジェクトのクラスパスに次のJARファイルを追加する必要があります。

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
   * jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

1. BackupService Client APIオブジェクトの作成

   オブジェクトとBackupServiceク `ServiceClientFactory` ライアントAPIオブジェクトを一緒に使用します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * Create an `BackupService` object by using its constructor and passing the `ServiceClientFactory` object.

1. 一意のラベルを決定し、バックアップの実行時間を決定し、継続的なバックアップ・モードにするかどうかを決定

   一意のラベルを決定し、バックアップの実行に割り当てる時間を決定し、formsサーバーを継続的なバックアップモードにするかどうかを決定します。

1. バックアップモードの開始

   次のパラメーターを指定してメソッドを呼び出し、 `enterBackupMode` バックアップモードに入ります。

   * バック `String` アップモードセッションを識別する一意の人間が読み取り可能なラベルを指定する値。 XML形式にエンコードできないスペースや文字は使用しないことをお勧めします。
   * バッ `int` クアップモードを維持する時間（分）を指定する値。 からまでの値を指 `1` 定で `10080` きます（1週間の分数）。 連続バックアップモードを使用する場合、この値は無視されます。
   * 連続バ `Boolean` ックアップモードにするかどうかを指定する値です。 値は、連続バッ `True` クアップモードであることを指定します。 連続バックアップモードの場合、バックアップモードを維持する時間（分）に指定した値は無視されます。

      連続バックアップモードとは、現在のバックアップモードセッションが完了した後に新しいバックアップモードセッションが開始されることを意味します。 値は、連続バッ `False` クアップモードが使用されないことを意味し、バックアップモードを終了すると、GDSからのファイルの削除が再開されます。

1. サーバー上のバックアップモードセッションに関する情報を取得します

   メソッドを呼び出した後 `BackupModeEntryResult` に返されるオブジェクトを使用して情報を取得 `enterBackupMode` します。 バックアップモードに入った後に取得できる情報は、バックアップ手順との統合に役立つ場合があります。 例えば、ラベル、バックアップID、開始時間は、バックアップ手順のファイル名の入力として役立つ場合があります。

1. GDSとデータベースのバックアップの実行

   グローバルドキュメントストレージ(GDS)とformsサーバーが接続されているデータベースをバックアップします。 バックアップを実行するアクションはAEM Forms SDKの一部ではなく、組織のバックアップ手順に固有の手動手順を含む場合もあります。

### WebサービスAPIを使用してバックアップモードに入る {#enter-backup-mode-using-the-web-service-api}

バックアップと復元サービスAPIが提供するWebサービスを使用して、バックアップモードに入ります。

1. プロジェクトファイルを含める

   * Backup and Restore Service API WSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. BackupService Client APIオブジェクトの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンス `BackupServiceService` トラクターを呼び出してオブジェクトを作成し、メソッドを使用して秘密鍵証明書を指 `Credentials` 定します。

1. 一意のラベルを決定し、バックアップの実行時間を決定し、継続的なバックアップ・モードにするかどうかを決定

   一意のラベルを決定し、バックアップの実行に割り当てる時間を決定し、formsサーバーを継続的なバックアップモードにするかどうかを決定します。

1. バックアップモードの開始

   バックアップモードに入るには、enterBackupModeメソッドを呼び出し、次の値を渡します。

   * バック `String` アップモードセッションを識別する一意の人間が読み取り可能なラベルを指定する値。 XML形式にエンコードできないスペースや文字は使用しないことをお勧めします。
   * バッ `Uint32` クアップモードを維持する時間（分）を指定する値。 ～の値を指定で `1` きま `10080` す（1週間の分数）。 連続バックアップモードを使用する場合、この値は無視されます。
   * 連続バ `Boolean` ックアップモードにするかどうかを指定する値です。 値は、連続バッ `True` クアップモードであることを指定します。 連続バックアップモードの場合、バックアップモードを維持する時間（分）に指定した値は無視されます。 連続バックアップモードとは、現在のバックアップモードセッションが完了した後に新しいバックアップモードセッションが開始されることを意味します。

      値は、連続バッ `False` クアップモードが使用されないことを意味し、バックアップモードを終了すると、GDSからのファイルの削除が再開されます。

1. サーバー上のバックアップモードセッションに関する情報を取得します

   BackupModeEntryResultからenterBackupModeメソッドを呼び出し、成功したことを確認するために返された後、バックアップモードセッションに関する情報を取得します。 バックアップモードに入った後に取得できる情報は、バックアップ手順との統合に役立つ場合があります。 例えば、ラベル、バックアップID、開始時間は、バックアップ手順のファイル名の入力として役立つ場合があります。

1. GDSとデータベースのバックアップの実行

   グローバルドキュメントストレージ(GDS)とformsサーバーが接続されているデータベースをバックアップします。 バックアップを実行するアクションはAEM Forms SDKの一部ではなく、組織のバックアップ手順に固有の手動手順を含む場合もあります。

## formsサーバーでのバックアップモードの終了 {#leaving-backup-mode-on-the-forms-server}

バックアップモードを終了すると、formsサーバーがformsサーバー上のGDS（グローバルドキュメントストレージ）からのファイルの削除を再開します。

終了モードに入るアプリケーションを作成する前に、AEM Formsで使用するバックアップ手順を理解することをお勧めします。 AEM Formsのバックアップを実行する際に考慮すべき事項について詳しくは、管理ヘルプを参照 [してください](https://www.adobe.com/go/learn_aemforms_admin_63)。

>[!NOTE]
>
>For more information about the Backup and Restore service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

バックアップモードを終了するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. BackupServiceクライアントオブジェクトを作成します。
1. バックアップモードを終了します。
1. （オプション）formsサーバーで実行されていたバックアップモードセッションに関する情報を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルをすべて含めます。 これらのファイルは、コードを正しくコンパイルし、Backup and Restore Service APIを使用するために重要です。

これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**BackupService Client APIオブジェクトの作成**

プログラムでバックアップモードを終了するには、Backup and Restore Service APIを使用するBackupServiceクライアントオブジェクトを作成します。

**バックアップモードを終了**

バックアップモードを終了して、グローバルドキュメントストレージ(GDS)からのファイルの通常の削除を再開します。 バックアップモードを終了する前に、バックアップ手順が完了していることを確認する必要があります。

**終了したバックアップモードセッションに関する情報を取得します**

バックアップモードを終了した後、セッションに関する情報を取得できます。 この情報は、バックアップ手順との統合に使用できます。

### Java APIを使用したバックアップモードの終了 {#leave-backup-mode-using-the-java-api}

バックアップと復元サービスAPI(Java)を使用して、バックアップモードを終了します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-backup-restore-client-sdk.jarなど、必要なクライアントJARファイルを含めます。 Javaクライアントアプリケーションを作成するには、次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
   * jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

1. BackupService Client APIオブジェクトの作成

   オブジェクトとBackupServiceク `ServiceClientFactory` ライアントAPIオブジェクトを一緒に使用します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * Create a `BackupService` object by using its constructor and passing the `ServiceClientFactory` object as parameter.

1. バックアップモードの開始

   メソッドを呼び出して、バックアップモードを `leaveBackupMode` 終了します。

1. サーバー上のバックアップモードセッションに関する情報を取得します

   返されるオブジェクトを使用して、操作に関 `BackupModeResult` する情報を取得します。 バックアップモードに入った後に取得できる情報は、バックアップ手順との統合に役立つ場合があります。 例えば、ラベル、バックアップID、開始時間は、バックアップ手順のファイル名の入力として役立つ場合があります。

### WebサービスAPIを使用したバックアップモードの終了 {#leave-backup-mode-using-the-web-service-api}

Backup and Restore Service API（Webサービス）を使用してバックアップモードを終了します。

1. プロジェクトファイルを含める

   Webサービスを使用するには、必ずプロキシファイルを含める必要があります。 Backup and Restore Service APIをWebサービスとして使用するようにプロジェクトを設定するには、次の手順に従います。

   * Backup and Restore Service API WSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. BackupService Client APIオブジェクトの作成

   Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタ `BackupServiceService` ーを呼び出してオブジェクトを作成します。

1. バックアップモードの開始

   Webサービス操作を呼び出して、バックアップ `leaveBackupMode` モードを終了します。

1. サーバー上のバックアップモードセッションに関する情報を取得します

   操作の後にバックアップモード識別子を取得し、正常に実行されたことを確認します。 バックアップモードを終了した後に取得できる情報は、バックアップ手順との統合に役立つ場合があります。

