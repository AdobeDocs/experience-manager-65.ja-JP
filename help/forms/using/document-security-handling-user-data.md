---
title: Document Security | ユーザーデータの処理
seo-title: Document Security | ユーザーデータの処理
description: ドキュメントセキュリティ |ユーザーデータの処理
uuid: 1624a465-8b0c-4347-a53f-1118bfa6e18f
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 898268cb-4426-421f-8f63-d75bd85cb57f
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 58%

---


# Document Security | ユーザーデータの処理 {#document-security-handling-user-data}

AEM Formsドキュメントセキュリティでは、定義済みのセキュリティ設定を作成、保存、ドキュメントに適用できます。 これにより、許可されたユーザーだけがドキュメントを使用できるように指定できます。ドキュメントを保護するには、ポリシーを使用します。ポリシーは、セキュリティ設定および許可されたユーザーの一覧を含む情報の集合です。1 つまたは複数のドキュメントにポリシーを適用して、AEM Forms JEE User Management に追加されるユーザーを許可します。

<!-- Fix broken link For more information about how document security works, see AEM Forms JEE administration help. -->

## ユーザーデータとデータストア {#user-data-and-data-stores}

Document Security は保護されたドキュメントに関するポリシーとデータを格納します。また、My Sql、Oracle、MS SQL Server、IBM DB2 などのデータベースに含まれるユーザーデータも格納します。また、ポリシーで許可されているユーザーに関するデータも Management に格納されます。ユーザー管理に保存されるデータについて詳しくは、[Formsユーザー管理：ユーザーデータ](/help/forms/using/user-management-handling-user-data.md)を処理しています。

次の表は、Document Security がデータベーステーブルでデータをどのようにまとめているかを示しています。

<table>
 <tbody>
  <tr>
   <td>データベーステーブル</td>
   <td>説明</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalKeyEntity</code></td>
   <td>ユーザーのプリンシパルキーに関する情報を格納します。このキーは、オフラインのドキュメントセキュリティワークフローで使用されます。</td>
  </tr>
  <tr>
   <td><code>EdcAuditEntity</code></td>
   <td>ユーザーイベント、ドキュメントイベント、ポリシーイベントなどの監査イベントに関する情報を格納します。</td>
  </tr>
  <tr>
   <td><p><code>EdcLicenseEntity</code></p> </td>
   <td>保護されたドキュメントのレコードを格納します。すべての保護されたドキュメントのライセンス詳細を格納します。</td>
  </tr>
  <tr>
   <td><p><code>EdcDocumentEntity</code></p> </td>
   <td>システムで作成されたすべてのライセンスのドキュメント名を格納します。</td>
  </tr>
  <tr>
   <td><p><code>EdcRevokationEntity</code></p> </td>
   <td>保護されたドキュメントの失効および復元に関する情報が格納されます。</td>
  </tr>
  <tr>
   <td><code>EdcMyPolicyListEntity</code></td>
   <td>個人用ポリシーを作成できるユーザーに関する情報を格納します。この個人用ポリシーはポリシーページの「マイポリシー」タブに表示されます。 </td>
  </tr>
  <tr>
   <td><code>EdcPolicyEntity</code></td>
   <td>ポリシーに関する情報を格納します。各ポリシーは、この表の行に対応しています。</td>
  </tr>
  <tr>
   <td><code>EdcPolicyXmlEntity</code></td>
   <td>アクティブなポリシーの XML ファイルを格納します。ポリシーXML<sup> </sup>には、ポリシーに関連付けられたユーザーのプリンシパルIDへの参照が含まれます。 ポリシー XML は、Blob オブジェクトとして格納されます。</td>
  </tr>
  <tr>
   <td><code>EdcPolicyArchiveEntity</code></td>
   <td>アーカイブされたポリシーに関する情報を格納します。アーカイブポリシーには、Blobオブジェクトとして保存されたポリシーXMLが含まれます。</td>
  </tr>
  <tr>
   <td><p><code>EdcPolicySetPrincipalEntity</code></p> <p><code>EdcPolicySetPrincipalEnt</code> (OracleおよびMS SQLデータベース)</p> </td>
   <td>ポリシーセットとユーザー間のマッピングを格納します。</td>
  </tr>
  <tr>
   <td><code>EdcInvitedUserEntity</code></td>
   <td>招待されたユーザーに関する情報を格納します。</td>
  </tr>
 </tbody>
</table>

## ユーザーデータへのアクセスと削除  {#access-and-delete-user-data}

データベースにあるユーザーの Document Security データにアクセスしてデータを書き出すことができます。また、必要に応じてデータを永続的に削除できます。

データベースからユーザーデータを書き出すまたは削除するには、データベースクライアントを使用してデータベースに接続し、個人が特定できるユーザー情報に基づいてプリンシパル ID を検索します。例えば、ログイン ID を使用してユーザーのプリンシパル ID を取得するには、次の `select` コマンドをデータベースで実行します。

`select`コマンドで、`<user_login_id>`を`EdcPrincipalUserEntity`データベーステーブルから取得するプリンシパルIDを持つユーザーのログインIDに置き換えます。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

プリンシパル ID が分かったら、ユーザーデータを書き出したり、削除したりすることができます。

### ユーザーデータの書き出し  {#export-user-data}

次のデータベースコマンドを実行して、プリンシパル ID のユーザーデータをデータベーステーブルから書き出します。`select`コマンドで、`<principal_id>`を書き出すデータのユーザーのプリンシパルIDに置き換えます。

>[!NOTE]
>
>次のコマンドでは、My SQL および IBM DB2 データベースのデータベーステーブル名を使用しています。oracleおよびMS SQLデータベースでこれらのコマンドを実行する場合は、コマンドの`EdcPolicySetPrincipalEntity`を`EdcPolicySetPrincipalEnt`に置き換えます。

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
>`EdcAuditEntity`テーブルからデータを書き出すには、`principalId`、`policyId`、または`licenseId`に基づいて監査データを書き出すパラメーターとして[EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html)を取る[EventManager.exportEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) APIを使用します。

システム内のユーザーに関する完全なデータを取得するには、User Management データベースのデータにアクセスしてデータを書き出す必要があります。詳しくは、[Formsのユーザー管理を参照してください。ユーザーデータ](/help/forms/using/user-management-handling-user-data.md)を処理しています。

### ユーザーデータの削除 {#delete-user-data}

特定のプリンシパル ID の Document Security データをデータベーステーブルから削除するには、次の手順を実行します。

1. AEM Forms サーバーをシャットダウンします。
1. 次のデータベースコマンドを実行して、目的のプリンシパル ID の データを Document Security のデータベーステーブルから削除します。`Delete`コマンドで、`<principal_id>`を削除するデータのユーザーのプリンシパルIDに置き換えます。

   ```sql
   Delete from EdcPrincipalKeyEntity where principalid = '<principal_id>';
   
   Delete from EdcMyPolicyListEntity where principalId = '<principal_id>';
   
   Delete from edcpolicyarchiveentity where policyownerId = '<principal_id>';
   
   Delete from edcpolicysetprincipalentity where principalId = '<principal_id>';
   
   Delete from edcinviteduserentity where principalId = '<principal_id>';
   ```

   >[!NOTE]
   >
   >`EdcAuditEntity`テーブルからデータを削除するには、`principalId`、`policyId`、または`licenseId`に基づいて監査データを削除するパラメーターとして[EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html)を取る[EventManager.deleteEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) APIを使用します。

1. アクティブなポリシーのXMLファイルとアーカイブされたポリシーのXMLファイルは、それぞれ`EdcPolicyXmlEntity`と`EdcPolicyArchiveEntity`のデータベーステーブルに保存されます。 これらのテーブルからユーザーのデータを削除するには、次を実行します。

   1. `EdcPolicyXMLEntity`または`EdcPolicyArchiveEntity`テーブルの各行のXML BLOBを開き、XMLファイルを抽出します。 XMLファイルは、次に示すファイルに似ています。
   1. XML ファイルを編集して、目的のプリンシパル ID の Blob を削除します。
   1. その他のファイルで手順 1 と 2 を繰り返します。

   >[!NOTE]
   >
   >プリンシパルIDの`Principal`タグ内の完全なBLOBを削除する必要があります。削除しないと、ポリシーXMLが壊れたり、使用できなくなったりする場合があります。

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

   `EdcPolicyXmlEntity` テーブルから直接データを削除する方法に加えて、次の 2 つの方法でデータを削除できます。

   **管理コンソールの使用**

   1. 管理者として、https://[*server*]:[*port*]/adminuiで、FormsJEE管理コンソールにログインします。
   1. **[!UICONTROL サービス/ドキュメントセキュリティ/ポリシーセット]**&#x200B;に移動します。
   1. ポリシーセットを開き、ポリシーからユーザーを削除します。

   **Document Security の Web ページの使用**

   個人用ポリシーを作成できる権限を持つ Document Security ユーザーは、そのポリシーからユーザーデータを削除できます。この作業を行うには：

   1. 個人用のポリシーを持つユーザーは、https://[*server*]:[*port*]/edcのドキュメントセキュリティWebページにログインします。
   1. **[!UICONTROL サービス/ドキュメントセキュリティ/マイポリシー]**&#x200B;に移動します。
   1. ポリシーを開き、ポリシーからユーザーを削除します。

   >[!NOTE]
   >
   >管理者は、管理コンソールを使用して、**[!UICONTROL サービス/ドキュメントセキュリティ/マイポリシー]**&#x200B;で、他のユーザーの個人用ポリシーのユーザーデータを検索、アクセスおよび削除できます。

1. プリンシパル ID のデータを User Management のデータベースから削除します。詳細な手順については、[Formsユーザー管理を参照してください |ユーザーデータ](/help/forms/using/user-management-handling-user-data.md)を処理しています。
1. AEM Forms サーバーを開始します。

