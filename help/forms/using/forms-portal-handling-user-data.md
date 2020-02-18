---
title: Forms Portal | ユーザーデータの処理
seo-title: Forms Portal | ユーザーデータの処理
description: 'null'
seo-description: 'null'
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Forms Portal | ユーザーデータの処理 {#forms-portal-handling-user-data}

AEM Forms ポータルには、AEM Sites ページにアダプティブフォーム、HTML5 フォームおよびその他のフォームアセットを一覧表示するために使用できるコンポーネントが用意されています。さらに、ログインしたユーザーのためにドラフトや送信済みのアダプティブフォームおよび HTML5 フォームを表示するように構成することもできます。For more information about forms portal, see [Introduction to publishing forms on a portal](/help/forms/using/introduction-publishing-forms.md).

ログインしたユーザーがアダプティブフォームをドラフトとして保存したり、送信したりすると、これらのアダプティブフォームが Forms Portal の「ドラフト」タブおよび「送信」タブに表示されます。ドラフトまたは送信済みフォームのデータは、AEM デプロイメント用に構成されたデータストアに格納されます。Forms Portal ページには、匿名ユーザーのドラフトおよび送信は表示されません。ただし、データは構成済みのデータストアに格納されます。詳しくは、「[ドラフトと送信に使用するストレージサービスの設定](/help/forms/using/configuring-draft-submission-storage.md)」を参照してください。

## ユーザーデータとデータストア {#user-data-and-data-stores}

Forms Portal は、次のシナリオではドラフトフォームと送信済みフォームのデータを格納します。

* The submit action configured in the adaptive form is **Forms Portal Submit Action**.
* For submit actions other than **Forms Portal Submit Action**, the **[!UICONTROL Store data in forms portal]** option is enabled in the **Submission** properties of the adaptive form container.

ログインしたユーザーと匿名ユーザーのすべてのドラフトと送信済みフォームの場合、Forms Portal には次のデータが格納されます。

* フォーム名、フォームパス、ドラフトまたは送信 ID、添付ファイルのパス、ユーザーデータ ID などのフォームメタデータ
* データバイトとしてのフォーム添付ファイル
* データバイトとしてのフォームデータ

設定されたデータストアの永続性に応じて、ドラフトおよび送信済みフォームデータは次の場所に格納されます。

<table>
 <tbody>
  <tr>
   <td><p><strong>永続性タイプ</strong></p> </td>
   <td><p><strong>データストア</strong></p> </td>
   <td><p><strong>場所</strong></p> </td>
  </tr>
  <tr>
   <td><p>デフォルト値は</p> </td>
   <td><p>オーサーインスタンスおよび発行インスタンスの AEM リポジトリ</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>リモート</p> </td>
   <td><p>オーサーインスタンスおよびリモート AEM インスタンスの AEM リポジトリ</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>データベース</p> </td>
   <td><p>オーサーインスタンスおよびデータベーステーブルの AEM リポジトリ</p> </td>
   <td>データベース <code>data</code>テーブル、 <code>metadata</code>および <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

ログインしたユーザーおよび匿名ユーザーのドラフトと送信済みフォームデータには、設定したデータストアからアクセスし、必要に応じて削除できます。

### AEM インスタンス {#aem-instances}

All drafts and submitted forms data in AEM instances (author, publish, or remote) for logged-in and anonymous users are stored in the `/content/forms/fp/` node of the applicable AEM repository. Every time a logged-in or anonymous user saves a draft or submits a form, a `draft ID` or `submission ID`, a `user data ID`, and a random `ID` for each attachment (if applicable) is generated, which is associated with the respective draft or submission.

#### ユーザーデータへのアクセス {#access-user-data}

ログインしたユーザーがドラフトを保存またはフォームを送信すると、そのユーザー ID を使用して子ノードが作成されます。For example, drafts and submissions data for Sarah Rose whose user ID is `srose` are stored in `/content/forms/fp/srose/` node in AEM repository. このユーザー ID ノード内では、データが階層構造で整理されます。

The following table explains how the data for all drafts by `srose` is stored in AEM repository.

>[!NOTE]
>
>An exact structure like `drafts` is replicated for submitted forms for `srose` under the `/content/forms/fp/srose/submit/` node.
>
>All drafts and submissions by `anonymous` users are stored under the `/content/forms/fp/anonymous/` node, which organizes drafts and submissions for all anonymous users under the `draft` and `submit` nodes.

| Node | 説明 |
|---|---|
| `/content/forms/fp/srose/drafts` | ユーザーが作成したすべてのドラフトデータが含まれる |
| `/content/forms/fp/srose/drafts/attachments/` | ドラフト ID に基づいてユーザーのすべての添付ファイルがまとめられる |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 選択した ID の添付ファイルがバイナリ形式で含まれる |
| `/content/forms/fp/srose/drafts/metadata/` | ドラフトIDに基づいてユーザーのフォームメタデータを整理します |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 選択したドラフト ID のフォームメタデータが含まれる |
| `/content/forms/fp/srose/drafts/data/` | ユーザーデータ ID に基づいてユーザーのフォームデータがまとめられる |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 選択したユーザーデータ ID のフォームデータがバイナリ形式で含まれる |

#### ユーザーデータの削除 {#delete-user-data}

AEM システムで、ログインしたユーザーのドラフトおよび送信済みフォームに含まれるユーザーデータを完全に削除するには、特定ユーザーの `user ID` ノードを作成者ノードから削除する必要があります。該当するすべてのAEMインスタンスからデータを手動で削除する必要があります。

Drafts and submission data for all anonymous users is stored within the common `drafts` and `submit` nodes under `/content/forms/fp/anonymous`. 匿名ユーザーのデータは、識別情報がない限り検索することはできません。このような場合、AEM リポジトリで匿名ユーザーを特定する情報を検索し、その情報が含まれているノードをすべての AEM インスタンスから手動で削除します。これにより、AEM システムからデータを削除できます。However, to delete data for all anonymous users, you can delete the `anonymous` node to remove drafts and submissions data for all anonymous users.

### データベース {#database}

AEM がデータベースにデータを格納するように構成されている場合、Forms Portal のドラフトと送信データは、ログインしたユーザーまたは匿名ユーザーを問わず、次のデータベーステーブルに格納されます。

* data
* メタデータ
* additionalmetadata

#### ユーザーデータへのアクセス {#access-user-data-1}

ログインしたユーザーおよび匿名ユーザーのドラフトおよび送信データにデータベーステーブルからアクセスするには、次のデータベースコマンドを実行します。In the query, replace `logged-in user` with the user ID whose data you want to access or with `anonymous` for anonymous users.

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### ユーザーデータの削除 {#delete-user-data-1}

ログインしたユーザーのドラフトおよび送信データをデータベーステーブルから削除するには、次のデータベースコマンドを実行します。In the query, replace `logged-in user` with the user ID whose data you want to delete or with `anonymous` for anonymous users. 匿名ユーザーのデータをデータベースから削除するには、識別可能な情報を使用してデータを検索し、その情報が含まれるデータベーステーブルからデータを削除する必要があります。

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```

