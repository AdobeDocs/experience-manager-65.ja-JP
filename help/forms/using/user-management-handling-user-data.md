---
title: Forms User Management | ユーザーデータの処理
seo-title: Forms user management | Handling user data
description: Forms User Management | ユーザーデータの処理
uuid: 2b76b69f-6f3a-4f1a-a2a4-d39f5e529f75
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a88fc933-f1af-4798-b72f-10e7b0d2fd11
role: Admin
exl-id: eeeab5d1-073a-4e13-a781-391dfe70bb37
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 100%

---

# Forms User Management | ユーザーデータの処理 {#forms-user-management-handling-user-data}

User Management は、AEM Forms にアクセスするために AEM Forms ユーザーを作成、管理および認証することができる AEM Forms JEE コンポーネントです。User Management は、ユーザー情報を取得するためのディレクトリとしてドメインを使用します。次の種類のドメインがサポートされます。

**ローカルドメイン**：この種類のドメインは、サードパーティーのストレージシステムに接続されません。代わりに、ユーザーおよびグループがローカルに作成され、User Management データベースに格納されます。パスワードはローカルに保存され、認証はローカルデータベースを使用して実行されます。

**ハイブリッドドメイン**：この種類のドメインは、サードパーティーのストレージシステムには接続されません。代わりに、ユーザーおよびグループがローカルに作成され、User Management データベースに格納されます。ローカルドメインと異なり、ハイブリッドドメインは、外部認証プロバイダー（LDAP、Kerberos、SAML またはカスタム）を使用します。

**エンタープライズドメイン**：LDAP ディレクトリなどのサードパーティーのストレージシステムに格納されているユーザーおよびグループで構成されます。User Management では、サードパーティのストレージシステムに対する書き込みは行われません。代わりに、User Management によってユーザーおよびグループの情報が User Management データベースと同期されます。エンタープライズドメインでは、外部認証プロバイダー（LDAP、Kerberos、SAML またはカスタム）も使用します。

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## ユーザーデータとデータストア {#user-data-and-data-stores}

User Management は、My Sql、Oracle、MS SQL Server、IBM DB2 などのデータベースにユーザーデータを格納します。また、`https://'[server]:[port]'lc` から AEM オーサーの Forms アプリケーションに一度でもログインすると、AEM リポジトリにユーザーデータが作成されます。したがって、User Management のデータは、次のデータストアに格納されます。

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
       </code>（Oracle データベースおよび MS SQL データベース）</p> </td>
   <td>ローカルユーザーのデータのみを格納します。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>（Oracle データベースおよび MS SQL データベース）</p> </td>
   <td>ローカル、エンタープライズおよびハイブリッドの各ドメインに含まれるすべてのユーザーのエントリが含まれます。これにはユーザーの電子メール ID が含まれます。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code> （Oracle データベースおよび MS SQL データベース）</p> </td>
   <td>ユーザーとグループのマッピングを格納します。</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>ユーザーとグループの両方について、ロールとプリンシパルのマッピングを格納します。</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>ユーザーとグループの両方について、プリンシパルと権限のマッピングを格納します。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code> （Oracle データベースおよび MS SQL データベース）</p> </td>
   <td>プリンシパルに対応する古い属性値と新しい属性値を格納します。<br /> </td>
  </tr>
 </tbody>
</table>

### AEM リポジトリ {#aem-repository}

`https://'[server]:[port]'lc` から Forms アプリケーションに一度でもログインすると、User Management データも AEM リポジトリに格納されます。

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

User Management データベースおよび AEM リポジトリにあるユーザーの User Management データにアクセスしてデータを書き出すことができます。また、必要に応じてデータを永続的に削除できます。

### データベース {#database-1}

User Management データベースのユーザーデータを書き出すまたは削除するには、データベースクライアントを使用してデータベースに接続し、ユーザーの PII に基づいてプリンシパル ID を検索します。例えば、ログイン ID を使用してユーザーのプリンシパル ID を取得するには、次の `select` コマンドをデータベースで実行します。

`select` コマンドで、`<user_login_id>` をプリンシパル ID を取得したいユーザーのログイン ID に置き換えます。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

プリンシパル ID が分かったら、ユーザーデータを書き出したり、削除したりすることができます。

#### ユーザーデータの書き出し {#export-user-data}

次のデータベースコマンドを実行して、プリンシパル ID の User Management データをデータベーステーブルから書き出します。`select` コマンドで、`<principal_id>` を書き出すデータのユーザーに割り当てられたプリンシパル ID に置き換えます。

>[!NOTE]
>
>次のコマンドでは、My SQL および IBM DB2 データベースのデータベーステーブル名を使用しています。これらのコマンドを Oracle および MS SQL データベースで実行するときは、コマンドの次のテーブル名を置き換えます。
>
>* `EdcPrincipalLocalAccountEntity` を `EdcPrincipalLocalAccount` に置き換えます。
>
>* `EdcPrincipalEmailAliasEntity` を `EdcPrincipalEmailAliasEn` に置き換えます。
>
>* `EdcPrincipalMappingEntity` を `EdcPrincipalMappingEntit` に置き換えます。
>
>* `EdcPrincipalGrpCtmntEntity` を `EdcPrincipalGrpCtmntEnti` に置き換えます。
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
1. 次のデータベースコマンドを実行して、目的のプリンシパル ID の User Management データをデータベーステーブルから削除します。`Delete` コマンドで、`<principal_id>` を、削除するデータのユーザーに割り当てられたプリンシパル ID に置き換えます。

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

1. AEM Forms サーバーを起動します。

### AEM リポジトリ {#aem-repository-1}

Forms JEE ユーザーは、AEM Forms オーサーインスタンスに少なくとも一度アクセスしている場合、AEM リポジトリにデータが格納されています。AEM リポジトリのユーザーデータにアクセスして削除することができます。

#### ユーザーデータへのアクセス {#access-user-data}

AEM リポジトリで作成されたユーザーを表示するには、AEM 管理者の資格情報を使用して `https://'[server]:[port]'/lc/useradmin` にログインします。URL の `server` と `port` は、AEM オーサーインスタンスのサーバーとポートであることに注意してください。ここでは、ユーザー名でユーザーを検索できます。ユーザーをダブルクリックすると、ユーザーのプロパティ、権限、グループなどの情報が表示されます。ユーザーの `Path` プロパティは、AEM リポジトリで作成されたユーザーノードへのパスを指定します。

#### ユーザーデータの削除 {#delete-aem}

ユーザを削除するには：

1. AEM 管理者の資格情報を使用して、`https://'[server]:[port]'/lc/useradmin` に移動します。
1. ユーザーを検索してユーザー名をダブルクリックし、ユーザープロパティを開きます。`Path` プロパティをコピーします。
1. `https://'[server]:[port]'/lc/crx/de/index.jsp` にある AEM CRX DELite にアクセスし、ユーザーパスに移動するか、ユーザーパスを検索します。
1. パスを削除して「**[!UICONTROL すべて保存]**」をクリックし、AEM リポジトリからこのユーザーを永続的に削除します。
