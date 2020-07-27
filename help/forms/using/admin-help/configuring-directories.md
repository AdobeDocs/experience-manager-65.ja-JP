---
title: ディレクトリの設定
seo-title: ディレクトリの設定
description: ディレクトリの追加、編集、削除の方法、および仮想一覧表示を使用するようにユーザー管理を設定する方法を学習します。
seo-description: ディレクトリの追加、編集、削除の方法、および仮想一覧表示を使用するようにユーザー管理を設定する方法を学習します。
uuid: 0bf1a8a7-c917-4248-9937-d24e31c5ba17
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1f15f028-aa81-478e-97eb-f83a4dc0418c
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '3246'
ht-degree: 79%

---


# ディレクトリの設定 {#configuring-directories}

設定するエンタープライズドメインごとに、認証プロバイダーがユーザー情報のクエリーを実行するディレクトリを指定します。1 つのドメインに対して複数のディレクトリを設定できます。

## ディレクトリまたはカスタム SPI の追加 {#adding-directories-or-custom-spis}

設定するエンタープライズドメインごとに、認証プロバイダーがユーザー情報のクエリーを実行するディレクトリを指定します。既存のエンタープライズドメインまたは追加する新しいエンタープライズドメインにディレクトリを追加できます。1 つのドメインに対して複数のディレクトリを設定できます。また、ドメインでカスタムのサービスプロバイダーインターフェイス（SPI）を同期に使用するように設定することもできます。

### ディレクトリの追加 {#add-a-directory}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
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

カスタム SPI の作成について詳しくは、「[AEM Forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63)」の「AEM Forms の SPI の開発」を参照してください。新しくデプロイしたカスタム SPI をドメインとの関連付けに使用できるようにするには、サーバーを再起動します。

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 「新規エンタープライズドメイン」をクリックするか、既存のエンタープライズドメインを選択します。
1. 「ディレクトリを追加」をクリックします。
1. 「プロファイル名」ボックスに名前を入力するか、「カスタム SPI プロバイダー」を選択し、「次へ」をクリックします。
1. リストからカスタムユーザープロバイダーを選択し、「次へ」をクリックします。
1. リストからカスタムグループプロバイダーを選択し、「完了」をクリックします。

## ディレクトリの編集 {#edit-a-directory}

設定済みのディレクトリの詳細を編集できます。

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. リストから目的のドメインをクリックし、表示されるページで、リストから目的のディレクトリを選択します。
1. 必要に応じて、ディレクトリ、ユーザーおよびグループの設定を行います（[ディレクトリ設定](configuring-directories.md#directory-settings)を参照）。
1. 「OK」をクリックします。

## ディレクトリの削除 {#delete-a-directory}

ディレクトリの削除後にドメインを同期すると、そのディレクトリ内のすべてのユーザーとグループはデータベース内で古い情報としてマークされます。これらの情報は、管理コンソールで検索しても返されません。

>[!NOTE]
>
>エンタープライズドメインには、少なくとも 1 つの認証プロバイダーまたはディレクトリプロバイダーが必要です。

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. リストから目的のドメインをクリックします。
1. 目的のディレクトリのチェックボックスをオンにし、「削除」をクリックします。
1. 表示される確認ページで「OK」をクリックし、もう一度「OK」をクリックします。

## ディレクトリ設定 {#directory-settings}

ディレクトリをドメインに追加するときは、次のディレクトリ設定を指定します。

**サーバー：** （必須）ディレクトリサーバーの完全修飾ドメイン名(FQDN)。 例えば、corp.adobe.com ネットワーク上の x というコンピューターの場合、FQDN は x.corp.adobe.com です。FQDN サーバー名の代わりに IP アドレスを使用することもできます。

**ポート：** （必須）ディレクトリサーバーが使用するポート。 通常は 389 で、Secure Sockets Layer（SSL）プロトコルを使用してネットワーク経由で認証情報を送信する場合は 636 です。

**SSL:** （必須）ネットワーク経由でデータを送信する際に、ディレクトリサーバーでSSLを使用するかどうかを指定します。 デフォルトは「いいえ」です。「はい」に設定する場合、対応する LDAP サーバー証明書はアプリケーションサーバーの Java™ ランタイム環境（JRE）によって信頼されている必要があります。

**連結** （必須）ディレクトリへのアクセス方法を指定します。

**匿名：** ユーザー名やパスワードは不要です。 匿名ユーザーは、限定されたデータ量のみ取得することができます。このオプションは、初期テストに役立ちます。

**ユーザー：** 認証が必要です。 「名前」ボックスに、ディレクトリにアクセスできるユーザーレコードの名前を指定します。ユーザーアカウントの完全な識別名（DN）を入力することをお勧めします。例えば、cn=Jane Doe, ou=user, dc=can, dc=com などです。「パスワード」ボックスに、関連付けられているパスワードを指定します。これらの設定は、「バインド」オプションとして「ユーザー」を選択する場合は必須です。

**名前：** 匿名アクセスが有効になっていない場合に、LDAPデータベースへの接続に使用できる名前。 For Active Directory 2003, specify `[domain name]\[userid]`. Sun™ One、eDirectory または IBM Tivoli Directory Server の場合、uid=lcus r,ou=it,o=company.com のようにユーザーの完全修飾名を指定します。

**パスワード：** 匿名アクセスが有効になっていない場合に、LDAPデータベースに接続するために指定した名前に対応するパスワード。

**ページに次を入力：** 選択すると、ユーザー設定ページおよびグループ設定ページの属性に、対応するデフォルトのLDAP値が設定されます。

**BaseDNを取得：** BaseDNを取得し、ドロップダウンリストに表示します。 この設定は、複数の BaseDN がある場合に 1 つの値を選択する必要があるときに便利です。

**照会を有効にする：** この設定は、組織が階層構造で編成された複数のActive Directoryドメインを使用し、親ドメインのみに対してディレクトリ設定を指定した場合に適用されます。 この状況で、このオプションを選択すると、User Management は子ドメインからユーザーおよびグループの詳細にアクセスできます。

>[!NOTE]
>
>「テスト」をクリックして、LDAP サーバーに接続できることを確認します。エラーの根本原因を特定するには、アプリケーションサーバーのログファイルで例外を確認します。

### ユーザー設定 {#user-settings}

**一意の識別子：** （必須）ユーザーの識別に使用される一意で一定の属性。 ユーザーが組織の別部門に異動した場合、ユーザーの DN は変わる可能性があるので、固有な識別子として非 DN 属性を使用します。この設定は、ディレクトリサーバーによって異なります。Active Directory 2003 での値は objectGUID、Sun™ One では nsuniqueID、eDirectory では guid です。

>[!NOTE]
>
>組織内で一意となっている属性が入力されていることを確認してください。入力した値が正しくない場合、システムに重大な問題が発生します。

**BaseDN:** LDAP階層からユーザーとグループを同期するための開始点として設定します。 サービスのために同期する必要があるすべてのユーザーおよびグループを含む階層の最下位レベルの BaseDN を指定することをお勧めします。

ディレクトリ設定で「リファラルを有効にする」オプションを選択した場合、DN の *dc* 部分に「BaseDN」オプションを設定します。リファラルが機能するには、検索範囲に親ドメインと子ドメインの両方が含まれている必要があります。

>[!NOTE]
>
>この設定にユーザーの DN は含めないでください。特定のユーザーを同期するには、検索フィルター設定を使用します。

「BaseDN」は管理コンソールの必須の設定ですが、IBM Domino Enterprise Server などのディレクトリサーバーでは、空の BaseDN が必要になる場合があります。空の BaseDN を指定するには、config.xml ファイルを書き出し、config.xml ファイルの設定を編集して、再度読み込みます（[設定ファイルの読み込みと書き出し](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)を参照）。

**検索フィルタ：** （必須）ユーザーに関連付けられているレコードを検索するために使用する検索フィルター。 1 レベル検索またはサブレベル検索を実行できます（Search Filter Syntax または RFC 2254 を参照）。Microsoft AD スキーマについて詳しくは、Active Directory Schema を参照してください。

**説明：** ユーザーの説明のスキーマ属性。

**フルネーム：** （必須）ユーザーのフルネームのスキーマ属性。

**ログインID:** （必須）ユーザーのログインIDのスキーマ属性。

**姓：** （必須）ユーザーの姓のスキーマ属性。

**名前：** （必須）ユーザーの名のスキーマ属性。

**イニシャル：** ユーザーのイニシャルのスキーマ属性。

**業務カレンダー：** この設定の値（業務カレンダーキー）に基づいて、業務カレンダーをユーザーにマップできます。 業務カレンダーによって稼働日と非稼働日が定義されます。AEM Forms では、リマインダー、デッドラインおよびエスカレーションなどのイベントの今後の日付や時間を計算するときに、この業務カレンダーを使用できます。業務カレンダーキーをユーザーに割り当てる方法は、エンタープライズドメイン、ローカルドメイン、ハイブリッドドメインのどれを使用しているかによって異なります（業務カレンダーの設定を参照）。

エンタープライズドメインを使用している場合は、業務カレンダー設定を LDAP ディレクトリのフィールドにマップできます。例えば、ディレクトリ内の各ユーザーレコードに「*国*」フィールドがあり、ユーザーの所在地に基づいて業務カレンダーを割り当てる場合は、「*国*」のフィールド名を業務カレンダー設定の値として指定します。その後、業務カレンダーキー（LDAP ディレクトリの「*国*」フィールドに対して定義された値）を forms ワークフローの業務カレンダーにマップできます。

forms ワークフローのページで業務カレンダーキーの名前を表示するために使用される領域のサイズには制限があります。これらのページで業務カレンダーキーの名前が切り捨てられないようにするには、名前を 53 文字未満に制限します。

**タイムスタンプの変更：** 差分ディレクトリ同期を有効にするには、この値をmodify TimeStampに設定します。 （差分ディレクトリ同期の有効化を参照）。

**組織：** ユーザーが属する組織の名前のスキーマ属性。

**プライマリ電子メール：** ユーザーのプライマリ電子メールアドレスのスキーマ属性。

**セカンダリ電子メール：** ユーザーのセカンダリ電子メールアドレスのスキーマ属性。

**電話番号：** ユーザーの電話番号のスキーマ属性。

**住所：** ユーザーの住所のスキーマ属性。

**ロケール：** ISOロケール情報を含むスキーマ属性。 この値は 2 文字の言語コードまたは言語および国コードです。

**タイムゾーン：** ユーザーの所在地のタイムゾーンを含むスキーマ属性。 この値は「市区町村／国」などの文字列です。

**仮想リスト表示(VLV)コントロールを有効にする：** AEM Formsがディレクトリサーバーからデータをバッチで取得できるようにするLDAPコントロール。 LDAP ディレクトリとして Sun One を使用しており、ディレクトリに含まれるユーザー数が多い場合は、VLV を有効にすると User Management がユーザーの検索に使用できるインデックスが作成されます。この機能は、限定された量のデータのみ同期できる標準ユーザーアカウントを使用するときに役立ちます。VLV をグループに有効化することもできます。「仮想一覧表示（VLV）コントロールを有効にする」を選択する場合は、「フィールドをソート」ボックスに名前を指定します。

>[!NOTE]
>
>VLV を有効にするには、Sun One を設定しますSee [Configure User Management to use Virtual List View (VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**フィールドの並べ替え：** 「仮想リスト表示(VLV)コントロールを有効にする」を選択した場合は、インデックスの並べ替えに使用する属性名を指定します。 この属性名（uid など）は、ディレクトリサーバーに VLV のインデックスを作成したときに指定した名前です。

### グループの設定 {#group-settings}

**一意の識別子：** （必須）グループの識別に使用する一意で一定の属性。 固有な識別子として DN 以外の属性を使用します。この設定は、ディレクトリサーバーによって異なります。Active Directory 2003 での値は objectGUID、Sun One では nsuniqueID、eDirectory では guid です。

>[!NOTE]
>
>組織内で一意となっている属性が入力されていることを確認してください。入力した値が正しくない場合、システムに重大な問題が発生します。

**BaseDN:** （必須）ディレクトリの基本識別名。

「BaseDN」は管理コンソールの必須の設定ですが、IBM Domino Enterprise Server などのディレクトリサーバーでは、空の BaseDN が必要です。空の BaseDN を指定するには、config.xml ファイルを書き出し、config.xml ファイルの設定を編集して、再度読み込みます（[設定ファイルの読み込みと書き出し](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)を参照）。

**検索フィルタ：** （必須）グループに関連付けられているレコードを検索するために使用する検索フィルター。 1 レベル検索またはサブレベル検索を実行できます。

**説明：** グループの説明のスキーマ属性。

**フルネーム：** （必須）グループのフルネームのスキーマ属性。

**メンバDN:** （必須）グループ内のメンバーの識別名のスキーマ属性。

**Member Unique Identifier:** 選択したグループのメンバーであるユーザーまたはグループの一意の識別子。 この値は、ディレクトリサーバーによって異なります。AD2003 の場合の値は objectSID、Sun One の場合は nsuniqueID、eDirectory の場合は guid です。

「メンバー DN」に DN 以外の属性を指定した場合、User Management では「固有な識別子」の値を使用して LDAP に対するクエリーが実行され、固有な識別子の値に対応するユーザーの DN が収集されます。

固有な識別子として DN を指定した場合は、「固有な識別子」の値を設定する必要はありません。

**組織：** グループが属する組織の名前のスキーマ属性。

**プライマリ電子メール：** グループのプライマリ電子メールアドレスのスキーマ属性。

**セカンダリ電子メール：** グループのセカンダリ電子メールアドレスのスキーマ属性。

**タイムスタンプの変更：** 差分ディレクトリ同期を有効にするには、この値をmodify TimeStampに設定します。 （差分ディレクトリ同期の有効化を参照）。

**仮想リスト表示(VLV)コントロールを有効にする：** AEM Formsがディレクトリサーバーからデータをバッチで取得できるようにするLDAPコントロール。 LDAP ディレクトリとして Sun One を使用しており、ディレクトリに含まれるグループ数が多い場合は、VLV を有効にすると User Management がグループの検索に使用できるインデックスが作成されます。この機能は、限定された量のデータのみ同期できる標準ユーザーアカウントを使用するときに役立ちます。VLV をユーザーに有効化することもできます。「仮想一覧表示（VLV）コントロールを有効にする」を選択する場合は、「Sort Field Name」を指定します。

>[!NOTE]
>
>VLV を有効にするには、Sun One を設定しますSee [Configure User Management to use Virtual List View (VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Sort Field Name:** 「仮想リスト表示(VLV)コントロールを有効にする」を選択した場合は、インデックスの並べ替えに使用する属性名を指定します。 この属性名は、ディレクトリサーバーに VLV のインデックスを作成したときに指定した名前です。

>[!NOTE]
>
>「テスト」をクリックして、ユーザー設定とグループ設定が BaseDN および検索条件に基づいて収集されることを確認します。

ユーザーおよびグループが返される場合、属性セットに従って各フィールドに割り当てられる値が結果に示されます。

>[!NOTE]
>
>User Management では 1 つのドメイン内でのユーザー ID の重複はサポートされておらず、1 つのユーザー ID について 1 人のユーザーのみが同期されます。

## 仮想一覧表示（VLV）での User Management の設定 {#configure-user-management-to-use-virtual-list-view-vlv}

ディレクトリ同期は、User Management にとって重要な要件です。ユーザーやグループは、ロールおよび権限の割り当てのために、エンタープライズディレクトリから AEM Forms データベースに同期されます。ユーザーの数は要件によって 100 から 100,000 以上と様々であり、データを効率的に同期させる際の技術的課題となっています。

LDAP プロトコルには、要求コントロールを使用したページ分割という方法でサイズの大きなデータセットに対してクエリーを実行するメカニズムがあります。Microsoft Active Directory を使用している場合、LDAP から AEM Forms データベースへの同期を実行すると、PagedResultsControl によって特定のサイズのデータがまとめて取得されます。Sun ONE Directory Server は、PagedResultsControl をサポートしていません。Sun ONE Directory Server に対してページ分割クエリーを完了するには、仮想一覧表示（VLV）コントロールを使用します。このコントロールを使用するには、ディレクトリサーバー側での設定とクライアント側での実装が必要です。

>[!NOTE]
>
>ここでは、Sun ONE Directory Server に VLV コントロールを使用する場合について説明します。ただし、VLV コントロールをサポートするディレクトリサーバーであれば、VLV コントロールを使用できます。

1. ディレクトリを設定する場合は、ユーザー設定ページとグループの設定ページの両方で「仮想一覧表示（VLV）コントロールを有効にする」を選択します。このチェックボックスを選択する場合は、「フィールドをソート」ボックスでソート名も指定する必要があります。デフォルト値は「uid」です（[ディレクトリまたはカスタム SPI の追加](configuring-directories.md#adding-directories-or-custom-spis)または [ディレクトリの編集](configuring-directories.md#edit-a-directory)を参照）。
1. ユーザーおよびグループに対して LDAP VLV エントリを作成するには、Sun ONE 管理コンソールまたはコマンドラインスクリプトを使用します。コマンドラインスクリプトでは、ユーザーおよびグループに関するサンプルの LDIF ファイルを使用できます（[VLV 用の Sun ONE Directory Server の設定](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv)を参照）。
1. サーバーを停止し、必要なインデックスを作成します（[ディレクトリサーバーでの VLV のインデックスの作成](configuring-directories.md#create-the-directory-server-index-for-vlv)を参照）。

### VLV 用の Sun ONE Directory Server の設定 {#configuring-the-sun-one-directory-server-for-vlv}

VLV を作成するには、`vlvSearch` および `vlvIndex` の各オブジェクトクラスが含まれている 1 組のエントリが必要です。vlvSearch エントリには検索ベースおよび `vlvFilter` 属性が含まれており、このうち vlvFilter 属性ではソート対象の属性が含まれているオブジェクトクラスを指定します。`vlvIndex` オブジェクトクラスには、ソート対象の属性とソート順序を指定する `vlvSort` 属性が含まれています（「-」符号はアルファベットの逆順であることを示します）。AEM Forms で VLV を使用するには、ユーザーのエントリとグループのエントリを個別に作成する必要があります。

>[!NOTE]
>
>オブジェクトエントリを作成するには、Sun ONE グラフィカルユーザーインターフェイス（GUI）またはコマンドラインスクリプトを使用します。GUI を使用してオブジェクトエントリを作成する手順については、Sun One のマニュアルを参照してください。

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

   **エントリ名：**&#x200B;このサンプルのエントリ名は `lcuser` です。`lcuser` を変更する場合は、サンプルスクリプトのすべての領域で lcuser を変更する必要があります。

   **vlvBase：**&#x200B;ユーザー設定ページに指定されている BaseDN です。

   **vlvFilter：**&#x200B;ユーザー設定ページに指定されている検索フィルターです。

   **vlvSort：**&#x200B;ユーザー設定ページの VLV 設定セクションに指定されているソートフィールドです。VLV コントロールには、ソートコントロールを指定する必要があります。このフィールドは、作成した vlv インデックスのソートパラメーターとして使用されます。

   **aci：**&#x200B;サンプルスクリプトに指定されているアクセス制御は、認証済みユーザーに対して、VLV インデックスにアクセスして読み取り、検索、比較の各操作を実行する権限を付与します。管理者は、User Management ユーザーインターフェイスのディレクトリサーバー設定ページに設定されているバインドユーザーにアクセスを制限できます。権限が付与されていない場合、ユーザー検索で VLV を使用できなくなり、LDAP サーバーで権限の例外が発生します。

   >[!NOTE]
   >
   >慣例により、vlvIndex エントリ名も `lcuser` に設定しますが、異なる名前を付けることもできます。vlvindex ツールにも同じ名前を使用します（[ディレクトリサーバーでの VLV のインデックスの作成](configuring-directories.md#create-the-directory-server-index-for-vlv)*を参照）。*

1. Sun ONE サーバーに付属の `ldapmodify` ツールを使用して、グループの Base DN、検索フィルターおよびソートフィールドをそれぞれ使用して、グループに同様のエントリを作成します。

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   例えば、次のようにテキストを入力します。

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

   vlvindex ツールは、ディレクトリサーバーインスタンスディレクトリにあります。Sun ONE サーバーで server1 および server2 の 2 つのインスタンスが動作している場合、vlvindex ツールは、*Sun ONE server directory*\server1 directory ディレクトリにあります。The value for parameter `-T` is the value of the `cn` attribute of the vlvindex entry created previously in the sample LDIF. この場合、値は `lcuser` です。

1. VLV がグループに対しても有効になっている場合は、グループについて対応するインデックスを作成します。次のコマンドを実行して、インデックスが作成されているかどうかを確認します。

   *sun one server directory* hostname `\shared\bin>ldapsearch -h`**`-p`*port no* `-s base -b "" objectclass=*`

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

