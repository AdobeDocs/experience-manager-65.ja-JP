---
title: フォームポータル | ユーザーデータの処理
description: AEM Forms Portal でのユーザーデータの管理（アクセス、削除、データストアなど）について説明します。
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin
exl-id: 791524a4-a8bb-4632-a68d-e96864e139a9
source-git-commit: 000c22028259eb05a61625d43526a2e8314a1d60
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 73%

---

# フォームポータル | ユーザーデータの処理 {#forms-portal-handling-user-data}

[!DNL AEM Forms] ポータルには、アダプティブフォーム、HTML5 フォーム、その他のFormsアセットを [!DNL AEM Sites] ページに貼り付けます。 さらに、ログインしたユーザーのためにドラフトや送信済みのアダプティブフォームおよび HTML5 フォームを表示するように構成することもできます。Forms Portal について詳しくは、 [ポータル上のフォーム発行の概要](/help/forms/using/introduction-publishing-forms.md).

ログインしているユーザーがアダプティブフォームをドラフトとして保存したり送信したりすると、Forms Portal の「ドラフト」タブと「送信」タブに表示されます。 ドラフトおよび送信済みフォームのデータは、AEM デプロイメント用に設定されたデータストアに格納されます。匿名ユーザーのドラフトと送信は、Forms Portal ページに表示されませんが、データは設定済みのデータストアに保存されます。 [ドラフトと送信に使用するストレージサービスの設定](/help/forms/using/configuring-draft-submission-storage.md)を参照してください。

## ユーザーデータとデータストア {#user-data-and-data-stores}

Forms Portal では、次のシナリオでドラフトフォームおよび送信済みフォームのデータを保存します。

* アダプティブフォームに設定された送信アクションが **Forms Portal 送信アクション**&#x200B;である。
* 次以外の送信アクション： **Forms Portal 送信アクション**、 **[!UICONTROL Forms Portal でのデータの保存]** オプションが有効になっている場合は、 **[!UICONTROL 送信]** アダプティブフォームコンテナのプロパティ。

Forms Portal には、ログインしたユーザーと匿名ユーザーのドラフトおよび送信済みフォームごとに、次のデータが保存されます。

* フォーム名、フォームパス、ドラフトまたは送信 ID、添付ファイルのパス、ユーザーデータ ID などのフォームメタデータ
* データバイトとしてのフォームの添付ファイル
* データバイトとしてのフォームデータ

設定されたデータストアの永続性に応じて、ドラフトおよび送信済みフォームのデータは次の場所に格納されます。

<table>
 <tbody>
  <tr>
   <td><p><strong>永続性タイプ</strong></p> </td>
   <td><p><strong>データストア</strong></p> </td>
   <td><p><strong>場所</strong></p> </td>
  </tr>
  <tr>
   <td><p>デフォルト</p> </td>
   <td><p>オーサーインスタンスとパブリッシュインスタンスのAEMリポジトリ</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>リモート</p> </td>
   <td><p>オーサーインスタンスとリモートAEMインスタンスのAEMリポジトリ</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>データベース</p> </td>
   <td><p>オーサーインスタンスとデータベーステーブルのAEMリポジトリ</p> </td>
   <td>データベーステーブル <code>data</code>、<code>metadata</code> および <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

設定したデータストア内にあるログインしたユーザーと匿名ユーザーのドラフトおよび送信済みフォームのデータにアクセスし、必要に応じて削除できます。

### AEM インスタンス {#aem-instances}

ログインしたユーザーおよび匿名ユーザーの AEM インスタンス（作成者、発行またはリモート）のすべてのドラフトと送信済みフォームのデータは、該当する AEM リポジトリの `/content/forms/fp/` ノードに格納されます。ログインしたユーザーまたは匿名ユーザーがドラフトを保存するかフォームを送信するたびに、`draft ID` または `submission ID`、`user data ID`、および各添付ファイルのランダム `ID`（該当する場合）が生成され、それぞれのドラフトまたは送信に関連付けられます。

#### ユーザーデータにアクセス {#access-user-data}

ログインしているユーザーがドラフトを保存したり、フォームを送信したりすると、そのユーザー ID を持つ子ノードが作成されます。 例えば、ユーザー ID が `srose` である Sarah Rose のドラフトデータと送信データが AEM リポジトリの `/content/forms/fp/srose/` ノードに格納されるとします。このユーザー ID ノード内では、データが階層構造で整理されます。

以下の表は、`srose` を使用して作成されたすべてのドラフトのデータが、どのように AEM リポジトリに格納されるのかを説明しています。

>[!NOTE]
>
>`drafts` と同一の構造が `srose` に送信されたフォーム用に `/content/forms/fp/srose/submit/` ノード下にレプリケートされます。
>
>`anonymous` ユーザーによるすべてのドラフトと送信済みフォームは、`/content/forms/fp/anonymous/` ノードに格納されます。このノードでは、匿名ユーザーのすべてのドラフトと送信済みフォームが、`draft` ノードと `submit` ノードによって整理されます。

| ノード | 説明 |
|---|---|
| `/content/forms/fp/srose/drafts` | ユーザーが作成したすべてのドラフトが含まれるコンテナノードデータ |
| `/content/forms/fp/srose/drafts/attachments/` | ドラフト ID に基づいてユーザーのすべての添付ファイルがまとめられる |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 選択した ID の添付ファイルがバイナリ形式で含まれる |
| `/content/forms/fp/srose/drafts/metadata/` | ドラフト ID にもとづいてユーザーのフォームメタデータがまとめられる |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 選択したドラフト ID のフォームメタデータが含まれる |
| `/content/forms/fp/srose/drafts/data/` | ユーザーデータ ID に基づいてユーザーのフォームデータがまとめられる |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 選択したユーザーデータ ID のフォームデータがバイナリ形式で含まれる |

#### ユーザーデータの削除 {#delete-user-data}

AEM システムで、ログインしたユーザーのドラフトおよび送信済みフォームに含まれるユーザーデータを完全に削除するには、特定ユーザーの `user ID` ノードを作成者ノードから削除する必要があります。該当するすべての AEM インスタンスから手動でデータを削除する必要があります。

すべての匿名ユーザーのドラフトデータと送信データは、共通の `drafts` ノードと `submit` ノード内に格納されます。これらのノードは、`/content/forms/fp/anonymous` にあります。識別可能な情報がない限り、特定の匿名ユーザーのデータを検索する方法はありません。その場合、AEM リポジトリで匿名ユーザーを識別する情報を検索し、該当するすべての AEM インスタンスからその情報を含むノードを手動で削除して、AEM システムからデータを削除できます。ただし、すべての匿名ユーザーのデータを削除する場合は、`anonymous` ノードを削除することで、すべての匿名ユーザーのドラフトデータと送信データを削除できます。

### データベース {#database}

データをデータベースに格納するようにAEMが設定されている場合、Forms Portal のドラフトと送信データは、ログインしているユーザーと匿名ユーザーの両方について、次のデータベーステーブルに格納されます。

* data
* メタデータ
* additionalmetadata

#### ユーザーデータにアクセス {#access-user-data-1}

ログインしたユーザーおよび匿名ユーザーのドラフトおよび送信データにデータベーステーブルからアクセスするには、次のデータベースコマンドを実行します。クエリで、`logged-in user` を、アクセスするデータのユーザー ID または匿名ユーザーの `anonymous` と置き換えます。

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### ユーザーデータの削除 {#delete-user-data-1}

ログインしたユーザーのドラフトおよび送信データをデータベーステーブルから削除するには、次のデータベースコマンドを実行します。クエリで、`logged-in user` を、削除するデータのユーザー ID または匿名ユーザーの `anonymous` と置き換えます。匿名ユーザーのデータをデータベースから削除するには、識別可能な情報を使用してデータを検索し、その情報が含まれるデータベーステーブルからデータを削除する必要があります。

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```
