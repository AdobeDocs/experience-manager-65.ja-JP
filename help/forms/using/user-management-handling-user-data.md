---
title: Forms User Management | ユーザーデータの処理
description: AEM Forms JEE の User Management コンポーネントを使用して、AEM Formsへのアクセスを必要とするユーザーを作成、承認および管理する方法について説明します。
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin
exl-id: eeeab5d1-073a-4e13-a781-391dfe70bb37
source-git-commit: 000c22028259eb05a61625d43526a2e8314a1d60
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 30%

---

# Forms User Management | ユーザーデータの処理 {#forms-user-management-handling-user-data}

ユーザー管理は、AEM Forms JEE コンポーネントで、AEM Formsユーザーを作成、管理および承認して、AEM Formsにアクセスすることを許可します。 ユーザー管理では、ドメインをディレクトリとして使用し、ユーザー情報を取得します。 次のドメインタイプがサポートされています。

**ローカルドメイン**：このタイプのドメインは、サードパーティのストレージシステムに接続されていません。 代わりに、ユーザーとグループがローカルに作成され、User Management データベースに格納されます。 パスワードはローカルに保存され、認証はローカルデータベースを使用しておこなわれます。

**ハイブリッドドメイン**：このタイプのドメインは、サードパーティのストレージシステムに接続されていません。 代わりに、ユーザーとグループがローカルに作成され、User Management データベースに格納されます。 ローカルドメインとは異なり、ハイブリッドドメインは、外部認証プロバイダーを使用します。外部認証プロバイダーは、LDAP、Kerberos、SAML、またはカスタム認証プロバイダーです。

**エンタープライズドメイン**:LDAP ディレクトリなど、サードパーティのストレージシステムに存在するユーザーとグループで構成されます。 User Management では、サードパーティのストレージシステムに対する書き込みが行われません。代わりに、User Management はユーザーおよびグループの情報を User Management データベースと同期します。 エンタープライズドメインは、外部認証プロバイダも使用します。外部認証プロバイダは、LDAP、Kerberos、SAML、またはカスタム認証プロバイダです。

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## ユーザーデータとデータストア {#user-data-and-data-stores}

ユーザー管理では、My Sql、Oracle、MS® SQL Server、IBM® DB2®などのデータベースにユーザーデータを格納します。 また、`https://'[server]:[port]'lc` から AEM オーサーの Forms アプリケーションに一度でもログインすると、AEM リポジトリにユーザーデータが作成されます。したがって、ユーザー管理は次のデータストアに保存されます。

* データベース
* AEMリポジトリ
* LDAP ディレクトリなどのサードパーティストレージ

>[!NOTE]
>
>サードパーティのストレージに保存されたデータは、このドキュメントの範囲外です。 サードパーティベンダーに直接問い合わせて、そのようなストレージ内のユーザーデータを管理します。

### データベース {#database}

ユーザー管理では、次のデータベーステーブルにユーザーデータを格納します。

<table>
 <tbody>
  <tr>
   <td>データベーステーブル</td>
   <td>説明</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalEntity</code></td>
   <td><p>プリンシパルエンティティに関する情報を格納します。 プリンシパルは、ユーザー、グループ、または役割です。</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>ユーザーの個人を特定できる情報 (PII) を格納します。 ローカルドメイン、エンタープライズドメイン、ハイブリッドドメインの各ユーザーのエントリが含まれます。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>(Oracleおよび MS® SQL データベース )</p> </td>
   <td>ローカルユーザーのデータのみを格納します。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>(Oracleおよび MS® SQL データベース )</p> </td>
   <td>ローカルドメイン、エンタープライズドメイン、ハイブリッドドメインのすべてのユーザーのエントリが含まれます。 ユーザーの電子メール ID が含まれます。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code><br /> (Oracleおよび MS® SQL データベース )</p> </td>
   <td>ユーザーとグループのマッピングを格納します。</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>ユーザーとグループの両方の役割とプリンシパル間のマッピングを格納します。</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>ユーザーとグループの両方について、プリンシパルと権限のマッピングを格納します。</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code><br /> (Oracleおよび MS® SQL データベース )</p> </td>
   <td>プリンシパルに対応する古い属性値と新しい属性値を格納します。<br /> </td>
  </tr>
 </tbody>
</table>

### AEMリポジトリ {#aem-repository}

`https://'[server]:[port]'lc` から Forms アプリケーションに一度でもログインすると、User Management データも AEM リポジトリに格納されます。

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

User Management データベースおよびAEMリポジトリのユーザーのユーザー管理データにアクセスして書き出すことができ、必要に応じて永久に削除できます。

### データベース {#database-1}

ユーザー管理データベースからユーザーデータを書き出しまたは削除するには、データベースクライアントを使用してデータベースに接続し、ユーザーの PII に基づいてプリンシパル ID を見つける必要があります。 例えば、ログイン ID を使用してユーザーのプリンシパル ID を取得するには、次の `select` コマンドをデータベースで実行します。

`select` コマンドで、`<user_login_id>` をプリンシパル ID を取得したいユーザーのログイン ID に置き換えます。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

プリンシパル ID がわかったら、ユーザーデータを書き出したり、削除したりできます。

#### ユーザーデータの書き出し {#export-user-data}

次のデータベースコマンドを実行して、プリンシパル ID のユーザー管理データをデータベーステーブルから書き出すことができます。 `select` コマンドで、`<principal_id>` を、書き出すデータを持つユーザーのプリンシパル ID に置き換えます。

>[!NOTE]
>
>次のコマンドでは、My SQL データベースとIBM® DB2®データベースのデータベーステーブル名を使用します。 oracleおよび MS® SQL データベースでこれらのコマンドを実行する場合は、コマンドで次のテーブル名を置き換えます。
>
* `EdcPrincipalLocalAccountEntity` を `EdcPrincipalLocalAccount` に置き換えます。
>
* `EdcPrincipalEmailAliasEntity` を `EdcPrincipalEmailAliasEn` に置き換えます。
>
* `EdcPrincipalMappingEntity` を `EdcPrincipalMappingEntit` に置き換えます。
>
* `EdcPrincipalGrpCtmntEntity` を `EdcPrincipalGrpCtmntEnti` に置き換えます。
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

プリンシパル ID のユーザー管理データをデータベーステーブルから削除するには、次の手順を実行します。

1. 必要に応じて、AEMリポジトリからユーザーデータを削除します。詳しくは、 [ユーザーデータを削除](/help/forms/using/user-management-handling-user-data.md#delete-aem).
1. AEM Formsサーバーをシャットダウンします。
1. 次のデータベースコマンドを実行して、プリンシパル ID のユーザー管理データをデータベーステーブルから削除できます。 `Delete` コマンドで、`<principal_id>` を、削除するデータを持つユーザーのプリンシパル ID に置き換えます。

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

1. AEM Forms Server を起動します。

### AEMリポジトリ {#aem-repository-1}

Forms JEE ユーザーが少なくとも 1 つのAEM Formsオーサーインスタンスにアクセスした場合、AEMリポジトリにデータが格納されます。 ユーザーデータにアクセスしてAEMリポジトリから削除できます。

#### ユーザーデータへのアクセス {#access-user-data}

AEM リポジトリで作成されたユーザーを表示するには、AEM 管理者の資格情報を使用して `https://'[server]:[port]'/lc/useradmin` にログインします。URL の `server` と `port` は、AEM オーサーインスタンスのサーバーとポートであることに注意してください。ここでは、ユーザー名を使用してユーザーを検索できます。 ユーザーをダブルクリックして、そのユーザーのプロパティ、権限、グループなどの情報を表示できます。 ユーザーの `Path` プロパティは、AEM リポジトリで作成されたユーザーノードへのパスを指定します。

#### ユーザーデータの削除 {#delete-aem}

ユーザーを削除するには：

1. AEM 管理者の資格情報を使用して、`https://'[server]:[port]'/lc/useradmin` に移動します。
1. ユーザーを検索してユーザー名をダブルクリックし、ユーザープロパティを開きます。`Path` プロパティをコピーします。
1. AEMCRXDE Lite( ) に移動します。 `https://'[server]:[port]'/lc/crx/de/index.jsp` ユーザーパスに移動または検索します。
1. パスを削除して「**[!UICONTROL すべて保存]**」をクリックし、AEM リポジトリからこのユーザーを永続的に削除します。
