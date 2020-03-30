---
title: Forms User Management | ユーザーデータの処理
seo-title: Forms User Management | ユーザーデータの処理
description: 'null'
seo-description: 'null'
uuid: 2b76b69f-6f3a-4f1a-a2a4-d39f5e529f75
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a88fc933-f1af-4798-b72f-10e7b0d2fd11
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Forms User Management | ユーザーデータの処理 {#forms-user-management-handling-user-data}

User Management は、AEM Forms にアクセスするために AEM Forms ユーザーを作成、管理および認証することができる AEM Forms JEE コンポーネントです。User Management は、ユーザー情報を取得するためのディレクトリとしてドメインを使用します。次の種類のドメインがサポートされます。

**ローカルドメイン**：この種類のドメインは、サードパーティーのストレージシステムに接続されません。代わりに、ユーザーおよびグループがローカルに作成され、User Management データベースに格納されます。パスワードはローカルに保存され、認証はローカルデータベースを使用して実行されます。

**ハイブリッドドメイン**：この種類のドメインは、サードパーティーのストレージシステムには接続されません。代わりに、ユーザーおよびグループがローカルに作成され、User Management データベースに格納されます。ローカルドメインと異なり、ハイブリッドドメインは、外部認証プロバイダー（LDAP、Kerberos、SAML またはカスタム）を使用します。

**エンタープライズドメイン**：LDAP ディレクトリなどのサードパーティーのストレージシステムに格納されているユーザーおよびグループで構成されます。User Management では、サードパーティのストレージシステムに対する書き込みは行われません。代わりに、User Management によってユーザーおよびグループの情報が User Management データベースと同期されます。エンタープライズドメインでは、外部認証プロバイダー（LDAP、Kerberos、SAML またはカスタム）も使用します。

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## ユーザーデータとデータストア {#user-data-and-data-stores}

User Management は、My Sql、Oracle、MS SQL Server、IBM DB2 などのデータベースにユーザーデータを格納します。In addition, any user who has logged in at least once in Forms applications on AEM author at `https://'[server]:[port]'lc`, the user gets created in AEM repository. したがって、User Management のデータは、次のデータストアに格納されます。

* データベース
* AEM リポジトリ
* LDAP ディレクトリなどのサードパーティーストレージ

>[!NOTE]
>
>サードパーティーストレージに格納されたデータについては、この文書で説明していません。このようなストレージでユーザーデータを管理する場合は、サードパーティーのベンダーに直接問い合わせてください。

### データベース {#database}

User Management では、次のデータベーステーブルにユーザーデータが格納されます。

<table>
 <tbody>
  <tr>
   <td>データベーステーブル</td>
   <td>説明</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalEntity</code></td>
   <td><p>プリンシパルエンティティに関する情報を格納します。プリンシパルは、ユーザー、グループ、またはロールのいずれかになります。</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>ユーザーの個人が特定できる情報（PII）を格納します。ローカル、エンタープライズおよびハイブリッドの各ドメインに含まれるすべてのユーザーのエントリが含まれます。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>（OracleおよびMS SQLデータベース）</p> </td>
   <td>ローカルユーザーデータのみを格納します。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>（OracleおよびMS SQLデータベース）</p> </td>
   <td>ローカル、エンタープライズおよびハイブリッドの各ドメインに含まれるすべてのユーザーのエントリが含まれます。これにはユーザーの電子メール ID が含まれます。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code> （OracleおよびMS SQLデータベース）</p> </td>
   <td>ユーザーとグループ間のマッピングを格納します。</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>ユーザーとグループ両方についてロールとプリンシパル間のマッピングを格納します。</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>ユーザーとグループ両方についてプリンシパルとアクセス許可間のマッピングを格納します。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code> （OracleおよびMS SQLデータベース）</p> </td>
   <td>プリンシパルに対応する古い属性値と新しい属性値を格納します。<br /> </td>
  </tr>
 </tbody>
</table>

### AEM リポジトリ {#aem-repository}

User management data for users who have at least once accessed the Forms applications under `https://'[server]:[port]'lc` is stored in AEM repository as well.

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

User Management データベースおよび AEM リポジトリにあるユーザーの User Management データにアクセスしてデータを書き出すことができます。また、必要に応じてデータを永続的に削除できます。

### データベース {#database-1}

User Management データベースのユーザーデータを書き出すまたは削除するには、データベースクライアントを使用してデータベースに接続し、ユーザーの PII に基づいてプリンシパル ID を検索します。例えば、ログイン ID を使用してユーザーのプリンシパル ID を取得するには、次の `select` コマンドをデータベースで実行します。

In the `select` command, replace the `<user_login_id>` with the login ID of the user whose principal ID you want to retrieve.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

プリンシパル ID が分かったら、ユーザーデータを書き出したり、削除したりすることができます。

#### ユーザーデータの書き出し {#export-user-data}

次のデータベースコマンドを実行して、プリンシパル ID の User Management データをデータベーステーブルから書き出します。In the `select` command, replace `<principal_id>` with the principal ID of the user whose data you want to export.

>[!NOTE]
>
>次のコマンドでは、My SQL および IBM DB2 データベースのデータベーステーブル名を使用しています。これらのコマンドを Oracle および MS SQL データベースで実行するときは、コマンドの次のテーブル名を置き換えます。
>
>* Replace `EdcPrincipalLocalAccountEntity` with `EdcPrincipalLocalAccount`
   >
   >
* Replace `EdcPrincipalEmailAliasEntity` with `EdcPrincipalEmailAliasEn`
   >
   >
* Replace `EdcPrincipalMappingEntity` with `EdcPrincipalMappingEntit`
   >
   >
* Replace `EdcPrincipalGrpCtmntEntity` with `EdcPrincipalGrpCtmntEnti`
>



```sql
Select * from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (Select id from EDCPRINCIPALENTITY where id='<principal_id>'));

Select * from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalEntity where id='<principal_id>';
```

#### ユーザーデータの削除 {#delete-user-data}

特定のプリンシパル ID の User Management データをデータベーステーブルから削除するには、次の手順を実行します。

1. 「[ユーザーデータの削除](/help/forms/using/user-management-handling-user-data.md#delete-aem)」の説明に従って AEM リポジトリからユーザーデータを削除します（該当する場合）。
1. AEM Forms サーバーをシャットダウンします。
1. 次のデータベースコマンドを実行して、目的のプリンシパル ID の User Management データをデータベーステーブルから削除します。In the `Delete` command, replace `<principal_id>` with the principal ID of the user whose data you want to delete.

   ```sql
   Delete from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (select id from EdcPrincipalEntity where id='<principal_id>'));
   
   Delete from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalEntity where id='<principal_id>';
   ```

1. AEM Forms サーバーを開始します。

### AEM リポジトリ {#aem-repository-1}

Forms JEE ユーザーは、AEM Forms オーサーインスタンスに少なくとも一度アクセスしている場合、AEM リポジトリにデータが格納されています。AEM リポジトリのユーザーデータにアクセスして削除することができます。

#### ユーザーデータへのアクセス {#access-user-data}

To view user created in AEM repository, log into `https://'[server]:[port]'/lc/useradmin` with AEM administrator credentials. URL の `server` と `port` は、AEM オーサーインスタンスのサーバーとポートであることに注意してください。ここでは、ユーザー名でユーザーを検索できます。ユーザーをダブルクリックすると、ユーザーのプロパティ、権限、グループなどの情報が表示されます。ユーザーの `Path` プロパティは、AEM リポジトリで作成されたユーザーノードへのパスを指定します。

#### ユーザーデータの削除 {#delete-aem}

ユーザを削除するには：

1. AEM管理者の資 `https://'[server]:[port]'/lc/useradmin` 格情報を使用してに移動します。
1. ユーザーを検索してユーザー名をダブルクリックし、ユーザープロパティを開きます。Copy the `Path` property.
1. Go to AEM CRX DELite at `https://'[server]:[port]'/lc/crx/de/index.jsp` and navigate or search the user path.
1. Delete the path and click **[!UICONTROL Save All]** to permanently delete the user from AEM repository.

