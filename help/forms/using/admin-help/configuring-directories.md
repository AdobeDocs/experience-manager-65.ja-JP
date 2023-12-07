---
title: ディレクトリの設定
description: ディレクトリを追加、編集、削除し、仮想リスト表示を使用するようにユーザー管理を設定する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 30edcef2-e8fa-403a-9850-b8dfeeb9ac65
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '3229'
ht-degree: 38%

---

# ディレクトリの設定 {#configuring-directories}

設定した各エンタープライズドメインに対して、認証プロバイダーがユーザー情報に対して問い合わせるディレクトリを指定します。 1 つのドメインに対して複数のディレクトリを設定できます。

## ディレクトリまたはカスタム SPI の追加 {#adding-directories-or-custom-spis}

設定した各エンタープライズドメインに対して、認証プロバイダーがユーザー情報に対して問い合わせるディレクトリを指定します。 ディレクトリは、既存のエンタープライズドメインに追加するか、追加する新しいエンタープライズドメインに追加できます。 1 つのドメインに対して複数のディレクトリを設定できます。 また、ドメインを構成して、カスタムの SPI(Service Provider Interface) を同期に使用することもできます。

### ディレクトリを追加 {#add-a-directory}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 「新規エンタープライズドメイン」をクリックするか、既存のエンタープライズドメインを選択します。
1. 「ディレクトリを追加」をクリックします。
1. 「プロファイル名」ボックスに、このディレクトリを区別する名前を入力し、「次へ」をクリックします。
1. ディレクトリサーバーを設定します。 ( 詳しくは、 [ディレクトリ設定](configuring-directories.md#directory-settings).)
1. LDAP サーバーに接続できることを確認するには、「テスト」をクリックします。 テストが失敗した場合は、アプリケーションサーバーのログファイルで例外を確認し、失敗の根本原因を特定します。 「閉じる」をクリックし、「次へ」をクリックします。
1. 「ユーザー設定」を選択し、必要に応じて設定を行います。 ( 詳しくは、 [ディレクトリ設定](configuring-directories.md#directory-settings).)
1. BaseDN やその他の設定済み属性が正しいユーザーのバッチを収集していることを確認するには、「テスト」をクリックします。 LDAP は、指定された設定（ベース DN、検索フィルター、すべての属性など）を使用して、最初の 200 件のレコードを取得しようとします。

   ユーザーが返された場合、属性セットに従って各フィールドに割り当てられた値が結果に表示されます。 サーバー名が存在しない、認証情報が正しくない、または属性が正しくないことが原因でテストが失敗した場合は、「指定した検索条件で結果が返されませんでした」というエラーメッセージが表示されます。 失敗の根本原因を特定するには、アプリケーションサーバーのログファイルで例外を確認します。 「閉じる」をクリックし、「次へ」をクリックします。

1. 「グループ設定」を選択し、必要に応じて設定を行います。 ( 詳しくは、 [ディレクトリ設定](configuring-directories.md#directory-settings).)
1. BaseDN やその他の設定済み属性が正しいグループのバッチを収集していることを確認するには、「テスト」をクリックします。 グループが返される場合、属性セットに従って各フィールドに割り当てられた値が結果に表示されます。 「閉じる」をクリックします。

### カスタム SPI を追加 {#add-a-custom-spi}

カスタム SPI の作成について詳しくは、「AEM forms の SPI の開発」( [AEM forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63_jp). 新しくデプロイしたカスタム SPI をドメインとの関連付けに使用できるようにするには、サーバーを再起動します。

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 「新規エンタープライズドメイン」をクリックするか、既存のエンタープライズドメインを選択します。
1. 「ディレクトリを追加」をクリックします。
1. 「プロファイル名」ボックスに名前を入力し、「カスタム SPI プロバイダー」を選択して、「次へ」をクリックします。
1. リストからカスタムユーザープロバイダーを選択し、「次へ」をクリックします。
1. リストからカスタムグループプロバイダーを選択し、「完了」をクリックします。

## ディレクトリの編集 {#edit-a-directory}

以前に設定したディレクトリの詳細を編集できます。

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. リスト内の適切なドメインをクリックし、表示されるページで、リストから適切なディレクトリを選択します。
1. 必要に応じて、ディレクトリ、ユーザー、グループの設定を指定します。 ( 詳しくは、 [ディレクトリ設定](configuring-directories.md#directory-settings).)
1. 「OK」をクリックします。

## ディレクトリの削除 {#delete-a-directory}

ディレクトリを削除した後でドメインを同期すると、そのディレクトリ内のすべてのユーザーとグループは、データベースで古いものとしてマークされます。 管理コンソールからの検索では返されません。

>[!NOTE]
>
>エンタープライズドメインには、1 つ以上の認証プロバイダーとディレクトリプロバイダーが必要です。

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. リストで適切なドメインをクリックします。
1. 適切なディレクトリのチェックボックスを選択し、「削除」をクリックします。
1. 表示される確認ページで「 OK 」をクリックし、もう一度「 OK 」をクリックします。

## ディレクトリ設定 {#directory-settings}

ドメインにディレクトリを追加する場合は、次のディレクトリ設定を指定します。

**サーバー：**（必須）ディレクトリサーバーの完全修飾ドメイン名（FQDN）。例えば、adobe.com ネットワーク上の x というコンピューターの場合、FQDN は x.adobe.com です。FQDN サーバー名の代わりに IP アドレスを使用することもできます。

**ポート：**（必須）ディレクトリサーバーによって使用されるポート。通常は 389 で、Secure Sockets Layer（SSL）プロトコルを使用してネットワーク経由で認証情報を送信する場合は 636 です。

**SSL：**（必須）ネットワーク経由でデータを送信するときにディレクトリサーバーで SSL を使用するかどうかを指定します。デフォルトは「いいえ」です。 「はい」に設定した場合、対応する LDAP サーバー証明書は、アプリケーションサーバーの Java™ランタイム環境 (JRE) によって信頼される必要があります。

**連結**（必須）ディレクトリへのアクセス方法を指定します。

**匿名：**&#x200B;ユーザー名またはパスワードは不要です。匿名ユーザーは、限られた量のデータのみを取得できます。 このオプションは、初期テストに役立つ場合があります。

**ユーザー：**&#x200B;認証が必要です。 「名前」ボックスに、ディレクトリにアクセスできるユーザーレコードの名前を指定します。ユーザーアカウントの完全な識別名（DN）を入力することをお勧めします。例えば、cn=Jane Doe, ou=user, dc=can, dc=com などです。「パスワード」ボックスに、関連するパスワードを指定します。 これらの設定は、「連結」オプションとして「ユーザー」を選択した場合に必要です。

**名前：**&#x200B;匿名アクセスが有効になっていないときに、LDAP データベースに接続するために使用できる名前です。Active Directory 2003 の場合、`[domain name]\[userid]` を指定します。Sun™ One、eDirectory または IBM Tivoli Directory Server の場合、uid=lcuser,ou=it,o=company.com のようにユーザーの完全修飾名を指定します。

**パスワード：**&#x200B;匿名アクセスが有効になっていないときに、LDAP データベースに接続するために指定した名前に対応するパスワードです。

**ページに次の情報を入力：**&#x200B;選択すると、ユーザー設定ページおよびグループの設定ページの属性に、対応するデフォルトの LDAP 値が設定されます。

**BaseDN を取得：** BaseDN を取得し、ドロップダウンリストに表示します。この設定は、複数の BaseDN がある場合に 1 つの値を選択する必要があるときに便利です。

**リファラルを有効にする：**&#x200B;この設定は、組織が階層構造で編成されている複数の Active Directory ドメインを使用し、1 つの親ドメインにのみディレクトリ設定を指定した場合に適用されます。この場合、このオプションを選択すると、User Management は子ドメインからユーザーおよびグループの詳細にアクセスできます。

>[!NOTE]
>
>「テスト」をクリックして、LDAP サーバーに接続できることを確認します。 エラーの根本原因を特定するには、アプリケーションサーバーのログファイルで例外を確認します。

### ユーザー設定 {#user-settings}

**固有な識別子：**（必須）ユーザーの識別に使用する固有で一定の属性。ユーザーが組織の別の部分に移動するとユーザーの DN が変わる場合があるので、DN 以外の属性を一意の識別子として使用します。 この設定は、ディレクトリサーバーによって異なります。Active Directory 2003 での値は objectGUID、Sun™ One では nsuniqueID、eDirectory では guid です。

>[!NOTE]
>
>組織内で一意であることが保証された属性を入力していることを確認してください。 誤った値を入力すると、システムに重大な問題が発生する可能性があります。

**BaseDN：** LDAP 階層からユーザーおよびグループを同期するための開始点として設定されます。サービスに対して同期する必要のあるすべてのユーザーとグループを含む階層の最下位レベルで BaseDN を指定することをお勧めします。

ディレクトリ設定で「リファラルを有効にする」オプションを選択した場合、「 Base DN 」オプションを *dc* DN の一部。 リファラルが機能するには、検索範囲に親ドメインと子ドメインの両方を含める必要があります。

>[!NOTE]
>
>この設定にユーザーの DN を含めないでください。 特定のユーザーを同期するには、検索フィルター設定を使用します。

BaseDN は管理コンソールの必須の設定ですが、IBM Domino Enterprise Server などの一部のディレクトリサーバーでは空の BaseDN が必要になる場合があります。 空の BaseDN を指定するには、config.xml ファイルを書き出し、config.xml ファイルの設定を編集してから、再度読み込みます。 ( 詳しくは、 [設定ファイルの読み込みと書き出し](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**検索フィルター：**（必須）ユーザーに関連付けられているレコードを検索するために使用する検索フィルターです。1 レベル検索またはサブレベル検索を実行できます。（検索フィルター構文または RFC 2254 を参照。）Microsoft AD スキーマのその他の情報については「Active Directory スキーマ」を参照してください。

**説明：**&#x200B;ユーザーについての説明のスキーマ属性

**フルネーム：** （必須）ユーザーのフルネームのスキーマ属性

**ログイン ID :** （必須）ユーザーのログイン ID のスキーマ属性。

**姓：** （必須）ユーザーの姓のスキーマ属性。

**名前：** （必須）ユーザーの名のスキーマ属性。

**イニシャル：** ユーザーのイニシャルのスキーマ属性

**ビジネスカレンダー：**&#x200B;この設定の値（ビジネスカレンダーキー）に基づいて、ビジネスカレンダーをユーザーにマッピングできます。業務カレンダーでは、営業日と休業日を定義します。AEM forms では、リマインダー、締め切り、エスカレーションなどのイベントに関する今後の日時を計算するときに、この業務カレンダーを使用できます。業務カレンダーキーをユーザーに割り当てる方法は、エンタープライズドメイン、ローカルドメイン、ハイブリッドドメインのどちらを使用しているかによって異なります。 （ビジネスカレンダーの設定を参照。）

エンタープライズドメインを使用している場合は、業務カレンダー設定を LDAP ディレクトリ内のフィールドにマップできます。 例えば、ディレクトリ内の各ユーザーレコードに *国* 」フィールドにユーザーがいる国に基づいて業務カレンダーを割り当てる場合は、 *国* 業務カレンダー設定の値としてのフィールド名。 その後、業務カレンダーキー ( *国* LDAP ディレクトリの「 」フィールド ) を、forms ワークフローの業務カレンダーに追加します。

Forms ワークフローページで業務カレンダーキーの名前を表示するために使用される容量は制限されます。 業務カレンダーキーの名前を 53 文字未満に制限して、これらのページで切り捨てないようにします。

**タイムスタンプを変更：**&#x200B;差分ディレクトリ同期を有効にするには、この値を設定してタイムスタンプを変更します。（差分ディレクトリ同期の有効化を参照。）

**組織：**&#x200B;ユーザーが所属している組織の名前のスキーマ属性。

**プライマリメール：** ユーザーのプライマリメールアドレスのスキーマ属性。

**セカンダリメール：**&#x200B;ユーザーのセカンダリメールアドレスのスキーマ属性。

**電話：** ユーザーの電話番号のスキーマ属性。

**郵送先住所：** ユーザーの郵送先住所のスキーマ属性。

**ロケール：** ISO ロケール情報を含むスキーマ属性。この値は 2 文字の言語コードまたは言語および国コードです。

**タイムゾーン：**&#x200B;ユーザーの所在地のタイムゾーンを含むスキーマ属性。この値は市区町村／国などの文字列です。

**仮想一覧表示（VLV）コントロールを有効にする：** AEM forms でディレクトリサーバーからデータを一括で取得できる LDAP コントロール。LDAP ディレクトリとして Sun One を使用していて、ディレクトリに含まれるユーザー数が多い場合は、VLV を有効にすると User Management がユーザーの検索に使用できるインデックスが作成されます。この機能は、限定された量のデータしか同期できない標準ユーザーアカウントを使用するときに役立ちます。VLV をグループに対して有効にすることもできます。 「仮想一覧表示 (VLV) コントロールを有効にする」を選択した場合は、「フィールドを並べ替え」ボックスに名前を指定します。

>[!NOTE]
>
>VLV を有効にするには、Sun One を設定します。 （[仮想一覧表示（VLV）を使用するように User Management を設定する](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv)を参照。）

**ソートフィールド：**「仮想一覧表示（VLV）コントロールを有効にする」を選択した場合、インデックスのソートに使用する属性名を指定します。この属性名（uid など）は、ディレクトリサーバーで VLV のインデックスを作成したときに指定した名前です。

### グループ設定 {#group-settings}

**一意の ID：**（必須）グループの識別に使用する一意で固定の属性。DN 以外の属性を一意の識別子として使用します。 この設定は、ディレクトリサーバーによって異なります。Active Directory 2003 での値は objectGUID、Sun One では nsuniqueID、eDirectory では guid です。

>[!NOTE]
>
>組織内で一意であることが保証された属性を入力していることを確認してください。 誤った値を入力すると、システムに重大な問題が発生する可能性があります。

**ベース DN：**（必須）ディレクトリの基本識別名。

BaseDN は管理コンソールの必須の設定ですが、IBM Domino Enterprise Server などの一部のディレクトリサーバーでは空の BaseDN が必要です。 空の BaseDN を指定するには、config.xml ファイルを書き出し、config.xml ファイルの設定を編集してから、再度読み込みます。 ( 詳しくは、 [設定ファイルの読み込みと書き出し](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**検索フィルター：**（必須）グループに関連付けられているレコードを検索するために使用する検索フィルター。1 レベル検索またはサブレベル検索を実行できます。

**説明：**&#x200B;グループの説明のスキーマ属性。

**フルネーム：**（必須）グループのフルネームのスキーマ属性。

**メンバー DN：**（必須）グループ内のメンバーの識別名のスキーマ属性。

**メンバーの一意の ID：**&#x200B;選択したグループのメンバーであるユーザーまたはグループのユニークな識別子。この値は、ディレクトリサーバーによって異なります。AD2003 の場合の値は objectSID、Sun One の場合は nsuniqueID、eDirectory の場合は guid です。

Member DN が DN 以外の属性で指定されている場合、User Management は Member Unique Identifier を使用して LDAP に問い合わせ、一意の識別子値に対応するユーザーの DN を収集します。

一意の識別子として DN を指定する場合は、メンバーの一意の識別子を設定する必要はありません。

**組織：**&#x200B;グループが所属している組織の名前のスキーマ属性。

**プライマリメール：**&#x200B;グループのプライマリメールアドレスのスキーマ属性。

**セカンダリメール：**&#x200B;グループのセカンダリメールアドレスのスキーマ属性。

**タイムスタンプを変更：**&#x200B;差分ディレクトリ同期を有効にするには、この値を modify TimeStamp に設定します。（「差分ディレクトリ同期の有効化」を参照）。

**仮想一覧表示（VLV）コントロールを有効にする：** AEM Forms がディレクトリサーバーからデータをバッチで取得できるようにする LDAP コントロール。LDAP ディレクトリとして Sun One を使用しており、ディレクトリに含まれるグループ数が多い場合は、VLV を有効にすると User Management がグループの検索に使用できるインデックスが作成されます。この機能は、限定された量のデータのみ同期できる標準ユーザーアカウントを使用するときに役立ちます。VLV をユーザーに対して有効にすることもできます。 「仮想一覧表示 (VLV) コントロールを有効にする」を選択した場合は、並べ替えフィールド名を指定します。

>[!NOTE]
>
>VLV を有効にするには、Sun One を設定します。 [仮想一覧表示（VLV）での User Management の設定](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv)を参照。

**ソートフィールド名：**「仮想一覧表示（VLV）コントロールを有効にする」を選択した場合、インデックスのソートに使用する属性名を指定します。この属性名は、ディレクトリサーバーに VLV のインデックスを作成したときに指定した名前です。

>[!NOTE]
>
>「テスト」をクリックして、ユーザー設定とグループ設定が BaseDN および検索条件に基づいて収集されることを確認します。

ユーザーとグループが返される場合、属性セットに従って各フィールドに割り当てられた値が結果に表示されます。

>[!NOTE]
>
>User Management は、1 つのドメイン内でのユーザー ID の重複をサポートしていません。同期されるのは、そのユーザー ID を持つ 1 人のユーザーのみです。

## Virtual List View (VLV) を使用するように User Management を設定する {#configure-user-management-to-use-virtual-list-view-vlv}

ディレクトリの同期は、User Management にとって重要な要件です。 役割と権限を割り当てるために、エンタープライズディレクトリからAEM forms データベースにユーザーとグループが同期されます。 ユーザー数は要件に応じて 100 ～ 100000以降で異なり、データを効率的に同期するためのエンジニアリング上の課題となります。

LDAP プロトコルは、要求制御を使用して大きなデータセットをページ分けされた方法でクエリするメカニズムを提供します。 Microsoft Active Directory を使用する場合、LDAP からAEM forms へのデータベース同期では、PagedResultsControl を使用して、特定のサイズのデータを一括で取得します。 Sun ONE Directory Server はこのコントロールをサポートしていません。 Sun ONE Directory Server に対するページ分割クエリを完了するには、Virtual List View(VLV) コントロールを使用します。 このコントロールには、ディレクトリサーバー側の設定とクライアント側の実装の両方が含まれます。

>[!NOTE]
>
>この節では、Sun ONE Directory Server に対する VLV コントロールの使用について説明します。 ただし、VLV コントロールをサポートする任意のディレクトリサーバーに対して、このコントロールを使用することができます。

1. ディレクトリを設定する際に、ユーザー設定ページとグループ設定ページの両方で、「仮想一覧表示 (VLV) コントロールを有効にする」を選択します。 このチェックボックスをオンにした場合は、[ フィールドの並べ替え ] ボックスで並べ替え名を指定する必要があります。 デフォルト値は uid です。 ( 詳しくは、 [ディレクトリまたはカスタム SPI の追加](configuring-directories.md#adding-directories-or-custom-spis) または [ディレクトリの編集](configuring-directories.md#edit-a-directory).)
1. Sun ONE 管理コンソールまたはコマンドラインスクリプトを使用して、ユーザーおよびグループの LDAP VLV エントリを作成します。 コマンドラインスクリプトを使用する場合は、サンプルのユーザーおよびグループ LDIF ファイルを使用できます。 ( 詳しくは、 [VLV 用の Sun ONE Directory Server の設定](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv).)
1. サーバーを停止し、必要なインデックスを作成します。 ( 詳しくは、 [VLV のディレクトリサーバーインデックスの作成](configuring-directories.md#create-the-directory-server-index-for-vlv).)

### VLV 用の Sun ONE Directory Server の設定 {#configuring-the-sun-one-directory-server-for-vlv}

VLV を作成するには、`vlvSearch` および `vlvIndex` の各オブジェクトクラスが含まれている 1 組のエントリが必要です。vlvSearch エントリには検索ベースおよび `vlvFilter` 属性が含まれており、このうち vlvFilter 属性ではソート対象の属性が含まれているオブジェクトクラスを指定します。`vlvIndex` オブジェクトクラスには、ソート対象の属性とソート順序を指定する `vlvSort` 属性が含まれています。( マイナス記号 (-) はアルファベットの逆順を表します )。 AEM forms で VLV を使用するには、ユーザーとグループに対して別々のエントリが必要です。

>[!NOTE]
>
>Object エントリは、Sun ONE のグラフィカルユーザーインターフェイス (GUI) を使用するか、コマンドラインスクリプトを使用して作成できます。 GUI を使用してオブジェクトエントリを作成する手順については、Sun ONE のマニュアルを参照してください。

ユーザー向けの VLV エントリ用のサンプルスクリプト LDIF を次に示します。

```text
 dn: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 objectclass: top
 objectclass: vlvSearch
 cn: lcuser
 vlvBase: dc=corp,dc=adobe,dc=com
 vlvScope: 2
 vlvFilter: (&(objectclass=inetOrgPerson))
 aci: (target="ldap:///cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config")(targetattr="*")(version 3.0; acl "Config"
 ;allow(read,search,compare) userdn="ldap:///all"; )
 dn: cn=lcuser,cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 cn: lcuser
 vlvSort: cn
 objectclass: top
 objectclass: vlvIndex
```

**スクリプトを使用してオブジェクトエントリを作成する**

1. サンプルスクリプトには `lcuser` という LDAP エントリがあります。このエントリは、AEM forms でのユーザー同期用の VLV 関連の設定用です。 それに応じて、次のプロパティを変更します。

   **エントリ名：**&#x200B;このサンプルのエントリ名は `lcuser` です。`lcuser` を変更する場合は、サンプルスクリプトのすべての領域で変更する必要があります。

   **vlvBase:** ユーザー設定ページで指定された BaseDN。

   **vlvFilter:** ユーザー設定ページで指定された検索フィルター。

   **vlvSort:** ユーザー設定ページの VLV 設定セクションで指定された並べ替えフィールドです。 VLV コントロールでは、並べ替えコントロールを指定する必要があります。 このフィールドは、作成された vlv インデックスの並べ替えパラメーターとして使用されます。

   **aci:** サンプルスクリプトで指定されたアクセス制御は、認証済みユーザーに対し、VLV インデックスにアクセスして読み取り、検索、比較の各操作をおこなう権限を付与します。 管理者は、User Management ユーザーインターフェイスで指定されたディレクトリサーバー設定ページで設定された、バインドユーザーに対するアクセスを制限できます。 権限が与えられていない場合、ユーザー検索で VLV を使用できず、LDAP サーバーが権限の例外をスローします。

   >[!NOTE]
   >
   >慣例により、vlvIndex エントリ名も `lcuser` に設定しますが、異なる名前を付けることもできます。vlvindex ツールには同じ名前を使用します。（[ディレクトリサーバーでの VLV のインデックスの作成&#x200B;](configuring-directories.md#create-the-directory-server-index-for-vlv)*を参照。）*

1. Sun ONE サーバーに付属の `ldapmodify` ツールを使用して、グループのベース DN、検索フィルターおよびソートフィールドをそれぞれ使用して、グループに同様のエントリを作成します。

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   例えば、次のテキストを入力します。

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### VLV のディレクトリサーバーインデックスの作成 {#create-the-directory-server-index-for-vlv}

ディレクトリ設定を指定し、ユーザーおよびグループの LDAP VLV エントリを作成したら、サーバーを停止し、必要なインデックスを作成します。

1. オブジェクトエントリを作成した後、Sun ONE Server を停止します。
1. vlvindex ツールを使用して、次のテキストを入力してインデックスを生成します。

   *ディレクトリサーバーインスタンス* `\vlvindex.bat -n userRoot -T lcuser`

   次の出力が生成されます。

   ```shell
    D:\tools\ldap\sun\shared\bin>..\..\slapd-chetanmeh-xp3\vlvindex.bat -n userRoot -T livecycle
    [21/Nov/2007:16:47:26 +051800] - userRoot: Indexing VLV: livecycle
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 1000 entries (5%).
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 2000 entries (9%).
    ...
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 20000 entries (94%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 21000 entries (99%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Finished indexing.
   ```

   vlvindex ツールは、ディレクトリサーバーインスタンスディレクトリに存在します。 Sun ONE Server に server1 と server2 を実行する 2 つのインスタンスがある場合、vlvindex ツールは *Sun ONE サーバディレクトリ*\server1 ディレクトリ。 パラメーター `-T` の値は、サンプル LDIF で既に作成した vlvindex エントリの `cn` 属性の値となります。この場合、値は `lcuser` です。

1. VLV がグループに対しても有効になっている場合は、グループに対応するインデックスを作成します。 次のコマンドを実行して、インデックスが作成されているかどうかを確認します。

   *sun one server directory* `\shared\bin>ldapsearch -h`*hostname* `-p`*port no* `-s base -b "" objectclass=*`

   次のサンプルデータのような出力が生成されます。

   ```shell
    D:\tools\ldap\sun\shared\bin>ldapsearch.exe -h localhost -p 55850 -s base -b "" objectclass=*
    ldapsearch.exe: started Tue Nov 27 16:34:20 2007
    version: 1
    dn:
    objectClass: top
    namingContexts: dc=corp,dc=adobe,dc=com
    supportedExtension: 2.16.840.1.113730.3.5.7
    ...
    vlvsearch: cn=MCC ou=testdata dc=corp dc=adobe dc=com, cn=userRoot,cn=ldbm dat
        abase,cn=plugins,cn=config
    vlvsearch: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
    vlvsearch: cn=Browsing ou=testdata,cn=userRoot,cn=ldbm database,cn=plugins,cn=
        config
    1 matches
   ```
