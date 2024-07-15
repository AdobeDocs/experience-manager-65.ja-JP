---
title: ディレクトリの設定
description: ディレクトリの追加、編集、削除の方法、および仮想一覧表示を使用するようにユーザー管理を設定する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 30edcef2-e8fa-403a-9850-b8dfeeb9ac65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '3229'
ht-degree: 100%

---

# ディレクトリの設定 {#configuring-directories}

設定するエンタープライズドメインごとに、認証プロバイダーがユーザー情報のクエリーを実行するディレクトリを指定します。1 つのドメインに対して複数のディレクトリを設定できます。

## ディレクトリまたはカスタム SPI の追加 {#adding-directories-or-custom-spis}

設定するエンタープライズドメインごとに、認証プロバイダーがユーザー情報のクエリーを実行するディレクトリを指定します。既存のエンタープライズドメインまたは追加する新しいエンタープライズドメインにディレクトリを追加できます。1 つのドメインに対して複数のディレクトリを設定できます。また、ドメインでカスタムのサービスプロバイダーインターフェイス（SPI）を同期に使用するように設定することもできます。

### ディレクトリの追加 {#add-a-directory}

1. 管理コンソールで、設定／User Management／ドメイン管理をクリックします。
1. 「新規エンタープライズドメイン」をクリックするか、既存のエンタープライズドメインを選択します。
1. 「ディレクトリを追加」をクリックします。
1. 「プロファイル名」ボックスに、このディレクトリを識別できる名前を入力し、「次へ」をクリックします。
1. ディレクトリサーバーの設定を行います（[ディレクトリ設定](configuring-directories.md#directory-settings)を参照）。
1. LDAP サーバーに接続できることを確認するには、「テスト」をクリックします。テストが失敗した場合は、エラーの根本原因を特定するために、アプリケーションサーバーのログファイルで例外を確認します。「閉じる」をクリックし、「次へ」をクリックします。
1. 「ユーザー設定」を選択し、必要に応じて設定を行います（[ディレクトリ設定](configuring-directories.md#directory-settings)を参照）。
1. BaseDN など設定した属性で正しいユーザーの集合が収集されることを確認するには、「テスト」をクリックします。LDAP で、指定された設定（BaseDN、検索フィルター、すべての属性など）を使用して最初の 200 件のレコードの取得が試行されます。

   ユーザーが返される場合、属性セットに従って各フィールドに割り当てられる値が結果に示されます。サーバー名が存在しないこと、認証情報が正しくないことまたは属性が正しくないことが原因でテストが失敗した場合は、「指定した検索条件では結果が返されませんでした」というエラーメッセージが表示されます。エラーの根本原因を特定するには、アプリケーションサーバーのログファイルで例外を確認します。「閉じる」をクリックし、「次へ」をクリックします。

1. 「グループ設定」を選択し、必要に応じて設定を行います（[ディレクトリ設定](configuring-directories.md#directory-settings)を参照）。
1. BaseDN などの設定した属性で正しいグループの集合が収集されることを確認するには、「テスト」をクリックします。グループが返される場合、属性セットに従って各フィールドに割り当てられる値が結果に示されます。「閉じる」をクリックします。

### カスタム SPI の追加 {#add-a-custom-spi}

カスタム SPI の作成について詳しくは、「[AEM Forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63_jp)」内の「AEM Forms の SPI の開発」を参照してください。新しくデプロイしたカスタム SPI をドメインとの関連付けに使用できるようにするには、サーバーを再起動します。

1. 管理コンソールで、設定／User Management／ドメイン管理をクリックします。
1. 「新規エンタープライズドメイン」をクリックするか、既存のエンタープライズドメインを選択します。
1. 「ディレクトリを追加」をクリックします。
1. 「プロファイル名」ボックスに名前を入力するか、「カスタム SPI プロバイダー」を選択し、「次へ」をクリックします。
1. リストからカスタムユーザープロバイダーを選択し、「次へ」をクリックします。
1. リストからカスタムグループプロバイダーを選択し、「完了」をクリックします。

## ディレクトリの編集 {#edit-a-directory}

設定済みのディレクトリの詳細を編集できます。

1. 管理コンソールで、設定／User Management／ドメイン管理をクリックします。
1. リストから目的のドメインをクリックし、表示されるページで、リストから目的のディレクトリを選択します。
1. 必要に応じて、ディレクトリ、ユーザーおよびグループの設定を行います（[ディレクトリ設定](configuring-directories.md#directory-settings)を参照）。
1. 「OK」をクリックします。

## ディレクトリの削除 {#delete-a-directory}

ディレクトリを削除した後にドメインを同期すると、そのディレクトリ内のすべてのユーザーとグループがデータベース内で古いものとしてマークされます。これらは、管理コンソールからの検索では返されません。

>[!NOTE]
>
>エンタープライズドメインには、少なくとも 1 つの認証プロバイダーとディレクトリプロバイダーが必要です。

1. 管理コンソールで、設定／User Management／ドメイン管理をクリックします。
1. リストから目的のドメインをクリックします。
1. 適切なディレクトリのチェックボックスを選択し、「削除」をクリックします。
1. 表示される確認ページで「OK」をクリックし、「OK」を再度クリックします。

## ディレクトリ設定 {#directory-settings}

ドメインにディレクトリを追加するときは、次のディレクトリ設定を指定します。

**サーバー：**（必須）ディレクトリサーバーの完全修飾ドメイン名（FQDN）。例えば、adobe.com ネットワーク上の x というコンピューターの場合、FQDN は x.adobe.com です。FQDN サーバー名の代わりに IP アドレスを使用することもできます。

**ポート：**（必須）ディレクトリサーバーによって使用されるポート。通常は 389 で、Secure Sockets Layer（SSL）プロトコルを使用してネットワーク経由で認証情報を送信する場合は 636 です。

**SSL：**（必須）ネットワーク経由でデータを送信するときにディレクトリサーバーで SSL を使用するかどうかを指定します。デフォルトは「いいえ」です。「はい」に設定する場合、対応する LDAP サーバー証明書はアプリケーションサーバーの Java™ ランタイム環境（JRE）によって信頼されている必要があります。

**連結**（必須）ディレクトリへのアクセス方法を指定します。

**匿名：**&#x200B;ユーザー名またはパスワードは不要です。匿名ユーザーは限られた量のデータしか取得できない場合があります。このオプションは、初期テストに役立つ場合があります。

**ユーザー：**&#x200B;認証が必要です。 「名前」ボックスに、ディレクトリにアクセスできるユーザーレコードの名前を指定します。ユーザーアカウントの完全な識別名（DN）を入力することをお勧めします。例えば、cn=Jane Doe, ou=user, dc=can, dc=com などです。「パスワード」ボックスに、関連付けられているパスワードを指定します。これらの設定は、「バインド」オプションとして「ユーザー」を選択する場合は必須です。

**名前：**&#x200B;匿名アクセスが有効になっていないときに、LDAP データベースに接続するために使用できる名前です。Active Directory 2003 の場合、`[domain name]\[userid]` を指定します。Sun™ One、eDirectory または IBM Tivoli Directory Server の場合、uid=lcuser,ou=it,o=company.com のようにユーザーの完全修飾名を指定します。

**パスワード：**&#x200B;匿名アクセスが有効になっていないときに、LDAP データベースに接続するために指定した名前に対応するパスワードです。

**ページに次の情報を入力：**&#x200B;選択すると、ユーザー設定ページおよびグループの設定ページの属性に、対応するデフォルトの LDAP 値が設定されます。

**BaseDN を取得：** BaseDN を取得し、ドロップダウンリストに表示します。この設定は、複数の BaseDN がある場合に 1 つの値を選択する必要があるときに便利です。

**リファラルを有効にする：**&#x200B;この設定は、組織が階層構造で編成されている複数の Active Directory ドメインを使用し、1 つの親ドメインにのみディレクトリ設定を指定した場合に適用されます。この状況では、このオプションを選択すると、User Management は子ドメインからユーザーとグループの詳細にアクセスできます。

>[!NOTE]
>
>「テスト」をクリックして、LDAP サーバーに接続できることを確認します。エラーの根本原因を特定するには、アプリケーションサーバーのログファイル内の例外を確認してください。

### ユーザー設定 {#user-settings}

**固有な識別子：**（必須）ユーザーの識別に使用する固有で一定の属性。ユーザーが組織の別部門に異動すると、ユーザーの DN が変わる可能性があるので、一意の ID として DN 以外の属性をを使用します。この設定は、ディレクトリサーバーによって異なります。Active Directory 2003 での値は objectGUID、Sun™ One では nsuniqueID、eDirectory では guid です。

>[!NOTE]
>
>組織内で一意であることが保証される属性を入力してください。間違った値を入力すると、システムに重大な問題が発生する可能性があります。

**BaseDN：** LDAP 階層からユーザーおよびグループを同期するための開始点として設定されます。サービスのために同期する必要があるすべてのユーザーおよびグループを含む、階層の最下位レベルでベース DN を指定することをお勧めします。

ディレクトリ設定で「リファラルを有効にする」オプションを選択した場合は、「ベース DN」オプションを DN の *dc* 部分に設定します。リファラルが機能するには、検索スパンに親ドメインと子ドメインの両方が含まれている必要があります。

>[!NOTE]
>
>この設定にはユーザーの DN を含めないでください。特定のユーザーを同期するには、検索フィルター設定を使用します。

ベース DN は管理コンソールの必須設定ですが、IBM Domino Enterprise Server などの一部のディレクトリ サーバーでは空の BaseDN が必要です。空のベース DN を指定するには、config.xml ファイルを書き出し、config.xml ファイル内の設定を編集して、再度読み込みします（[設定ファイルの読み込みと書き出し](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)を参照）。

**検索フィルター：**（必須）ユーザーに関連付けられているレコードを検索するために使用する検索フィルターです。1 レベル検索またはサブレベル検索を実行できます。（検索フィルター構文または RFC 2254 を参照。）Microsoft AD スキーマのその他の情報については「Active Directory スキーマ」を参照してください。

**説明：**&#x200B;ユーザーについての説明のスキーマ属性

**フルネーム：** （必須）ユーザーのフルネームのスキーマ属性

**ログイン ID：**（必須）ユーザーのログイン ID のスキーマ属性

**姓：**（必須）ユーザーの姓のスキーマ属性

**名：**（必須）ユーザーの名前のスキーマ属性

**イニシャル：**&#x200B;ユーザーのイニシャルのスキーマ属性

**ビジネスカレンダー：**&#x200B;この設定の値（ビジネスカレンダーキー）に基づいて、ビジネスカレンダーをユーザーにマッピングできます。業務カレンダーでは、営業日と休業日を定義します。AEM forms では、リマインダー、締め切り、エスカレーションなどのイベントに関する今後の日時を計算するときに、この業務カレンダーを使用できます。業務カレンダーキーをユーザーに割り当てる方法は、エンタープライズドメイン、ローカルドメイン、ハイブリッドドメインのどれを使用しているかによって異なります。（ビジネスカレンダーの設定を参照。）

エンタープライズドメインを使用している場合は、業務カレンダー設定を LDAP ディレクトリのフィールドにマッピングできます。例えば、ディレクトリ内の各ユーザーレコードに「*国*」フィールドがあり、ユーザーの所在地に基づいて業務カレンダーを割り当てる場合は、「*国*」のフィールド名を業務カレンダー設定の値として指定します。その後、業務カレンダーキー（LDAP ディレクトリの「*国*」フィールドに対して定義された値）を Forms Workflow の業務カレンダーにマッピングできます。

Forms Workflow のページで業務カレンダーキーの名前を表示するために使用される領域のサイズには制限があります。これらのページで業務カレンダーキーの名前が切り捨てられないようにするには、名前を 53 文字未満に制限します。

**タイムスタンプを変更：**&#x200B;差分ディレクトリ同期を有効にするには、この値を設定してタイムスタンプを変更します。（差分ディレクトリ同期の有効化を参照。）

**組織：**&#x200B;ユーザーが所属している組織の名前のスキーマ属性。

**プライマリメール：** ユーザーのプライマリメールアドレスのスキーマ属性。

**セカンダリメール：**&#x200B;ユーザーのセカンダリメールアドレスのスキーマ属性。

**電話：**&#x200B;ユーザーの電話番号のスキーマ属性。

**住所：**&#x200B;ユーザーの郵送先住所のスキーマ属性。

**ロケール：** ISO ロケール情報を含むスキーマ属性。この値は 2 文字の言語コードまたは言語および国コードです。

**タイムゾーン：**&#x200B;ユーザーの所在地のタイムゾーンを含むスキーマ属性。この値は市区町村／国などの文字列です。

**仮想一覧表示（VLV）コントロールを有効にする：** AEM forms でディレクトリサーバーからデータを一括で取得できる LDAP コントロール。LDAP ディレクトリとして Sun One を使用していて、ディレクトリに含まれるユーザー数が多い場合は、VLV を有効にすると User Management がユーザーの検索に使用できるインデックスが作成されます。この機能は、限定された量のデータしか同期できない標準ユーザーアカウントを使用するときに役立ちます。VLV をグループに対して有効にすることもできます。「仮想リストビュー（VLV）コントロールを有効にする」を選択する場合は、「フィールドを並べ替え」ボックスに名前を指定します。

>[!NOTE]
>
>VLV を有効にするには、Sun One を構成します。（[仮想一覧表示（VLV）を使用するように User Management を設定する](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv)を参照。）

**ソートフィールド：**「仮想一覧表示（VLV）コントロールを有効にする」を選択した場合、インデックスのソートに使用する属性名を指定します。この属性名（uid など）は、ディレクトリサーバーに VLV のインデックスを作成したときに指定した名前です。

### グループ設定 {#group-settings}

**一意の ID：**（必須）グループの識別に使用する一意で固定の属性。一意の ID には、DN 以外の属性を使用します。この設定は、ディレクトリサーバーによって異なります。Active Directory 2003 での値は objectGUID、Sun One では nsuniqueID、eDirectory では guid です。

>[!NOTE]
>
>組織内で一意であることが保証される属性を入力してください。間違った値を入力すると、システムに重大な問題が発生する可能性があります。

**ベース DN：**（必須）ディレクトリの基本識別名。

ベース DN は管理コンソールの必須設定ですが、IBM Domino Enterprise Server などの一部のディレクトリ サーバーでは空の BaseDN が必要です。空のベース DN を指定するには、config.xml ファイルを書き出し、config.xml ファイル内の設定を編集して、再度読み込みします（[設定ファイルの読み込みと書き出し](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)を参照）。

**検索フィルター：**（必須）グループに関連付けられているレコードを検索するために使用する検索フィルター。1 レベル検索またはサブレベル検索を実行できます。

**説明：**&#x200B;グループの説明のスキーマ属性。

**フルネーム：**（必須）グループのフルネームのスキーマ属性。

**メンバー DN：**（必須）グループ内のメンバーの識別名のスキーマ属性。

**メンバーの一意の ID：**&#x200B;選択したグループのメンバーであるユーザーまたはグループのユニークな識別子。この値は、ディレクトリサーバーによって異なります。AD2003 の場合の値は objectSID、Sun One の場合は nsuniqueID、eDirectory の場合は guid です。

メンバー DN が DN 以外の属性で指定されている場合、User Management はメンバーの一意の ID を使用して LDAP にクエリを実行し、一意の ID の値に対応するユーザーの DN を収集します。

一意の ID として DN が指定されている場合は、メンバーの一意の ID を設定する必要はありません。

**組織：**&#x200B;グループが所属している組織の名前のスキーマ属性。

**プライマリメール：**&#x200B;グループのプライマリメールアドレスのスキーマ属性。

**セカンダリメール：**&#x200B;グループのセカンダリメールアドレスのスキーマ属性。

**タイムスタンプを変更：**&#x200B;差分ディレクトリ同期を有効にするには、この値を modify TimeStamp に設定します。（「差分ディレクトリ同期の有効化」を参照）。

**仮想一覧表示（VLV）コントロールを有効にする：** AEM Forms がディレクトリサーバーからデータをバッチで取得できるようにする LDAP コントロール。LDAP ディレクトリとして Sun One を使用しており、ディレクトリに含まれるグループ数が多い場合は、VLV を有効にすると User Management がグループの検索に使用できるインデックスが作成されます。この機能は、限定された量のデータのみ同期できる標準ユーザーアカウントを使用するときに役立ちます。ユーザーに対して VLV を有効にすることもできます。「仮想リストビュー（VLV）コントロールを有効にする」を選択した場合は、並べ替えフィールド名を指定します。

>[!NOTE]
>
>VLV を有効にするには、Sun One を構成します。[仮想一覧表示（VLV）での User Management の設定](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv)を参照。

**ソートフィールド名：**「仮想一覧表示（VLV）コントロールを有効にする」を選択した場合、インデックスのソートに使用する属性名を指定します。この属性名は、ディレクトリサーバーに VLV のインデックスを作成したときに指定した名前です。

>[!NOTE]
>
>「テスト」をクリックして、ユーザー設定とグループ設定が BaseDN および検索条件に基づいて収集されることを確認します。

ユーザーとグループが返された場合、結果には、属性セットに従って各フィールドに割り当てられた値が表示されます。

>[!NOTE]
>
>User Management では、ドメイン内でのユーザー ID の重複をサポートしていません。ユーザー ID を持つ 1 人のユーザーのみが同期されます。

## 仮想リストビュー（VLV）での User Management の設定 {#configure-user-management-to-use-virtual-list-view-vlv}

ディレクトリの同期は、User Management の重要な要件です。ユーザーとグループは、ロールと権限を割り当てるために、エンタープライズディレクトリから AEM Forms データベースに同期されます。ユーザー数は要件に応じて 100 から 100,000 まで変化し、データを効率的に同期することがエンジニアリング上の課題となります。

LDAP プロトコルは、リクエストコントロールを使用して、ページ分割された方法で大規模なデータセットをクエリするメカニズムを提供します。Microsoft Active Directory を使用する場合、LDAP から AEM Forms データベースへの同期では PagedResultsControl を使用して、特定のサイズのバッチでデータを取得します。Sun ONE Directory Server は、この制御をサポートしていません。Sun ONE Directory Server に対するページ分割されたクエリを完了するには、仮想リストビュー（VLV）コントロールを使用します。このコントロールには、ディレクトリのサーバーサイドの設定とクライアントサイドの実装の両方が含まれます。

>[!NOTE]
>
>このセクションでは、Sun ONE Directory Server の VLV コントロールの使用について説明します。ただし、このコントロールは、VLV コントロールをサポートする任意のディレクトリサーバーに使用できます。

1. ディレクトリを構成するときは、「ユーザー設定」ページと「グループ設定」ページの両方で「仮想リスト ビュー（VLV）コントロールを有効にする」を選択します。チェックボックスをオンにした場合は、並べ替えフィールドボックスに並べ替え名も指定する必要があります。デフォルト値は「uid」です。（[ディレクトリまたはカスタム SPI の追加](configuring-directories.md#adding-directories-or-custom-spis)または[ディレクトリの編集](configuring-directories.md#edit-a-directory)を参照してください。）
1. Sun ONE 管理コンソールまたはコマンド行スクリプトを使用して、ユーザーおよびグループの LDAP VLV エントリを作成します。コマンドラインスクリプトを使用する場合は、サンプルのユーザーとグループの LDIF ファイルを使用できます（[VLV 用の Sun ONE Directory Server の構成](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv)を参照）。
1. サーバーを停止し、必要なインデックスを作成します（[ディレクトリサーバーでの VLV のインデックスの作成](configuring-directories.md#create-the-directory-server-index-for-vlv)を参照）。

### VLV 用の Sun ONE Directory Server の設定 {#configuring-the-sun-one-directory-server-for-vlv}

VLV を作成するには、`vlvSearch` および `vlvIndex` の各オブジェクトクラスが含まれている 1 組のエントリが必要です。vlvSearch エントリには検索ベースおよび `vlvFilter` 属性が含まれており、このうち vlvFilter 属性ではソート対象の属性が含まれているオブジェクトクラスを指定します。`vlvIndex` オブジェクトクラスには、ソート対象の属性とソート順序を指定する `vlvSort` 属性が含まれています。（「-」符号はアルファベットの逆順であることを示します）。AEM Forms で VLV を使用するには、ユーザーのエントリとグループのエントリを個別に作成する必要があります。

>[!NOTE]
>
>オブジェクトエントリを作成するには、Sun ONE グラフィカルユーザーインターフェイス（GUI）またはコマンドラインスクリプトを使用します。GUI を使用してオブジェクトエントリを作成する手順については、Sun One のドキュメントを参照してください。

ここでは、ユーザーの VLV エントリ用のサンプルスクリプト LDIF を示します。

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

**スクリプトを使用したオブジェクトエントリの作成**

1. サンプルスクリプトには `lcuser` という LDAP エントリがあります。このエントリは、AEM Forms でユーザー同期を実現する VLV 関連設定用のエントリです。適宜、次のプロパティを変更します。

   **エントリ名：**&#x200B;このサンプルのエントリ名は `lcuser` です。`lcuser` を変更する場合は、サンプルスクリプトのすべての領域で変更する必要があります。

   **vlvBase：**&#x200B;ユーザー設定ページに指定されている BaseDN です。

   **vlvFilter：**&#x200B;ユーザー設定ページに指定されている検索フィルターです。

   **vlvSort：**&#x200B;ユーザー設定ページの VLV 設定セクションに指定されているソートフィールドです。VLV コントロールには、ソートコントロールを指定する必要があります。このフィールドは、作成した vlv インデックスのソートパラメーターとして使用されます。

   **aci：**&#x200B;サンプルスクリプトで指定されているアクセス制御は、認証済みユーザーに対して、VLV インデックスにアクセスして読み取り、検索、比較の各操作を実行する権限を付与します。管理者は、User Management ユーザーインターフェイスのディレクトリサーバー設定ページに設定されているバインドユーザーにアクセスを制限できます。権限が付与されていない場合、ユーザー検索で VLV を使用できなくなり、LDAP サーバーで権限の例外が発生します。

   >[!NOTE]
   >
   >慣例により、vlvIndex エントリ名も `lcuser` に設定しますが、異なる名前を付けることもできます。vlvindex ツールには同じ名前を使用します。（[ディレクトリサーバーでの VLV のインデックスの作成&#x200B;](configuring-directories.md#create-the-directory-server-index-for-vlv)*を参照。）*

1. Sun ONE サーバーに付属の `ldapmodify` ツールを使用して、グループのベース DN、検索フィルターおよびソートフィールドをそれぞれ使用して、グループに同様のエントリを作成します。

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   例えば、次のテキストを入力します。

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### ディレクトリサーバーでの VLV のインデックスの作成 {#create-the-directory-server-index-for-vlv}

ディレクトリの設定を行い、ユーザーおよびグループに対して LDAP VLV エントリを作成したら、サーバーを停止し、必要なインデックスを作成します。

1. オブジェクトエントリを作成した後、Sun ONE サーバーを停止します。
1. vlvindex ツールを使用し、次のテキストを入力してインデックスを生成します。

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

   vlvindex ツールは、ディレクトリサーバーインスタンスディレクトリにあります。Sun ONE サーバーで server1 および server2 の 2 つのインスタンスが動作している場合、vlvindex ツールは、*Sun ONE server directory*\server1 directory ディレクトリにあります。パラメーター `-T` の値は、サンプル LDIF で既に作成した vlvindex エントリの `cn` 属性の値となります。この場合、値は `lcuser` です。

1. VLV がグループに対しても有効になっている場合は、グループについて対応するインデックスを作成します。次のコマンドを実行して、インデックスが作成されているかどうかを確認します。

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
