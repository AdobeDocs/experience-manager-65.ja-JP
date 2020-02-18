---
title: ポリシーを使用したドキュメントの保護
seo-title: ポリシーを使用したドキュメントの保護
description: 'null'
seo-description: 'null'
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# ポリシーを使用したドキュメントの保護 {#protecting-documents-with-policies}

**Document Securityサービスについて**

Document Securityサービスを使用すると、ユーザーはAdobe PDFドキュメントに動的に機密設定を適用し、ドキュメントの配布範囲に関係なく、ドキュメントの制御を維持できます。

Document Securityサービスは、ポリシーで保護されたPDFドキュメントを受信者がどのように使用するかをユーザーが制御できるようにすることで、ユーザーの手の届く範囲を超えて情報が広がるのを防ぎます。 ユーザーは、ドキュメントを開くことのできるユーザーを指定し、ドキュメントの使用方法を制限し、ドキュメントの配布後にドキュメントを監視できます。 また、ユーザーは、ポリシーで保護されたドキュメントへのアクセスを動的に制御し、ドキュメントへのアクセスを動的に取り消すこともできます。

また、Document Securityサービスは、Microsoft wordファイル（DOCファイル）など、他のファイルタイプも保護します。 Document Security Client APIを使用して、これらのファイルタイプを操作できます。 次のバージョンがサポートされています。

* Microsoft Office 2003ファイル（DOC、XLS、PPTファイル）
* Microsoft Office 2007ファイル（DOCX、XLSX、PPTXファイル）
* PTC Pro/Eファイル

Wordドキュメントの使い方を明確にするために、次の2つの節で説明します。

* [Wordドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Wordドキュメントからのポリシーの削除](protecting-documents-policies.md#removing-policies-from-word-documents)

Document Securityサービスを使用して、次のタスクを実行できます。

* ポリシーの作成. 詳しくは、「ポリシーの作成」 [を参照してください](protecting-documents-policies.md#creating-policies)。
* ポリシーを変更します。 詳しくは、「ポリシーの変更」 [を参照してくださ](protecting-documents-policies.md#modifying-policies)い。
* ポリシーを削除します。 詳しくは、「ポリシーの削除」 [を参照してください](protecting-documents-policies.md#deleting-policies)。
* PDFドキュメントへのポリシーの適用を参照してください。 詳しくは、「PDFドキュメントへ [のポリシーの適用」を参照してくださ](protecting-documents-policies.md#applying-policies-to-pdf-documents)い。
* PDFドキュメントからのポリシーの削除 詳しくは、「PDFドキュメントか [らのポリシーの削除」を参照してくださ](protecting-documents-policies.md#removing-policies-from-pdf-documents)い。
* ポリシーで保護されたドキュメントの検査。 詳しくは、ポリシーで保護さ [れたPDFドキュメントの検査を参照してください](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents)。
* PDFドキュメントへのアクセス権限の失効 詳しくは、「ドキュメントへのア [クセス権限の失効」を参照してくださ](protecting-documents-policies.md#revoking-access-to-documents)い。
* 失効したドキュメントへのアクセス権の復元。 詳しくは、失効したドキュメ [ントへのアクセス権限の復元を参照してくださ](protecting-documents-policies.md#reinstating-access-to-revoked-documents)い。
* 透かしを作成します。 詳しくは、「透かしの作成」 [を参照してください](protecting-documents-policies.md#creating-watermarks)。
* イベントを検索します。 詳しくは、「イベントの [検索」を参照してください](protecting-documents-policies.md#searching-for-events)。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## ポリシーの作成 {#creating-policies}

Document Security Java APIまたはWebサービスAPIを使用して、プログラムによってポリシーを作成できます。 ポリ *シーは* 、Document Securityの設定、許可されたユーザー、使用権限などの情報の集まりです。 様々な状況やユーザーに適したセキュリティ設定を使用して、任意の数のポリシーを作成および保存できます。

ポリシーを使用すると、次のタスクを実行できます。

* ドキュメントを開くことができるユーザーを指定します。 受信者は、組織に属するか、組織外に属することができます。
* 受信者がドキュメントを使用する方法を指定します。 AcrobatとAdobe readerの様々な機能へのアクセスを制限できます。 これらの機能には、テキストの印刷とコピー、署名の追加、ドキュメントへのコメントの追加が含まれます。
* ポリシーで保護されたドキュメントを配布した後でも、いつでもアクセスとセキュリティの設定を変更できます。
* ドキュメントを配布した後、ドキュメントの使用を監視します。 ドキュメントの使用方法と使用者を確認できます。 例えば、誰かがドキュメントを開いたタイミングを調べることができます。

### Webサービスを使用したポリシーの作成 {#creating-a-policy-using-web-services}

WebサービスAPIを使用してポリシーを作成する場合は、そのポリシーを記述した既存のPortable Document Rights Language(PDRL)XMLファイルを参照します。 ポリシー権限とプリンシパルは、PDRLドキュメントで定義されます。 次のXMLドキュメントは、PDRLドキュメントの例です。

```as3
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
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

ポリシーを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client APIオブジェクトを作成します。
1. ポリシーの属性を設定します。
1. ポリシーエントリを作成します。
1. ポリシーを登録します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-rightsmanagement-client.jar
* namespace.jar （AEM formsがJBossにデプロイされている場合）
* jaxb-api.jar（AEM formsがJBossにデプロイされている場合）
* jaxb-impl.jar（AEM FormsがJBossにデプロイされている場合）
* jaxb-libs.jar（AEM formsがJBossにデプロイされている場合）
* jaxb-xjc.jar（JBossにAEM formsがデプロイされている場合）
* relaxingDatatype.jar（AEM FormsがJBossにデプロイされている場合）
* xsdlib.jar（AEM FormsがJBossにデプロイされている場合）
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar（AEM formsがJBossにデプロイされていない場合は、別のJARファイルを使用）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Document Security Client APIオブジェクトの作成**

プログラムを使用してDocument Securityサービスの操作を実行する前に、Document Securityサービスクライアントオブジェクトを作成します。

**ポリシーの属性の設定**

ポリシーを作成するには、ポリシー属性を設定します。 必須属性はポリシー名です。 ポリシー名は、各ポリシーセットに対して一意である必要があります。 ポリシーセットは、単なるポリシーの集まりです。 ポリシーが別々のポリシーセットに属する場合は、同じ名前の2つのポリシーを使用できます。 ただし、1つのポリシーセット内の2つのポリシーに同じポリシー名を付けることはできません。

設定するもう1つの便利な属性は、有効期間です。 有効期間とは、ポリシーで保護されたドキュメントが許可された受信者にアクセスできる期間です。 この属性を設定しない場合、ポリシーは常に有効です。

有効期間は、次のいずれかのオプションに設定できます。

* ドキュメントが発行された時点からドキュメントにアクセスできる日数
* ドキュメントにアクセスできない終了日
* ドキュメントにアクセスできる特定の日付範囲
* 常に有効

開始日のみを指定できます。これにより、ポリシーは開始日より後に有効になります。 終了日のみを指定した場合、ポリシーは終了日まで有効です。 ただし、開始日と終了日の両方が定義されていない場合は例外がスローされます。

ポリシーに属する属性を設定する場合は、暗号化の設定も指定できます。 これらの暗号化設定は、ポリシーがドキュメントに適用される場合に有効になります。 次の暗号化値を指定できます。

* **AES256**:256ビットキーを持つAES暗号化アルゴリズムを表します。
* **AES128**:128ビットキーを持つAES暗号化アルゴリズムを表します。
* **** NoEncryption:暗号化なしを表します。

このオプションを `NoEncryption` 指定する場合、このオプションをに設定するこ `PlaintextMetadata` とはできま `false`せん。 これを行うと、例外が発生します。

>[!NOTE]
>
>設定可能なその他の属性について詳しくは、『 `Policy` AEM Forms APIリファレンス』のインターフェ [イスの説明を参照し](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)てください。

**ポリシーエントリの作成**

ポリシーエントリは、プリンシパル（グループとユーザー、権限）をポリシーに添付します。 ポリシーには少なくとも1つのポリシーエントリが必要です。 例えば、次のタスクを実行するとします。

* ポリシーエントリを作成して登録します。このエントリを使用すると、グループはオンライン時にドキュメントのみを表示でき、受信者はドキュメントをコピーできなくなります。
* ポリシーエントリをポリシーに添付します。
* Acrobatを使用して、ポリシーでドキュメントを保護します。

これらの操作により、受信者はドキュメントをオンラインでのみ表示でき、コピーできなくなります。 ドキュメントからセキュリティが削除されるまで、ドキュメントはセキュリティ保護された状態のままです。

**ポリシーの登録**

新しいポリシーを使用するには、そのポリシーを登録する必要があります。 登録したポリシーは、ドキュメントの保護に使用できます。

### Java APIを使用したポリシーの作成 {#create-a-policy-using-the-java-api}

Document Security API(Java)を使用してポリシーを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. Document Security Client APIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーの属性を設定します。

   * オブジェクト `Policy` の静的メソッドを呼び出し `InfomodelObjectFactory` て、オブジェクトを作成 `createPolicy` します。 このメソッドは、オブジェクトを `Policy` 返します。
   * オブジェクトのメソッドを呼び出し、ポリシー名を `Policy` 指定する文字 `setName` 列値を渡して、ポリシーのname属性を設定します。
   * オブジェクトのメソッドを呼び出し、ポリシ `Policy` ーの説明を指 `setDescription` 定する文字列値を渡して、ポリシーの説明を設定します。
   * オブジェクトのメソッドを呼び出し、ポリシーセット名を指 `Policy` 定する文字列値を `setPolicySetName` 渡して、新しいポリシーが属するポリシーセットを設定します。 (このパラメーター `null` 値を指定すると、ポリシーが「 *My Policies* 」ポリシーセットに追加されます)。
   * オブジェクトの静的メソッドを呼び出して、ポリシ `InfomodelObjectFactory` ーの有効期間を作成 `createValidityPeriod` します。 このメソッドは、オブジェクトを `ValidityPeriod` 返します。
   * ポリシーで保護されたドキュメントにアクセスする日数を設定するには、オブジェクトのメソッドを呼び出し、 `ValidityPeriod` 日数を `setRelativeExpirationDays` 指定する整数値を渡します。
   * オブジェクトのメソッドを呼び出し、オブジェクトを渡すこ `Policy` とで、ポリシー `setValidityPeriod` の有効期間を設定 `ValidityPeriod` します。

1. ポリシーエントリを作成します。

   * オブジェクトの静的メソッドを呼び出して、 `InfomodelObjectFactory` ポリシーエントリを作成 `createPolicyEntry` します。 このメソッドは、オブジェクトを `PolicyEntry` 返します。
   * オブジェクトの静的メソッドを呼び出して、ポリ `InfomodelObjectFactory` シーの権限を指定 `createPermission` します。 権限を表すインターフェイスに属する静的デ `Permission` ータメンバーを渡します。 このメソッドは、オブジェクトを `Permission` 返します。 例えば、ポリシーで保護されたPDFドキュメントからユーザーがデータをコピーできる権限を追加するには、を渡しま `Permission.COPY`す。 （追加する権限ごとに、この手順を繰り返します）。
   * オブジェクトのメソッドを呼び出し、オブジェクトを渡すこ `PolicyEntry` とで、ポリシーエン `addPermission` トリに権限を追加 `Permission` します。 (作成した各オブジェクトに対し `Permission` てこの手順を繰り返します)。
   * オブジェクトの静的メソッドを呼び出して、 `InfomodelObjectFactory` ポリシープリンシパルを作成 `createSpecialPrincipal` します。 プリンシパルを表すオブジェクトに属するデ `InfomodelObjectFactory` ータメンバーを渡します。 このメソッドは、オブジェクトを `Principal` 返します。 例えば、ドキュメントの発行者をプリンシパルとして追加するには、を渡しま `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`す。
   * オブジェクトのメソッドを呼び出し、オブジェクトを渡すこ `PolicyEntry` とで、プリンシパル `setPrincipal`をポリシーエントリに追加 `Principal` します。
   * オブジェクトのメソッドを呼び出し、オブジェクトを渡すこ `Policy` とで、ポリシー `addPolicyEntry` エントリをポリシーに追加 `PolicyEntry` します。

1. ポリシーを登録します。

   * オブジェクト `PolicyManager` のメソッドを呼び出して、オ `DocumentSecurityClient` ブジェクトを作成 `getPolicyManager` します。
   * オブジェクトのメソッドを呼び出し、次 `PolicyManager` の値を渡し `registerPolicy` て、ポリシーを登録します。

      * 登録す `Policy` るポリシーを表すオブジェクトです。
   * ポリシーが属するポリシーセットを表すstring値です。
   接続設定内でAEM forms管理者アカウントを使用してオブジェクトを作成する場 `DocumentSecurityClient` 合は、メソッドの呼び出し時にポリシーセット名を指定 `registerPolicy` します。 ポリシーセットの値 `null` を渡すと、そのポリシーは管理者の「マイポリシー」ポリシーセットに *作成されます* 。

   接続設定内でDocument Securityユーザーを使用する場合は、ポリシーのみを受け入れるオーバーロードさ `registerPolicy` れたメソッドを呼び出すことができます。 つまり、ポリシーセット名を指定する必要はありません。 ただし、このポリシーは「マイポリシー」という名前のポリシーセットに追 *加されます*。 このポリシーセットに新しいポリシーを追加しない場合は、メソッドの呼び出し時にポリシーセット名を指定し `registerPolicy` ます。

   >[!NOTE]
   >
   >ポリシーを作成する場合は、既存のポリシーセットを参照します。 存在しないポリシーセットを指定した場合は、例外が発生します。

Document Securityサービスを使用するコードの例については、次を参照してください。

* 「クイックスタート（SOAPモード）:Java APIを使用したポリシーの作成」

### WebサービスAPIを使用したポリシーの作成 {#create-a-policy-using-the-web-service-api}

Document Security API（Webサービス）を使用してポリシーを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Document Security Client APIオブジェクトを作成します。

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/RightsManagementService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `RightsManagementServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `RightsManagementServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `RightsManagementServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。


1. ポリシーの属性を設定します。

   * コンストラクタを使用して `PolicySpec` オブジェクトを作成します。
   * オブジェクトのデータメンバーに文字列値を割り当てて、ポリシー `PolicySpec` の名前を設 `name` 定します。
   * オブジェクトのデータメンバーに文字列値を割り当てて、ポリシー `PolicySpec` の説明を設 `description` 定します。
   * オブジェクトのデータメンバーに文字列値を割り当てて、ポリシーが属するポリシーセ `PolicySpec` ットを設 `policySetName` 定します。 既存のポリシーセット名を指定する必要があります。 (このパラメーター `null` 値を指定すると、ポリシーが「マイポリシー」に追加 *されます*。)
   * オブジェクトのデータメンバーに整数値を割り当てて、ポリシーのオフラインリ `PolicySpec` ース期間を `offlineLeasePeriod` 設定します。
   * PDRL XMLデータ `PolicySpec` を表すstring値を使 `policyXml` 用して、オブジェクトのデータメンバーを設定します。 このタスクを実行するには、コンストラクターを使用し `StreamReader` て.NETオブジェクトを作成します。 ポリシーを表すPDRL XMLファイルの場所をコンストラクターに渡し `StreamReader` ます。 次に、オブジェクト `StreamReader` のメソッドを呼 `ReadLine` び出し、戻り値を文字列変数に割り当てます。 メソッドがnullを返す `StreamReader` まで、オブジェクト `ReadLine` を繰り返し処理します。 文字列変数をオブジェクトのデー `PolicySpec` タメンバーに割り `policyXml` 当てます。

1. ポリシーエントリを作成します。

   Document Security webサービスAPIを使用してポリシーを作成する場合は、ポリシーエントリを作成する必要はありません。 ポリシーエントリはPDRLドキュメントで定義されています。

1. ポリシーを登録します。

   オブジェクトのメソッドを呼び出し、次 `DocumentSecurityServiceClient` の値を渡し `registerPolicy` て、ポリシーを登録します。

   * 登録す `PolicySpec` るポリシーを表すオブジェクトです。
   * ポリシーが属するポリシーセットを表すstring値です。 MyPolicesポリシーセット `null` にポリシーを追加する値を指 *定でき* ます。
   接続設定内でAEM forms管理者アカウントを使用してオブジェクトを作成する場合は、 `DocumentSecurityClient` メソッドの呼び出し時にポリシーセット名を指定 `registerPolicy` します。

   接続設定内でDocument Security Document Securityユーザーを使用する場合は、ポリシーのみを受け入れるオーバーロー `registerPolicy` ドされたメソッドを呼び出すことができます。 つまり、ポリシーセット名を指定する必要はありません。 ただし、このポリシーは「マイポリシー」という名前のポリシーセットに追 *加されます*。 このポリシーセットに新しいポリシーを追加しない場合は、メソッドの呼び出し時にポリシーセット名を指定し `registerPolicy` ます。

   >[!NOTE]
   >
   >ポリシーを作成し、ポリシーセットを指定する場合は、既存のポリシーセットを必ず指定してください。 存在しないポリシーセットを指定した場合は、例外が発生します。

Document Securityサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「Quick Start(MTOM):WebサービスAPIを使用したポリシーの作成」
* &quot;クイックスタート(SwaRef):WebサービスAPIを使用したポリシーの作成」

## ポリシーの変更 {#modifying-policies}

Document Security Java APIまたはWebサービスAPIを使用して、既存のポリシーを変更できます。 既存のポリシーを変更するには、そのポリシーを取得し、変更してから、サーバー上のポリシーを更新します。 例えば、既存のポリシーを取得し、その有効期間を延長したとします。 変更を有効にする前に、ポリシーを更新する必要があります。

ビジネス要件が変更され、ポリシーにこれらの要件が反映されなくなった場合は、ポリシーを変更できます。 新しいポリシーを作成する代わりに、既存のポリシーを更新するだけで済みます。

Webサービスを使用してポリシー属性を変更する（例えば、JAX-WSで作成されたJavaプロキシクラスを使用する）には、ポリシーがDocument Securityサービスに登録されていることを確認する必要があります。 その後、メソッドを使用して既存のポリシーを参照し、適 `PolicySpec.getPolicyXml` 切なメソッドを使用してポリシー属性を変更できます。 例えば、メソッドを呼び出して、オフラインリース期間を変更で `PolicySpec.setOfflineLeasePeriod` きます。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

既存のポリシーを変更するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client APIオブジェクトを作成します。
1. 既存のポリシーを取得します。
1. ポリシー属性を変更します。
1. ポリシーを更新します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Document Security Client APIオブジェクトの作成**

Document Securityサービスの操作をプログラムで実行する前に、Document Securityサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `RightsManagementClient` ます。 Document Security webサービスAPIを使用している場合は、オブジェクトを作成し `RightsManagementServiceService` ます。

**既存のポリシーの取得**

既存のポリシーを変更するには、そのポリシーを取得する必要があります。 ポリシーを取得するには、ポリシー名とポリシーが属するポリシーセットを指定します。 ポリシーセット名の `null` 値を指定した場合、ポリシーは「 *My Policies* 」ポリシーセットから取得されます。

**ポリシーの属性の設定**

ポリシーを変更するには、ポリシー属性の値を変更します。 変更できない唯一のポリシー属性はname属性です。 例えば、ポリシーのオフラインリース期間を変更するには、ポリシーのオフラインリース期間属性の値を変更します。

Webサービスを使用してポリシーのオフラインリース期間を変更する場合、インターフェイス上 `offlineLeasePeriod` のフィールド `PolicySpec` は無視されます。 オフラインリース期間を更新するには、PDRL XMLドキュメ `OfflineLeasePeriod` ント内の要素を変更します。 次に、インターフェイスのデータメンバーを使用して、更新されたPDRL XML `PolicySpec` ドキュメント `policyXML` を参照します。

>[!NOTE]
>
>設定可能なその他の属性について詳しくは、『 `Policy` AEM Forms APIリファレンス』のインターフェ [イスの説明を参照し](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)てください。

**ポリシーの更新**

ポリシーに対して行った変更を有効にする前に、Document Securityサービスでポリシーを更新する必要があります。 ドキュメントを保護するポリシーに対する変更は、次にポリシーで保護されたドキュメントがDocument Securityサービスと同期されたときに更新されます。

### Java APIを使用した既存のポリシーの変更 {#modify-existing-policies-using-the-java-api}

Document Security API(Java)を使用して既存のポリシーを変更します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. Document Security Client APIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 既存のポリシーを取得します。

   * オブジェクト `PolicyManager` のメソッドを呼び出して、オ `RightsManagementClient` ブジェクトを作成 `getPolicyManager` します。
   * オブジェクト `Policy` のメソッドを呼び出し、次の値を渡すことで、更新するポリ `PolicyManager` シーを表 `getPolicy` すオブジェクトを作成します。」

      * ポリシーが属するポリシーセット名を表すstring値です。 ポリシーセット `null` を使用する結果を指 `MyPolicies` 定することができます。
      * ポリシー名を表すstring値です。

1. ポリシーの属性を設定します。

   ビジネス要件に合わせてポリシーの属性を変更します。 例えば、ポリシーのオフラインリース期間を変更するには、オブジェクトのメソ `Policy` ッドを呼び出 `setOfflineLeasePeriod` します。

1. ポリシーを更新します。

   オブジェクトのメソッドを呼び出し `PolicyManager` てポリシーを更新 `updatePolicy` します。 更新するポ `Policy` リシーを表すオブジェクトを渡します。

**コードの例**

Document Securityサービスを使用するコードの例については、クイックスタート（SOAPモード）を参照してください。「Java API」セクションを使用したポリシーの変更

### WebサービスAPIを使用して既存のポリシーを変更する {#modify-existing-policies-using-the-web-service-api}

Document Security API（Webサービス）を使用して既存のポリシーを変更します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Document Security Client APIオブジェクトを作成します。

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/RightsManagementService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `RightsManagementServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `RightsManagementServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `RightsManagementServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。


1. 既存のポリシーを取得します。

   オブジェクト `PolicySpec` のメソッドを呼び出し、次の値を渡すことで、変更するポリ `RightsManagementServiceClient` シーを表 `getPolicy` すオブジェクトを作成します。

   * ポリシーが属するポリシーセット名を指定するstring値です。 ポリシーセット `null` を使用する結果を指 `MyPolicies` 定することができます。
   * ポリシーの名前を指定するstring値です。

1. ポリシーの属性を設定します。

   ビジネス要件に合わせてポリシーの属性を変更します。

1. ポリシーを更新します。

   オブジェクトのメソッドを呼び出し、更 `RightsManagementServiceClient` 新するポリ `updatePolicyFromSDK` シーを表すオ `PolicySpec` ブジェクトを渡して、ポリシーを更新します。

**コードの例**

Document Securityサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「Quick Start(MTOM):WebサービスAPIを使用したポリシーの変更」
* &quot;クイックスタート(SwaRef):WebサービスAPIを使用したポリシーの変更」

## ポリシーの削除 {#deleting-policies}

既存のポリシーは、Document Security Java APIまたはWebサービスAPIを使用して削除できます。 ポリシーを削除すると、ドキュメントの保護にポリシーを使用できなくなります。 ただし、ポリシーを使用している既存のポリシーで保護されたドキュメントは、引き続き保護されます。 新しいポリシーが利用可能になった場合は、ポリシーを削除できます。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

既存のポリシーを削除するには、次の手順を実行します。

1. プロジェクトファイルを含める
1. Document Security Client APIオブジェクトを作成します。
1. ポリシーを削除します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Document Security Client APIオブジェクトの作成**

Document Securityサービスの操作をプログラムで実行する前に、Document Securityサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `RightsManagementClient` ます。 Document Security webサービスAPIを使用している場合は、オブジェクトを作成し `RightsManagementServiceService` ます。

**ポリシーの削除**

ポリシーを削除するには、削除するポリシーと、そのポリシーが属するポリシーセットを指定します。 AEM Formsの呼び出しに使用される設定を持つユーザーは、ポリシーを削除する権限を持っている必要があります。それ以外の場合は例外が発生します。 同様に、存在しないポリシーを削除しようとすると、例外が発生します。

### Java APIを使用したポリシーの削除 {#delete-policies-using-the-java-api}

Document Security API(Java)を使用してポリシーを削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. Document Security Client APIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーを削除します。

   * オブジェクト `PolicyManager` のメソッドを呼び出して、オ `RightsManagementClient` ブジェクトを作成 `getPolicyManager` します。
   * オブジェクトのメソッドを呼び出し、次 `PolicyManager` の値を渡し `deletePolicy` て、ポリシーを削除します。

      * ポリシーが属するポリシーセット名を指定するstring値です。 ポリシーセット `null` を使用する結果を指 `MyPolicies` 定することができます。
      * 削除するポリシーの名前を指定するstring値です。

**コードの例**

Document Securityサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAPモード）:Java APIを使用したポリシーの削除」

### WebサービスAPIを使用したポリシーの削除 {#delete-policies-using-the-web-service-api}

Document Security API（Webサービス）を使用してポリシーを削除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Document Security Client APIオブジェクトを作成します。

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/RightsManagementService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `RightsManagementServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `RightsManagementServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `RightsManagementServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。


1. ポリシーを削除します。

   Delete a policy by invoking the `RightsManagementServiceClient` object’s `deletePolicy` method and passing the following values:

   * ポリシーが属するポリシーセット名を指定するstring値です。 ポリシーセット `null` を使用する結果を指 `MyPolicies` 定することができます。
   * 削除するポリシーの名前を指定するstring値です。

**コードの例**

Document Securityサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「Quick Start(MTOM):WebサービスAPIを使用したポリシーの削除
* &quot;クイックスタート(SwaRef):WebサービスAPIを使用したポリシーの削除

## PDFドキュメントへのポリシーの適用 {#applying-policies-to-pdf-documents}

ドキュメントを保護するために、PDFドキュメントにポリシーを適用できます。 PDFドキュメントにポリシーを適用すると、ドキュメントへのアクセスを制限できます。 ドキュメントが既にポリシーで保護されている場合は、ドキュメントにポリシーを適用できません。

ドキュメントを開いている間は、テキストの印刷とコピー、変更、ドキュメントへの署名とコメントの追加など、AcrobatおよびAdobe Readerの機能へのアクセスを制限することもできます。 また、ポリシーで保護されたPDFドキュメントは、ユーザーがドキュメントにアクセスできなくなった場合に失効させることもできます。

ポリシーで保護されたドキュメントを配布した後で、その使用を監視できます。 つまり、ドキュメントの使用方法と使用者を確認できます。 例えば、誰かがドキュメントを開いたタイミングを調べることができます。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-3}

PDFドキュメントにポリシーを適用するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client APIオブジェクトを作成します。
1. ポリシーが適用されるPDFドキュメントを取得します。
1. PDFドキュメントに既存のポリシーを適用します。
1. ポリシーで保護されたPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Document Security Client APIオブジェクトの作成**

プログラムを使用してDocument Securityサービスの操作を実行する前に、Document Securityサービスクライアントオブジェクトを作成します。 Java APIを使用している場合は、オブジェクトを作成し `DocumentSecurityClient` ます。 Document Security webサービスAPIを使用している場合は、オブジェクトを作成し `DocumentSecurityServiceService` ます。

**PDFドキュメントの取得**

PDFドキュメントを取得してポリシーを適用できます。 PDFドキュメントにポリシーを適用すると、ドキュメントの使用時にユーザーが制限されます。 例えば、オフライン時にドキュメントを開くことをポリシーで有効にしていない場合、ドキュメントを開くにはユーザーがオンラインになっている必要があります。

**PDFドキュメントへの既存のポリシーの適用**

PDFドキュメントにポリシーを適用するには、既存のポリシーを参照し、ポリシーが属するポリシーセットを指定します。 接続プロパティを設定するユーザーは、指定したポリシーにアクセスできる必要があります。 そうでない場合は、例外が発生します。

**PDFドキュメントの保存**

Document SecurityサービスがPDFドキュメントにポリシーを適用した後、ポリシーで保護されたPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ドキュメントへのアクセス権限の失効](protecting-documents-policies.md#revoking-access-to-documents)

### Java APIを使用したPDFドキュメントへのポリシーの適用 {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Document Security API(Java)を使用してPDFドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. Document Security Client APIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントを取得します。

   * PDFドキュメント `java.io.FileInputStream` を表すオブジェクトを作成するには、そのコンストラクターを使用します。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントに既存のポリシーを適用します。

   * オブジェクト `DocumentManager` のメソッドを呼び出して、オ `RightsManagementClient` ブジェクトを作成 `getDocumentManager` します。
   * オブジェクトのメソッドを呼び出し、次の値を渡して、PDF `DocumentManager` ドキュメント `protectDocument` にポリシーを適用します。

      * ポリシ `com.adobe.idp.Document` ーが適用されるPDFドキュメントを含むオブジェクトです。
      * ドキュメントの名前を指定するstring値。
      * ポリシーが属するポリシーセットの名前を指定するstring値です。 ポリシーセットが使 `null` 用される結果となる値 `MyPolicies` を指定できます。
      * ポリシー名を指定するstring値です。
      * ドキュメントのパブリッシャーであるユーザーのユーザーマネージャードメインの名前を表すstring値です。 このパラメーター値はオプションで、nullに設定できます（このパラメーターがnullの場合、次のパラメーター値はnullに設定する必要があります）。
      * ドキュメントのパブリッシャーであるユーザーマネージャーユーザーの正規名を表すstring値です。 このパラメーター値はオプションで、値を指 `null` 定できます(このパラメーターがnullの場合、前のパラメーター値を指定する必要があ `null`ります)。
      * MS officeテ `com.adobe.livecycle.rightsmanagement.Locale` ンプレートの選択に使用されるロケールを表す。 このパラメーター値はオプションで、PDFドキュメントには使用されません。 PDFドキュメントを保護するには、を指定しま `null`す。
      このメソ `protectDocument` ッドは、ポリシーで保護 `RMSecureDocumentResult` されたPDFドキュメントを含むオブジェクトを返します。


1. PDFドキュメントを保存します。

   * オブジェクト `RMSecureDocumentResult` のメソッドを呼び `getProtectedDoc` 出して、ポリシーで保護されたPDFドキュメントを取得します。 このメソッドは、オブジェクトを `com.adobe.idp.Document` 返します。
   * Create a `java.io.File` object and ensure that the file extension is PDF.
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出 `copyToFile` して、オブジェクトの内容をファイルにコピ `Document` ーします(メソッドによって返されたオブジェクトを使用 `Document` していることを確 `getProtectedDoc` 認します)。

**コードの例**

Document Securityサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「クイックスタート（EJBモード）:Java APIを使用したPDFドキュメントへのポリシーの適用」
* 「クイックスタート（SOAPモード）:Java APIを使用したPDFドキュメントへのポリシーの適用」

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントへのポリシーの適用 {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Document Security API（Webサービス）を使用してPDFドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Document Security Client APIオブジェクトを作成します。

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をFormsサービスに渡します(例： `http://localhost:8080/soap/services/RightsManagementService?WSDL`.)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `RightsManagementServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `RightsManagementServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `RightsManagementServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。


1. PDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、ポリシーが適用されるPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 オブジェクトのプロパティを取得して、バイト配列 `System.IO.FileStream` のサイズを決定 `Length` します。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデ `System.IO.FileStream` ータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. PDFドキュメントに既存のポリシーを適用します。

   オブジェクトのメソッドを呼び出し、次の値を渡して、PDF `RightsManagementServiceClient` ドキュメント `protectDocument` にポリシーを適用します。

   * ポリシ `BLOB` ーが適用されるPDFドキュメントを含むオブジェクトです。
   * ドキュメントの名前を指定するstring値。
   * ポリシーが属するポリシーセットの名前を指定するstring値です。 ポリシーセットが使 `null` 用される結果となる値 `MyPolicies` を指定できます。
   * ポリシー名を指定するstring値です。
   * ドキュメントのパブリッシャーであるユーザーのユーザーマネージャードメインの名前を表すstring値です。 このパラメーター値はオプションで、nullに設定できます(このパラメーターがnullの場合、次のパラメーター値を指定する必要があり `null`ます)。
   * ドキュメントのパブリッシャーであるユーザーマネージャーユーザーの正規名を表すstring値です。 このパラメーター値はオプションで、nullに設定できます(このパラメーターがnullの場合、前のパラメーター値を必須とし `null`ます)。
   * ロケ `RMLocale` ール値(例えば、 `RMLocale.en`)を指定する値。
   * ポリシー識別子の値の保存に使用される文字列出力パラメーターです。
   * ポリシーで保護された識別子の値の保存に使用される文字列出力パラメーターです。
   * MIMEタイプの格納に使用される文字列出力パラメーター(例： `application/pdf`)。
   このメソ `protectDocument` ッドは、ポリシーで保護 `BLOB` されたPDFドキュメントを含むオブジェクトを返します。

1. PDFドキュメントを保存します。

   * オブジェクトを `System.IO.FileStream` 作成するには、コンストラクターを呼び出し、ポリシーで保護されたPDFドキュメントのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトのデータ内容を格納 `BLOB` するバイト配列を作成 `protectDocument` します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**コードの例**

Document Securityサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「Quick Start(MTOM):WebサービスAPIを使用したPDFドキュメントへのポリシーの適用」
* &quot;クイックスタート(SwaRef):WebサービスAPIを使用したPDFドキュメントへのポリシーの適用」

## PDFドキュメントからのポリシーの削除 {#removing-policies-from-pdf-documents}

ポリシーで保護されたドキュメントからポリシーを削除して、ドキュメントからセキュリティを削除できます。 つまり、ドキュメントをポリシーで保護しない場合です。 ポリシーで保護されたドキュメントを新しいポリシーで更新する場合は、ポリシーを削除して更新されたポリシーを追加する代わりに、ポリシーを切り替える方が効率的です。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-4}

ポリシーで保護されたPDFドキュメントからポリシーを削除するには、次の手順を実行します。

1. プロジェクトファイルを含める
1. Document Security Client APIオブジェクトを作成します。
1. ポリシーで保護されたPDFドキュメントを取得します。
1. PDFドキュメントからポリシーを削除します。
1. 保護されていないPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Document Security Client APIオブジェクトの作成**

プログラムを使用してDocument Securityサービスの操作を実行する前に、Document Securityサービスクライアントオブジェクトを作成します。

**ポリシーで保護されたPDFドキュメントの取得**

ポリシーで保護されたPDFドキュメントを取得して、ポリシーを削除できます。 ポリシーで保護されていないPDFドキュメントからポリシーを削除しようとすると、例外が発生します。

**PDFドキュメントからのポリシーの削除**

接続設定で管理者が指定されている場合は、ポリシーで保護されたPDFドキュメントからポリシーを削除できます。 ポリシーがない場合は、PDFドキュメントからポリシーを削除するために、ドキュメントのセキュリテ `SWITCH_POLICY` ィ保護に使用されるポリシーに権限が含まれている必要があります。 また、AEM Formsの接続設定で指定したユーザーにも、その権限が必要です。 それ以外の場合は、例外がスローされます。

**保護されていないPDFドキュメントの保存**

Document SecurityサービスがPDFドキュメントからポリシーを削除した後、保護されていないPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Java APIを使用したPDFドキュメントからのポリシーの削除 {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Document Security API(Java)を使用して、ポリシーで保護されたPDFドキュメントからポリシーを削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. Document Security Client APIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護されたPDFドキュメントを取得します。

   * コンストラ `java.io.FileInputStream` クターを使用し、PDFドキュメントの場所を指定するstring値を渡して、ポリシーで保護されたPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントからポリシーを削除します。

   * オブジェクト `DocumentManager` のメソッドを呼び出して、オ `DocumentSecurityClient` ブジェクトを作成 `getDocumentManager` します。
   * オブジェクトのメソッドを呼び出し、ポリシーで保護されたPDFドキ `DocumentManager` ュメントを含むオ `removeSecurity` ブジェクトを渡すこ `com.adobe.idp.Document` とで、PDFドキュメントからポリシーを削除します。 このメソッドは、保護されて `com.adobe.idp.Document` いないPDFドキュメントを含むオブジェクトを返します。

1. 保護されていないPDFドキュメントを保存します。

   * Create a `java.io.File` object and ensure that the file extension is PDF.
   * オブジェクト `Document` のメソッドを呼び出 `copyToFile` して、オブジェクトの内容をファイルにコピ `Document` ーします(メソッドによって返されたオブジェクトを使用 `Document` していることを確 `removeSecurity` 認します)。

**コードの例**

Document Securityサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAPモード）:Java APIを使用したPDFドキュメントからのポリシーの削除」

### WebサービスAPIを使用したポリシーの削除 {#remove-a-policy-using-the-web-service-api}

Document Security API（Webサービス）を使用して、ポリシーで保護されたPDFドキュメントからポリシーを削除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Document Security Client APIオブジェクトを作成します。

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/RightsManagementService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `DocumentSecurityServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。


1. ポリシーで保護されたPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、ポリシーが削除されたポリシーで保護されたPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. PDFドキュメントからポリシーを削除します。

   オブジェクトのメソッドを呼び出し、ポリシーで保護されたPDFドキ `DocumentSecurityServiceClient` ュメントを含むオ `removePolicySecurity` ブジェクトを渡すこ `BLOB` とで、PDFドキュメントからポリシーを削除します。 このメソッドは、保護されて `BLOB` いないPDFドキュメントを含むオブジェクトを返します。

1. 保護されていないPDFドキュメントを保存します。

   * オブジェクトを `System.IO.FileStream` 作成するには、コンストラクターを呼び出し、保護されていないPDFドキュメントのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトのデータ内容を格納 `BLOB` するバイト配列を作成 `removePolicySecurity` します。 オブジェクトのフィールドの値を取得して、バイト `BLOB` 配列を設定し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.

**コードの例**

Document Securityサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「Quick Start(MTOM):WebサービスAPIを使用したPDFドキュメントからのポリシーの削除」
* &quot;クイックスタート(SwaRef):WebサービスAPIを使用したPDFドキュメントからのポリシーの削除」

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## ドキュメントへのアクセス権限の失効 {#revoking-access-to-documents}

ポリシーで保護されたPDFドキュメントへのアクセス権限を失効させると、ドキュメントのすべてのコピーがユーザーにアクセスできなくなります。 失効したPDFドキュメントをユーザーが開こうとすると、指定されたURLにリダイレクトされ、変更後のドキュメントを表示できます。 ユーザーがリダイレクトされるURLは、プログラムで指定する必要があります。 ドキュメントへのアクセス権限を失効すると、ユーザーが次回、ポリシーで保護されたドキュメントをオンラインで開いてDocument Securityサービスと同期したときに、変更が反映されます。

ドキュメントへのアクセス権限を失効させる機能は、セキュリティを強化します。 例えば、新しいバージョンのドキュメントが利用可能で、古いバージョンを表示するユーザーが不要になったとします。 この場合、古いドキュメントへのアクセス権を取り消し、アクセス権を復元しない限りドキュメントを表示できません。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-5}

ポリシーで保護されたドキュメントを失効させるには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client APIオブジェクトを作成します。
1. ポリシーで保護されたPDFドキュメントを取得します。
1. ポリシーで保護されたドキュメントを失効させます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Document Security Client APIオブジェクトの作成**

Document Securityサービスの操作をプログラムで実行する前に、Document Securityサービスクライアントオブジェクトを作成する必要があります。

**ポリシーで保護されたPDFドキュメントの取得**

ポリシーで保護されたPDFドキュメントを失効させるには、そのドキュメントを取得する必要があります。 失効済みのドキュメントや、ポリシーで保護されたドキュメントではないドキュメントは失効できません。

ポリシーで保護されたドキュメントのライセンス識別子の値がわかっている場合は、ポリシーで保護されたPDFドキュメントを取得する必要はありません。 ただし、ほとんどの場合、ライセンス識別子の値を取得するにはPDFドキュメントを取得する必要があります。

**ポリシーで保護されたドキュメントの失効**

ポリシーで保護されたドキュメントを失効させるには、ポリシーで保護されたドキュメントのライセンス識別子を指定します。 また、失効したドキュメントをユーザーが開こうとしたときに表示できるドキュメントのURLを指定できます。 つまり、古いドキュメントが失効したとします。 失効したドキュメントを開こうとすると、失効したドキュメントではなく更新されたドキュメントが表示されます。

>[!NOTE]
>
>既に失効したドキュメントを失効させようとすると、例外がスローされます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[取り消されたドキュメントへのアクセスの復元](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Java APIを使用したドキュメントへのアクセス権限の失効 {#revoke-access-to-documents-using-the-java-api}

Document Security API(Java)を使用して、ポリシーで保護されたPDFドキュメントへのアクセス権限を失効させます。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. Document Security Client APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護されたPDFドキュメントの取得

   * コンストラク `java.io.FileInputStream` ターを使用し、PDFドキュメントの場所を指定するstring値を渡すことで、ポリシーで保護されたPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ポリシーで保護されたドキュメントの失効

   * オブジェクト `DocumentManager` のメソッドを呼び出して、オ `DocumentSecurityClient` ブジェクトを作成 `getDocumentManager` します。
   * オブジェクトのメソッドを呼び出して、ポリシーで保護されたドキュメントのライ `DocumentManager` センス識別子の値を取得 `getLicenseId` します。 ポリシーで保護 `com.adobe.idp.Document` されたドキュメントを表すオブジェクトを渡します。 このメソッドは、ライセンス識別子の値を表すstring値を返します。
   * オブジェクト `LicenseManager` のメソッドを呼び出して、オ `DocumentSecurityClient` ブジェクトを作成 `getLicenseManager` します。
   * オブジェクトのメソッドを呼び出し、次の値を渡して、ポ `LicenseManager` リシーで保護され `revokeLicense` たドキュメントを失効させます。

      * ポリシーで保護されたドキュメントのライセンス識別子の値(オブジェクトのメソッドの戻 `DocumentManager` り値を指定 `getLicenseId` )を指定するstring値。
      * ドキュメントを失効させる理由を指 `License` 定するインターフェイスの静的データメンバーです。 例えば、を指定できます `License.DOCUMENT_REVISED`。
      * 改訂 `java.net.URL` されたドキュメントの場所を指定する値。 ユーザーを別のURLにリダイレクトしない場合は、を渡すことができます `null`。

**コードの例**

Document Securityサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAPモード）:Java APIを使用したドキュメントの失効」

### WebサービスAPIを使用したドキュメントへのアクセス権限の失効 {#revoke-access-to-documents-using-the-web-service-api}

Document Security API（Webサービス）を使用して、ポリシーで保護されたPDFドキュメントへのアクセス権限を失効させます。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Document Security Client APIオブジェクトの作成

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/RightsManagementService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `DocumentSecurityServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。


1. ポリシーで保護されたPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、失効したポリシーで保護されたPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、失効するポリシーで保護されたPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. ポリシーで保護されたドキュメントの失効

   * オブジェクトのメソッドを呼び出し、ポリシーで保護されたドキュメントを表 `DocumentSecurityServiceClient` すオブジェクトを `getLicenseID` 渡すことで、ポリシーで保護さ `BLOB` れたドキュメントのライセンス識別子の値を取得します。 このメソッドは、ライセンス識別子を表すstring値を返します。
   * オブジェクトのメソッドを呼び出し、次の値を渡して、ポ `DocumentSecurityServiceClient` リシーで保護され `revokeLicense` たドキュメントを失効させます。

      * ポリシーで保護されたドキュメントのライセンス識別子の値(オブジェクトのメソッドの戻 `DocumentSecurityServiceService` り値を指定 `getLicenseId` )を指定するstring値。
      * ドキュメントを失効させる理由を `Reason` 指定する、列挙型の静的データメンバーです。 例えば、を指定できます `Reason.DOCUMENT_REVISED`。
      * 改訂 `string` されたドキュメントのURL位置を指定する値。 ユーザーを別のURLにリダイレクトしない場合は、を渡すことができます `null`。

**コードの例**

Document Securityサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「Quick Start(MTOM):WebサービスAPIを使用したドキュメントの失効」
* &quot;クイックスタート(SwaRef):WebサービスAPIを使用したドキュメントの失効」

**関連トピック**

[Wordドキュメントからのポリシーの削除](protecting-documents-policies.md#removing-policies-from-word-documents)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 取り消されたドキュメントへのアクセスの復元 {#reinstating-access-to-revoked-documents}

失効したPDFドキュメントへのアクセス権限を復元できるので、失効したドキュメントのすべてのコピーにユーザーがアクセスできます。 ユーザーが失効した復元済みドキュメントを開くと、そのドキュメントを表示できます。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-6}

失効したPDFドキュメントへのアクセス権を復元するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client APIオブジェクトを作成します。
1. 失効したPDFドキュメントのライセンス識別子を取得します。
1. 失効したPDFドキュメントへのアクセス権限の復元。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Document Security Client APIオブジェクトの作成**

Document Securityサービスの操作をプログラムで実行する前に、Document Securityサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `DocumentSecurityClient` ます。 Document Security webサービスAPIを使用している場合は、オブジェクトを作成し `DocumentSecurityServiceService` ます。

**失効したPDFドキュメントのライセンス識別子の取得**

失効したPDFドキュメントを復元するには、失効したPDFドキュメントのライセンス識別子を取得する必要があります。 ライセンス識別子の値を取得した後、失効したドキュメントを復元できます。 失効していないドキュメントを元に戻そうとすると、例外が発生します。

**失効したPDFドキュメントへのアクセス権限の復元**

失効したPDFドキュメントへのアクセス権を復元するには、失効したドキュメントのライセンス識別子を指定する必要があります。 失効していないPDFドキュメントへのアクセス権を復元しようとすると、例外が発生します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[ドキュメントへのアクセス権限の失効](protecting-documents-policies.md#revoking-access-to-documents)

### Java APIを使用した失効したドキュメントへのアクセスの復元 {#reinstate-access-to-revoked-documents-using-the-java-api}

Document Security API (Java)を使用して、失効したドキュメントへのアクセス権限を復元します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. Document Security Client APIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 失効したPDFドキュメントのライセンス識別子を取得します。

   * コンストラ `java.io.FileInputStream` クターを使用し、PDFドキュメントの場所を指定するstring値を渡して、失効したPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * オブジェクト `DocumentManager` のメソッドを呼び出して、オ `DocumentSecurityClient` ブジェクトを作成 `getDocumentManager` します。
   * オブジェクトのメソッドを呼び出し、失効したドキュメントを表 `DocumentManager` すオブジェクトを `getLicenseId` 渡すことで、失効したドキュ `com.adobe.idp.Document` メントのライセンス識別子の値を取得します。 このメソッドは、ライセンス識別子を表すstring値を返します。

1. 失効したPDFドキュメントへのアクセス権限の復元。

   * オブジェクト `LicenseManager` のメソッドを呼び出して、オ `DocumentSecurityClient` ブジェクトを作成 `getLicenseManager` します。
   * オブジェクトのメソッドを呼び出し、失効したドキュメントのライ `LicenseManager` センス識別子の値を渡 `unrevokeLicense` すことで、失効したPDFドキュメントへのアクセス権限を復元します。

**コードの例**

Document Securityサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAPモード）:WebサービスAPIを使用した失効したドキュメントへのアクセスの復元」

### WebサービスAPIを使用した失効したドキュメントへのアクセスの復元 {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Document Security API（Webサービス）を使用して、失効したドキュメントへのアクセス権を復元します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Document Security Client APIオブジェクトを作成します。

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/RightsManagementService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `DocumentSecurityServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。


1. 失効したPDFドキュメントのライセンス識別子を取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブ `BLOB` ジェクトは、アクセス権が復元された失効したPDFドキュメントを保存するために使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、失効したPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. 失効したPDFドキュメントへのアクセス権限の復元。

   * オブジェクトのメソッドを呼び出し、失効したドキュメントを表 `DocumentSecurityServiceClient` すオブジェクトを `getLicenseID` 渡すことで、失効したドキュ `BLOB` メントのライセンス識別子の値を取得します。 このメソッドは、ライセンス識別子を表すstring値を返します。
   * 失効したPDFドキュメントへのアクセス権限を復元するには、オブジェクトのメソッドを呼び出し、失効したPDFドキュメントのライセンス識別子の値を指定する `DocumentSecurityServiceClient` string値を渡します(オブジェクトのメソッドの戻り値を渡 `unrevokeLicense``DocumentSecurityServiceClient``getLicenseId` します)。

**コードの例**

Document Securityサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「Quick Start(MTOM):WebサービスAPIを使用した失効したドキュメントへのアクセスの復元」
* &quot;クイックスタート(SwaRef):WebサービスAPIを使用した失効したドキュメントへのアクセスの復元」

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## ポリシーで保護されたPDFドキュメントの検査 {#inspecting-policy-protected-pdf-documents}

Document Security Service API（JavaおよびWebサービス）を使用して、ポリシーで保護されたPDFドキュメントを検査できます。 ポリシーで保護されたPDFドキュメントを検査すると、ポリシーで保護されたPDFドキュメントに関する情報が返されます。 例えば、ドキュメントの保護に使用したポリシーやドキュメントの保護日を指定できます。

お使いのLiveCycleのバージョンが8.x以前の場合は、このタスクを実行できません。 ポリシーで保護されたドキュメントの検査のサポートがAEM Formsに追加されました。 LiveCycle 8.x（またはそれ以前）を使用してポリシーで保護されたドキュメントを検査しようとすると、例外がスローされます。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-7}

ポリシーで保護されたPDFドキュメントを検査するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client APIオブジェクトを作成します。
1. 検査するポリシーで保護されたドキュメントを取得します。
1. ポリシーで保護されたドキュメントに関する情報を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Document Security Client APIオブジェクトの作成**

プログラムを使用してDocument Securityサービスの操作を実行する前に、Document Securityサービスクライアントオブジェクトを作成します。 Java APIを使用している場合は、オブジェクトを作成し `RightsManagementClient` ます。 Document Security webサービスAPIを使用している場合は、オブジェクトを作成し `RightsManagementServiceService` ます。

**ポリシーで保護されたドキュメントを取得して検査する**

ポリシーで保護されたドキュメントを検査するには、ドキュメントを取得します。 ポリシーで保護されていないドキュメントや失効したドキュメントを検査しようとすると、例外がスローされます。

**ドキュメントの検査**

ポリシーで保護されたドキュメントを取得した後、それを検査できます。

**ポリシーで保護されたドキュメントに関する情報の取得**

ポリシーで保護されたPDFドキュメントを検査した後、そのドキュメントに関する情報を取得できます。 例えば、ドキュメントの保護に使用するポリシーを指定できます。

「マイポリシー」に属するポリシーでドキュメントを保護した後、またはを呼び出す `RMInspectResult.getPolicysetName` と、 `RMInspectResult.getPolicysetId`nullが返されます。

ポリシーセットに含まれるポリシー（「マイポリシー」以外）を使用してドキュメントが保護されている場合は、有効な文 `RMInspectResult.getPolicysetName` 字列 `RMInspectResult.getPolicysetId` を返します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したポリシーで保護されたPDFドキュメントの検査 {#inspect-policy-protected-pdf-documents-using-the-java-api}

Document Security Service API(Java)を使用して、ポリシーで保護されたPDFドキュメントを検査します。

1. プロジェクトファイルを含めます。

   adobe-rightsmanagement-client.jarなどのクライアントJARファイルをJavaプロジェクトのクラスパスに含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

1. Document Security Client APIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 検査するポリシーで保護されたドキュメントを取得します。

   * ポリシーで保護 `java.io.FileInputStream` されたPDFドキュメントを表すオブジェクトを、そのコンストラクターを使用して作成します。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ドキュメントを検査します。

   * オブジェクト `DocumentManager` のメソッドを呼び出して、オ `RightsManagementClient` ブジェクトを作成 `getDocumentManager` します。
   * オブジェクトのメソッドを呼び出して、ポリシーで保護された `LicenseManager` ドキュメントを検査 `inspectDocument` します。 ポリシーで保護 `com.adobe.idp.Document` されたPDFドキュメントを含むオブジェクトを渡します。 このメソッドは、ポリシー `RMInspectResult` で保護されたドキュメントに関する情報を含むオブジェクトを返します。

1. ポリシーで保護されたドキュメントに関する情報を取得します。

   ポリシーで保護されたドキュメントに関する情報を取得するには、オブジェクトに属する適切なメソッドを呼び出 `RMInspectResult` します。 例えば、ポリシー名を取得するには、オブジェクトのメ `RMInspectResult` ソッドを呼び出 `getPolicyName` します。

**コードの例**

Document Securityサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAPモード）:Java APIを使用したポリシーで保護されたPDFドキュメントの検査」

### WebサービスAPIを使用したポリシーで保護されたPDFドキュメントの検査 {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Document Security Service API（Webサービス）を使用して、ポリシーで保護されたPDFドキュメントを検査します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Document Security Client APIオブジェクトを作成します。

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/RightsManagementService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `RightsManagementServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `RightsManagementServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `RightsManagementServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。


1. 検査するポリシーで保護されたドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、検査するPDFドキュメントの保存に使用されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. PDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデ `System.IO.FileStream` ータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. ドキュメントを検査します。

   オブジェクトのメソッドを呼び出して、ポリシーで保護された `RightsManagementServiceClient` ドキュメントを検査 `inspectDocument` します。 ポリシーで保護 `BLOB` されたPDFドキュメントを含むオブジェクトを渡します。 このメソッドは、ポリシー `RMInspectResult` で保護されたドキュメントに関する情報を含むオブジェクトを返します。

1. ポリシーで保護されたドキュメントに関する情報を取得します。

   ポリシーで保護されたドキュメントに関する情報を取得するには、オブジェクトに属する適切なフィールドの値を取得 `RMInspectResult` します。 例えば、ポリシー名を取得するには、オブジェクトのフィールドの値 `RMInspectResult` を取得し `policyName` ます。

**コードの例**

Document Securityサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「Quick Start(MTOM):WebサービスAPIを使用したポリシーで保護されたPDFドキュメントの検査」
* &quot;クイックスタート(SwaRef):WebサービスAPIを使用したポリシーで保護されたPDFドキュメントの検査」

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 透かしの作成 {#creating-watermarks}

透かしは、ドキュメントを一意に識別し、著作権侵害を制御することで、ドキュメントのセキュリティを確保するのに役立ちます。 例えば、「機密」という内容の透かしを作成し、ドキュメントのすべてのページに配置することができます。 透かしを作成した後に、その透かしをポリシーの一部として含めることができます。 つまり、新しく作成した透かしにポリシーの透かし属性を設定できます。 透かしを含むポリシーがドキュメントに適用されると、その透かしはポリシーで保護されたドキュメントに表示されます。

>[!NOTE]
>
>透かしを作成できるのは、Document Securityの管理者権限を持つユーザーのみです。 つまり、Document Securityサービスクライアントオブジェクトの作成に必要な接続設定を定義する場合は、このようなユーザーを指定する必要があります。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-8}

透かしを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client APIオブジェクトを作成します。
1. 透かしの属性を設定します。
1. 透かしをDocument Securityサービスに登録します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Document Security Client APIオブジェクトの作成**

Document Securityサービスの操作をプログラムで実行する前に、Document Securityサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `RightsManagementClient` ます。 Document Security webサービスAPIを使用している場合は、オブジェクトを作成し `RightsManagementServiceService` ます。

**透かし属性の設定**

新しい透かしを作成するには、透かしの属性を設定する必要があります。 name属性は必ず定義する必要があります。 name属性に加えて、次の属性の少なくとも1つを設定する必要があります。

* カスタムテキスト
* DateIncluded
* UserIdIncluded
* UserNameIncluded

次の表に、Webサービスを使用して透かしを作成する際に必要なキーと値のペアを示します。

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
   <td><p>ドキュメントを開くユーザーのIDが透かしの一部であるかどうかを指定します。</p></td>
   <td><p>True または False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>現在の日付が透かしの一部であるかどうかを指定します。</p></td>
   <td><p>True または False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>この値がtrueの場合、カスタムテキストの値は、を使用して指定する必要がありま <code>WaterBackCmd:SRCTEXT</code>す。</p></td>
   <td><p>True または False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>透かしの不透明度を指定します。 デフォルト値は0.5です（指定しない場合）。</p></td>
   <td><p>0.0 ～ 1.0の値です。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>透かしの回転を指定します。 デフォルト値は0度です。</p></td>
   <td><p>0 ～ 359の値です。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>この値を指定する場合は、値 <code>WaterBackCmd:IS_SIZE_ENABLED</code> が存在し、値がtrueである必要があります。 この属性を指定しない場合、デフォルトの動作はページに合わせて調整されます。</p></td>
   <td><p>0.0 より大きく 1.0 以下の値。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>透かしの水平方向の配置を指定します。 デフォルト値はcenterです。</p></td>
   <td><p>left、centerまたはright</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td>
   <td><p>透かしの垂直方向の配置を指定します。 デフォルト値はcenterです。</p></td>
   <td><p>上、中央、下</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td>
   <td><p>透かしが背景かどうかを指定します。 デフォルト値は false です。</p></td>
   <td><p>True または False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td>
   <td><p>カスタムの尺度が指定されている場合はtrue。 この値がtrueの場合、SCALEも指定する必要があります。 この値がfalseの場合、デフォルトはページに合わせて調整されます。</p></td>
   <td><p>True または False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>透かしのカスタムテキストを指定します。 この値が存在する場合は、同じ値が存 <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> 在し、trueに設定されている必要があります。</p></td>
   <td><p>True または False</p></td>
  </tr>
 </tbody>
</table>

すべての透かしに、次の属性のいずれかが定義されている必要があります。

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

その他の属性はすべてオプションです。

**透かしの登録**

新しい透かしを使用するには、Document Securityサービスに新しい透かしを登録する必要があります。 透かしを登録した後は、ポリシー内で使用できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Java APIを使用した透かしの作成 {#create-watermarks-using-the-java-api}

Document Security API(Java)を使用して透かしを作成します。

1. プロジェクトファイルを含めます。

   Include client JAR files, such as the `adobe-rightsmanagement-client.jar`, in your Java project’s class path.

1. Document Security Client APIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 透かしの属性の設定

   * オブジェクト `Watermark` の静的メソッドを呼び出し `InfomodelObjectFactory` て、オブジェクトを作成 `createWatermark` します。 このメソッドは、オブジェクトを `Watermark` 返します。
   * オブジェクトのメソッドを呼び出し、ポリシー名を `Watermark` 指定するstring値 `setName` を渡して、透かしのname属性を設定します。
   * オブジェクトのメソッドを呼び出して渡すことで、透か `Watermark` しの背景属性 `setBackground` を設定しま `true`す。 この属性を設定すると、透かしがドキュメントの背景に表示されます。
   * オブジェクトのメソッドを呼び出し、透かしのテキストを表 `Watermark` す文字列値を `setCustomText` 渡して、透かしのカスタムテキスト属性を設定します。
   * 透かしの不透明度属性を設定するには、オブジェクトの `Watermark` メソッドを `setOpacity` 呼び出し、不透明度レベルを指定する整数値を渡します。 値を100に設定した場合、透かしは完全に不透明になり、値を0に設定した場合、透かしは完全に透明になります。

1. 透かしを登録します。

   * オブジェクト `WatermarkManager` のメソッドを呼び出して、オ `RightsManagementClient` ブジェクトを作成 `getWatermarkManager` します。 このメソッドは、オブジェクトを `WatermarkManager` 返します。
   * オブジェクトのメソッドを呼び出し、 `WatermarkManager` 登録する透かしを `registerWatermark` 表すオブジェクトを `Watermark` 渡すことで、透かしを登録します。 このメソッドは、透かしの識別値を表すstring値を返します。

**コードの例**

Document Securityサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAPモード）:Java APIを使用した透かしの作成」

### WebサービスAPIを使用した透かしの作成 {#create-watermarks-using-the-web-service-api}

Document Security API（Webサービス）を使用して透かしを作成します。

1. Document Security Client APIオブジェクトを作成します。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Document Security Client APIオブジェクトを作成します。

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/RightsManagementService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `RightsManagementServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `RightsManagementServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `RightsManagementServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。


1. 透かしの属性を設定します。

   * コンストラクターを `WatermarkSpec` 呼び出して、オブジェクトを作 `WatermarkSpec` 成します。
   * オブジェクトのデータメンバーに文字列値を割り当てて、透かし `WatermarkSpec` の名前を設 `name` 定します。
   * オブジェクトのデータメンバ `id` ーに文字列値を割り当てて、透かしの `WatermarkSpec` 属性を設 `id` 定します。
   * 設定する透かしプロパティごとに、別々のオブジェクトを作成 `MyMapOf_xsd_string_To_xsd_anyType_Item` します。
   * キーの値を設定するには、オブジェクトのデータメ `MyMapOf_xsd_string_To_xsd_anyType_Item` ンバーに値を `key` 割り当てます(例 `WaterBackCmd:OPACITY)`:
   * 値を設定するには、オブジェクトのデータメ `MyMapOf_xsd_string_To_xsd_anyType_Item` ンバーに値を `value` 割り当てます(例 `.25`えば)。
   * Create a `MyArrayOf_xsd_anyType` object. 各オブジェクト `MyMapOf_xsd_string_To_xsd_anyType_Item` に対して、オブジェクトの `MyArrayOf_xsd_anyType` メソッドを呼び出 `Add` します。 Pass the `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * オブジェクト `MyArrayOf_xsd_anyType` をオブジェクトのデ `WatermarkSpec` ータメンバーに `values` 割り当てます。

1. 透かしを登録します。

   オブジェクトのメソッドを呼び出し、 `RightsManagementServiceClient` 登録する透かしを `registerWatermark` 表すオブジェクトを `WatermarkSpec` 渡すことで、透かしを登録します。

**コードの例**

Document Securityサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「Quick Start(MTOM):WebサービスAPIを使用した透かしの作成」
* &quot;クイックスタート(SwaRef):WebサービスAPIを使用した透かしの作成」

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 透かしの変更 {#modifying-watermarks}

Document Security Java APIまたはWebサービスAPIを使用して、既存の透かしを変更できます。 既存の透かしを変更するには、その透かしを取得し、その属性を変更してから、サーバ上で更新します。 例えば、透かしを取得し、その不透明度属性を変更したとします。 変更を有効にする前に、透かしを更新する必要があります。

透かしを変更すると、その透かしが適用された後のドキュメントに影響が及びます。 つまり、透かしを含む既存のPDFドキュメントは影響を受けません。

>[!NOTE]
>
>透かしを変更できるのは、Document Securityの管理者権限を持つユーザーのみです。 つまり、Document Securityサービスクライアントオブジェクトの作成に必要な接続設定を定義する場合は、このようなユーザーを指定する必要があります。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-9}

透かしを変更するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client APIオブジェクトを作成します。
1. 変更する透かしを取得します。
1. 透かしの属性を設定します。
1. 透かしを更新します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Document Security Client APIオブジェクトの作成**

Document Securityサービスの操作をプログラムで実行する前に、Document Securityサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `DocumentSecurityClient` ます。 Document Security webサービスAPIを使用している場合は、オブジェクトを作成し `DocumentSecurityServiceService` ます。

**変更する透かしの取得**

透かしを変更するには、既存の透かしを取得する必要があります。 透かしの名前を指定するか、識別子の値を指定することで、透かしを取得できます。

**透かし属性の設定**

既存の透かしを変更するには、1つ以上の透かし属性の値を変更します。 Webサービスを使用してプログラムによって透かしを更新する場合、値が変更されなくても、元々設定されていたすべての属性を設定する必要があります。 例えば、次の透かし属性が設定されているとします。 `WaterBackCmd:IS_USERID_ENABLED`、 `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`、、 `WaterBackCmd:OPACITY`および `WaterBackCmd:SRCTEXT`。 変更する必要がある属性は1つだけですが、他 `WaterBackCmd:OPACITY`の値は適切な値を設定する必要があります。

>[!NOTE]
>
>Java APIを使用して透かしを変更する場合は、すべての属性を指定する必要はありません。 変更する透かし属性を設定します。

>[!NOTE]
>
>透かし属性名について詳しくは、「透かしの作成」を参 [照してください](protecting-documents-policies.md#creating-watermarks)。

**透かしの更新**

透かしの属性を変更した後、透かしを更新する必要があります。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[透かしの作成](protecting-documents-policies.md#creating-watermarks)

### Java APIを使用した透かしの変更 {#modify-watermarks-using-the-java-api}

Document Security API(Java)を使用して透かしを変更します。

1. プロジェクトファイルを含めます。

   adobe-rightsmanagement-client.jarなどのクライアントJARファイルをJavaプロジェクトのクラスパスに含めます。

1. Document Security Client APIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 変更する透かしを取得します。

   オブジェクト `WatermarkManager` のメソッドを呼び出 `DocumentSecurityClient` し、透か `getWatermarkManager` し名を指定する文字列値を渡して、オブジェクトを作成します。 このメソッドは、変更す `Watermark` る透かしを表すオブジェクトを返します。

1. 透かしの属性を設定します。

   透かしの不透明度属性を設定するには、オブジェクトの `Watermark` メソッドを `setOpacity` 呼び出し、不透明度レベルを指定する整数値を渡します。 値を100に設定した場合、透かしは完全に不透明になり、値を0に設定した場合、透かしは完全に透明になります。

   >[!NOTE]
   >
   >次の例では、opacity属性のみを変更します。

1. 透かしを更新します。

   * オブジェクトのメソッドを呼び出し、属 `WatermarkManager` 性が変更さ `updateWatermark` れたオブジェクトを `Watermark` 渡して、透かしを更新します。

**コードの例**

Document Securityサービスを使用するコードの例については、クイックスタート（SOAPモード）を参照してください。Java APIセクションを使用した透かしの変更

### WebサービスAPIを使用した透かしの変更 {#modify-watermarks-using-the-web-service-api}

Document Security API（Webサービス）を使用して透かしを変更します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Document Security Client APIオブジェクトを作成します。

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `DocumentSecurityServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。


1. 変更する透かしを取得します。

   オブジェクトのメソッドを呼び出して、変更する `DocumentSecurityServiceClient` 透かしを取得 `getWatermarkByName` します。 透かし名を指定するstring値を渡します。 このメソッドは、変更す `WatermarkSpec` る透かしを表すオブジェクトを返します。

1. 透かしの属性を設定します。

   * 更新する透かしのプロパティごとに、別々のオブジェクトを作成 `MyMapOf_xsd_string_To_xsd_anyType_Item` します。
   * キーの値を設定するには、オブジェクトのデータメ `MyMapOf_xsd_string_To_xsd_anyType_Item` ンバーに値を `key` 割り当てます(例 `WaterBackCmd:OPACITY)`:
   * 値を設定するには、オブジェクトのデータメ `MyMapOf_xsd_string_To_xsd_anyType_Item` ンバーに値を `value` 割り当てます(例 `.50`えば)。
   * Create a `MyArrayOf_xsd_anyType` object. 各オブジェクト `MyMapOf_xsd_string_To_xsd_anyType_Item` に対して、オブジェクトの `MyArrayOf_xsd_anyType` メソッドを呼び出 `Add` します。 Pass the `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * オブジェクト `MyArrayOf_xsd_anyType` をオブジェクトのデ `WatermarkSpec` ータメンバーに `values` 割り当てます。

1. 透かしを更新します。

   オブジェクトのメソッドを呼び出し、変 `DocumentSecurityServiceClient` 更する透かし `updateWatermark` を表すオブジ `WatermarkSpec` ェクトを渡して、透かしを更新します。

**コードの例**

Document Securityサービスを使用したコードの例については、次のクイックスタートを参照してください。

* 「Quick Start(MTOM):WebサービスAPIを使用した透かしの変更」

## イベントの検索 {#searching-for-events}

Rights Managementサービスは、ドキュメントへのポリシーの適用、ポリシーで保護されたドキュメントの開封、ドキュメントへのアクセスの取り消しなど、特定のアクションの発生を追跡します。 Rights Managementサービスでイベント監査を有効にする必要があります。有効にしないと、イベントが追跡されません。

イベントは、次のいずれかのカテゴリに分類されます。

* 管理者イベントは、新しい管理者アカウントの作成など、管理者に関連するアクションです。
* ドキュメントイベントは、ポリシーで保護されたドキュメントを閉じるなど、ドキュメントに関連するアクションです。
* ポリシーイベントは、新しいポリシーの作成など、ポリシーに関連するアクションです。
* サービスイベントは、ユーザーディレクトリとの同期など、Rights Managementサービスに関連するアクションです。

Rights Management Java APIまたはWebサービスAPIを使用して、特定のイベントを検索できます。 イベントを検索することで、特定のイベントのログファイルの作成などのタスクを実行できます。

>[!NOTE]
>
>For more information about the Rights Management service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-10}

Rights Managementイベントを検索するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Rights Management Client APIオブジェクトを作成します。
1. 検索するイベントを指定します。
1. イベントを検索します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Rights Management Client APIオブジェクトの作成**

プログラムでRights Managementサービス操作を実行する前に、Rights Managementサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `DocumentSecurityClient` ます。 Rights Management webサービスAPIを使用している場合は、オブジェクトを作成し `DocumentSecurityServiceService` ます。

**検索するイベントの指定**

検索するイベントを指定する必要があります。 例えば、新しいポリシーが作成されたときに発生するポリシー作成イベントを検索できます。

**イベントの検索**

検索するイベントを指定した後、Rights Management Java APIまたはRights Management webサービスAPIを使用してイベントを検索できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したイベントの検索 {#search-for-events-using-the-java-api}

Rights Management API(Java)を使用してイベントを検索します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. Rights Management Client APIオブジェクトの作成

   コンストラク `DocumentSecurityClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. 検索するイベントの指定

   * オブジェクトの `EventManager` メソッドを呼び出して、オ `DocumentSecurityClient` ブジェクトを作成 `getEventManager` します。 このメソッドは、オブジェクトを `EventManager` 返します。
   * コンストラクタを呼 `EventSearchFilter` び出して、オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、検索するイベントを表すクラスに属する静的データメンバーを渡すことによって、検索 `EventSearchFilter``setEventCode``EventManager` するイベントを指定します。 例えば、ポリシー作成イベントを検索するには、を渡しま `EventManager.POLICY_CREATE_EVENT`す。
   >[!NOTE]
   >
   >オブジェクトメソッドを呼び出して、追加の検索条件を定 `EventSearchFilter` 義できます。 例えば、このメソッドを呼び出 `setUserName` して、イベントに関連付けられたユーザーを指定します。

1. イベントの検索

   オブジェクトのメソッドを呼び出し、イベ `EventManager` ント検索条件を `searchForEvents` 定義するオブジ `EventSearchFilter` ェクトを渡して、イベントを検索します。 このメソッドは、オブジェクトの配列を返 `Event` します。

**コードの例**

Rights Managementサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「Quick Start(SOAP):Java APIを使用したイベントの検索»

### WebサービスAPIを使用したイベントの検索 {#search-for-events-using-the-web-service-api}

Rights Management API（Webサービス）を使用してイベントを検索します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Rights Management Client APIオブジェクトの作成

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/RightsManagementService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `DocumentSecurityServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。


1. 検索するイベントの指定

   * Create an `EventSpec` object by using its constructor.
   * イベントが発生した期間の開始を指定するには、イベントが発生した日付範囲の開始を表すインスタンスを使用して、オ `EventSpec` ブジェクトの `firstTime.date` デ `DataTime` ータメンバーに設定します。
   * 値をオブジェクト `true` のデータメ `EventSpec` ンバーに割り `firstTime.dateSpecified` 当てます。
   * イベントが発生した期間の終わりを指定するには、イベントが発生した日付範囲の終わりを表すインスタンスを使用して、オブジェクトの `EventSpec` デ `lastTime.date``DataTime` ータメンバーにイベントが発生した期間の終わりを指定します。
   * 値をオブジェクト `true` のデータメ `EventSpec` ンバーに割り `lastTime.dateSpecified` 当てます。
   * オブジェクトのデータメンバーに文字列値を割り当てて、検索するイベ `EventSpec` ントを設 `eventCode` 定します。 次の表に、このプロパティに割り当てることのできる数値を示します。
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

   オブジェクトのメソッドを呼び出し、 `DocumentSecurityServiceClient` 検索するイベ `searchForEvents` ントを表すオ `EventSpec` ブジェクトを渡して、イベントを検索します。検索結果の最大数も同様です。 このメソッドは、各要素 `MyArrayOf_xsd_anyType` がインスタンスであるコレクションを返 `AuditSpec` します。 インスタ `AuditSpec` ンスを使用して、発生した時刻などのイベントに関する情報を取得できます。 インスタ `AuditSpec` ンスには、この情報を `timestamp` 指定するデータメンバーが含まれます。

**コードの例**

Rights Managementサービスを使用するコードの例については、次のクイックスタートを参照してください。

* 「Quick Start(MTOM):WebサービスAPIを使用したイベントの検索」
* &quot;クイックスタート(SwaRef):WebサービスAPIを使用したイベントの検索」

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Wordドキュメントへのポリシーの適用 {#applying-policies-to-word-documents}

Rights Managementサービスは、PDFドキュメントに加えて、Microsoft wordドキュメント（DOCファイル）やその他のMicrosoft Officeファイル形式などの追加のドキュメント形式もサポートします。 例えば、Wordドキュメントを保護するために、Wordドキュメントにポリシーを適用することができます。 Wordドキュメントにポリシーを適用すると、ドキュメントへのアクセスを制限できます。 ドキュメントが既にポリシーで保護されている場合は、ドキュメントにポリシーを適用できません。

ポリシーで保護されたWord文書は、配布後に使用を監視できます。 つまり、ドキュメントの使用方法と使用者を確認できます。 例えば、誰かがドキュメントを開いたタイミングを調べることができます。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-11}

Wordドキュメントにポリシーを適用するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client APIオブジェクトを作成します。
1. ポリシーが適用されるWordドキュメントを取得します。
1. Wordドキュメントに既存のポリシーを適用します。
1. ポリシーで保護されたWordドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Document Security Client APIオブジェクトの作成**

Document Securityサービスの操作をプログラムで実行する前に、Document Securityサービスクライアントオブジェクトを作成する必要があります。

**Wordドキュメントの取得**

ポリシーを適用するには、Wordドキュメントを取得する必要があります。 Wordドキュメントにポリシーを適用すると、ドキュメントの使用時にユーザーが制限されます。 例えば、オフライン時にドキュメントを開くことをポリシーで有効にしていない場合、ドキュメントを開くにはユーザーがオンラインになっている必要があります。

**Wordドキュメントへの既存のポリシーの適用**

Wordドキュメントにポリシーを適用するには、既存のポリシーを参照し、そのポリシーが属するポリシーセットを指定する必要があります。 接続プロパティを設定するユーザーは、指定したポリシーにアクセスできる必要があります。 そうでない場合は、例外が発生します。

**Wordドキュメントの保存**

Document SecurityサービスがWordドキュメントにポリシーを適用した後、ポリシーで保護されたWordドキュメントをDOCファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ドキュメントへのアクセス権限の失効](protecting-documents-policies.md#revoking-access-to-documents)

### Java APIを使用したWordドキュメントへのポリシーの適用 {#apply-a-policy-to-a-word-document-using-the-java-api}

Document Security API(Java)を使用してWordドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. Document Security Client APIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Wordドキュメントを取得します。

   * コンストラク `java.io.FileInputStream` ターを使用し、Wordドキュメントの場所を指定する文字列値を渡して、Wordドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. Wordドキュメントに既存のポリシーを適用します。

   * オブジェクト `DocumentManager` のメソッドを呼び出して、オ `DocumentSecurityClient` ブジェクトを作成 `getDocumentManager` します。
   * オブジェクトのメソッドを呼び出し、次の値を渡すこ `DocumentManager` とで、Wordドキュ `protectDocument` メントにポリシーを適用します。

      * ポリシ `com.adobe.idp.Document` ーが適用されるWordドキュメントを含むオブジェクトです。
      * ドキュメントの名前を指定するstring値。
      * ポリシーが属するポリシーセットの名前を指定するstring値です。 ポリシーセットが使 `null` 用される結果となる値 `MyPolicies` を指定できます。
      * ポリシー名を指定するstring値です。
      * ドキュメントのパブリッシャーであるユーザーのユーザーマネージャードメインの名前を表すstring値です。 このパラメーター値はオプションで、nullに設定できます（このパラメーターがnullの場合、次のパラメーター値はnullに設定する必要があります）。
      * ドキュメントのパブリッシャーであるユーザーマネージャーユーザーの正規名を表すstring値です。 このパラメーター値はオプションで、 `null` を指定できます(このパラメーター `null`の場合、前のパラメーター値を指定する必要があ `null`ります)。
      * MS officeテ `com.adobe.livecycle.rightsmanagement.Locale` ンプレートの選択に使用されるロケールを表す。 このパラメーター値はオプションで、指定できま `null`す。
      このメソ `protectDocument` ッドは、ポリシーで保護 `RMSecureDocumentResult` されたWordドキュメントを含むオブジェクトを返します。


1. Wordドキュメントを保存します。

   * オブジェクト `RMSecureDocumentResult` のメソッドを呼び `getProtectedDoc` 出して、ポリシーで保護されたWordドキュメントを取得します。 このメソッドは、オブジェクトを `com.adobe.idp.Document` 返します。
   * Create a `java.io.File` object and ensure that the file extension is DOC.
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出 `copyToFile` して、オブジェクトの内容をファイルにコピ `Document` ーします(メソッドによって返されたオブジェクトを使用 `Document` していることを確 `getProtectedDoc` 認します)。

**コードの例**

Document Securityサービスを使用したコードの例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAPモード）:Java APIを使用したWordドキュメントへのポリシーの適用」

### WebサービスAPIを使用したWordドキュメントへのポリシーの適用 {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Document Security API（Webサービス）を使用してWordドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Document Security Client APIオブジェクトを作成します。

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `DocumentSecurityServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。


1. Wordドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、ポリシーが適用されるWordドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、Wordドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 オブジェクトのプロパティを取得して、バイト配列 `System.IO.FileStream` のサイズを決定 `Length` します。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデ `System.IO.FileStream` ータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. Wordドキュメントに既存のポリシーを適用します。

   オブジェクトのメソッドを呼び出し、次の値を渡すこ `DocumentSecurityServiceClient` とで、Wordドキュ `protectDocument` メントにポリシーを適用します。

   * ポリシ `BLOB` ーが適用されるWordドキュメントを含むオブジェクトです。
   * ドキュメントの名前を指定するstring値。
   * ポリシーが属するポリシーセットの名前を指定するstring値です。 ポリシーセットが使 `null` 用される結果となる値 `MyPolicies` を指定できます。
   * ポリシー名を指定するstring値です。
   * ドキュメントのパブリッシャーであるユーザーのユーザーマネージャードメインの名前を表すstring値です。 このパラメーター値はオプションで、nullに設定できます(このパラメーターがnullの場合、次のパラメーター値を指定する必要があり `null`ます)。
   * ドキュメントのパブリッシャーであるユーザーマネージャーユーザーの正規名を表すstring値です。 このパラメーター値はオプションで、nullに設定できます(このパラメーターがnullの場合、前のパラメーター値を必須とし `null`ます)。
   * ロケ `RMLocale` ール値(例えば、 `RMLocale.en`)を指定する値。
   * ポリシー識別子の値の保存に使用される文字列出力パラメーターです。
   * ポリシーで保護された識別子の値の保存に使用される文字列出力パラメーターです。
   * MIMEタイプの格納に使用される文字列出力パラメーター(例： `application/doc`)。
   このメソ `protectDocument` ッドは、ポリシーで保護 `BLOB` されたWordドキュメントを含むオブジェクトを返します。

1. Wordドキュメントを保存します。

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、ポリシーで保護されたWordドキュメントのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトのデータ内容を格納 `BLOB` するバイト配列を作成 `protectDocument` します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイ `System.IO.BinaryWriter` ト配列の内 `Write` 容をWordファイルに書き込みます。

**コードの例**

Document Securityサービスを使用したコードの例については、次のクイックスタートを参照してください。

* 「Quick Start(MTOM):WebサービスAPIを使用したWordドキュメントへのポリシーの適用」

## Wordドキュメントからのポリシーの削除 {#removing-policies-from-word-documents}

ポリシーで保護されたWordドキュメントからポリシーを削除して、ドキュメントからセキュリティを削除できます。 つまり、ドキュメントをポリシーで保護しない場合です。 ポリシーで保護されたWordドキュメントを新しいポリシーで更新する場合は、ポリシーを削除して更新されたポリシーを追加する代わりに、ポリシーを切り替える方が効率的です。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-12}

ポリシーで保護されたWordドキュメントからポリシーを削除するには、次の手順を実行します。

1. プロジェクトファイルを含める
1. Document Security Client APIオブジェクトを作成します。
1. ポリシーで保護されたWordドキュメントを取得します。
1. Wordドキュメントからポリシーを削除します。
1. 保護されていないWord文書を保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Document Security Client APIオブジェクトの作成**

プログラムを使用してDocument Securityサービスの操作を実行する前に、Document Securityサービスクライアントオブジェクトを作成します。

**ポリシーで保護されたWordドキュメントの取得**

ポリシーを削除するには、ポリシーで保護されたWordドキュメントを取得する必要があります。 ポリシーで保護されていないWordドキュメントからポリシーを削除しようとすると、例外が発生します。

**Wordドキュメントからポリシーを削除します**

接続設定で管理者が指定されている場合は、ポリシーで保護されたWordドキュメントからポリシーを削除できます。 そうでない場合は、Wordドキュメントからポリシーを削除するために、ドキュメントの保護に使用さ `SWITCH_POLICY` れるポリシーに権限が含まれている必要があります。 また、AEM Formsの接続設定で指定したユーザーにも、その権限が必要です。 それ以外の場合は、例外がスローされます。

**保護されていないWord文書を保存する**

Document SecurityサービスがWordドキュメントからポリシーを削除した後、保護されていないWordドキュメントをDOCファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Wordドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-word-documents)

### Java APIを使用したWordドキュメントからのポリシーの削除 {#remove-a-policy-from-a-word-document-using-the-java-api}

Document Security API(Java)を使用して、ポリシーで保護されたWordドキュメントからポリシーを削除します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. Document Security Client APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護されたWordドキュメントの取得

   * ポリシーで保 `java.io.FileInputStream` 護されたWordドキュメントを表すオブジェクトを作成します。このオブジェクトは、コンストラクターを使用し、Wordドキュメントの場所を指定するstring値を渡すことによって作成されます。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. Wordドキュメントからポリシーを削除します

   * オブジェクト `DocumentManager` のメソッドを呼び出して、オ `RightsManagementClient` ブジェクトを作成 `getDocumentManager` します。
   * オブジェクトのメソッドを呼び出し、ポリシーで保護されたWordドキ `DocumentManager` ュメントを含むオ `removeSecurity` ブジェクトを渡すこ `com.adobe.idp.Document` とで、Wordドキュメントからポリシーを削除します。 このメソッドは、保護されて `com.adobe.idp.Document` いないWord文書を含むオブジェクトを返します。

1. 保護されていないWord文書を保存する

   * Create a `java.io.File` object and ensure that the file extension is DOC.
   * オブジェクト `Document` のメソッドを呼び出 `copyToFile` して、オブジェクトの内容をファイルにコピ `Document` ーします(メソッドによって返されたオブジェクトを使用 `Document` していることを確 `removeSecurity` 認します)。

**コードの例**

Document Securityサービスを使用したコードの例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAPモード）:Java APIを使用したWordドキュメントからのポリシーの削除」

### WebサービスAPIを使用したWordドキュメントからのポリシーの削除 {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Document Security API（Webサービス）を使用して、ポリシーで保護されたWordドキュメントからポリシーを削除します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Document Security Client APIオブジェクトの作成

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/RightsManagementService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `RightsManagementServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `RightsManagementServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `RightsManagementServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。


1. ポリシーで保護されたWordドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、ポリシーが削除された、ポリシーで保護されたWordドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、Wordドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. Wordドキュメントからポリシーを削除します

   オブジェクトのメソッドを呼び出し、ポリシーで保護されたWordドキ `RightsManagementServiceClient` ュメントを含むオ `removePolicySecurity` ブジェクトを渡すこ `BLOB` とで、Wordドキュメントからポリシーを削除します。 このメソッドは、保護されて `BLOB` いないWord文書を含むオブジェクトを返します。

1. 保護されていないWord文書を保存する

   * オブジェクトを `System.IO.FileStream` 作成するには、コンストラクターを呼び出し、保護されていないWordドキュメントのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトのデータ内容を格納 `BLOB` するバイト配列を作成 `removePolicySecurity` します。 オブジェクトのフィールドの値を取得して、バイト `BLOB` 配列を設定し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.

**コードの例**

Document Securityサービスを使用したコードの例については、次のクイックスタートを参照してください。

* 「Quick Start(MTOM):WebサービスAPIを使用したWordドキュメントからのポリシーの削除

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
