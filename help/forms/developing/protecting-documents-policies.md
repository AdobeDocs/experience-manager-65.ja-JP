---
title: ポリシーを使用したドキュメントの保護
seo-title: Protecting Documents with Policies
description: Document Security サービスを使用すると、機密性の設定を Adobe PDF ドキュメントに動的に適用したり、ドキュメントを管理したりできます。また、Document Security サービスを使用すると、ユーザーは、ポリシーで保護された PDF ドキュメントを受信者が使用する方法を管理できます。
seo-description: Use the Document Security service to dynamically apply confidentiality settings to Adobe PDF documents and to maintain control over the documents. The Document Security service also enables the users to maintain control over how recipients use the policy-protected PDF document.
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
role: Developer
exl-id: ff42579e-6aaf-433d-8b5d-9e9dd0957250
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '15514'
ht-degree: 97%

---

# ポリシーを使用したドキュメントの保護 {#protecting-documents-with-policies}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

**Document Security サービスについて**

Document Security サービスを使用すると、ユーザーは、ドキュメントの配布範囲にかかわらず、Adobe PDF ドキュメントに機密性の設定を動的に適用したり、ドキュメントを管理したりできます。

Document Security サービスは、ポリシーで保護された PDF ドキュメントを受信者がどのように使用するかをユーザーが管理できるようにすることで、ユーザーの手の届かない範囲で情報が広がるのを防ぎます。 ユーザーは、配布後に、ドキュメントを誰が開くことができるかを指定でき、ドキュメントの使用方法を制限でき、ドキュメントを監視できます。 また、ユーザーは、ポリシーで保護されたドキュメントへのアクセスを動的に制御することもでき、ドキュメントへのアクセスを動的に取り消すことさえできます。

また、Document Security サービスでは、Microsoft Word ファイル（DOC ファイル）などの他のファイルタイプも保護します。 Document Security Client API を使用して、これらのファイルタイプを操作できます。 次のバージョンがサポートされています。

* Microsoft Office 2003 ファイル（DOC、XLS、PPT ファイル）
* Microsoft Office 2007 ファイル（DOCX、XLSX、PPTX ファイル）
* PTC Pro/E ファイル

次の 2 つの節で、Word ドキュメントの操作方法を説明します。

* [Word ドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Word ドキュメントからのポリシーの削除](protecting-documents-policies.md#removing-policies-from-word-documents)

Document Security サービスを使用して、次のタスクを実行できます。

* ポリシーの作成. 詳しくは、[ポリシーの作成](protecting-documents-policies.md#creating-policies)を参照してください。
* ポリシーの変更。 詳しくは、[ポリシーの変更](protecting-documents-policies.md#modifying-policies)を参照してください。
* ポリシーの削除。 詳しくは、[ポリシーの削除](protecting-documents-policies.md#deleting-policies)を参照してください。
* PDF ドキュメントへのポリシーの適用。詳しくは、[PDF ドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)を参照してください。
* PDF ドキュメントからのポリシーの削除。詳しくは、[PDF ドキュメントからのポリシーの削除](protecting-documents-policies.md#removing-policies-from-pdf-documents)を参照してください。
* ポリシーで保護されたドキュメントの検査。詳しくは、[ポリシーで保護された PDF ドキュメントの検査](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents)を参照してください。
* PDF ドキュメントへのアクセス権限の取り消し。詳しくは、[ドキュメントへのアクセス権の失効](protecting-documents-policies.md#revoking-access-to-documents)を参照してください。
* 取り消されたドキュメントへのアクセス権の回復。詳しくは、[失効したドキュメントへのアクセスの回復](protecting-documents-policies.md#reinstating-access-to-revoked-documents)を参照してください。
* 透かしの作成。 詳しくは、[透かしの作成](protecting-documents-policies.md#creating-watermarks)を参照してください。
* イベントの検索。 詳しくは、[イベントの検索](protecting-documents-policies.md#searching-for-events)を参照してください。

>[!NOTE]
>
>Document Security サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## ポリシーの作成 {#creating-policies}

Document Security Java API または Web サービス API を使用して、プログラムでポリシーを作成できます。 *ポリシー* は、Document Security の設定、許可されたユーザー、使用権限などの情報を集めたものです。 様々な状況やユーザーに適したセキュリティ設定を使用して、任意の数のポリシーを作成および保存できます。

ポリシーを使用すると、次のタスクを実行できます。

* ドキュメントを開くことができる個人の指定。 受信者は、組織に所属していても、組織の外部にいてもかまいません。
* 受信者によるドキュメントの使用方法の指定。 Acrobat と Adobe Reader の様々な機能へのアクセスを制限できます。 これらの機能には、テキストの印刷とコピー、署名の追加、ドキュメントへのコメントの追加などが含まれます。
* ポリシーで保護されたドキュメントの任意の時点（配布後も含む）でのアクセスおよびセキュリティ設定の変更。
* ドキュメントの配布後の使用状況の監視。 ドキュメントが誰にどのように使用されているかを確認できます。 例えば、誰かがドキュメントを開いた日時を調べることができます。

### Web サービスを使用したポリシーの作成 {#creating-a-policy-using-web-services}

Web サービス API を使用してポリシーを作成する場合は、そのポリシーを記述する既存の Portable Document Rights Language（PDRL）XML ファイルを参照します。ポリシー権限とプリンシパルは、PDRL ドキュメントで定義されます。次の XML ドキュメントは、PDRL ドキュメントの例です。

```xml
 <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
 <Policy PolicyInstanceVersion="1" PolicyID="5DA3F847-DE76-F9CC-63EA-49A8D59154DE" PolicyCreationTime="2004-08-30T00:02:28.294+00:00" PolicyType="1" PolicySchemaVersion="1.0" PolicyName="SDK Test Policy -4344050357301573237" PolicyDescription="An SDK Test policy" xmlns="https://www.adobe.com/schema/1.0/pdrl">
       <PolicyEntry>
          <ns1:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns1="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns2:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns2="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns3:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns3="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns4:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns4="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>all_internal_users</PrincipalName>
          </Principal>
       </PolicyEntry>
       <PolicyEntry>
          <ns5:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns5="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns6:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns6="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns7:Permission PermissionName="com.adobe.aps.pdf.copy" Access="ALLOW" xmlns:ns7="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns8:Permission PermissionName="com.adobe.aps.pdf.printLow" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns8="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns9:Permission PermissionName="com.adobe.aps.policySwitch" Access="ALLOW" xmlns:ns9="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns10:Permission PermissionName="com.adobe.aps.revoke" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns10="https://www.adobe.com/schema/1.0/pdrl" />
 
          <ns11:Permission PermissionName="com.adobe.aps.pdf.edit" Access="ALLOW" xmlns:ns11="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns12:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns12="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns13:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns13="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <ns14:Permission PermissionName="com.adobe.aps.pdf.printHigh" Access="ALLOW" xmlns:ns14="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" />
 
          <Principal PrincipalNameType="SYSTEM">
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain>
 
             <PrincipalName>publisher</PrincipalName>
          </Principal>
       </PolicyEntry>
 
       <OfflineLeasePeriod>
          <Duration>P31D</Duration>
       </OfflineLeasePeriod>
 
       <AuditSettings isTracked="true" />
 
       <PolicyValidityPeriod isAbsoluteTime="false">
          <ValidityPeriodRelative>
             <NotBeforeRelative>PT0S</NotBeforeRelative>
 
             <NotAfterRelative>P20D</NotAfterRelative>
          </ValidityPeriodRelative>
       </PolicyValidityPeriod>
 </Policy>
 
```

>[!NOTE]
>
>Document Security サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary-of-steps}

ポリシーを作成するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Document Security Client API オブジェクトを作成します。
1. ポリシーの属性を設定します。
1. ポリシーエントリを作成します。
1. ポリシーを登録します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-rightsmanagement-client.jar
* namespace.jar（AEM Forms が JBoss にデプロイされている場合）
* jaxb-api.jar（AEM Forms が JBoss にデプロイされている場合）
* jaxb-impl.jar（AEM Forms が JBoss にデプロイされている場合）
* jaxb-libs.jar（AEM Forms が JBoss にデプロイされている場合）
* jaxb-xjc.jar（AEM Forms が JBoss にデプロイされている場合）
* relaxingDatatype.jar（AEM Forms が JBoss にデプロイされている場合）
* xsdlib.jar（AEM Forms が JBoss にデプロイされている場合）
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar（AEM Forms が JBoss にデプロイされていない場合は、別の JAR ファイルを使用）

これらの JAR ファイルの場所について詳しくは、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**Document Security Client API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成します。

**ポリシー属性の設定**

ポリシーを作成するには、ポリシー属性を設定します。必須の属性は、ポリシー名です。ポリシー名は、ポリシーセットごとに一意である必要があります。ポリシーセットは、単にポリシーの集まりです。ポリシーが別々のポリシーセットに属している場合は、同じ名前の 2 つのポリシーを使用できます。ただし、1 つのポリシーセット内の 2 つのポリシーが同じポリシー名を持つことはできません。

有効期間も役に立つ属性です。有効期間とは、権限を持つ受信者がポリシーで保護されたドキュメントにアクセスできる期間を指します。この属性を設定しない場合、ポリシーは常に有効です。

有効期間は、次のいずれかのオプションに設定できます。

* ドキュメントが公開されてからドキュメントにアクセスできる日数
* ドキュメントにアクセスできなくなる終了日
* ドキュメントにアクセスできる特定の日付範囲
* 常に有効

開始日のみを指定した場合、ポリシーは開始日より後に有効になります。終了日のみを指定した場合、ポリシーは終了日まで有効です。ただし、開始日と終了日の両方が定義されていない場合は、例外が発生します。

ポリシーに属する属性を設定する場合は、暗号化設定も指定できます。これらの暗号化設定は、ポリシーがドキュメントに適用される際に影響を受けます。次の暗号化値を指定できます。

* **AES256**：256 ビットキーを持つ AES 暗号化アルゴリズムを表します。
* **AES128**：128 ビットキーを持つ AES 暗号化アルゴリズムを表します。
* **暗号化なし**：暗号化しないことを表します。

`NoEncryption` オプションを指定した場合、`PlaintextMetadata` オプションを `false` に設定することはできません。その場合は、例外が発生します。

>[!NOTE]
>
>設定可能なその他の属性について詳しくは、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)で `Policy` インターフェイスの説明について参照してください。

**ポリシーエントリの作成**

ポリシーエントリは、プリンシパル（グループとユーザー）と権限をポリシーに添付します。ポリシーには少なくとも 1 つのポリシーエントリが必要です。例えば、次のタスクを実行したとします。

* グループがオンライン中にのみドキュメントを表示できるようにし、受信者がドキュメントをコピーできないようにするポリシーエントリを作成して登録します。
* ポリシーにポリシーエントリを添付します。
* Acrobat を使用して、ポリシーでドキュメントを保護します。

これらのアクションを実行すると、受信者はドキュメントをオンラインで表示するだけで、コピーできなくなります。ドキュメントからセキュリティが削除されるまで、ドキュメントは安全なままです。

**ポリシーを登録**

新しいポリシーを使用するには、そのポリシーを登録する必要があります。ポリシーを登録すると、そのポリシーを使用してドキュメントを保護できます。

### Java API を使用したポリシーの作成 {#create-a-policy-using-the-java-api}

Document Security API（Java）を使用してポリシーを作成します。

1. プロジェクトファイルを含めます。

   adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Document Security Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーの属性を設定します。

   * `InfomodelObjectFactory` オブジェクトの静的 `createPolicy` メソッドを呼び出すことによって `Policy` オブジェクトを作成します。このメソッドは `Policy` オブジェクトを返します。
   * `Policy` オブジェクトの `setName` メソッドを呼び出し、ポリシー名を指定する文字列値を渡すことにより、ポリシーの名前属性を設定します。
   * `Policy` オブジェクトの `setDescription` メソッドを呼び出し、ポリシーの説明を指定する文字列値を渡すことにより、ポリシーの説明を設定します。
   * `Policy` オブジェクトの `setPolicySetName` メソッドを呼び出し、ポリシーセット名を指定する文字列値を渡すことにより、新しいポリシーが属するポリシーセットを設定します（このパラメーター値に `null` を指定すると、このポリシーが&#x200B;*マイポリシー*&#x200B;ポリシーセットに追加されます）。
   * `InfomodelObjectFactory` オブジェクトの静的 `createValidityPeriod` メソッドを呼び出して、ポリシーの有効期間を作成します。このメソッドは `ValidityPeriod` オブジェクトを返します。
   * `ValidityPeriod` オブジェクトの `setRelativeExpirationDays` メソッドを呼び出し、日数を指定する整数値を渡すことにより、ポリシーで保護されたドキュメントにアクセスできる日数を設定します。
   * `Policy` オブジェクトの `setValidityPeriod` メソッドを呼び出して `ValidityPeriod` オブジェクトを渡すことにより、ポリシーの有効期間を設定します。

1. ポリシーエントリを作成します。

   * `InfomodelObjectFactory` オブジェクトの静的 `createPolicyEntry` メソッドを呼び出してポリシーエントリを作成します。このメソッドは `PolicyEntry` オブジェクトを返します。
   * `InfomodelObjectFactory` オブジェクトの静的 `createPermission` メソッドを呼び出して、ポリシーの権限を指定します。権限を表す `Permission` インターフェイスに属する静的データメンバーを渡します。このメソッドは `Permission` オブジェクトを返します。例えば、ポリシーで保護された PDF ドキュメントのデータをユーザーがコピーできる権限を追加するには、`Permission.COPY` を渡します（追加する権限ごとに、この手順を繰り返します）。
   * `PolicyEntry` オブジェクトの `addPermission` メソッドを呼び出して `Permission` オブジェクトを渡すことにより、ポリシーエントリに権限を追加します（この手順を作成した各 `Permission` オブジェクトについて繰り返します）。
   * `InfomodelObjectFactory` オブジェクトの静的 `createSpecialPrincipal` メソッドを呼び出して、ポリシープリンシパルを作成します。プリンシパルを表す `InfomodelObjectFactory` オブジェクトに属するデータメンバーを渡します。このメソッドは `Principal` オブジェクトを返します。例えば、ドキュメントのパブリッシャーをプリンシパルとして追加するには、 `InfomodelObjectFactory.PUBLISHER_PRINCIPAL` を渡します。
   * `PolicyEntry` オブジェクトの `setPrincipal`メソッドを呼び出して `Principal` オブジェクトを渡すことにより、ポリシーエントリにプリンシパルを追加します。
   * `Policy` オブジェクトの `addPolicyEntry` メソッドを呼び出して `PolicyEntry` オブジェクトを渡すことにより、ポリシーエントリをポリシーに追加します。

1. ポリシーを登録します。

   * `DocumentSecurityClient` オブジェクトの `getPolicyManager` メソッドを呼び出すことによって `PolicyManager` オブジェクトを作成します。
   * `PolicyManager` オブジェクトの `registerPolicy` メソッドを呼び出して次の値を渡すことによって、ポリシーを登録します。

      * 登録するポリシーを表す `Policy` オブジェクト。
   * ポリシーが属するポリシーセットを表す文字列値。

   接続設定で AEM Forms 管理者アカウントを使用して `DocumentSecurityClient` オブジェクトを作成する場合は、`registerPolicy` メソッドを呼び出す際にポリシーセット名を指定します。ポリシーセットに `null` 値を渡すと、ポリシーは管理者の&#x200B;*マイポリシー*&#x200B;のポリシーセットに作成されます。

   接続設定内で Document Security ユーザーを使用する場合は、ポリシーのみを受け入れる過負荷の `registerPolicy` メソッドを呼び出すことができます。つまり、ポリシーセット名を指定する必要はありません。ただし、ポリシーは&#x200B;*マイポリシー*&#x200B;という名前のポリシーセットに追加されます。このポリシーセットに新しいポリシーを追加しない場合は、`registerPolicy` メソッドを呼び出す際にポリシーセット名を指定します。

   >[!NOTE]
   >
   >ポリシーを作成するとき、既存のポリシーセットを参照します。存在しないポリシーセットを指定すると、例外がスローされます。

Document Security サービスを使用するコード例については、次を参照してください。

* &quot;クイックスタート（SOAP モード）：Java API を使用したポリシーの作成&quot;

### Web サービス API を使用してポリシーを作成する {#create-a-policy-using-the-web-service-api}

Document Security API（web サービス）を使用してポリシーを作成します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Document Security Client API オブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `DocumentSecurityServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `DocumentSecurityServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `RightsManagementServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `RightsManagementServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `RightsManagementServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。


1. ポリシーの属性を設定します。

   * コンストラクタを使用して `PolicySpec` オブジェクトを作成します。
   * `PolicySpec` オブジェクトの `name` データメンバーに文字列値を割り当てることにより、ポリシーの名前を設定します。
   * `PolicySpec` オブジェクトの `description` データメンバーに文字列値を割り当てることにより、ポリシーの説明を設定します。
   * `PolicySpec` オブジェクトの `policySetName` データメンバーに文字列値を割り当てることにより、ポリシーが属するポリシーセットを設定します。既存のポリシーセット名を指定する必要があります（このパラメーター値に `null` を指定すると、このポリシーは&#x200B;*マイポリシー*&#x200B;に追加されます）。
   * `PolicySpec` オブジェクトの `offlineLeasePeriod` データメンバーに整数値を割り当てることにより、ポリシーのオフラインリース期間を設定します。
   * PDRL XML データを表す文字列値を使用して `PolicySpec` オブジェクトの `policyXml` データメンバーを設定します。このタスクを実行するには、コンストラクターを使用して .NET `StreamReader` オブジェクトを作成します。ポリシーを表す PDRL XML ファイルの場所を `StreamReader` コンストラクターに渡します。次に、`StreamReader` オブジェクトの `ReadLine` メソッドを呼び出し、戻り値を文字列変数に割り当てます。`ReadLine` メソッドが null を返すまで `StreamReader` オブジェクトを反復します。文字列変数を `PolicySpec` オブジェクトの `policyXml` データメンバーに割り当てます。

1. ポリシーエントリを作成します。

   Document Security web サービス API を使用してポリシーを作成する場合は、ポリシーエントリを作成する必要はありません。ポリシーエントリは、PDRL ドキュメントで定義されます。

1. ポリシーを登録します。

   `DocumentSecurityServiceClient` オブジェクトの `registerPolicy` メソッドを呼び出して、次の値を渡すことにより、ポリシーを登録します。

   * 登録するポリシーを表す `PolicySpec` オブジェクト。
   * ポリシーが属するポリシーセットを表す文字列値。`null` 値を指定すると、このポリシーは&#x200B;*マイポリシー* に追加されることになります。

   接続設定で AEM Forms 管理者アカウントを使用して `DocumentSecurityClient` オブジェクトを作成する場合は、`registerPolicy` メソッドを呼び出す際にポリシーセット名を指定します。

   接続設定内で Document Security ユーザーを使用する場合は、ポリシーのみを受け入れる過負荷の `registerPolicy` メソッドを呼び出すことができます。つまり、ポリシーセット名を指定する必要はありません。ただし、ポリシーは&#x200B;*マイポリシー*&#x200B;という名前のポリシーセットに追加されます。このポリシーセットに新しいポリシーを追加しない場合は、`registerPolicy` メソッドを呼び出す際にポリシーセット名を指定します。

   >[!NOTE]
   >
   >ポリシーを作成し、ポリシーセットを指定する場合は、既存のポリシーセットを指定してください。存在しないポリシーセットを指定すると、例外がスローされます。

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用したポリシーの作成»
* クイックスタート (SwaRef):Web サービス API を使用したポリシーの作成»

## ポリシーの変更 {#modifying-policies}

既存のポリシーは、Document Security Java API または web サービス API を使用して変更できます。既存のポリシーを変更するには、そのポリシーを取得し、変更してから、サーバー上のポリシーを更新します。例えば、既存のポリシーを取得し、その有効期間を延長するとします。変更を反映するには、ポリシーを更新する必要があります。

ビジネス要件が変わり、ポリシーがその要件を反映しなくなった場合、ポリシーを変更できます。新しいポリシーを作成しなくても、既存のポリシーを更新するだけで済みます。

Web サービスを使用してポリシー属性を変更するには（例えば、JAX-WS で作成された Java プロキシクラスを使用する場合）、ポリシーが Document Security サービスに登録されていることを確認する必要があります。その後、`PolicySpec.getPolicyXml` メソッドを使用して既存のポリシーを参照し、該当するメソッドを使用してポリシー属性を変更できます。たとえば、`PolicySpec.setOfflineLeasePeriod` メソッドを呼び出して、オフラインリース期間を変更できます。

>[!NOTE]
>
>Document Security サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-1}

既存のポリシーを変更するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client API オブジェクトを作成します。
1. 既存のポリシーを取得します。
1. ポリシー属性を変更します。
1. ポリシーを更新します。

**プロジェクトファイルの組み込み**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**Document Security Client API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成する必要があります。Java API を使用している場合は、`RightsManagementClient` オブジェクトを作成します。Document Security web サービス API を使用している場合は、`RightsManagementServiceService` オブジェクトを作成します。

**既存のポリシーの取得**

既存のポリシーを変更するには、そのポリシーを取得する必要があります。ポリシーを取得するには、ポリシー名とポリシーが属するポリシーセットを指定します。ポリシーセット名に `null` 値を指定すると、ポリシーは&#x200B;*マイポリシー*&#x200B;ポリシーセットから取得されます。

**ポリシーの属性の設定**

ポリシーを変更するには、ポリシー属性の値を変更します。変更できない唯一のポリシー属性は名前属性です。例えば、ポリシーのオフラインリース期間を変更するには、ポリシーのオフラインリース期間属性の値を変更します。

Web サービスを使用してポリシーのオフラインリース期間を変更する場合、`PolicySpec` インターフェイスの `offlineLeasePeriod` フィールドは無視されます。オフラインリース期間を更新するには、PDRL XML ドキュメントの `OfflineLeasePeriod` 要素を変更します。次に、`PolicySpec` インターフェイスの `policyXML` データメンバーを使用して、更新された PDRL XML ドキュメントを参照します。

>[!NOTE]
>
>設定可能なその他の属性については、[AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)の `Policy` インターフェイスの説明を参照してください。

**ポリシーの更新**

ポリシーに対して行った変更を有効にするには、Document Security サービスを使用してポリシーを更新する必要があります。ドキュメントを保護するポリシーに対する変更は、次にポリシーで保護されたドキュメントが Document Security サービスと同期されるときに更新されます。

### Java API を使用した既存のポリシーの変更 {#modify-existing-policies-using-the-java-api}

Document Security API（Java）を使用して既存のポリシーを変更します。

1. プロジェクトファイルを含めます。

   adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Document Security Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 既存のポリシーを取得します。

   * `RightsManagementClient` オブジェクトの `getPolicyManager` メソッドを呼び出すことによって `PolicyManager` オブジェクトを作成します。
   * の作成 `Policy` を呼び出して更新するポリシーを表すオブジェクト `PolicyManager` オブジェクトの `getPolicy` メソッドを使用して次の値を渡す»

      * ポリシーが属するポリシーセット名を表す文字列値。`null` を指定すると、`MyPolicies` ポリシーセットが使用されるようになります。
      * ポリシー名を表す文字列値。

1. ポリシーの属性を設定します。

   ビジネス要件に合わせてポリシーの属性を変更します。例えば、ポリシーのオフラインリース期間を変更するには、`Policy` オブジェクトの `setOfflineLeasePeriod` メソッドを呼び出します。

1. ポリシーを更新します。

   `PolicyManager` オブジェクトの `updatePolicy` メソッドを呼び出してポリシーを更新します。更新するポリシーを表す `Policy` オブジェクトを渡します。

**コード例**

Document Security サービスを使用するコード例については、「クイックスタート（SOAP モード）：Java API を使用したポリシーの変更」の節を参照してください。

### Web サービス API を使用して既存のポリシーを変更する {#modify-existing-policies-using-the-web-service-api}

Document Security API（web サービス）を使用して既存のポリシーを変更します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Document Security Client API オブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `RightsManagementServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `RightsManagementServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `RightsManagementServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `RightsManagementServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `RightsManagementServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。


1. 既存のポリシーを取得します。

   `RightsManagementServiceClient` オブジェクトの `getPolicy` メソッドを呼び出し、次の値を渡すことにより、変更するポリシーを表す `PolicySpec` オブジェクトを作成します。

   * ポリシーが属するポリシーセット名を指定する文字列値。`null` を指定すると、`MyPolicies` ポリシーセットが使用されます。
   * ポリシーの名前を指定する文字列値。

1. ポリシーの属性を設定します。

   ビジネス要件に合わせてポリシーの属性を変更します。

1. ポリシーを更新します。

   `RightsManagementServiceClient` オブジェクトの `updatePolicyFromSDK` メソッドを呼び出し、更新するポリシーを表す `PolicySpec` オブジェクトを渡すことにより、ポリシーを更新します。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用したポリシーの変更»
* クイックスタート (SwaRef):Web サービス API を使用したポリシーの変更»

## ポリシーの削除 {#deleting-policies}

既存のポリシーは、Document Security Java API または web サービス API を使用して削除できます。ポリシーを削除すると、そのポリシーをドキュメントの保護に使用できなくなります。ただし、ポリシーを使用している既存のポリシーで保護されたドキュメントは、引き続き保護されます。新しいポリシーが利用可能になったら、ポリシーを削除できます。

>[!NOTE]
>
>Document Security サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-2}

既存のポリシーを削除するには、次の手順に従います。

1. プロジェクトファイルを含める
1. Document Security Client API オブジェクトを作成します。
1. ポリシーを削除します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**Document Security Client API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行するには、事前に Document Security サービスのクライアントオブジェクトを作成する必要があります。Java API を使用している場合は、`RightsManagementClient` オブジェクトを作成します。Document Security web サービス API を使用している場合は、`RightsManagementServiceService` オブジェクトを作成します。

**ポリシーを削除**

ポリシーを削除するには、削除するポリシーと、そのポリシーが属するポリシーセットを指定します。AEM Forms の呼び出しに設定を使用するユーザーには、ポリシーを削除する権限が必要です。権限がない場合は、例外が発生します。同様に、存在しないポリシーを削除しようとすると、例外が発生します。

### Java API を使用したポリシーの削除 {#delete-policies-using-the-java-api}

Document Security API（Java）を使用してポリシーを削除します。

1. プロジェクトファイルを含めます。

   adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Document Security Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーを削除します。

   * `RightsManagementClient` オブジェクトの `getPolicyManager` メソッドを呼び出すことにより、`PolicyManager` オブジェクトを作成します。
   * `PolicyManager` オブジェクトの `deletePolicy` メソッドを呼び出し、次の値を渡すことにより、ポリシーを削除します。

      * ポリシーが属するポリシーセット名を指定する文字列値。`null` を指定すると、`MyPolicies` ポリシーセットが使用されます。
      * 削除するポリシーの名前を指定する文字列値。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* &quot;クイックスタート（SOAP モード）：Java API を使用したポリシーの削除&quot;

### Web サービス API を使用したポリシーの削除 {#delete-policies-using-the-web-service-api}

Document Security API（web サービス）を使用してポリシーを削除します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Document Security Client API オブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `RightsManagementServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `RightsManagementServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `RightsManagementServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `RightsManagementServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `RightsManagementServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。


1. ポリシーを削除します。

   `RightsManagementServiceClient` オブジェクトの `deletePolicy` メソッドを呼び出し次の値を渡すことによって、ポリシーを削除します。

   * ポリシーが属するポリシーセット名を指定する文字列値。`null` を指定すると、`MyPolicies` ポリシーセットが使用されます。
   * 削除するポリシーの名前を指定する文字列値。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用したポリシーの削除»
* クイックスタート (SwaRef):Web サービス API を使用したポリシーの削除»

## PDF ドキュメントへのポリシーの適用 {#applying-policies-to-pdf-documents}

ドキュメントを保護するために、PDF ドキュメントにポリシーを適用できます。 ポリシーを PDF ドキュメントに適用すると、ドキュメントへのアクセスを制限できます。ドキュメントを保護しているポリシーが既にある場合は、このドキュメントにポリシーを適用することはできません。

ドキュメントを開いている間は、テキストの印刷とコピー、変更、ドキュメントへの署名とコメントの追加など、Acrobat と Adobe Reader の機能へのアクセスを制限することもできます。 また、ユーザーのドキュメントへのアクセスを制限する場合に、ポリシーで保護された PDF ドキュメントを失効させることもできます。

ポリシーで保護されたドキュメントを配布した後で、そのドキュメントの使用を監視できます。つまり、ドキュメントが誰によって、どのように使用されているかを確認できるということです。例えば、誰かがそのドキュメントを開いた日時を知ることができます。

>[!NOTE]
>
>Document Security サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-3}

ポリシーを PDF ドキュメントに適用するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client API オブジェクトを作成します。
1. ポリシーが適用される PDF ドキュメントを取得します。
1. PDF ドキュメントに既存のポリシーを適用します。
1. ポリシーで保護された PDF ドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**Document Security クライアント API オブジェクトの作成**

Document Security サービスの操作をプログラム的に実行するには、その前にまず Document Security サービスのクライアントオブジェクトを作成します。 Java API を使用している場合は、`DocumentSecurityClient` オブジェクトを作成します。Document Security Web サービス API を使用する場合は、`DocumentSecurityServiceService` オブジェクトを作成します。

**PDF 文書の取得**

ポリシーを適用する PDF ドキュメントを取得できます。 ポリシーを PDF ドキュメントに適用すると、ユーザーはドキュメントを使用する際に制限を受けます。 例えば、ドキュメントをオフラインで開くことができないようポリシーで定められている場合、ユーザーがドキュメントを開くにはオンラインである必要があります。

**PDF ドキュメントに既存のポリシーを適用**

ポリシーを PDF ドキュメントに適用するには、既存のポリシーを参照し、ポリシーが属するポリシーセットを指定します。 接続プロパティを設定するユーザーは、指定したポリシーにアクセスできる必要があります。 できない場合は、例外が発生します。

**PDF ドキュメントを保存**

Document Security サービスによってポリシーが PDF ドキュメントに適用された後、ポリシーで保護された PDF ドキュメントを PDF ファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ドキュメントへのアクセス権の失効](protecting-documents-policies.md#revoking-access-to-documents)

### Java API を使用した PDF ドキュメントへのポリシーの適用 {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Document Security API（Java）を使用して、PDF ドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Document Security Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDF ドキュメントを取得します。

   * コンストラクターを使用して PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。PDF ドキュメントの場所を指定する文字列値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF ドキュメントに既存のポリシーを適用します。

   * `RightsManagementClient` オブジェクトの `getDocumentManager` メソッドを呼び出して `DocumentManager` オブジェクトを作成します。
   * `DocumentManager` オブジェクトの `protectDocument` メソッドを呼び出し、次の値を渡すことによって、PDF ドキュメントにポリシーを適用します。

      * このポリシーが適用される PDF ドキュメントが格納される `com.adobe.idp.Document` オブジェクト。
      * ドキュメントの名前を指定する文字列値。
      * ポリシーが属しているポリシーセットの名前を表す文字列値。`null` 値を指定すると、`MyPolicies` ポリシーセットが使用されます。
      * ポリシー名を指定する文字列値。
      * ドキュメントのパブリッシャーであるユーザーのユーザーマネージャードメインの名前を表す文字列値。このパラメーターの値はオプションであり、null にすることができます（このパラメーターが null の場合、次のパラメーターの値も null にする必要があります）。
      * ドキュメントのパブリッシャーであるユーザーマネージャーユーザーの正規名の名前を表す文字列値。このパラメーター値はオプションで、`null` にできます（このパラメーターを null にする場合、前のパラメーター値は `null` である必要があります）。
      * MS Office テンプレートの選択に使用されるロケールを表す `com.adobe.livecycle.rightsmanagement.Locale` です。このパラメーター値はオプションで、PDF ドキュメントには使用されません。 PDF ドキュメントを保護するには、`null` を指定します。

      `protectDocument` メソッドは、ポリシーで保護された PDF ドキュメントが格納される `RMSecureDocumentResult` オブジェクト。


1. PDF ドキュメントを保存します。

   * `RMSecureDocumentResult` オブジェクトの `getProtectedDoc` メソッドを呼び出して、ポリシーで保護された PDF ドキュメントを取得します。 このメソッドは `com.adobe.idp.Document` オブジェクトを返します。
   * `java.io.File` オブジェクトを作成し、ファイル拡張子が PDF であることを確認します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、`Document` オブジェクトの内容をファイルにコピーします（`getProtectedDoc` メソッドが返した `Document` オブジェクトを使用するようにしてください）。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート（EJB モード）:Java API を使用したPDFドキュメントへのポリシーの適用»
* &quot;クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントへのポリシーの適用&quot;

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した PDF ドキュメントへのポリシーの適用 {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Document Security API（web サービス）を使用して、PDF ドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Document Security Client API オブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `RightsManagementServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `RightsManagementServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を Forms サービスに渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `RightsManagementServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `RightsManagementServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `RightsManagementServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。


1. PDF ドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、ポリシーが適用される PDF ドキュメントを格納するために使用されます。
   * コンストラクターを呼び出し、PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクトの `Length` プロパティを取得してバイト配列を決定します。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出してバイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` フィールドを割り当てて、`BLOB` オブジェクトにバイト配列の内容を入力します。

1. PDF ドキュメントに既存のポリシーを適用します。

   `RightsManagementServiceClient` オブジェクトの `protectDocument` メソッドを呼び出して、次の値を渡して PDF ドキュメントにポリシーを適用します。

   * このポリシーが適用される PDF ドキュメントが格納される `BLOB` オブジェクト。
   * ドキュメントの名前を指定する文字列値。
   * ポリシーが属しているポリシーセットの名前を表す文字列値。`null` 値を指定すると、`MyPolicies` ポリシーセットが使用されます。
   * ポリシー名を指定する文字列値。
   * ドキュメントのパブリッシャーであるユーザーのユーザーマネージャードメインの名前を表す文字列値。このパラメーター値はオプションであり、null にすることができます（このパラメーターが null の場合、次のパラメーター値は `null` である必要があります）。
   * ドキュメントのパブリッシャーであるユーザーマネージャーユーザーの正規名の名前を表す文字列値。このパラメーター値はオプションであり、null にすることができます（このパラメーターが null の場合、前のパラメーター値は `null` である必要があります）。
   * ロケール値を指定する `RMLocale` 値（例： `RMLocale.en`）。
   * ポリシー識別子の値を格納するために使用される文字列出力パラメーター。
   * ポリシーで保護された識別子の値を保存するために使用される文字列出力パラメーター。
   * MIME タイプを保存するために使用される文字列出力パラメーター（例： `application/pdf`）。

   `protectDocument` メソッドは、 ポリシーで保護された PDF ドキュメントを含む `BLOB` オブジェクトを返します。

1. PDF ドキュメントを保存します。

   * コンストラクターを呼び出し、ポリシーで保護された PDF ドキュメントのファイルの場所を表す文字列値を渡すことで `System.IO.FileStream` オブジェクトを作成します。
   * `protectDocument` メソッドで返された `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` データメンバーの値を取得して、バイト配列を生成します。
   * コンストラクターを使用して `System.IO.BinaryWriter` オブジェクトを渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDF ファイルに書き込みます。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用してPDFドキュメントにポリシーを適用する»
* クイックスタート (SwaRef):Web サービス API「 」を使用してPDFドキュメントにポリシーを適用する

## PDF ドキュメントからのポリシーの削除 {#removing-policies-from-pdf-documents}

ポリシーで保護されたドキュメントからポリシーを削除して、ドキュメントからセキュリティを削除できます。つまり、ドキュメントをポリシーで保護したくない場合です。ポリシーで保護されたドキュメントを新しいポリシーで更新する場合は、ポリシーを削除して更新されたポリシーを追加する代わりに、ポリシーを切り替える方が効率的です。

>[!NOTE]
>
>Document Security サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63) を参照してください。

### 手順の概要 {#summary_of_steps-4}

ポリシーで保護された PDF ドキュメントからポリシーを削除するには、次の手順を実行します。

1. プロジェクトファイルを含める
1. Document Security Client API オブジェクトを作成します。
1. ポリシーで保護された PDF ドキュメントを取得します。
1. PDF ドキュメントからポリシーを削除します。
1. 保護されていない PDF ドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**ドキュメントセキュリティクライアント API オブジェクトを作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成します。

**ポリシーで保護された PDF ドキュメントの取得**

ポリシーで保護された PDF ドキュメントを取得してポリシーを削除できます。ポリシーで保護されていない PDF ドキュメントからポリシーを削除しようとすると、例外が発生します。

**PDF ドキュメントからポリシーを削除**

接続設定で管理者が指定されている場合は、ポリシーで保護された PDF ドキュメントからポリシーを削除できます。そうでない場合、PDF ドキュメントからポリシーを削除するには、ドキュメントを保護するポリシーに `SWITCH_POLICY` 権限が含まれている必要があります。また、AEM Forms 接続設定で指定したユーザーにも、その権限が必要です。それ以外の場合は、例外がスローされます。

**保護されていない PDF ドキュメントを保存**

Document Security サービスが PDF ドキュメントからポリシーを削除した後、保護されていない PDF ドキュメントを PDF ファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF ドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Java API を使用して PDF ドキュメントからポリシーを削除する {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Document Security API（Java）を使用して、ポリシーで保護された PDF ドキュメントからポリシーを削除します。

1. プロジェクトファイルを含めます。

   adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Document Security Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護された PDF ドキュメントを取得します。

   * コンストラクターを使用し、PDF ドキュメントの場所を指定する文字列値を渡して、ポリシーで保護された PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF ドキュメントからポリシーを削除します。

   * `DocumentSecurityClient` オブジェクトの `getDocumentManager` メソッドを呼び出して `DocumentManager` オブジェクトを作成します。
   * `DocumentManager` オブジェクトの `removeSecurity` メソッドを呼び出し、ポリシーで保護された PDF ドキュメントが格納された `com.adobe.idp.Document` オブジェクトを渡すことにより、PDF ドキュメントからポリシーを削除します。このメソッドは、保護されていない PDF ドキュメントが格納された `com.adobe.idp.Document` オブジェクトを返します。

1. 保護されていない PDF ドキュメントを保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が PDF であることを確認します。
   * `Document` オブジェクトの `copyToFile` メソッドを呼び出して、`Document` オブジェクトの内容をファイルにコピーします（`removeSecurity` メソッドが返した `Document` オブジェクトを使用するようにしてください）。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* &quot;クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントからのポリシーの削除&quot;

### Web サービス API を使用したポリシーの削除 {#remove-a-policy-using-the-web-service-api}

Document Security API（web サービス）を使用して、ポリシーで保護された PDF ドキュメントからポリシーを削除します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Document Security Client API オブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `DocumentSecurityServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `DocumentSecurityServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `DocumentSecurityServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `DocumentSecurityServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。


1. ポリシーで保護された PDF ドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、ポリシーの削除対象となる、ポリシーで保護された PDF ドキュメントを格納するために使用されます。
   * コンストラクターを呼び出し、PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * `MTOM` フィールドを割り当てて、`BLOB` オブジェクトにバイト配列の内容を入力します。

1. PDF ドキュメントからポリシーを削除します。

   PDF ドキュメントからポリシーを削除するには、`DocumentSecurityServiceClient` オブジェクトの `removePolicySecurity` メソッドを呼び出し、ポリシーで保護された PDF ドキュメントを含む `BLOB` オブジェクトを渡します。このメソッドは、保護されていない PDF ドキュメントを含む `BLOB` オブジェクトを返します。

1. 保護されていない PDF ドキュメントを保存します。

   * `System.IO.FileStream` オブジェクトを作成するには、そのコンストラクターを呼び出し、保護されていない PDF ドキュメントのファイルの場所を表す文字列の値を渡します。
   * `removePolicySecurity` メソッドによって返された `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` フィールドの値を取得してバイト配列を入力します。
   * コンストラクターを呼び出し、`System.IO.FileStream` オブジェクトを渡すことにより、`System.IO.BinaryWriter` オブジェクトを作成します。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API「 」を使用したPDFドキュメントからのポリシーの削除
* クイックスタート (SwaRef):Web サービス API を使用したPDFドキュメントからのポリシーの削除»

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## ドキュメントへのアクセス権の失効 {#revoking-access-to-documents}

ポリシーで保護された PDF ドキュメントへのアクセスを失効させると、ドキュメントのすべてのコピーにユーザーがアクセスできなくなります。失効した PDF ドキュメントを開こうとすると、ユーザーは指定された URL にリダイレクトされ、そこで改訂されたドキュメントを表示できます。ユーザーのリダイレクト先の URL をプログラムで指定する必要があります。 ドキュメントへのアクセスを取り消すと、ユーザーが次にポリシーで保護されたドキュメントをオンラインで開いて Document Security サービスと同期したときに、変更が反映されます。

ドキュメントへのアクセスを取り消す機能により、セキュリティが強化されます。 例えば、ドキュメントの新しいバージョンが使用可能で、古いバージョンを誰にも見られたくないとします。この場合、古いドキュメントへのアクセスを取り消し、アクセス権が復元されない限り、誰もドキュメントを表示できません。

>[!NOTE]
>
>Document Security サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-5}

ポリシーで保護されたドキュメントを失効するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client API オブジェクトを作成します。
1. ポリシーで保護された PDF ドキュメントを取得します。
1. ポリシーで保護されたドキュメントを失効させます。

**プロジェクトファイルの組み込み**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**Document Security Client API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成する必要があります。

**ポリシーで保護された PDF ドキュメントの取得**

ポリシーで保護された PDF ドキュメントを取り消すには、そのドキュメントを取得する必要があります。 失効済みのドキュメントや、ポリシーで保護されたドキュメントではないドキュメントを取り消すことはできません。

ポリシーで保護されたドキュメントのライセンス識別子の値がわかっている場合は、ポリシーで保護された PDF ドキュメントを取得する必要はありません。 ただし、ほとんどの場合、ライセンス識別子の値を取得するには、PDF ドキュメントを取得する必要があります。

**ポリシーで保護されたドキュメントの取り消し**

ポリシーで保護されたドキュメントを取り消すには、ポリシーで保護されたドキュメントのライセンス識別子を指定します。 さらに、失効したドキュメントを開こうとしたときにユーザーが表示できるドキュメントの URL を指定できます。つまり、古いドキュメントが取り消されたとします。 失効したドキュメントを開こうとすると、失効したドキュメントではなく、更新されたドキュメントが表示されます。

>[!NOTE]
>
>失効済みのドキュメントを取り消そうとすると、例外が発生します。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF ドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[失効したドキュメントへのアクセスの回復](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Java API を使用したドキュメントへのアクセスの取り消し {#revoke-access-to-documents-using-the-java-api}

Document Security API（Java）を使用して、ポリシーで保護された PDF ドキュメントへのアクセスを取り消します。

1. プロジェクトファイルを含める

   adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Document Security Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護された PDF ドキュメントの取得

   * コンストラクターを使用して、PDF ドキュメントの場所を指定する文字列値を渡すことで、ポリシーで保護された PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ポリシーで保護されたドキュメントの取り消し

   * `DocumentSecurityClient` オブジェクトの `getDocumentManager` メソッドを呼び出すことによって `DocumentManager` オブジェクトを作成します。
   * `DocumentManager` オブジェクトの `getLicenseId` メソッドを呼び出して、ポリシーで保護されたドキュメントのライセンス識別子の値を取得します。ポリシーで保護されたドキュメントを表す `com.adobe.idp.Document` オブジェクトを渡します。このメソッドは、ライセンス識別子の値を表す文字列値を返します。
   * `DocumentSecurityClient` オブジェクトの `getLicenseManager` メソッドを呼び出して `LicenseManager` オブジェクトを作成します。
   * `LicenseManager` オブジェクトの `revokeLicense` メソッドを呼び出し、次の値を渡して、ポリシーで保護されたドキュメントを取り消します。

      * ポリシーで保護されたドキュメントのライセンス識別子の値を指定する文字列値（`DocumentManager` オブジェクトの `getLicenseId` メソッドの戻り値を指定します）。
      * ドキュメントを取り消す理由を指定する `License` インターフェイスの静的データメンバーです。例えば、`License.DOCUMENT_REVISED` を指定できます。
      * 改訂済みドキュメントの場所を指定する `java.net.URL` 値です。 ユーザーを別の URL にリダイレクトしないようにする場合は、`null` を渡します。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* &quot;クイックスタート（SOAP モード）：Java API を使用したドキュメントの取り消し&quot;

### Web サービス API を使用したドキュメントへのアクセスの取り消し {#revoke-access-to-documents-using-the-web-service-api}

Document Security API（web サービス）を使用して、ポリシーで保護された PDF ドキュメントへのアクセスを取り消します。

1. プロジェクトファイルを含める

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置換します。

1. Document Security Client API オブジェクトの作成

   * デフォルトのコンストラクターを使用して `DocumentSecurityServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `DocumentSecurityServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `DocumentSecurityServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `DocumentSecurityServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。


1. ポリシーで保護された PDF ドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、失効したポリシーで保護された PDF ドキュメントを格納するために使用されます。
   * コンストラクターを呼び出し、失効させるポリシーで保護された PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   *  `MTOM` フィールドを割り当てて、`BLOB` オブジェクトにバイト配列の内容を入力します。

1. ポリシーで保護されたドキュメントを失効させる

   * `DocumentSecurityServiceClient` オブジェクトの `getLicenseID` メソッドを呼び出して、ポリシーで保護されたドキュメントを表す `BLOB` オブジェクトを渡して、ポリシーで保護されたドキュメントのライセンス識別子の値を取得します。このメソッドは、ライセンス識別子を表す文字列値を返します。
   * `DocumentSecurityServiceClient` オブジェクトの `revokeLicense` メソッドを呼び出して、次の値を渡すことにより、ポリシーで保護されたドキュメントを失効させます。

      * ポリシーで保護されたドキュメントのライセンス識別子の値を指定する文字列値（`DocumentSecurityServiceService` オブジェクトの `getLicenseId` メソッド）。
      * ドキュメントを失効させる理由を指定する `Reason` enum の静的データメンバー。例えば、`Reason.DOCUMENT_REVISED` を指定できます。
      * 改訂されたドキュメントの URL の場所を指定する `string` 値。ユーザーを別の URL にリダイレクトしたくない場合、`null` を渡すことができます。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用したドキュメントの取り消し»
* クイックスタート (SwaRef):Web サービス API を使用したドキュメントの取り消し»

**関連トピック**

[Word ドキュメントからのポリシーの削除](protecting-documents-policies.md#removing-policies-from-word-documents)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 失効したドキュメントへのアクセスの回復 {#reinstating-access-to-revoked-documents}

失効した PDF ドキュメントへのアクセス権を回復すると、失効したドキュメントのすべてのコピーにユーザーがアクセスできるようになります。ユーザーが失効した回復済みドキュメントを開くと、そのドキュメントを表示できます。

>[!NOTE]
>
> Document Security サービスについて詳しくは、[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63) を参照してください。

### 手順の概要 {#summary_of_steps-6}

失効した PDF ドキュメントへのアクセス権を回復するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client API オブジェクトを作成します。
1. 失効した PDF ドキュメントのライセンス識別子を取得します。
1. 失効した PDF ドキュメントへのアクセス権を回復します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**Document Security Client API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行するには、事前に Document Security サービスのクライアントオブジェクトを作成する必要があります。Java API を使用している場合は、`DocumentSecurityClient` オブジェクトを作成します。Document Security web サービス API を使用している場合は、`DocumentSecurityServiceService` オブジェクトを作成します。

**失効した PDF ドキュメントのライセンス識別子の取得**

失効した PDF ドキュメントを復元するには、失効した PDF ドキュメントのライセンス識別子を取得する必要があります。ライセンス識別子の値を取得した後、失効したドキュメントを復元できます。失効していないドキュメントを復元しようとすると、例外が発生します。

**失効した PDF ドキュメントへのアクセス権限の復元**

失効した PDF ドキュメントへのアクセス権限を復元するには、その失効したドキュメントのライセンス識別子を指定する必要があります。失効していない PDF ドキュメントへのアクセス権限を復元しようとすると、例外が発生します。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF ドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[ドキュメントへのアクセス権の失効](protecting-documents-policies.md#revoking-access-to-documents)

### 失効したドキュメントへのアクセス権限を Java API を使用して復元する {#reinstate-access-to-revoked-documents-using-the-java-api}

Document Security API（Java）を使用して、失効したドキュメントへのアクセス権限を復元します。

1. プロジェクトファイルを含めます。

   adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Document Security Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 失効した PDF ドキュメントのライセンス識別子を取得します。

   * コンストラクターを使用し、PDF ドキュメントの場所を指定する文字列値を渡すことによって、失効した PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * `DocumentSecurityClient` オブジェクトの `getDocumentManager` メソッドを呼び出すことによって `DocumentManager` オブジェクトを作成します。
   * `DocumentManager` オブジェクトの `getLicenseId` メソッドを呼び出し、失効したドキュメントを表す `com.adobe.idp.Document` オブジェクトを渡すことによって、失効したドキュメントのライセンス識別子の値を取得します。このメソッドは、ライセンス識別子を表す文字列値を返します。

1. 失効した PDF ドキュメントへのアクセス権を回復します。

   * `DocumentSecurityClient` オブジェクトの `getLicenseManager` メソッドを呼び出すことによって `LicenseManager` オブジェクトを作成します。
   * `LicenseManager` オブジェクトの `unrevokeLicense` メソッドを呼び出し、失効したドキュメントのライセンス識別子の値を渡すことによって、失効した PDF ドキュメントへのアクセス権限を復元します。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAP モード）:Web サービス API を使用した取り消されたドキュメントへのアクセス権の回復»

### 失効したドキュメントへのアクセス権限を web サービス API を使用して復元する {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Document Security API（web サービス）を使用して、失効したドキュメントへのアクセス権限を復元します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Document Security Client API オブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `DocumentSecurityServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `DocumentSecurityServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `DocumentSecurityServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `DocumentSecurityServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を `BasicHttpBindingSecurity.Security.Mode` フィールドに割り当てます。


1. 失効した PDF ドキュメントのライセンス識別子を取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、アクセス権が回復された失効済み PDF ドキュメントを格納するために使用されます。
   * コンストラクターを呼び出し、失効した PDF ドキュメントファイルの場所とファイルを開くモードを表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * `MTOM` フィールドを割り当てて、`BLOB` オブジェクトにバイト配列の内容を入力します。

1. 失効した PDF ドキュメントへのアクセス権を回復します。

   * `DocumentSecurityServiceClient` オブジェクトの `getLicenseID` メソッドを呼び出し、失効したドキュメントを表す `BLOB` オブジェクトを渡して、失効したドキュメントのライセンス識別子の値を取得します。このメソッドは、ライセンス識別子を表す文字列値を返します。
   * `DocumentSecurityServiceClient` オブジェクトの `unrevokeLicense` メソッドを呼び出して、失効した PDF ドキュメントのライセンス識別子の値を指定する文字列値を渡すことにより、失効した PDF ドキュメントへのアクセスを回復します（`DocumentSecurityServiceClient` オブジェクトの `getLicenseId` メソッドの値を渡します）。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用した取り消されたドキュメントへのアクセス権の回復»
* クイックスタート (SwaRef):Web サービス API を使用した取り消されたドキュメントへのアクセス権の回復»

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## ポリシーで保護された PDF ドキュメントの検査 {#inspecting-policy-protected-pdf-documents}

Document Security Service API（Java および web サービス）を使用すると、ポリシーで保護された PDF ドキュメントを検査できます。ポリシーで保護された PDF ドキュメントを検査すると、ポリシーで保護された PDF ドキュメントに関する情報が返されます。例えば、ドキュメントの保護に使用されたポリシーやドキュメントを保護した日付を確認できます。

使用しているバージョンが 8.x 以前の LiveCycle の場合、このタスクを実行できません。ポリシーで保護されたドキュメントの検査に関するサポートが AEM Forms に追加されました。LiveCycle 8.x（またはそれ以前）を使用してポリシーで保護されたドキュメントを検査しようとすると、例外がスローされます。

>[!NOTE]
>
>Document Security サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-7}

ポリシーで保護された PDF ドキュメントを検査するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client API オブジェクトを作成します。
1. 検査するポリシーで保護されたドキュメントを取得します。
1. ポリシーで保護されたドキュメントに関する情報を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

**Document Security Client API オブジェクトの作成**

Document Security サービスの操作をプログラム的に実行するには、その前にまず Document Security サービスのクライアントオブジェクトを作成します。 Java API を使用している場合は、`RightsManagementClient` オブジェクトを作成します。Document Security web サービス API を使用している場合は、 `RightsManagementServiceService` オブジェクトを作成します。

**ポリシーで保護されたドキュメントを取得して検査する**

ポリシーで保護されたドキュメントを検査するには、ドキュメントを取得します。ポリシーで保護されていないドキュメントや、失効したドキュメントを検査しようとすると、例外がスローされます。

**ドキュメントを検査する**

ポリシーで保護されたドキュメントを取得した後に、それを検査することができます。

**ポリシーで保護されたドキュメントに関する情報を取得する**

ポリシーで保護された PDF ドキュメントを検査した後、そのドキュメントに関する情報を取得できます。例えば、ドキュメントの保護に使用するポリシーを指定できます。

マイポリシーに属するポリシーでドキュメントを保護して `RMInspectResult.getPolicysetName` または `RMInspectResult.getPolicysetId` を呼び出した場合は、null が戻されます。

ポリシーセットに含まれるポリシー（マイポリシー以外）を使用してドキュメントを保護する場合は、 `RMInspectResult.getPolicysetName` および `RMInspectResult.getPolicysetId` は有効な文字列を返します。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用してポリシーで保護された PDF ドキュメントを検査する {#inspect-policy-protected-pdf-documents-using-the-java-api}

Document Security Service API（Java）を使用して、ポリシーで保護された PDF ドキュメントを検査します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

1. Document Security Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 検査するポリシーで保護されたドキュメントを取得します。

   * コンストラクタを使用して、ポリシーで保護された PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。PDF ドキュメントの場所を指定する文字列値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ドキュメントを検査します。

   * `RightsManagementClient` オブジェクトの `getDocumentManager` メソッドを呼び出して `DocumentManager` オブジェクトを作成します。
   * `LicenseManager` の `inspectDocument` メソッドを呼び出して、ポリシーで保護されたドキュメントを検査します。ポリシーで保護された PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクトを渡します。このメソッドは、ポリシーで保護されたドキュメントに関する情報を含む `RMInspectResult` オブジェクトを返します。

1. ポリシーで保護されたドキュメントに関する情報を取得します。

   ポリシーで保護されたドキュメントに関する情報を取得するには、`RMInspectResult` オブジェクトに属する適切なメソッドを呼び出します。例えば、ポリシー名を取得するには、`RMInspectResult` オブジェクトの `getPolicyName` メソッドを呼びします。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* &quot;クイックスタート（SOAP モード）：Java API を使用した PDF 保護ポリシードキュメントの検査&quot;

### Web サービス API を使用したポリシーで保護された PDF ドキュメントの検査 {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Document Security Service API（web サービス）を使用して、ポリシーで保護された PDF ドキュメントを検査します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Document Security Client API オブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `RightsManagementServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `RightsManagementServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `RightsManagementServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `RightsManagementServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `RightsManagementServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。


1. 検査するポリシーで保護されたドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、検査する PDF ドキュメントを格納するために使用されます。
   * コンストラクターを呼び出して、`System.IO.FileStream` オブジェクトを作成します。PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することでバイト配列のサイズを決定することができます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して、バイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` フィールドにバイト配列の内容を割り当てて、`BLOB` オブジェクトに入力します。

1. ドキュメントを検査します。

   `RightsManagementServiceClient` オブジェクトの `inspectDocument` メソッドを呼び出して、ポリシーで保護されたドキュメントを検査します。ポリシーで保護された PDF ドキュメントを含む `BLOB` オブジェクトを渡します。このメソッドは、ポリシーで保護されたドキュメントに関する情報を含む `RMInspectResult` オブジェクトを返します。

1. ポリシーで保護されたドキュメントに関する情報を取得します。

   ポリシーで保護されたドキュメントに関する情報を取得するには、`RMInspectResult` オブジェクトに属する適切なフィールドの値を取得します。例えば、ポリシー名を取得するには、`RMInspectResult` オブジェクトの `policyName` フィールドの値を取得します。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用したPDF保護ドキュメントの検査»
* クイックスタート (SwaRef):Web サービス API を使用したPDF保護ドキュメントの検査»

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 透かしの作成 {#creating-watermarks}

透かしを使用すると、ドキュメントを一意に識別し、著作権侵害を制御することにより、ドキュメントのセキュリティを確保できます。例えば、機密を示す透かしを作成して、ドキュメントのすべてのページに配置できます。透かしを作成した後は、その透かしをポリシーの一部として含めることができます。つまり、新しく作成した透かしにポリシーの透かし属性を設定できます。透かしを含むポリシーがドキュメントに適用されると、その透かしはポリシーで保護されたドキュメントに表示されます。

>[!NOTE]
>
>透かしを作成できるのは、Document Security 管理者権限を持つユーザーのみです。 つまり、Document Security サービスクライアントオブジェクトの作成に必要な接続設定を定義する際には、このようなユーザーを指定する必要があります。

>[!NOTE]
>
>Document Security サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-8}

透かしを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client API オブジェクトを作成します。
1. 透かし属性を設定します。
1. 透かしを Document Security サービスに登録します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**Document Security Client API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行するには、事前に Document Security サービスのクライアントオブジェクトを作成する必要があります。Java API を使用している場合は、`RightsManagementClient` オブジェクトを作成します。Document Security web サービス API を使用している場合は、`RightsManagementServiceService` オブジェクトを作成します。

**透かし属性を設定**

新しい透かしを作成するには、透かし属性を設定する必要があります。name 属性は必ず定義する必要があります。name 属性に加えて、次の属性のうち少なくとも 1 つを設定する必要があります。

* カスタムテキスト
* DateIncluded
* UserIdIncluded
* UserNameIncluded

次のテーブルに、web サービスを使用して透かしを作成する際に必要なキーと値のペアを示します。

<table>
 <thead>
  <tr>
   <th><p>キー名</p></th>
   <th><p>説明</p></th>
   <th><p>値</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERNAME_ENABLED</code></p></td>
   <td><p>ドキュメントを開くユーザーのユーザー名が透かしの一部であるかどうかを指定します。</p></td>
   <td><p>True または False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>ドキュメントを開くユーザーの ID が透かしの一部であるかどうかを指定します。</p></td>
   <td><p>True または False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>現在の日付が透かしの一部であるかどうかを指定します。</p></td>
   <td><p>True または False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>この値が true の場合、カスタムテキストの値は <code>WaterBackCmd:SRCTEXT</code> を使用して指定する必要があります。</p></td>
   <td><p>True または False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>透かしの不透明度を指定します。指定しない場合、デフォルト値は 0.5 です。</p></td>
   <td><p>0.0 ～ 1.0 の範囲の値。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>透かしの回転を指定します。デフォルト値は 0 度です。</p></td>
   <td><p>0 ～ 359 の範囲の値。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>この値を指定した場合、<code>WaterBackCmd:IS_SIZE_ENABLED</code> が存在し、その値が true である必要があります。この属性を指定しない場合、デフォルトの動作は全体表示です。</p></td>
   <td><p>0.0 より大きく 1.0 以下の値。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>透かしの水平方向の位置揃えを指定します。 デフォルト値は中央です。</p></td>
   <td><p>左、中央または右</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>透かしの垂直方向の位置揃えを指定します。デフォルト値は中央です。</p></td>
   <td><p>上、中央、下</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>透かしが背景かどうかを指定します。デフォルト値は false です。</p></td>
   <td><p>True または False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>カスタムスケールが指定されている場合は true。この値が true の場合は、SCALE も指定する必要があります。この値が false の場合、デフォルトは全体表示です。</p></td>
   <td><p>True または False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>透かしのカスタムテキストを指定します。この値が存在する場合、<code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> も存在し、true に設定されている必要があります。</p></td>
   <td><p>True または False</p></td>
  </tr>
 </tbody>
</table>

すべての透かしには、次の属性のいずれかが定義されている必要があります。

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

その他の属性はすべてオプションです。

**透かしを登録**

新しい透かしを使用するには、その透かしを Document Security サービスに登録しておく必要があります。透かしを登録した後、その透かしをポリシー内で使用できます。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF ドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Java API を使用して透かしを作成 {#create-watermarks-using-the-java-api}

Document Security API（Java）を使用して透かしを作成します。

1. プロジェクトファイルを含めます。

   `adobe-rightsmanagement-client.jar` などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Document Security Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 透かし属性を設定

   * `InfomodelObjectFactory` オブジェクトの静的 `createWatermark` メソッドを呼び出すことによって `Watermark` オブジェクトを作成します。このメソッドは `Watermark` オブジェクトを返します。
   * `Watermark` オブジェクトの `setName` メソッドを呼び出し、ポリシー名を指定する文字列値を渡すことにより、透かしの名前属性を設定します。
   * `Watermark` オブジェクトの `setBackground` メソッドを呼び出して `true` を渡すことにより、透かしの背景属性を設定します。この属性を設定すると、透かしがドキュメントの背景に表示されます。
   * `Watermark` オブジェクトの `setCustomText` メソッドを呼び出し、透かしのテキストを表す文字列値を渡すことにより、透かしのカスタムテキスト属性を設定します。
   * `Watermark` オブジェクトの `setOpacity` メソッドを呼び出し、不透明度レベルを指定する整数値を渡すことにより、透かしの不透明度属性を設定します。100 の値は透かしが完全に不透明であることを示し、0 の値は透かしが完全に透明であることを示します。

1. 透かしを登録します。

   * `RightsManagementClient` オブジェクトの `getWatermarkManager` メソッドを呼び出すことによって `WatermarkManager` オブジェクトを作成します。このメソッドは `WatermarkManager` オブジェクトを返します。
   * `WatermarkManager` オブジェクトの `registerWatermark` メソッドを呼び出し、透かしを表す `Watermark` オブジェクトを渡して、透かしを登録します。このメソッドは、透かしの識別値を表す文字列値を返します。

**コードの例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* &quot;クイックスタート（SOAP モード）：Java API を使用した透かしの作成&quot;

### Web サービス API を使用した透かしの作成 {#create-watermarks-using-the-web-service-api}

Document Security API（web サービス）を使用して透かしを作成します。

1. Document Security Client API オブジェクトを作成します。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Document Security Client API オブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `RightsManagementServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `RightsManagementServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `RightsManagementServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `RightsManagementServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `RightsManagementServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。


1. 透かしの属性を設定します。

   * `WatermarkSpec` コンストラクターを呼び出して `WatermarkSpec` オブジェクトを作成します。
   * `WatermarkSpec` オブジェクトの `name` データメンバーに文字列値を割り当てて、透かしの名前を設定します。
   * `WatermarkSpec` オブジェクトの `id` データメンバーに文字列値を割り当てて、透かしの `id` 属性を設定します。
   * 設定する透かしプロパティごとに、個別の `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` データメンバー（たとえば、`WaterBackCmd:OPACITY)`）に値を割り当てて、キー値を設定します。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` データメンバー（たとえば、`.25`）に値を割り当てて、値を設定します。
   * `MyArrayOf_xsd_anyType` オブジェクトを作成します。各 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトに対して、`MyArrayOf_xsd_anyType` オブジェクトの `Add` メソッドを呼び出します。`MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを渡します。
   * `MyArrayOf_xsd_anyType` オブジェクトを `WatermarkSpec` オブジェクトの `values` データメンバーに割り当てます。

1. 透かしを登録します。

   `RightsManagementServiceClient` オブジェクトの `registerWatermark` メソッドを呼び出し、透かしを表す `WatermarkSpec` オブジェクトを渡して、透かしを登録します。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用した透かしの作成»
* クイックスタート (SwaRef):Web サービス API を使用した透かしの作成»

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 透かしの変更 {#modifying-watermarks}

既存の透かしは、Document Security Java API または web サービス API を使用して変更できます。既存の透かしを変更するには、その透かしを取得し、属性を変更して、サーバー上で更新します。例えば、透かしを取得し、その不透明度属性を変更する場合を考えます。変更を有効にするには、透かしを更新する必要があります。

透かしを変更すると、変更後にその透かしを適用したドキュメントに変更内容が反映されます。つまり、透かしを含む既存の PDF ドキュメントは影響を受けません。

>[!NOTE]
>
>透かしを変更できるのは、Document Security 管理者権限を持つユーザーだけです。つまり、Document Security サービスクライアントオブジェクトの作成に必要な接続設定を定義する際には、このようなユーザーを指定する必要があります。

>[!NOTE]
>
>Document Security サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-9}

透かしを変更するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Document Security Client API オブジェクトを作成します。
1. 変更する透かしを取得します。
1. 透かし属性を設定します。
1. 透かしを更新します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**Document Security Client API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行するには、事前に Document Security サービスのクライアントオブジェクトを作成する必要があります。Java API を使用している場合は、`DocumentSecurityClient` オブジェクトを作成します。Document Security web サービス API を使用している場合は、`DocumentSecurityServiceService` オブジェクトを作成します。

**変更する透かしを取得します**

透かしを変更するには、既存の透かしを取得する必要があります。名前を指定するか、識別子の値を指定し、透かしを取得することができます。

**透かし属性の設定**

既存の透かしを変更するには、1 つ以上の透かし属性の値を変更します。Web サービスを使用してプログラムで透かしを更新する場合、値が変更されなくても、元々設定されていたすべての属性を設定する必要があります。例えば、次の透かし属性が設定されているとします。`WaterBackCmd:IS_USERID_ENABLED`、`WaterBackCmd:IS_CUSTOMTEXT_ENABLED`、`WaterBackCmd:OPACITY` および `WaterBackCmd:SRCTEXT` です。変更する属性は `WaterBackCmd:OPACITY` のみですが、他の値も正常に設定する必要があります。

>[!NOTE]
>
>Java API を使用して透かしを変更する場合、すべての属性を指定する必要はありません。変更する透かし属性を設定します。

>[!NOTE]
>
>透かしの属性の名前について詳しくは、[透かしの作成](protecting-documents-policies.md#creating-watermarks)を参照してください。

**透かしの更新**

透かしの属性を変更したら、透かしを更新する必要があります。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[透かしの作成](protecting-documents-policies.md#creating-watermarks)

### Java API を使用した透かしの変更 {#modify-watermarks-using-the-java-api}

Document Security API（Java）を使用して透かしを変更します。

1. プロジェクトファイルを含めます。

   adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Document Security Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 変更する透かしを取得します。

   `DocumentSecurityClient` オブジェクトの `getWatermarkManager` メソッドを呼び出すことにより、`WatermarkManager` オブジェクトを作成し、透かしの名前を指定する文字列値を渡します。このメソッドは、変更する透かしを表す `Watermark` オブジェクトを返します。

1. 透かしの属性を設定します。

   `Watermark` オブジェクトの `setOpacity` メソッドを呼び出し、不透明度を指定する整数値を渡すことにより、透かしの不透明度属性を設定します。100 の値は透かしが完全に不透明であることを示し、0 の値は透かしが完全に透明であることを示します。

   >[!NOTE]
   >
   >次の使用例では、不透明度の属性のみを変更します。

1. 透かしを更新します。

   * `WatermarkManager` オブジェクトの `updateWatermark` メソッドを呼び出すことにより透かしを更新し、属性が変更された `Watermark` オブジェクトを渡します。

**コード例**

Document Security サービスを使用するコード例については、「クイックスタート（SOAP モード）：Java API を使用した透かしの変更」の説を参照してください。

### Web サービス API を使用した透かしの変更 {#modify-watermarks-using-the-web-service-api}

Document Security API（web サービス）を使用して透かしを変更します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Document Security Client API オブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `DocumentSecurityServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `RightsManagementServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/DocumentSecurityService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `DocumentSecurityServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `DocumentSecurityServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を `BasicHttpBindingSecurity.Security.Mode` フィールドに割り当てます。


1. 変更する透かしを取得します。

   `DocumentSecurityServiceClient` オブジェクトの `getWatermarkByName` メソッドを呼び出して、変更する透かしを取得します。透かしの名前を指定する文字列値を渡します。このメソッドは、変更する透かしを表す `WatermarkSpec` オブジェクトを返します。

1. 透かしの属性を設定します。

   * 更新する透かしプロパティごとに、個別に `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` データメンバーに値を割り当てることによって、キーの値を設定します（例：`WaterBackCmd:OPACITY)`。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` データメンバー（たとえば、`.50`）に値を割り当てて、値を設定します。
   * `MyArrayOf_xsd_anyType` オブジェクトを作成します。各 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトに対して、`MyArrayOf_xsd_anyType` オブジェクトの `Add` メソッドを呼び出します。`MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを渡します。
   * `MyArrayOf_xsd_anyType` オブジェクトを `WatermarkSpec` オブジェクトの `values` データメンバーに割り当てます。

1. 透かしを更新します。

   `DocumentSecurityServiceClient` オブジェクトの `updateWatermark` メソッドを呼び出し、変更する透かしを表す `WatermarkSpec` オブジェクトを渡すことによって、透かしを更新します。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用した透かしの変更»

## イベントの検索 {#searching-for-events}

Rights Management サービスは、ドキュメントへのポリシーの適用、ポリシーで保護されたドキュメントを開く処理、ドキュメントへのアクセス権限の失効などといった特定のアクションの発生を追跡します。Rights Management サービスに対してイベント監査を有効にする必要があります。そうしないと、イベントが追跡されません。

イベントは、次のいずれかのカテゴリに分類されます。

* 管理者イベントは、新しい管理者アカウントの作成など、管理者に関連するアクションです。
* ドキュメントイベントは、ポリシーで保護されたドキュメントを閉じるなど、ドキュメントに関連するアクションです。
* ポリシーイベントは、新しいポリシーの作成など、ポリシーに関連するアクションです。
* サービスイベントは、ユーザーディレクトリとの同期など、Rights Management サービスに関連するアクションです。

Rights Management Java API または web サービス API を使用して、特定のイベントを検索できます。イベントを検索することで、特定のイベントのログファイル作成などといったタスクを実行できます。

>[!NOTE]
>
>Rights Management サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-10}

Rights Management イベントを検索するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Rights Management Client API オブジェクトを作成します。
1. 検索するイベントを指定します。
1. イベントを検索します。

**プロジェクトファイルの組み込み**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**Rights Management Client API オブジェクトの作成**

プログラムで Rights Management サービスの操作を実行するには、Rights Management サービスのクライアントオブジェクトを作成する必要があります。Java API を使用している場合は、`DocumentSecurityClient` オブジェクトを作成します。Rights Management Web サービス API を使用している場合は、 `DocumentSecurityServiceService` オブジェクトを作成します。

**検索するイベントの指定**

検索するイベントを指定する必要があります。例えば、新しいポリシーの作成時に発生するポリシー作成イベントを検索できます。

**イベントの検索**

検索するイベントを指定した後、Rights Management Java API または Rights Management web サービス API を使用して、イベントを検索できます。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したイベントの検索 {#search-for-events-using-the-java-api}

Rights Management API（Java）を使用してイベントを検索します。

1. プロジェクトファイルを含める

   adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Rights Management クライアント API オブジェクトの作成

   コンストラクターを使用し、接続プロパティが格納される `ServiceClientFactory` オブジェクトを渡すことにより、`DocumentSecurityClient` オブジェクトを作成します。

1. 検索するイベントの指定

   * `DocumentSecurityClient` オブジェクトの `getEventManager` メソッドを呼び出すことによって `EventManager` オブジェクトを作成します。このメソッドは `EventManager` オブジェクトを返します。
   * コンストラクターを呼び出して `EventSearchFilter` オブジェクトを作成します。
   * `EventSearchFilter` オブジェクトの `setEventCode` メソッドを呼び出し、検索するイベントを表す `EventManager` クラスに属する静的データメンバーを渡すことにより、検索するイベントを指定します。例えば、ポリシー作成イベントを検索するには、`EventManager.POLICY_CREATE_EVENT` を渡します。

   >[!NOTE]
   >
   >`EventSearchFilter` オブジェクトメソッドを呼び出して、追加の検索条件を定義します。例えば、`setUserName` メソッドを呼び出して、イベントに関連付けられているユーザーを指定します。

1. イベントの検索

   `EventManager` オブジェクトの `searchForEvents` メソッドを呼び出し、イベント検索条件を定義する `EventSearchFilter` オブジェクトを渡すことにより、イベントを検索します。このメソッドは、 `Event` オブジェクトの配列を返します。

**コード例**

Rights Management サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (SOAP):Java API を使用したイベントの検索»

### Web サービス API を使用したイベントの検索 {#search-for-events-using-the-web-service-api}

Rights Management API（web サービス）を使用してイベントを検索します。

1. プロジェクトファイルを含める

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置換します。

1. Rights Management クライアント API オブジェクトの作成

   * デフォルトのコンストラクターを使用して `DocumentSecurityServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `DocumentSecurityServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `DocumentSecurityServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `DocumentSecurityServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。


1. 検索するイベントの指定

   * コンストラクターを使用して `EventSpec` オブジェクトを作成します。
   * イベントが発生した期間の開始時点を指定するには、`EventSpec` オブジェクトの `firstTime.date` データメンバーに、イベントが発生した日付範囲の開始日を表す `DataTime` インスタンスを設定します。
   * `EventSpec` オブジェクトの `firstTime.dateSpecified` データメンバーに値 `true` を割り当てます。
   * イベントが発生した期間の終了時点を指定するには、`EventSpec` オブジェクトの `lastTime.date` データメンバーに、イベントが発生した日付範囲の終了日を表す `DataTime` インスタンスを設定します。
   * `EventSpec` オブジェクトの `lastTime.dateSpecified` データメンバーに 値 `true` を割り当てます。
   * `EventSpec` オブジェクトの `eventCode` データメンバーに文字列値を割り当てて、検索するイベントを設定します。次の表に、このプロパティに割り当てることができる数値を示します。

   <table>
    <thead>
    <tr>
    <th><p>イベントタイプ</p></th>
    <th><p>値</p></th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td><p><code>ALL_EVENTS</code></p></td>
    <td><p>999</p></td>
    </tr>
    <tr>
    <td><p><code>USER_CHANGE_PASSWORD_EVENT</code></p></td>
    <td><p>1000</p></td>
    </tr>
    <tr>
    <td><p><code>USER_REGISTER_EVENT</code></p></td>
    <td><p>1001</p></td>
    </tr>
    <tr>
    <td><p><code>USER_PREREGISTER_EVENT</code></p></td>
    <td><p>1002</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACTIVATE_EVENT</code></p></td>
    <td><p>1003</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DEACTIVATE_EVENT</code></p></td>
    <td><p>1004</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_EVENT</code></p></td>
    <td><p>1005</p></td>
    </tr>
    <tr>
    <td><p><code>USER_AUTHENTICATE_DENY_EVENT </code></p></td>
    <td><p>1006</p></td>
    </tr>
    <tr>
    <td><p><code>USER_ACCOUNT_LOCK_EVENT</code></p></td>
    <td><p>1007</p></td>
    </tr>
    <tr>
    <td><p><code>USER_DELETE_EVENT </code></p></td>
    <td><p>1008</p></td>
    </tr>
    <tr>
    <td><p><code>USER_UPDATE_PROFILE_EVENT </code></p></td>
    <td><p>1009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_VIEW_EVENT </code></p></td>
    <td><p>2,000</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_LOW_EVENT </code></p></td>
    <td><p>2001</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_PRINT_HIGH_EVENT </code></p></td>
    <td><p>2002</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SIGN_EVENT </code></p></td>
    <td><p>2003</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_ADD_ANNOTATION_EVENT </code></p></td>
    <td><p>2004</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_FORM_FILL_EVENT </code></p></td>
    <td><p>2005</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CLOSE_EVENT </code></p></td>
    <td><p>2006</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_MODIFY_EVENT </code></p></td>
    <td><p>2007</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_SECURITY_HANDLER_EVENT </code></p></td>
    <td><p>2008</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SWITCH_POLICY_EVENT </code></p></td>
    <td><p>2009</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_REVOKE_EVENT </code></p></td>
    <td><p>2010</p></td>
    </tr>
    <tr>
    <td><p><code>$1</code></p></td>
    <td><p>2011</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_SECURE_EVENT </code></p></td>
    <td><p>2012</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_UNKNOWN_CLIENT_EVENT </code></p></td>
    <td><p>2013</p></td>
    </tr>
    <tr>
    <td><p><code>DOCUMENT_CHANGE_REVOKE_URL_EVENT </code></p></td>
    <td><p>2014</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_EVENT </code></p></td>
    <td><p>3000</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_ENABLE_EVENT </code></p></td>
    <td><p>3001</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DISABLE_EVENT </code></p></td>
    <td><p>3002</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CREATE_EVENT </code></p></td>
    <td><p>3003</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_DELETE_EVENT </code></p></td>
    <td><p>3004</p></td>
    </tr>
    <tr>
    <td><p><code>POLICY_CHANGE_OWNER_EVENT </code></p></td>
    <td><p>3005</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CLIENT_SYNC_EVENT </code></p></td>
    <td><p>4000</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_INFO_EVENT </code></p></td>
    <td><p>4001</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_SYNC_DIR_COMPLETE_EVENT </code></p></td>
    <td><p>4002</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_VERSION_MISMATCH_EVENT </code></p></td>
    <td><p>4003</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_CONFIG_CHANGE_EVENT </code></p></td>
    <td><p>4004</p></td>
    </tr>
    <tr>
    <td><p><code>SERVER_ENABLE_OFFLINE_ACCESS_EVENT </code></p></td>
    <td><p>4005</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ADD_EVENT </code></p></td>
    <td><p>5,000</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DELETE_EVENT </code></p></td>
    <td><p>5001</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_EDIT_EVENT </code></p></td>
    <td><p>5002</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_ACTIVATE_EVENT </code></p></td>
    <td><p>5003</p></td>
    </tr>
    <tr>
    <td><p><code>ADMIN_DEACTIVATE_EVENT </code></p></td>
    <td><p>5004</p></td>
    </tr>
    <tr>
    <td><p><code>ERROR_DIRECTORY_SERVICE_EVENT </code></p></td>
    <td><p>6000</p></td>
    </tr>
    <tr>
    <td><p><code>CREATED_POLICYSET_EVENT</code></p></td>
    <td><p>7000</p></td>
    </tr>
    <tr>
    <td><p><code>DELETED_POLICYSET_EVENT</code></p></td>
    <td><p>7001</p></td>
    </tr>
    <tr>
    <td><p><code>MODIFIED_POLICYSET_EVENT</code></p></td>
    <td><p>7002</p></td>
    </tr>
    </tbody>
    </table>

1. イベントの検索

   `DocumentSecurityServiceClient` オブジェクトの `searchForEvents` メソッドを呼び出して、検索対象のイベントと検索の最大件数を表す `EventSpec` オブジェクトを渡すことにより、イベントを検索します。このメソッドは、`MyArrayOf_xsd_anyType` のコレクション（個々の要素はそれぞれ 1 つの `AuditSpec` インスタンスに相当します）を返します。`AuditSpec` インスタンスを使用して、発生した時刻など、イベントに関する情報を取得できます。`AuditSpec` インスタンスには、この情報を指定する `timestamp` データメンバーが含まれます。

**コード例**

Rights Management サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用したイベントの検索»
* クイックスタート (SwaRef):Web サービス API を使用したイベントの検索»

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Word ドキュメントへのポリシーの適用 {#applying-policies-to-word-documents}

Rights Management サービスでは、PDF ドキュメント以外に、Microsoft Word ドキュメント（DOC ファイル）やその他の Micosoft Office ファイルフォーマットなどのドキュメント形式もサポートしています。例えば、Word のドキュメントに特定のポリシーを適用して、セキュリティで保護することができます。Word のドキュメントにポリシーを適用することにより、ドキュメントへのアクセスを制限することができます。ドキュメントを保護しているポリシーが既にある場合は、このドキュメントにポリシーを適用することはできません。

ポリシーで保護された Word ドキュメントを配布すると、そのドキュメントの使用状況を監視できます。つまり、ドキュメントが誰によって、どのように使用されているかを確認できるということです。例えば、誰かがそのドキュメントを開いた日時を知ることができます。

>[!NOTE]
>
>Document Security サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-11}

Word ドキュメントにポリシーを適用する場合は、次の手順に従ってください。

1. プロジェクトファイルを含めます。
1. Document Security Client API オブジェクトを作成します。
1. ポリシーを適用する Word ドキュメントを取得します。
1. Word ドキュメントに既存のポリシーを適用します。
1. ポリシーで保護された Word ドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**Document Security Client API オブジェクトを作成する**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成する必要があります。

**Word ドキュメントを取得する**

ポリシーを適用するには、Word ドキュメントを取得する必要があります。Word ドキュメントにポリシーを適用すると、ユーザーはそのドキュメントを使用するときに制限を受けます。例えば、ドキュメントをオフラインで開くことができないようポリシーで定められている場合、ユーザーがドキュメントを開くにはオンラインである必要があります。

**既存のポリシーを Word ドキュメントに適用する**

Word ドキュメントにポリシーを適用するには、既存のポリシーを参照し、そのポリシーが属するポリシーセットを指定する必要があります。接続プロパティを設定するユーザーは、指定したポリシーにアクセスできる必要があります。 できない場合は、例外が発生します。

**Word ドキュメントを保存する**

Document Security サービスによって Word ドキュメントにポリシーが適用されたら、ポリシーで保護された Word ドキュメントを DOC ファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ドキュメントへのアクセス権の失効](protecting-documents-policies.md#revoking-access-to-documents)

### Java API を使用して Word ドキュメントにポリシーを適用する {#apply-a-policy-to-a-word-document-using-the-java-api}

Document Security API（Java）を使用して、Word ドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Document Security Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Word ドキュメントを取得します。

   * コンストラクターを使用して Word ドキュメントの場所を指定する文字列値を渡すことによって、Word ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. Word ドキュメントに既存のポリシーを適用します。

   * `DocumentSecurityClient` オブジェクトの `getDocumentManager` メソッドを呼び出して、`DocumentManager` オブジェクトを作成します。
   * `DocumentManager` オブジェクトの `protectDocument` メソッドを呼び出して次の値を渡すことによって、Word ドキュメントにポリシーを適用します。

      * ポリシーが適用される Word ドキュメントを含む `com.adobe.idp.Document` オブジェクト。
      * ドキュメントの名前を指定する文字列値。
      * ポリシーが属しているポリシーセットの名前を表す文字列値。`null` 値を指定すると、`MyPolicies` ポリシーセットが使用されます。
      * ポリシー名を指定する文字列値。
      * ドキュメントのパブリッシャーであるユーザーのユーザーマネージャードメインの名前を表す文字列値。このパラメーターの値はオプションであり、null にすることができます（このパラメーターが null の場合、次のパラメーターの値も null にする必要があります）。
      * ドキュメントのパブリッシャーであるユーザーマネージャーユーザーの正規名の名前を表す文字列値。このパラメーター値はオプションであり、 `null` にすることができます（このパラメーターが `null` の場合、前のパラメーター値も `null` である必要があります）。
      * MS Office テンプレートの選択に使用されるロケールを表す `com.adobe.livecycle.rightsmanagement.Locale`。このパラメーター値はオプションであり、`null` を指定できます。

      `protectDocument` メソッドは、ポリシーで保護された Word ドキュメントを含む `RMSecureDocumentResult` オブジェクトを返します。


1. Word ドキュメントを保存します。

   * `RMSecureDocumentResult` オブジェクトの `getProtectedDoc` メソッドを呼び出して、ポリシーで保護された Word ドキュメントを取得します。このメソッドは `com.adobe.idp.Document` オブジェクトを返します。
   * `java.io.File` オブジェクトを作成し、ファイル拡張子が DOC であることを確認します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、`Document` オブジェクトの内容をファイルにコピーします（`getProtectedDoc` メソッドが返した `Document` オブジェクトを使用してください）。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAP モード）:Java API を使用して Word ドキュメントにポリシーを適用する»

### Web サービス API を使用して Word ドキュメントにポリシーを適用する {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Document Security API（web サービス）を使用して、Word ドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Document Security Client API オブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `DocumentSecurityServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `DocumentSecurityServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/DocumentSecurityService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `DocumentSecurityServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `DocumentSecurityServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を `BasicHttpBindingSecurity.Security.Mode` フィールドに割り当てます。


1. Word ドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、ポリシーが適用される Word ドキュメントを格納するために使用されます。
   * コンストラクターを呼び出し、Word ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクトの `Length` プロパティを取得してバイト配列を決定します。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出してバイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` フィールドにバイト配列の内容を割り当てて、`BLOB` オブジェクトにデータを入力します。

1. Word ドキュメントに既存のポリシーを適用します。

   `DocumentSecurityServiceClient` オブジェクトの `protectDocument` メソッドを呼び出して、次の値を渡すことにより、Word ドキュメントにポリシーを適用します。

   * ポリシーが適用される Word ドキュメントを含む `BLOB` オブジェクト。
   * ドキュメントの名前を指定する文字列値。
   * ポリシーが属しているポリシーセットの名前を表す文字列値。`null` 値を指定すると、`MyPolicies` ポリシーセットが使用されます。
   * ポリシー名を指定する文字列値。
   * ドキュメントのパブリッシャーであるユーザーのユーザーマネージャードメインの名前を表す文字列値。このパラメーター値はオプションであり、null にすることができます（このパラメーターが null の場合、次のパラメーター値は `null` である必要があります）。
   * ドキュメントのパブリッシャーであるユーザーマネージャーユーザーの正規名の名前を表す文字列値。このパラメーター値はオプションであり、null にすることができます（このパラメーターが null の場合、前のパラメーター値は `null` である必要があります）。
   * ロケール値を指定する `RMLocale` 値（例： `RMLocale.en`）。
   * ポリシー識別子の値を格納するために使用される文字列出力パラメーター。
   * ポリシーで保護された識別子の値を保存するために使用される文字列出力パラメーター。
   * MIME タイプを格納するのに使用する文字列出力パラメーター（例えば、`application/doc`）。

   `protectDocument` メソッドは、ポリシーで保護された Word ドキュメントを含む `BLOB` オブジェクトを返します。

1. Word ドキュメントを保存します。

   * コンストラクターを呼び出し、ポリシーで保護された Word ドキュメントファイルの場所を表す 文字列値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * `protectDocument` メソッドによって返された `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` データメンバーの値を取得して、バイト配列を生成します。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出してバイト配列を渡すことにより、バイト配列の内容を Word ファイルに書き込みます。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用して Word ドキュメントにポリシーを適用する

## Word ドキュメントからのポリシーの削除 {#removing-policies-from-word-documents}

ポリシーで保護された Word ドキュメントからポリシーを削除して、ドキュメントからセキュリティを削除することができます。つまり、ドキュメントをポリシーで保護したくない場合です。ポリシーで保護された Word ドキュメントを新しいポリシーで更新する場合は、ポリシーを削除して更新したポリシーを追加するのではなく、ポリシーを切り替える方が効率的です。

>[!NOTE]
>
>Document Security サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-12}

ポリシーで保護された Word ドキュメントからポリシーを削除するには、次の手順を実行します。

1. プロジェクトファイルを含める
1. Document Security Client API オブジェクトを作成します。
1. ポリシーで保護された Word ドキュメントを取得します。
1. Word ドキュメントからポリシーを削除します。
1. 保護されていない Word ドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**ドキュメントセキュリティクライアント API オブジェクトを作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成します。

**ポリシーで保護された Word ドキュメントを取得**

ポリシーを削除するには、ポリシーで保護された Word ドキュメントを取得する必要があります。ポリシーで保護されていない Word ドキュメントからポリシーを削除しようとすると、例外が発生します。

**Word ドキュメントからポリシーを削除**

接続設定で管理者が指定されている場合は、ポリシーで保護された Word ドキュメントからポリシーを削除できます。そうでない場合、Word ドキュメントからポリシーを削除するには、ドキュメントの保護に使用するポリシーに `SWITCH_POLICY` 権限が含まれている必要があります。また、AEM Forms 接続設定で指定したユーザーにも、その権限が必要です。それ以外の場合は、例外がスローされます。

**保護されていない Word ドキュメントを保存**

Document Security サービスで Word ドキュメントからポリシーを削除した後、保護されていない Word ドキュメントを DOC ファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Word ドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-word-documents)

### Java API を使用して Word ドキュメントからポリシーを削除 {#remove-a-policy-from-a-word-document-using-the-java-api}

Document Security API（Java） を使用して、ポリシーで保護された Word ドキュメントからポリシーを削除します。

1. プロジェクトファイルを含める

   adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Document Security Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護された Word ドキュメントの取得

   * コンストラクターを使用して、Word ドキュメントの場所を指定する文字列値を渡すことにより、ポリシーで保護された Word ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. Word ドキュメントからポリシーを削除する

   * `RightsManagementClient` オブジェクトの `getDocumentManager` メソッドを呼び出すことによって、`DocumentManager` オブジェクトを作成します。
   * `DocumentManager` オブジェクトの `removeSecurity` メソッドを呼び出し、ポリシーで保護された Word ドキュメントを含む `com.adobe.idp.Document` オブジェクトを渡すことにより、Word ドキュメントからポリシーを削除します。このメソッドは、セキュリティで保護されていない Word ドキュメントを含む `com.adobe.idp.Document` オブジェクトを返します。

1. 保護されていない Word ドキュメントを保存する

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が DOC であることを確認します。
   * `Document` オブジェクトの `copyToFile` メソッドを呼び出して、`Document` オブジェクトの内容をファイルにコピーします（`removeSecurity` メソッドが返した `Document` オブジェクトを使用してください）。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* &quot;クイックスタート（SOAP モード）：Java API を使用した Word ドキュメントからのポリシーの削除 &quot;

### Web サービス API を使用して Word ドキュメントからポリシーを削除 {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Document Security API（web サービス）を使用して、ポリシーで保護された Word ドキュメントからポリシーを削除します。

1. プロジェクトファイルを含める

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置換します。

1. Document Security Client API オブジェクトの作成

   * デフォルトのコンストラクターを使用して `RightsManagementServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `RightsManagementServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `RightsManagementServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `RightsManagementServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `RightsManagementServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。


1. ポリシーで保護された Word ドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、ポリシーの削除対象となる、ポリシーで保護された Word ドキュメントを保存するために使用されます。
   * コンストラクターを呼び出し、Word ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡して `System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * `MTOM` フィールドを割り当てて `BLOB` オブジェクトにバイト配列の内容を入力します。

1. Word ドキュメントからポリシーを削除する

   `RightsManagementServiceClient` オブジェクトの `removePolicySecurity` メソッドを呼び出して、ポリシーで保護された Word ドキュメントを含む `BLOB` オブジェクトを渡すことにより、Word ドキュメントからポリシーを削除します。このメソッドは、 保護されていない Word ドキュメントを含む `BLOB` オブジェクトを返します。

1. 保護されていない Word ドキュメントを保存する

   * コンストラクターを呼び出し、保護されていない Word ドキュメントを含むファイルの場所を表す文字列値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * `removePolicySecurity` メソッドで返された `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` フィールドの値を取得してバイト配列を入力します。
   * コンストラクターを呼び出し、`System.IO.FileStream` オブジェクトを渡すことにより、`System.IO.BinaryWriter` オブジェクトを作成します。

**コードの例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用した Word ドキュメントからのポリシーの削除»

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
