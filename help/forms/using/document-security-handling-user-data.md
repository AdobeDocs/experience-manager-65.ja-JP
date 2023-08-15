---
title: Document Security | ユーザーデータの処理
seo-title: Document Security | Handling user data
description: Document Security | ユーザーデータの処理
uuid: 1624a465-8b0c-4347-a53f-1118bfa6e18f
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 898268cb-4426-421f-8f63-d75bd85cb57f
role: Admin
exl-id: 00c01a12-1180-4f35-9179-461bf177c787
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 65%

---

# Document Security | ユーザーデータの処理 {#document-security-handling-user-data}

AEM Forms Document Security を使用すると、事前定義済みのセキュリティ設定を作成、保存、ドキュメントに適用できます。 これにより、許可されたユーザーのみがドキュメントを使用できるようになります。 ドキュメントを保護するには、ポリシーを使用します。ポリシーとは、セキュリティ設定と、許可されたユーザーのリストを含む情報の集まりです。 1 つ以上のドキュメントにポリシーを適用し、AEM Forms JEE のユーザー管理に追加されたユーザーを許可することができます。

<!-- Fix broken link For more information about how document security works, see AEM Forms JEE administration help. -->

## ユーザーデータとデータストア {#user-data-and-data-stores}

Document Security は、My Sql、Oracle、MS SQL Server、IBM DB2 など、保護されたドキュメントに関連するポリシーとデータをデータベースに格納します。 さらに、ポリシー内の承認済みユーザーのデータは、ユーザー管理に保存されます。 User Management に格納されるデータについて詳しくは、[Forms User Management | ユーザーデータの処理](/help/forms/using/user-management-handling-user-data.md)を参照してください。

次の表は、Document Security がデータベーステーブル内のデータを整理する方法を示しています。

<table>
 <tbody>
  <tr>
   <td>データベーステーブル</td>
   <td>説明</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalKeyEntity</code></td>
   <td>ユーザーのプリンシパルキーに関する情報を格納します。 キーは、オフラインの Document Security ワークフローで使用されます。</td>
  </tr>
  <tr>
   <td><code>EdcAuditEntity</code></td>
   <td>ユーザーイベント、ドキュメントイベント、ポリシーイベントなどの監査イベントに関する情報を格納します。</td>
  </tr>
  <tr>
   <td><p><code>EdcLicenseEntity</code></p> </td>
   <td>保護されたドキュメントのレコードを格納します。 保護されたすべてのドキュメントのライセンスの詳細を保存します。</td>
  </tr>
  <tr>
   <td><p><code>EdcDocumentEntity</code></p> </td>
   <td>システムで作成されたすべてのライセンスのドキュメント名を格納します。</td>
  </tr>
  <tr>
   <td><p><code>EdcRevokationEntity</code></p> </td>
   <td>保護されたドキュメントの失効および復元に関する情報を格納します。</td>
  </tr>
  <tr>
   <td><code>EdcMyPolicyListEntity</code></td>
   <td>個人用ポリシーを作成できるユーザーに関する情報を格納します。この個人用ポリシーはポリシーページの「マイポリシー」タブに表示されます。 </td>
  </tr>
  <tr>
   <td><code>EdcPolicyEntity</code></td>
   <td>ポリシーに関する情報を格納します。 各ポリシーは、この表の行に対応します。</td>
  </tr>
  <tr>
   <td><code>EdcPolicyXmlEntity</code></td>
   <td>アクティブなポリシーの XML ファイルを格納します。ポリシー XML<sup> </sup>には、ポリシーに関連付けられたユーザーのプリンシパル ID への参照が含まれます。ポリシー XML は、Blob オブジェクトとして格納されます。</td>
  </tr>
  <tr>
   <td><code>EdcPolicyArchiveEntity</code></td>
   <td>アーカイブされたポリシーに関する情報を格納します。アーカイブされたポリシーには、Blob オブジェクトとして格納されたポリシー XML が含まれます。</td>
  </tr>
  <tr>
   <td><p><code>EdcPolicySetPrincipalEntity</code></p> <p><code>EdcPolicySetPrincipalEnt</code><br /> （Oracle データベースおよび MS SQL データベース）</p> </td>
   <td>ポリシーセットとユーザー間のマッピングを格納します。</td>
  </tr>
  <tr>
   <td><code>EdcInvitedUserEntity</code></td>
   <td>招待ユーザーに関する情報を格納します。</td>
  </tr>
 </tbody>
</table>

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

データベース内のユーザーの Document Security データにアクセスして書き出すことができ、必要に応じて、データベースを完全に削除できます。

データベースからユーザーデータを書き出しまたは削除するには、データベースクライアントを使用してデータベースに接続し、ユーザーの個人情報に基づいてプリンシパル ID を見つける必要があります。 例えば、ログイン ID を使用してユーザーのプリンシパル ID を取得するには、次の `select` コマンドをデータベースで実行します。

`select` コマンドで、`<user_login_id>` を、`EdcPrincipalUserEntity` データベーステーブルから取得するプリンシパル ID を持つユーザーのログイン ID に置き換えます。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

プリンシパル ID がわかったら、ユーザーデータを書き出したり、削除したりできます。

### ユーザーデータの書き出し {#export-user-data}

次のデータベースコマンドを実行して、プリンシパル ID のユーザーデータをデータベーステーブルから書き出します。 `select` コマンドで、`<principal_id>` を、書き出すデータを持つユーザーのプリンシパル ID に置き換えます。

>[!NOTE]
>
>次のコマンドでは、My SQL および IBM DB2 データベースのデータベーステーブル名を使用しています。これらのコマンドを Oracle および MS SQL データベースで実行する際に、コマンドの `EdcPolicySetPrincipalEntity` を `EdcPolicySetPrincipalEnt` に置き換えます。

```sql
Select * from EdcPrincipalKeyEntity where principalid = '<principal_id>';

Select * from EdcLicenseEntity where publisherId = '<principal_id>';

Select * from EdcDocumentEntity where id in (Select documentid from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcRevokationEntity where licenseid in (Select id from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcMyPolicyListEntity where principalId = '<principal_id>';

Select * from edcpolicyentity where policyownerId = '<principal_id>';

Select * from edcpolicyxmlentity where policyidref in (Select id from edcpolicyentity where policyownerId = '<principal_id>');

Select * from edcpolicyarchiveentity where policyownerId = '<principal_id>';

Select * from edcpolicysetprincipalentity where principalId = '<principal_id>';

Select * from edcinviteduserentity where principalId = '<principal_id>';
```

>[!NOTE]
>
>`EdcAuditEntity` テーブルからデータを書き出すには、[EventManager.exportEvents](https://helpx.adobe.com/jp/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) API を使用します。これは、[EventSearchFilter](https://helpx.adobe.com/jp/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) をパラメーターとして受け取り、`principalId`、`policyId`、`licenseId` のいずれかに基づいて監査データを書き出します。

システム内のユーザーに関する完全なデータを取得するには、User Management データベースのデータにアクセスしてデータを書き出す必要があります。詳しくは、[Forms User Management | ユーザーデータの処理](/help/forms/using/user-management-handling-user-data.md)を参照してください。

### ユーザーデータの削除 {#delete-user-data}

データベーステーブルからプリンシパル ID の Document Security データを削除するには、次の手順を実行します。

1. AEM Formsサーバーをシャットダウンします。
1. 次のデータベースコマンドを実行して、目的のプリンシパル ID の データを Document Security のデータベーステーブルから削除します。`Delete` コマンドで、`<principal_id>` を、削除するデータを持つユーザーのプリンシパル ID に置き換えます。

   ```sql
   Delete from EdcPrincipalKeyEntity where principalid = '<principal_id>';
   
   Delete from EdcMyPolicyListEntity where principalId = '<principal_id>';
   
   Delete from edcpolicyarchiveentity where policyownerId = '<principal_id>';
   
   Delete from edcpolicysetprincipalentity where principalId = '<principal_id>';
   
   Delete from edcinviteduserentity where principalId = '<principal_id>';
   ```

   >[!NOTE]
   >
   >`EdcAuditEntity` テーブルからデータを削除するには、[EventManager.deleteEvents](https://helpx.adobe.com/jp/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) API を使用します。これは、[EventSearchFilter](https://helpx.adobe.com/jp/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) をパラメーターとして受け取り、`principalId`、`policyId`、`licenseId` のいずれかに基づいて監査データを削除します。

1. アクティブなポリシー XML ファイルとアーカイブされたポリシー XML ファイルは、それぞれ `EdcPolicyXmlEntity` および `EdcPolicyArchiveEntity` データベーステーブルに格納されます。これらのテーブルからユーザーのデータを削除するには、次を実行します。

   1. `EdcPolicyXMLEntity` または `EdcPolicyArchiveEntity` テーブルの各行の XML Blob を開き、XML ファイルを抽出します。XML ファイルの内容は、以下に示すようなものになります。
   1. XML ファイルを編集して、プリンシパル ID の BLOB を削除します。
   1. 他のファイルに対して、手順 1 と 2 を繰り返します。

   >[!NOTE]
   >
   >プリンシパル ID の `Principal` タグ内で Blob を完全に削除する必要があります。完全に削除しないと、ポリシー XML が破損するか、使用できなくなる可能性があります。

   ```xml
   <ns2:Principal PrincipalNameType="USER">
       <ns2:PrincipalDomain>OID</ns2:PrincipalDomain>
       <ns2:PrincipalName>56F33FEB-098A-1036-A651-00000A2A2656</ns2:PrincipalName>
   </ns2:Principal>
   </ns2:PolicyEntry>
       <ns2:Property PropertyName="isCertified">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">false</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="encryptionAlgorithm">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">AES128</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="AccessDeniedErrorMessage">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string"></ns2:PropertyValue>
       </ns2:Property>
   <ns2:PolicyEntry>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.onlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.copy" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.offlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.accessible" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.editNotes" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.edit" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.fillAndSign" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printHigh" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printLow" Access="ALLOW"/>
   ```

   `EdcPolicyXmlEntity` テーブルから直接データを削除する方法に加えて、次の 2 つの方法でもデータを削除することができます。

   **管理コンソールの使用**

   1. Forms JEE 管理コンソール（https://[*server*]:[*port*]/adminui）に管理者としてログインします。
   1. **[!UICONTROL サービス／Document Security／ポリシーセット]**&#x200B;に移動します。
   1. ポリシーセットを開き、ポリシーからユーザーを削除します。

   **Document Security Web ページの使用**

   個人用ポリシーを作成する権限を持つ Document Security ユーザーは、自分のポリシーからユーザーデータを削除できます。 この作業を行うには、以下の手順を実行します。

   1. 個人用ポリシーを持つユーザーが、Document Security Web ページ（https://[*server*]:[*port*]/edc）にログインします。
   1. **[!UICONTROL サービス／Document Security／マイポリシー]**&#x200B;に移動します。
   1. ポリシーを開き、ポリシーからユーザーを削除します。

   >[!NOTE]
   >
   >管理者は、管理コンソールの&#x200B;**[!UICONTROL サービス／Document Security／マイポリシー]**&#x200B;で、他のユーザーの個人用ポリシーからユーザーデータを検索、アクセスおよび削除できます。 

1. プリンシパル ID のデータを User Management のデータベースから削除します。詳しい手順については、[Forms User Management | ユーザーデータの処理](/help/forms/using/user-management-handling-user-data.md)を参照してください。
1. AEM Forms サーバーを開始します。
