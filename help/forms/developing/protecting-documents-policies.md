---
title: ポリシーによるドキュメントの保護
seo-title: ポリシーによるドキュメントの保護
description: 'null'
seo-description: 'null'
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '15466'
ht-degree: 4%

---


# ポリシーによるドキュメントの保護 {#protecting-documents-with-policies}

**ドキュメントセキュリティサービスについて**

ドキュメントセキュリティサービスを使用すると、Adobe PDFドキュメントに動的に機密設定を適用し、ドキュメントの広範性に関係なく、ユーザーの制御を維持できます。

ドキュメントセキュリティサービスは、ユーザーがポリシーで保護されたPDFドキュメントを受信者がどのように使用するかを制御できるようにし、ユーザーの手の届く範囲を超えて情報が広がるのを防ぎます。 ユーザーは、ドキュメントを開くことのできるユーザーを指定し、そのユーザーがを使用する方法を制限し、配布後にドキュメントを監視できます。 また、ポリシーで保護されたドキュメントへのアクセスを動的に制御し、ドキュメントへのアクセスを動的に取り消すこともできます。

ドキュメントセキュリティサービスは、Microsoft Wordファイル（DOCファイル）など、他のファイルタイプも保護します。 ドキュメントセキュリティクライアントAPIを使用して、これらのファイルタイプを操作できます。 次のバージョンがサポートされています。

* Microsoft Office 2003ファイル（DOC、XLS、PPTファイル）
* Microsoft Office 2007ファイル（DOCX、XLSX、PPTXファイル）
* PTC Pro/Eファイル

次の2つの節で、Wordドキュメントの使い方を説明します。

* [Wordドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Wordドキュメントからのポリシーの削除](protecting-documents-policies.md#removing-policies-from-word-documents)

ドキュメントセキュリティサービスを使用して、次のタスクを実行できます。

* ポリシーの作成. 詳しくは、「ポリシーの [作成](protecting-documents-policies.md#creating-policies)」を参照してください。
* ポリシーを変更します。 詳しくは、「ポリシーの [変更](protecting-documents-policies.md#modifying-policies)」を参照してください。
* ポリシーの削除 詳しくは、「ポリシーの [削除](protecting-documents-policies.md#deleting-policies)」を参照してください。
* PDFドキュメントにポリシーを適用します。 詳しくは、「PDFドキュメントへのポリシーの [適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)」を参照してください。
* PDFドキュメントからポリシーを削除します。 詳しくは、「PDFドキュメントからのポリシーの [削除](protecting-documents-policies.md#removing-policies-from-pdf-documents)」を参照してください。
* ポリシーで保護されたドキュメントの検査。 詳しくは、ポリシーで保護されたPDFドキュメントの [検査を参照してください](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents)。
* PDFドキュメントへのアクセス権限を失効させます。 詳しくは、「ドキュメントへのアクセス [の取り消し](protecting-documents-policies.md#revoking-access-to-documents)」を参照してください。
* 失効したドキュメントへのアクセス権限の復元。 詳しくは、失効したドキュメントへの [アクセス権限の復元を参照してください](protecting-documents-policies.md#reinstating-access-to-revoked-documents)。
* 透かしを作成します。 詳しくは、「透かしの [作成](protecting-documents-policies.md#creating-watermarks)」を参照してください。
* イベントを検索します。 詳しくは、「イベントの [検索](protecting-documents-policies.md#searching-for-events)」を参照してください。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## ポリシーの作成 {#creating-policies}

ドキュメントセキュリティJava APIまたはWebサービスAPIを使用して、プログラムによってポリシーを作成できます。 *ポリシー* とは、ドキュメントセキュリティ設定、許可されたユーザー、使用権限などの情報を集めたものです。 様々な状況やユーザーに適したセキュリティ設定を使用して、任意の数のポリシーを作成および保存できます。

ポリシーを使用すると、次のタスクを実行できます。

* ドキュメントを開くことができるユーザーを指定します。 受信者は、組織に属するか、組織外に属することができます。
* 受信者がドキュメントを使用する方法を指定します。 AcrobatとAdobe Readerの異なる機能へのアクセスを制限できます。 これらの機能には、テキストの印刷とコピー、ドキュメントの追加、署名へのコメントの追加が含まれます。
* ポリシーで保護されたドキュメントを配布した後でも、いつでもアクセスおよびセキュリティの設定を変更できます。
* ドキュメントを配布した後、その使用状況を監視します。 ドキュメントの使用方法と使用者を確認できます。 例えば、誰かがドキュメントを開いた日時を調べることができます。

### Webサービスを使用したポリシーの作成 {#creating-a-policy-using-web-services}

WebサービスAPIを使用してポリシーを作成する場合は、ポリシーを記述した既存のPortable PortableドキュメントRights Language(PDRL)XMLファイルを参照します。 ポリシー権限とプリンシパルは、PDRLドキュメントで定義されます。 次のXMLドキュメントは、PDRLドキュメントの例です。

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
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

ポリシーを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. ポリシーの属性を設定します。
1. ポリシーエントリを作成します。
1. ポリシーを登録します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-rightsmanagement-client.jar
* namespace.jar (AEM FormsがJBossにデプロイされている場合)
* jaxb-api.jar(AEM FormsがJBossにデプロイされている場合)
* jaxb-impl.jar(AEM FormsがJBossにデプロイされている場合)
* jaxb-libs.jar(AEM FormsがJBossにデプロイされている場合)
* jaxb-xjc.jar(AEM FormsがJBossにデプロイされている場合)
* relaxingDatatype.jar(AEM FormsがJBossにデプロイされている場合)
* xsdlib.jar(AEM FormsがJBossにデプロイされている場合)
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar(AEM FormsがJBossにデプロイされていない場合は、別のJARファイルを使用)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムを使用してドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成します。

**ポリシーの属性の設定**

ポリシーを作成するには、ポリシー属性を設定します。 必須属性はポリシー名です。 ポリシー名は、ポリシーセットごとに一意にする必要があります。 ポリシーセットは、単なるポリシーの集まりです。 ポリシーが別々のポリシーセットに属する場合は、同じ名前の2つのポリシーを指定できます。 ただし、1つのポリシーセット内の2つのポリシーに同じポリシー名を付けることはできません。

設定する別の便利な属性は、有効期間です。 有効期間とは、許可された受信者がポリシーで保護されたドキュメントにアクセスできる期間です。 この属性を設定しない場合、ポリシーは常に有効です。

有効期間は、次のいずれかのオプションに設定できます。

* ドキュメントが公開されてからドキュメントにアクセスできる日数
* 終了日を過ぎるとドキュメントにアクセスできなくなります
* ドキュメントにアクセスできる特定の日付範囲
* 常に有効

開始日のみを指定できます。指定すると、開始日より後にポリシーが有効になります。 終了日のみを指定した場合、ポリシーは終了日まで有効です。 ただし、開始日と終了日の両方が定義されていない場合は、例外が発生します。

ポリシーに属する属性を設定する場合は、暗号化設定も設定できます。 これらの暗号化設定は、ポリシーがドキュメントに適用される場合に影響を受けます。 次の暗号化値を指定できます。

* **AES256**: 256ビットキーを持つAES暗号化アルゴリズムを表します。
* **AES128**: 128ビットキーを持つAES暗号化アルゴリズムを表します。
* **NoEncryption:** 暗号化なしを表します。

この `NoEncryption` オプションを指定する場合、この `PlaintextMetadata` オプションをに設定することはできません `false`。 これを行うと、例外が発生します。

>[!NOTE]
>
>設定できるその他の属性について詳しくは、『 `Policy` AEM FormsAPIリファレンス [](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』のインターフェイスの説明を参照してください。

**ポリシーエントリの作成**

ポリシーエントリは、プリンシパル（グループとユーザー、権限）をポリシーに添付します。 ポリシーには少なくとも1つのポリシーエントリが必要です。 例えば、次のタスクを実行するとします。

* ポリシーエントリを作成して登録します。このエントリを使用すると、オンライン時にグループがドキュメントを表示するだけで、受信者はポリシーエントリをコピーできなくなります。
* ポリシーエントリをポリシーに添付します。
* Acrobatを使用して、ポリシーでドキュメントを保護します。

これらの操作により、受信者はドキュメントをオンラインで表示することのみができ、コピーすることができません。 セキュリティが解除されるまで、ドキュメントはセキュリティで保護された状態のままです。

**ポリシーの登録**

新しいポリシーを使用するには、そのポリシーを登録する必要があります。 登録したポリシーは、ドキュメントの保護に使用できます。

### Java APIを使用したポリシーの作成 {#create-a-policy-using-the-java-api}

ドキュメントセキュリティAPI(Java)を使用してポリシーを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーの属性を設定します。

   * オブジェクトのスタティック `Policy` メソッドを呼び出して、 `InfomodelObjectFactory``createPolicy` オブジェクトを作成します。 このメソッドは、 `Policy` オブジェクトを返します。
   * オブジェクトの `Policy` メソッドを呼び出し、ポリシー名を指定する文字列値を渡して、ポリシーの名前属性を設定し `setName` ます。
   * オブジェクトの `Policy` メソッドを呼び出し、ポリシーの説明を指定する文字列値を渡して、ポリシーの説明を設定し `setDescription` ます。
   * オブジェクトの `Policy``setPolicySetName` メソッドを呼び出し、ポリシーセット名を指定する文字列値を渡して、新しいポリシーが属するポリシーセットを設定します。 (このパラメーター値 `null` を指定すると、ポリシーが *My Policies* （マイポリシー）ポリシーセットに追加されます)。
   * オブジェクトの静的な `InfomodelObjectFactory``createValidityPeriod` メソッドを呼び出して、ポリシーの有効期間を作成します。 このメソッドは、 `ValidityPeriod` オブジェクトを返します。
   * ポリシーで保護されたドキュメントにアクセスする日数を設定するには、 `ValidityPeriod` オブジェクトの `setRelativeExpirationDays` メソッドを呼び出し、日数を指定する整数値を渡します。
   * オブジェクトのメソッドを呼び出し、オブジェクトを渡すことで、 `Policy` ポリシーの有効期間 `setValidityPeriod` を設定し `ValidityPeriod` ます。

1. ポリシーエントリを作成します。

   * オブジェクトの静的なメソッドを呼び出して、ポリシー `InfomodelObjectFactory` エントリを作成し `createPolicyEntry` ます。 このメソッドは、 `PolicyEntry` オブジェクトを返します。
   * オブジェクトの静的なメソッドを呼び出して、ポリシーの権限 `InfomodelObjectFactory` を指定し `createPermission` ます。 権限を表すインター `Permission` フェイスに属する静的データメンバーを渡します。 このメソッドは、 `Permission` オブジェクトを返します。 例えば、ポリシーで保護されたPDFドキュメントからのデータのコピーをユーザーに許可する権限を追加するには、を渡し `Permission.COPY`ます。 （追加する権限ごとに、この手順を繰り返します）。
   * オ追加ブジェクトのメソッドを呼び出し、オブジェクトを渡すことで、ポリシーエントリに対する権限を与え `PolicyEntry``addPermission``Permission` ます。 (作成した各 `Permission` オブジェクトに対して、この手順を繰り返します)。
   * オブジェクトの静的なメソッドを呼び出して、ポリシー `InfomodelObjectFactory` プリンシパルを作成し `createSpecialPrincipal` ます。 プリンシパルを表す `InfomodelObjectFactory` オブジェクトに属するデータメンバーを渡します。 このメソッドは、 `Principal` オブジェクトを返します。 例えば、ドキュメントのパブリッシャーをプリンシパルとして追加するには、を渡し `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`ます。
   * オ追加ブジェクトの `PolicyEntry` メソッドを呼び出し、オブジェクトを渡すことにより、ポリシーエントリのプリンシパル `setPrincipal`になり `Principal` ます。
   * オ追加ブジェクトのメソッドを呼び出し、オブジェクトを渡すことで、ポリシーに対するポリシーエントリを指定し `Policy``addPolicyEntry``PolicyEntry` ます。

1. ポリシーを登録します。

   * オブジェクトの `PolicyManager` メソッドを呼び出して、 `DocumentSecurityClient` オブジェクトを作成 `getPolicyManager` します。
   * オブジェクトの `PolicyManager``registerPolicy` メソッドを呼び出し、次の値を渡して、ポリシーを登録します。

      * 登録するポリシーを表す `Policy` オブジェクトです。
   * ポリシーが属するポリシーセットを表すstring値です。

   接続設定内でAEM forms管理者アカウントを使用して `DocumentSecurityClient` オブジェクトを作成する場合は、 `registerPolicy` メソッドの呼び出し時にポリシーセット名を指定します。 ポリシーセットの `null` 値を渡すと、そのポリシーは管理者の「 *マイポリシー* 」ポリシーセットに作成されます。

   ドキュメントセキュリティユーザーを接続設定内で使用する場合は、ポリシーのみを受け入れる、過負荷の `registerPolicy` メソッドを呼び出すことができます。 つまり、ポリシーセット名を指定する必要はありません。 ただし、このポリシーは「 *マイポリシー*」という名前のポリシーセットに追加されます。 このポリシーセットに新しいポリシーを追加しない場合は、この `registerPolicy` メソッドを呼び出すときにポリシーセット名を指定します。

   >[!NOTE]
   >
   >ポリシーを作成する場合は、既存のポリシーセットを参照します。 存在しないポリシーセットを指定すると、例外が発生します。

ドキュメントセキュリティサービスを使用したコードの例については、次を参照してください。

* 「クイック開始（SOAPモード）: Java APIを使用したポリシーの作成»

### WebサービスAPIを使用したポリシーの作成 {#create-a-policy-using-the-web-service-api}

ドキュメントセキュリティAPI（Webサービス）を使用してポリシーを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/RightsManagementService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `RightsManagementServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `RightsManagementServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `RightsManagementServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。


1. ポリシーの属性を設定します。

   * コンストラクタを使用して `PolicySpec` オブジェクトを作成します。
   * オブジェクトの `PolicySpec``name` データメンバーに文字列値を割り当てて、ポリシー名を設定します。
   * オブジェクトの `PolicySpec``description` データメンバーに文字列値を割り当てて、ポリシーの説明を設定します。
   * オブジェクトの `PolicySpec``policySetName` データメンバに文字列値を割り当てて、ポリシーが属するポリシーセットを設定します。 既存のポリシーセット名を指定する必要があります。 (このパラメーター値 `null` を指定すると、ポリシーが「 *マイポリシー*」に追加されます)。
   * オブジェクトの `PolicySpec``offlineLeasePeriod` データメンバに整数値を割り当てて、ポリシーのオフラインリース期間を設定します。
   * PDRL XMLデータを表す文字列値を使用して、 `PolicySpec` オブジェクトの `policyXml` データメンバーを設定します。 このタスクを実行するには、コンストラクタを使用して.NET `StreamReader` オブジェクトを作成します。 ポリシーを表すPDRL XMLファイルの場所をコンストラクターに渡し `StreamReader` ます。 次に、 `StreamReader` オブジェクトの `ReadLine` メソッドを呼び出し、戻り値を文字列変数に割り当てます。 メソッドがnullを返すまで、 `StreamReader` オブジェクトを繰り返し処理し `ReadLine` ます。 文字列変数を `PolicySpec` オブジェクトの `policyXml` データメンバに割り当てます。

1. ポリシーエントリを作成します。

   ドキュメントセキュリティWebサービスAPIを使用してポリシーを作成する場合、ポリシーエントリを作成する必要はありません。 ポリシーエントリは、PDRLドキュメントで定義されます。

1. ポリシーを登録します。

   オブジェクトの `DocumentSecurityServiceClient``registerPolicy` メソッドを呼び出し、次の値を渡して、ポリシーを登録します。

   * 登録するポリシーを表す `PolicySpec` オブジェクトです。
   * ポリシーが属するポリシーセットを表すstring値です。 ポリシーをMyPolices `null` ポリシーセットに追加する結果となる ** 値を指定できます。

   接続設定内でAEM forms管理者アカウントを使用して `DocumentSecurityClient` オブジェクトを作成する場合は、 `registerPolicy` メソッドの呼び出し時にポリシーセット名を指定します。

   接続設定内でドキュメントのSecurityDocument Securityユーザーを使用する場合は、ポリシーのみを受け入れる、過負荷の `registerPolicy` メソッドを呼び出すことができます。 つまり、ポリシーセット名を指定する必要はありません。 ただし、このポリシーは「 *マイポリシー*」という名前のポリシーセットに追加されます。 このポリシーセットに新しいポリシーを追加しない場合は、この `registerPolicy` メソッドを呼び出すときにポリシーセット名を指定します。

   >[!NOTE]
   >
   >ポリシーを作成し、ポリシーセットを指定する場合は、既存のポリシーセットを必ず指定してください。 存在しないポリシーセットを指定すると、例外が発生します。

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM): WebサービスAPIを使用したポリシーの作成」
* &quot;クイック開始(SwaRef): WebサービスAPIを使用したポリシーの作成」

## ポリシーの変更 {#modifying-policies}

ドキュメントセキュリティJava APIまたはWebサービスAPIを使用して、既存のポリシーを変更できます。 既存のポリシーを変更するには、そのポリシーを取得し、変更してから、サーバー上のポリシーを更新します。 例えば、既存のポリシーを取得し、その有効期間を延長したとします。 変更を有効にする前に、ポリシーを更新する必要があります。

ビジネス要件が変更され、ポリシーにこれらの要件が反映されなくなった場合は、ポリシーを変更できます。 新しいポリシーを作成する代わりに、既存のポリシーを更新するだけで済みます。

Webサービス（例えば、JAX-WSで作成されたJavaプロキシクラスを使用）を使用してポリシー属性を変更するには、ポリシーがドキュメントセキュリティサービスに登録されていることを確認する必要があります。 その後、メソッドを使用して既存のポリシーを参照し、該当するメソッドを使用してポリシー属性を変更でき `PolicySpec.getPolicyXml` ます。 例えば、 `PolicySpec.setOfflineLeasePeriod` メソッドを呼び出して、オフラインリース期間を変更できます。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

既存のポリシーを変更するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. 既存のポリシーを取得します。
1. ポリシー属性を変更します。
1. ポリシーを更新します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムを使用してドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、 `RightsManagementClient` オブジェクトを作成します。 ドキュメントセキュリティWebサービスAPIを使用している場合は、 `RightsManagementServiceService` オブジェクトを作成します。

**既存のポリシーの取得**

既存のポリシーを変更するには、そのポリシーを取得する必要があります。 ポリシーを取得するには、ポリシー名とポリシーが属するポリシーセットを指定します。 ポリシーセット名の `null` 値を指定した場合、ポリシーは「 *マイポリシー* 」ポリシーセットから取得されます。

**ポリシーの属性の設定**

ポリシーを変更するには、ポリシー属性の値を変更します。 変更できない唯一のポリシー属性はname属性です。 例えば、ポリシーのオフラインリース期間を変更するには、ポリシーのオフラインリース期間属性の値を変更します。

Webサービスを使用してポリシーのオフラインリース期間を変更する場合、インターフェイス上の `offlineLeasePeriod` フィールドは無視さ `PolicySpec` れます。 オフラインリース期間を更新するには、PDRL XMLドキュメントの `OfflineLeasePeriod` 要素を変更します。 次に、インターフェイスのデータメンバを使用して、更新されたPDRL XMLドキュメント `PolicySpec` を参照し `policyXML` ます。

>[!NOTE]
>
>設定できるその他の属性について詳しくは、『 `Policy` AEM FormsAPIリファレンス [](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』のインターフェイスの説明を参照してください。

**ポリシーの更新**

ポリシーに対して行った変更を有効にする前に、ドキュメントセキュリティサービスを使用してポリシーを更新する必要があります。 ドキュメントを保護するポリシーに対する変更は、次回、ポリシーで保護されたドキュメントがドキュメントセキュリティサービスと同期されたときに更新されます。

### Java APIを使用した既存のポリシーの変更 {#modify-existing-policies-using-the-java-api}

ドキュメントセキュリティAPI(Java)を使用して既存のポリシーを変更します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 既存のポリシーを取得します。

   * オブジェクトの `PolicyManager` メソッドを呼び出して、 `RightsManagementClient` オブジェクトを作成 `getPolicyManager` します。
   * オブジェクトの `Policy` メソッドを呼び出し、次の値を渡すことで、更新するポリシーを表す `PolicyManager``getPolicy` オブジェクトを作成します。」

      * ポリシーが属するポリシーセット名を表すstring値です。 ポリシーセット `null` を使用する結果を指定でき `MyPolicies` ます。
      * ポリシー名を表すstring値です。

1. ポリシーの属性を設定します。

   ビジネス要件に合わせてポリシーの属性を変更します。 例えば、ポリシーのオフラインリース期間を変更するには、 `Policy` オブジェクトの `setOfflineLeasePeriod` メソッドを呼び出します。

1. ポリシーを更新します。

   オブジェクトのメソッドを呼び出して、 `PolicyManager` ポリシーを更新し `updatePolicy` ます。 更新するポリシーを表す `Policy` オブジェクトを渡します。

**コードの例**

ドキュメントセキュリティサービスを使用したコード例については、クイック開始（SOAPモード）を参照してください。 「Java API」セクションを使用してポリシーを変更する。

### WebサービスAPIを使用した既存のポリシーの変更 {#modify-existing-policies-using-the-web-service-api}

ドキュメントセキュリティAPI （Webサービス）を使用して既存のポリシーを変更します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/RightsManagementService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `RightsManagementServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `RightsManagementServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `RightsManagementServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。


1. 既存のポリシーを取得します。

   オブジェクトの `PolicySpec` メソッドを呼び出し、次の値を渡して、変更するポリシーを表す `RightsManagementServiceClient``getPolicy` オブジェクトを作成します。

   * ポリシーが属するポリシーセット名を指定するstring値です。 ポリシーセット `null` を使用する結果を指定でき `MyPolicies` ます。
   * ポリシーの名前を指定するstring値です。

1. ポリシーの属性を設定します。

   ビジネス要件に合わせてポリシーの属性を変更します。

1. ポリシーを更新します。

   オブジェクトの `RightsManagementServiceClient` メソッドを呼び出し、更新するポリシーを表す `updatePolicyFromSDK``PolicySpec` オブジェクトを渡して、ポリシーを更新します。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM): WebサービスAPIを使用したポリシーの変更」
* &quot;クイック開始(SwaRef): WebサービスAPIを使用したポリシーの変更」

## ポリシーの削除 {#deleting-policies}

ドキュメントセキュリティJava APIまたはWebサービスAPIを使用して、既存のポリシーを削除できます。 ポリシーを削除すると、ドキュメントの保護にポリシーを使用できなくなります。 ただし、ポリシーを使用している既存のポリシーで保護されたドキュメントは、引き続き保護されます。 新しいポリシーが利用可能になった場合は、ポリシーを削除できます。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

既存のポリシーを削除するには、次の手順を実行します。

1. プロジェクトファイルを含める
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. ポリシーを削除します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムによってドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、 `RightsManagementClient` オブジェクトを作成します。 ドキュメントセキュリティWebサービスAPIを使用している場合は、 `RightsManagementServiceService` オブジェクトを作成します。

**ポリシーの削除**

ポリシーを削除するには、削除するポリシーと、そのポリシーが属するポリシーセットを指定します。 AEM Formsの呼び出しに使用される設定を持つユーザーは、ポリシーを削除する権限が必要です。 それ以外の場合は、例外が発生します。 同様に、存在しないポリシーを削除しようとすると、例外が発生します。

### Java APIを使用したポリシーの削除 {#delete-policies-using-the-java-api}

ドキュメントセキュリティAPI(Java)を使用してポリシーを削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーを削除します。

   * オブジェクトの `PolicyManager` メソッドを呼び出して、 `RightsManagementClient` オブジェクトを作成 `getPolicyManager` します。
   * オブジェクトの `PolicyManager``deletePolicy` メソッドを呼び出し、次の値を渡して、ポリシーを削除します。

      * ポリシーが属するポリシーセット名を指定するstring値です。 ポリシーセット `null` を使用する結果を指定でき `MyPolicies` ます。
      * 削除するポリシーの名前を指定するstring値です。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（SOAPモード）: Java APIを使用したポリシーの削除」

### WebサービスAPIを使用したポリシーの削除 {#delete-policies-using-the-web-service-api}

ドキュメントセキュリティAPI （Webサービス）を使用してポリシーを削除する：

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/RightsManagementService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `RightsManagementServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `RightsManagementServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `RightsManagementServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。


1. ポリシーを削除します。

   Delete a policy by invoking the `RightsManagementServiceClient` object’s `deletePolicy` method and passing the following values:

   * ポリシーが属するポリシーセット名を指定するstring値です。 ポリシーセット `null` を使用する結果を指定でき `MyPolicies` ます。
   * 削除するポリシーの名前を指定するstring値です。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM): WebサービスAPIを使用したポリシーの削除」
* &quot;クイック開始(SwaRef): WebサービスAPIを使用したポリシーの削除」

## PDFドキュメントへのポリシーの適用 {#applying-policies-to-pdf-documents}

ドキュメントを保護するために、PDFドキュメントにポリシーを適用できます。 ポリシーをPDFドキュメントに適用すると、ドキュメントへのアクセスを制限できます。 ドキュメントが既にポリシーで保護されている場合は、ドキュメントにポリシーを適用できません。

ドキュメントが開いている間は、テキストの印刷やコピー、変更、ドキュメントや注釈の追加など、AcrobatおよびAdobe Readerの機能へのアクセスを制限することもできます。 また、ドキュメントにアクセスしたくなくなった場合に、ポリシーで保護されたPDFドキュメントを無効にすることもできます。

ポリシーで保護されたドキュメントを配布した後、その使用を監視できます。 つまり、ドキュメントの使用状況と使用者を確認できます。 例えば、誰かがドキュメントを開いた日時を調べることができます。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-3}

PDFドキュメントにポリシーを適用するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. ポリシーが適用されるPDFドキュメントを取得します。
1. 既存のポリシーをPDFドキュメントに適用します。
1. ポリシーで保護されたPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムを使用してドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成します。 Java APIを使用している場合は、 `DocumentSecurityClient` オブジェクトを作成します。 ドキュメントセキュリティWebサービスAPIを使用している場合は、 `DocumentSecurityServiceService` オブジェクトを作成します。

**PDFドキュメントの取得**

ポリシーを適用するために、PDFドキュメントを取得できます。 PDFドキュメントにポリシーを適用すると、ドキュメントの使用時にユーザーが制限されます。 例えば、オフライン時にドキュメントを開くことをポリシーで有効にしていない場合、ドキュメントを開くには、ユーザーがオンラインである必要があります。

**PDFドキュメントへの既存のポリシーの適用**

ポリシーをPDFドキュメントに適用するには、既存のポリシーを参照し、ポリシーが属するポリシーセットを指定します。 接続プロパティを設定するユーザーは、指定したポリシーにアクセスできる必要があります。 そうでない場合は、例外が発生します。

**PDFドキュメントの保存**

ドキュメントセキュリティサービスがポリシーをPDFドキュメントに適用した後、ポリシーで保護されたPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ドキュメントへのアクセスの失効](protecting-documents-policies.md#revoking-access-to-documents)

### Java APIを使用したPDFドキュメントへのポリシーの適用 {#apply-a-policy-to-a-pdf-document-using-the-java-api}

ドキュメントセキュリティAPI(Java)を使用してPDFドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントを取得します。

   * PDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成するには、コンストラクターを使用します。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 既存のポリシーをPDFドキュメントに適用します。

   * オブジェクトの `DocumentManager` メソッドを呼び出して、 `RightsManagementClient` オブジェクトを作成 `getDocumentManager` します。
   * オブジェクトの `DocumentManager` メソッドを呼び出し、次の値を渡して、ポリシーをPDFドキュメントに適用し `protectDocument` ます。

      * ポリシーが適用されるPDFドキュメントが含まれる `com.adobe.idp.Document` オブジェクトです。
      * ドキュメントの名前を指定するstring値です。
      * ポリシーが属するポリシーセットの名前を指定するstring値です。 ポリシーセットを使用する結果として得られる `null` 値を指定でき `MyPolicies` ます。
      * ポリシー名を指定するstring値です。
      * ドキュメントのパブリッシャであるユーザーのUser Managerドメインの名前を表すstring値です。 このパラメーター値はオプションであり、nullにすることができます（このパラメーターがnullの場合、次のパラメーター値はnullにする必要があります）。
      * ドキュメントのパブリッシャであるUser Managerユーザーの正規名の名前を表すstring値です。 このパラメーターの値はオプションで、値を指定できます `null` (このパラメーターがnullの場合、前のパラメーターの値にする必要があり `null`ます)。
      * MS Officeテンプレートの選択に使用されるロケールを表す `com.adobe.livecycle.rightsmanagement.Locale` 。 このパラメーター値はオプションで、PDFドキュメントでは使用されません。 PDFドキュメントを保護するには、を指定し `null`ます。

      ポリシーで保護されたPDFドキュメントを含む `protectDocument``RMSecureDocumentResult` オブジェクトを返します。


1. PDFドキュメントを保存します。

   * オブジェクトの `RMSecureDocumentResult``getProtectedDoc` メソッドを呼び出して、ポリシーで保護されたPDFドキュメントを取得します。 このメソッドは、 `com.adobe.idp.Document` オブジェクトを返します。
   * Create a `java.io.File` object and ensure that the file extension is PDF.
   * オブジェクトのメ `com.adobe.idp.Document` ソッドを呼び出して、 `copyToFile` オブジェクトの内容をファイルにコピーします(メソッドから返された `Document``Document``getProtectedDoc` オブジェクトを必ず使用してください)。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（EJBモード）: Java APIを使用したPDFドキュメントへのポリシーの適用」
* 「クイック開始（SOAPモード）: Java APIを使用したPDFドキュメントへのポリシーの適用」

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントへのポリシーの適用 {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

ドキュメントセキュリティAPI（Webサービス）を使用してPDFドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをFormsサービス(例えば、 `http://localhost:8080/soap/services/RightsManagementService?WSDL`.)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `RightsManagementServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `RightsManagementServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `RightsManagementServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。


1. PDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、ポリシーが適用されるPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 オブジェクトのプロパティを取得して、バイト配列のサイズ `System.IO.FileStream` を決定し `Length` ます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. 既存のポリシーをPDFドキュメントに適用します。

   オブジェクトの `RightsManagementServiceClient` メソッドを呼び出し、次の値を渡して、ポリシーをPDFドキュメントに適用し `protectDocument` ます。

   * ポリシーが適用されるPDFドキュメントが含まれる `BLOB` オブジェクトです。
   * ドキュメントの名前を指定するstring値です。
   * ポリシーが属するポリシーセットの名前を指定するstring値です。 ポリシーセットを使用する結果として得られる `null` 値を指定でき `MyPolicies` ます。
   * ポリシー名を指定するstring値です。
   * ドキュメントのパブリッシャであるユーザーのUser Managerドメインの名前を表すstring値です。 このパラメーターの値はオプションであり、nullにすることができます(このパラメーターがnullの場合、次のパラメーターの値にする必要があり `null`ます)。
   * ドキュメントのパブリッシャであるUser Managerユーザーの正規名の名前を表すstring値です。 このパラメーターの値はオプションであり、nullにすることができます(このパラメーターがnullの場合、前のパラメーターの値を `null`必ず指定してください)。
   * ロケール値を指定する `RMLocale` 値(例えば、 `RMLocale.en`)。
   * ポリシー識別子の値を保存するために使用される文字列出力パラメーターです。
   * ポリシーで保護された識別子の値の保存に使用される文字列出力パラメーターです。
   * MIMEタイプの格納に使用される文字列出力パラメーター(例： `application/pdf`)。

   ポリシーで保護されたPDFドキュメントを含む `protectDocument``BLOB` オブジェクトを返します。

1. PDFドキュメントを保存します。

   * コンストラクターを呼び出し、ポリシーで保護されたPDFドキュメントのファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトのデータ内容を格納するバイト配列を作成し `protectDocument` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM): WebサービスAPIを使用したPDFドキュメントへのポリシーの適用」
* &quot;クイック開始(SwaRef): WebサービスAPIを使用したPDFドキュメントへのポリシーの適用」

## PDFドキュメントからのポリシーの削除 {#removing-policies-from-pdf-documents}

ポリシーで保護されたドキュメントからポリシーを削除して、ドキュメントからセキュリティを削除できます。 つまり、ドキュメントをポリシーで保護したくない場合です。 ポリシーで保護されたドキュメントを新しいポリシーで更新する場合は、ポリシーを削除して更新されたポリシーを追加する代わりに、ポリシーを切り替える方が効率的です。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-4}

ポリシーで保護されたPDFドキュメントからポリシーを削除するには、次の手順を実行します。

1. プロジェクトファイルを含める
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. ポリシーで保護されたPDFドキュメントを取得します。
1. ポリシーをPDFドキュメントから削除します。
1. 保護されていないPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムを使用してドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成します。

**ポリシーで保護されたPDFドキュメントの取得**

ポリシーを削除するために、ポリシーで保護されたPDFドキュメントを取得できます。 ポリシーで保護されていないPDFドキュメントからポリシーを削除しようとすると、例外が発生します。

**PDFドキュメントからのポリシーの削除**

接続設定で管理者が指定されている場合は、ポリシーで保護されたPDFドキュメントからポリシーを削除できます。 ポリシーがない場合は、PDFドキュメントからポリシーを削除するには、ドキュメントを保護するために使用されるポリシーに `SWITCH_POLICY` 権限が含まれている必要があります。 また、AEM Forms接続設定で指定したユーザーにも、その権限が必要です。 それ以外の場合は、例外が発生します。

**保護されていないPDFドキュメントの保存**

ドキュメントセキュリティサービスがPDFドキュメントからポリシーを削除した後、保護されていないPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Java APIを使用したPDFドキュメントからのポリシーの削除 {#remove-a-policy-from-a-pdf-document-using-the-java-api}

ドキュメントセキュリティAPI(Java)を使用して、ポリシーで保護されたPDFドキュメントからポリシーを削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護されたPDFドキュメントを取得します。

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡すことで、ポリシーで保護されたPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ポリシーをPDFドキュメントから削除します。

   * オブジェクトの `DocumentManager` メソッドを呼び出して、 `DocumentSecurityClient` オブジェクトを作成 `getDocumentManager` します。
   * オブジェクトのドキュメントを呼び出し、ポリシーで保護されたPDFドキュメントを含む `DocumentManager``removeSecurity``com.adobe.idp.Document` オブジェクトを渡すことで、PDFからポリシーを削除します。 このメソッドは、保護されていないPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトを返します。

1. 保護されていないPDFドキュメントを保存します。

   * Create a `java.io.File` object and ensure that the file extension is PDF.
   * オブジェクトのメ `Document` ソッドを呼び出して、 `copyToFile` オブジェクトの内容をファイルにコピーします(メソッドから返された `Document``Document``removeSecurity` オブジェクトを必ず使用してください)。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（SOAPモード）: Java APIを使用したPDFドキュメントからのポリシーの削除»

### WebサービスAPIを使用したポリシーの削除 {#remove-a-policy-using-the-web-service-api}

ドキュメントセキュリティAPI（Webサービス）を使用して、ポリシーで保護されたPDFドキュメントからポリシーを削除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/RightsManagementService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `DocumentSecurityServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。


1. ポリシーで保護されたPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、ポリシーが削除された、ポリシーで保護されたPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. ポリシーをPDFドキュメントから削除します。

   オブジェクトのドキュメントを呼び出し、ポリシーで保護されたPDFドキュメントを含む `DocumentSecurityServiceClient``removePolicySecurity``BLOB` オブジェクトを渡すことで、PDFメソッドからポリシーを削除します。 このメソッドは、保護されていないPDFドキュメントを含む `BLOB` オブジェクトを返します。

1. 保護されていないPDFドキュメントを保存します。

   * コンストラクターを呼び出し、保護されていないPDFドキュメントのファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトのデータ内容を格納するバイト配列を作成し `removePolicySecurity` ます。 オブジェクトのフィールドの値を取得して、 `BLOB` バイト配列を設定し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM): WebサービスAPIを使用したPDFドキュメントからのポリシーの削除」
* &quot;クイック開始(SwaRef): WebサービスAPIを使用したPDFドキュメントからのポリシーの削除」

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## ドキュメントへのアクセスの失効 {#revoking-access-to-documents}

ポリシーで保護されたPDFドキュメントへのアクセスを無効にすると、そのドキュメントのすべてのコピーにユーザーからアクセスできなくなります。 失効したPDFドキュメントを開こうとすると、指定したURLにリダイレクトされ、変更されたドキュメントを表示できます。 ユーザーのリダイレクト先のURLは、プログラムで指定する必要があります。 ドキュメントへのアクセスを無効にすると、ポリシーで保護されたドキュメントを次回オンラインで開いたときに、ドキュメントセキュリティサービスとの同期が行われます。

ドキュメントへのアクセスを取り消す機能により、セキュリティが強化されます。 例えば、新しいバージョンのドキュメントが利用可能で、古いバージョンを表示するユーザーが不要になったとします。 この場合、古いドキュメントへのアクセスを取り消すことができ、アクセスを元に戻さない限り、誰もドキュメントに表示できません。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-5}

ポリシーで保護されたドキュメントを失効させるには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. ポリシーで保護されたPDFドキュメントを取得します。
1. ポリシーで保護されたドキュメントを失効させます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムによってドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成する必要があります。

**ポリシーで保護されたPDFドキュメントの取得**

失効させるには、ポリシーで保護されたPDFドキュメントを取得する必要があります。 失効済みのドキュメント、またはポリシーで保護されたドキュメントでないは失効できません。

ポリシーで保護されたドキュメントのライセンス識別子の値がわかっている場合は、ポリシーで保護されたPDFドキュメントを取得する必要はありません。 ただし、ほとんどの場合、ライセンス識別子の値を取得するには、PDFドキュメントを取得する必要があります。

**ポリシーで保護されたドキュメントの失効**

ポリシーで保護されたドキュメントを取り消すには、ポリシーで保護されたドキュメントのライセンスIDを指定します。 また、失効したドキュメントを開こうとしたときにドキュメントが表示できるユーザーのURLを指定できます。 つまり、古いドキュメントが取り消されたとします。 失効したドキュメントを開こうとすると、失効したドキュメントではなく更新されたドキュメントが表示されます。

>[!NOTE]
>
>既に失効済みのドキュメントを失効しようとすると、例外が発生します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[取り消されたドキュメントへのアクセス権の復元](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Java APIを使用したドキュメントへのアクセス権限の失効 {#revoke-access-to-documents-using-the-java-api}

ドキュメントセキュリティAPI(Java)を使用して、ポリシーで保護されたPDFドキュメントへのアクセス権限を失効させます。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護されたPDFドキュメントの取得

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡すことで、ポリシーで保護されたPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ポリシーで保護されたドキュメントの失効

   * オブジェクトの `DocumentManager` メソッドを呼び出して、 `DocumentSecurityClient` オブジェクトを作成 `getDocumentManager` します。
   * オブジェクトのメソッドを呼び出して、ポリシーで保護されたドキュメントのライセンス識別子の値 `DocumentManager` を取得し `getLicenseId` ます。 ポリシーで保護されたドキュメントを表す `com.adobe.idp.Document` オブジェクトを渡します。 このメソッドは、ライセンス識別子の値を表すstring値を返します。
   * オブジェクトの `LicenseManager` メソッドを呼び出して、 `DocumentSecurityClient` オブジェクトを作成 `getLicenseManager` します。
   * オブジェクトのメソッドを呼び出し、次の値を渡して、ポリシーで保護された `LicenseManager` ドキュメントを失効させ `revokeLicense` ます。

      * ポリシーで保護されたドキュメントのライセンス識別子の値を指定するstring値( `DocumentManager` オブジェクトの `getLicenseId` メソッドの戻り値を指定)。
      * ドキュメントを取り消す理由を指定するインター `License` フェイスの静的データメンバーです。 例えば、を指定でき `License.DOCUMENT_REVISED`ます。
      * 改訂済みドキュメントの場所を指定する `java.net.URL` 値。 ユーザーを別のURLにリダイレクトしたくない場合は、を渡すことができ `null`ます。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（SOAPモード）: Java APIを使用したドキュメントの取り消し»

### WebサービスAPIを使用したドキュメントへのアクセス権限の失効 {#revoke-access-to-documents-using-the-web-service-api}

ドキュメントセキュリティAPI（Webサービス）を使用して、ポリシーで保護されたPDFドキュメントへのアクセス権限を失効させます。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトの作成

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/RightsManagementService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `DocumentSecurityServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。


1. ポリシーで保護されたPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、失効されたポリシーで保護されたPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、失効するポリシーで保護されたPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. ポリシーで保護されたドキュメントの失効

   * オブジェクトのメソッドを呼び出し、ポリシーで保護されたドキュメントを表す `DocumentSecurityServiceClient` オブジェクトを渡すことで、ポリシーで保護されたドキュメントのライセンス識別子の値を取得し `getLicenseID``BLOB` ます。 このメソッドは、ライセンス識別子を表すstring値を返します。
   * オブジェクトのメソッドを呼び出し、次の値を渡して、ポリシーで保護された `DocumentSecurityServiceClient` ドキュメントを失効させ `revokeLicense` ます。

      * ポリシーで保護されたドキュメントのライセンス識別子の値を指定するstring値( `DocumentSecurityServiceService` オブジェクトの `getLicenseId` メソッドの戻り値を指定)。
      * ドキュメントを取り消す理由を指定する、 `Reason` enumの静的データメンバです。 例えば、を指定でき `Reason.DOCUMENT_REVISED`ます。
      * 変更されたドキュメントの場所のURL位置を指定する `string` 値。 ユーザーを別のURLにリダイレクトしたくない場合は、を渡すことができ `null`ます。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM): WebサービスAPIを使用したドキュメントの取り消し
* &quot;クイック開始(SwaRef): WebサービスAPIを使用したドキュメントの取り消し

**関連トピック**

[Wordドキュメントからのポリシーの削除](protecting-documents-policies.md#removing-policies-from-word-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 取り消されたドキュメントへのアクセス権の復元 {#reinstating-access-to-revoked-documents}

失効したPDFドキュメントへのアクセス権限を復元できるので、失効したドキュメントのすべてのコピーにユーザーがアクセスできます。 ユーザーが失効した復元済みドキュメントを開くと、そのドキュメントを表示できます。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-6}

失効したPDFドキュメントへのアクセス権限を復元するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. 失効したPDFドキュメントのライセンスIDを取得します。
1. 失効したPDFドキュメントへのアクセス権限を復元しました。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムによってドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、 `DocumentSecurityClient` オブジェクトを作成します。 ドキュメントセキュリティWebサービスAPIを使用している場合は、 `DocumentSecurityServiceService` オブジェクトを作成します。

**失効したPDFドキュメントのライセンスIDを取得します**

失効したPDFドキュメントを復元するには、失効したPDFドキュメントのライセンスIDを取得する必要があります。 ライセンス識別子の値を取得した後、失効したドキュメントを復元できます。 失効していないドキュメントを復元しようとすると、例外が発生します。

**失効したPDFドキュメントへのアクセス権限の復元**

失効したPDFドキュメントへのアクセス権限を復元するには、失効したドキュメントのライセンスIDを指定する必要があります。 失効していないPDFドキュメントへのアクセス権限を復元しようとすると、例外が発生します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[ドキュメントへのアクセスの失効](protecting-documents-policies.md#revoking-access-to-documents)

### Java APIを使用した失効したドキュメントへのアクセス権の復元 {#reinstate-access-to-revoked-documents-using-the-java-api}

ドキュメントセキュリティAPI(Java)を使用して、失効したドキュメントへのアクセス権限を復元する：

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 失効したPDFドキュメントのライセンスIDを取得します。

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、失効したPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * オブジェクトの `DocumentManager` メソッドを呼び出して、 `DocumentSecurityClient` オブジェクトを作成 `getDocumentManager` します。
   * オブジェクトのメソッドを呼び出し、失効したドキュメントを表す `DocumentManager` オブジェクトを渡すことで、失効したドキュメントのライセンス識別子の値を取得し `getLicenseId``com.adobe.idp.Document` ます。 このメソッドは、ライセンス識別子を表すstring値を返します。

1. 失効したPDFドキュメントへのアクセス権限を復元しました。

   * オブジェクトの `LicenseManager` メソッドを呼び出して、 `DocumentSecurityClient` オブジェクトを作成 `getLicenseManager` します。
   * オブジェクトの `LicenseManager``unrevokeLicense` メソッドを呼び出し、取り消されたドキュメントのライセンス識別子の値を渡すことで、取り消されたPDFドキュメントへのアクセス権限を復元します。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（SOAPモード）: WebサービスAPIを使用した、失効したドキュメントへのアクセス権限の復元」

### WebサービスAPIを使用した、失効したドキュメントへのアクセス権の復元 {#reinstate-access-to-revoked-documents-using-the-web-service-api}

ドキュメントセキュリティAPI（Webサービス）を使用して、失効したドキュメントへのアクセス権限を復元する：

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/RightsManagementService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `DocumentSecurityServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。


1. 失効したPDFドキュメントのライセンスIDを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、アクセス権限が復元された失効済みPDFドキュメントを保存するために使用されます。
   * コンストラクターを呼び出し、失効したPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. 失効したPDFドキュメントへのアクセス権限を復元しました。

   * オブジェクトのメソッドを呼び出し、失効したドキュメントを表す `DocumentSecurityServiceClient` オブジェクトを渡すことで、失効したドキュメントのライセンス識別子の値を取得し `getLicenseID``BLOB` ます。 このメソッドは、ライセンス識別子を表すstring値を返します。
   * オブジェクトのメソッドを呼び出し、取り消されたPDFドキュメントのライセンス識別子の値を指定する文字列値を渡すことで、取り消されたPDFドキュメントへのアクセス権限を復元します(オ `DocumentSecurityServiceClient` ブジェクトのメ `unrevokeLicense``DocumentSecurityServiceClient``getLicenseId` ソッドの戻り値を渡します)。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM): WebサービスAPIを使用した、失効したドキュメントへのアクセス権限の復元」
* &quot;クイック開始(SwaRef): WebサービスAPIを使用した、失効したドキュメントへのアクセス権限の復元」

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## ポリシーで保護されたPDFドキュメントの検査 {#inspecting-policy-protected-pdf-documents}

ドキュメントセキュリティサービスAPI（JavaおよびWebサービス）を使用して、ポリシーで保護されたPDFドキュメントを検査できます。 ポリシーで保護されたPDFドキュメントを検査すると、ポリシーで保護されたPDFドキュメントに関する情報が返されます。 例えば、ドキュメントの保護に使用されたポリシーや、ドキュメントの保護日を決定できます。

お使いのLiveCycleのバージョンが8.x以前の場合は、このタスクを実行できません。 ポリシーで保護されたドキュメントの検査のサポートがAEM Formsに追加されました。 LiveCycle 8.x（またはそれ以前）を使用してポリシーで保護されたドキュメントを検査しようとすると、例外が発生します。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-7}

ポリシーで保護されたPDFドキュメントを検査するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. ポリシーで保護されたドキュメントを取得して検査します。
1. ポリシーで保護されたドキュメントに関する情報を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムを使用してドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成します。 Java APIを使用している場合は、 `RightsManagementClient` オブジェクトを作成します。 ドキュメントセキュリティWebサービスAPIを使用している場合は、 `RightsManagementServiceService` オブジェクトを作成します。

**ポリシーで保護されたドキュメントを取得して検査する**

ポリシーで保護されたドキュメントを検査するには、それを取得します。 ポリシーで保護されていないドキュメントや取り消された例外を検査しようとすると、例外が発生します。

**ドキュメントの検査**

ポリシーで保護されたドキュメントを取得したら、それを検査できます。

**ポリシーで保護されたドキュメントに関する情報の取得**

ポリシーで保護されたPDFドキュメントを検査した後、その情報を取得できます。 例えば、ドキュメントのセキュリティ保護に使用するポリシーを指定できます。

「マイポリシー」に属するポリシーでドキュメントを保護した後、 `RMInspectResult.getPolicysetName` またはを呼び出すと、nullが返され `RMInspectResult.getPolicysetId`ます。

ポリシーセットに含まれるポリシー（「マイポリシー」以外）を使用してドキュメントが保護されている場合は、有効な文字列 `RMInspectResult.getPolicysetName` を `RMInspectResult.getPolicysetId` 返します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したポリシーで保護されたPDFドキュメントの検査 {#inspect-policy-protected-pdf-documents-using-the-java-api}

ドキュメントセキュリティサービスAPI(Java)を使用して、ポリシーで保護されたPDFドキュメントを検査します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護されたドキュメントを取得して検査します。

   * コンストラクターを使用して、ポリシーで保護されたPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ドキュメントを検査します。

   * オブジェクトの `DocumentManager` メソッドを呼び出して、 `RightsManagementClient` オブジェクトを作成 `getDocumentManager` します。
   * オブジェクトのメソッドを呼び出して、ポリシーで保護されたドキュメント `LicenseManager` を検査し `inspectDocument` ます。 ポリシーで保護されたPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトを渡します。 ポリシーで保護されたドキュメントに関する情報を含む `RMInspectResult` オブジェクトを返します。

1. ポリシーで保護されたドキュメントに関する情報を取得します。

   ポリシーで保護されたドキュメントに関する情報を取得するには、オブジェクトに属する適切なメソッドを呼び出し `RMInspectResult` ます。 例えば、ポリシー名を取得するには、 `RMInspectResult` オブジェクトの `getPolicyName` メソッドを呼び出します。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（SOAPモード）: Java APIを使用したポリシーで保護されたPDFドキュメントの検査»

### WebサービスAPIを使用したポリシーで保護されたPDFドキュメントの検査 {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

ドキュメントセキュリティサービスAPI（Webサービス）を使用して、ポリシーで保護されたPDFドキュメントを検査します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/RightsManagementService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `RightsManagementServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `RightsManagementServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `RightsManagementServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。


1. ポリシーで保護されたドキュメントを取得して検査します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、検査対象のPDFドキュメントを保存するために使用されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. PDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. ドキュメントを検査します。

   オブジェクトのメソッドを呼び出して、ポリシーで保護されたドキュメント `RightsManagementServiceClient` を検査し `inspectDocument` ます。 ポリシーで保護されたPDFドキュメントを含む `BLOB` オブジェクトを渡します。 ポリシーで保護されたドキュメントに関する情報を含む `RMInspectResult` オブジェクトを返します。

1. ポリシーで保護されたドキュメントに関する情報を取得します。

   ポリシーで保護されたドキュメントに関する情報を取得するには、その `RMInspectResult` オブジェクトに属する適切なフィールドの値を取得します。 例えば、ポリシー名を取得するには、 `RMInspectResult` オブジェクトの `policyName` フィールドの値を取得します。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM): WebサービスAPIを使用したポリシーで保護されたPDFドキュメントの検査」
* &quot;クイック開始(SwaRef): WebサービスAPIを使用したポリシーで保護されたPDFドキュメントの検査」

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 透かしの作成 {#creating-watermarks}

透かしは、ドキュメントを一意に識別し、著作権侵害を制御することで、ドキュメントのセキュリティを確保するのに役立ちます。 例えば、「機密」という内容の透かしを作成し、ドキュメントのすべてのページに配置することができます。 透かしを作成した後、その透かしをポリシーの一部として含めることができます。 つまり、新しく作成した透かしをポリシーの透かし属性に設定できます。 透かしを含むポリシーがドキュメントに適用されると、その透かしはポリシーで保護されたドキュメントに表示されます。

>[!NOTE]
>
>ドキュメントセキュリティの管理者権限を持つユーザーのみが、透かしを作成できます。 つまり、ドキュメントセキュリティサービスクライアントオブジェクトの作成に必要な接続設定を定義する場合は、このようなユーザーを指定する必要があります。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-8}

透かしを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. 透かしの属性を設定します。
1. 透かしをドキュメントセキュリティサービスに登録します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムによってドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、 `RightsManagementClient` オブジェクトを作成します。 ドキュメントセキュリティWebサービスAPIを使用している場合は、 `RightsManagementServiceService` オブジェクトを作成します。

**透かしの属性の設定**

新しい透かしを作成するには、透かしの属性を設定する必要があります。 name属性は必ず定義する必要があります。 name属性に加えて、次の属性の少なくとも1つを設定する必要があります。

* カスタムテキスト
* DateIncluded
* UserIdIncluded
* UserNameIncluded

Webサービスを使用して透かしを作成する場合に必要なキーと値のペアを、次の表に示します。

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
   <td><p>ドキュメントを開いているユーザーのユーザー名を透かしの一部にするかどうかを指定します。</p></td>
   <td><p>True または False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td>
   <td><p>ドキュメントを開いているユーザーのIDが透かしの一部であるかどうかを指定します。</p></td>
   <td><p>True または False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td>
   <td><p>現在の日付が透かしの一部であるかどうかを指定します。</p></td>
   <td><p>True または False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td>
   <td><p>この値がtrueの場合、カスタムテキストの値はを使用して指定する必要があり <code>WaterBackCmd:SRCTEXT</code>ます。</p></td>
   <td><p>True または False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:OPACITY</code></p></td>
   <td><p>透かしの不透明度を指定します。 指定しない場合のデフォルト値は0.5です。</p></td>
   <td><p>0.0 ～ 1.0の値。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:ROTATION</code></p></td>
   <td><p>透かしの回転を指定します。 デフォルト値は0度です。</p></td>
   <td><p>0 ～ 359の値です。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SCALE</code></p></td>
   <td><p>この値を指定する場合は、値が存在し、値がtrueである必要があります。 <code>WaterBackCmd:IS_SIZE_ENABLED</code> この属性を指定しない場合、デフォルトの動作はページに合わせて調整されます。</p></td>
   <td><p>0.0 より大きく 1.0 以下の値。</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td>
   <td><p>透かしの水平方向の位置を指定します。 デフォルト値はcenterです。</p></td>
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
   <td><p>Trueを指定すると、カスタムの尺度が指定されます。 この値がtrueの場合は、SCALEも指定する必要があります。 この値がfalseの場合、デフォルトは「ページに合わせる」に設定されています。</p></td>
   <td><p>True または False</p></td>
  </tr>
  <tr>
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td>
   <td><p>透かしのカスタムテキストを指定します。 この値が存在する場合は、この値も存在し、trueに設定されている <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> 必要があります。</p></td>
   <td><p>True または False</p></td>
  </tr>
 </tbody>
</table>

すべての透かしに、次の属性のいずれかを定義する必要があります。

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

その他の属性はすべてオプションです。

**透かしの登録**

新しい透かしを使用するには、その透かしをドキュメントセキュリティサービスに登録する必要があります。 登録した透かしは、ポリシー内で使用できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Java APIを使用した透かしの作成 {#create-watermarks-using-the-java-api}

ドキュメントセキュリティAPI(Java)を使用して透かしを作成します。

1. プロジェクトファイルを含めます。

   Include client JAR files, such as the `adobe-rightsmanagement-client.jar`, in your Java project’s class path.

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 透かしの属性の設定

   * オブジェクトのスタティック `Watermark` メソッドを呼び出して、 `InfomodelObjectFactory``createWatermark` オブジェクトを作成します。 このメソッドは、 `Watermark` オブジェクトを返します。
   * オブジェクトのメソッドを呼び出し、ポリシー名を指定する文字列値を渡して、透かしの名前属性を設定し `Watermark` ま `setName` す。
   * オブジェクトのメソッドを呼び出して渡すことで、透かしの背景属性を設定し `Watermark` ます。そのためには、透かし `setBackground` の背景属性を指定 `true`します。 この属性を設定すると、透かしはドキュメントの背景に表示されます。
   * オブジェクトのメソッドを呼び出し、透かしのテキストを表す文字列値を渡して、透かしのカスタム `Watermark` テキスト属性を設定し `setCustomText` ます。
   * オブジェクトの `Watermark``setOpacity` メソッドを呼び出し、不透明度レベルを指定する整数値を渡して、透かしの不透明度属性を設定します。 値を100に設定した場合、透かしは完全に不透明になり、値を0に設定した場合、透かしは完全に透明になります。

1. 透かしを登録します。

   * オブジェクトの `WatermarkManager` メソッドを呼び出して、 `RightsManagementClient` オブジェクトを作成 `getWatermarkManager` します。 このメソッドは、 `WatermarkManager` オブジェクトを返します。
   * オブジェクトの `WatermarkManager` メソッドを呼び出し、登録する透かしを表す `registerWatermark``Watermark` オブジェクトを渡して、透かしを登録します。 このメソッドは、透かしの識別値を表すstring値を返します。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（SOAPモード）: Java APIを使用した透かしの作成»

### WebサービスAPIを使用した透かしの作成 {#create-watermarks-using-the-web-service-api}

ドキュメントセキュリティAPI（Webサービス）を使用して、透かしを作成します。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/RightsManagementService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `RightsManagementServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `RightsManagementServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `RightsManagementServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。


1. 透かしの属性を設定します。

   * コンストラクターを呼び出して、 `WatermarkSpec` オブジェクトを作成し `WatermarkSpec` ます。
   * オブジェクトのデータメンバに文字列値を割り当てて、透かしの名前を設定し `WatermarkSpec``name` ます。
   * オブジェクトの `id` データメンバに文字列値を割り当てて、透かしの `WatermarkSpec``id` 属性を設定します。
   * 設定する透かしのプロパティごとに、個別の `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。
   * キーの値を設定するには、 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` データメンバに値を割り当てます(例えば、 `WaterBackCmd:OPACITY)`)。
   * 値を設定するには、 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` データメンバーに値を割り当てます(例 `.25`)。
   * Create a `MyArrayOf_xsd_anyType` object. 各 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトに対して、 `MyArrayOf_xsd_anyType` オブジェクトの `Add` メソッドを呼び出します。 Pass the `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * オブジェクト `MyArrayOf_xsd_anyType` をオブジェクトの `WatermarkSpec``values` データメンバーに割り当てます。

1. 透かしを登録します。

   オブジェクトの `RightsManagementServiceClient` メソッドを呼び出し、登録する透かしを表す `registerWatermark``WatermarkSpec` オブジェクトを渡して、透かしを登録します。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM): WebサービスAPIを使用した透かしの作成」
* &quot;クイック開始(SwaRef): WebサービスAPIを使用した透かしの作成」

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 透かしの変更 {#modifying-watermarks}

ドキュメントセキュリティJava APIまたはWebサービスAPIを使用して、既存の透かしを変更できます。 既存の透かしを変更するには、その透かしを取得し、属性を変更して、サーバー上で更新します。 例えば、透かしを取得し、その不透明度属性を変更したとします。 変更を有効にする前に、透かしを更新する必要があります。

透かしを変更すると、その透かしが適用された後のドキュメントに影響します。 つまり、透かしを含む既存のPDFドキュメントは影響を受けません。

>[!NOTE]
>
>ドキュメントセキュリティの管理者権限を持つユーザーのみが、透かしを変更できます。 つまり、ドキュメントセキュリティサービスクライアントオブジェクトの作成に必要な接続設定を定義する場合は、このようなユーザーを指定する必要があります。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-9}

透かしを変更するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. 変更する透かしを取得します。
1. 透かしの属性を設定します。
1. 透かしを更新します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムによってドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、 `DocumentSecurityClient` オブジェクトを作成します。 ドキュメントセキュリティWebサービスAPIを使用している場合は、 `DocumentSecurityServiceService` オブジェクトを作成します。

**変更する透かしを取得する**

透かしを変更するには、既存の透かしを取得する必要があります。 透かしの名前を指定するか、識別子の値を指定することで、透かしを取得できます。

**透かしの属性の設定**

既存の透かしを変更するには、1つ以上の透かし属性の値を変更します。 Webサービスを使用してプログラムによって透かしを更新する場合は、値が変更されなくても、最初に設定されたすべての属性を設定する必要があります。 例えば、次の透かし属性が設定されているとします。 `WaterBackCmd:IS_USERID_ENABLED`、 `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`、、 `WaterBackCmd:OPACITY`および `WaterBackCmd:SRCTEXT`。 変更する属性は `WaterBackCmd:OPACITY`唯一ですが、他の値は適切に設定する必要があります。

>[!NOTE]
>
>Java APIを使用して透かしを変更する場合、すべての属性を指定する必要はありません。 変更する透かし属性を設定します。

>[!NOTE]
>
>透かしの属性名について詳しくは、「透かしの [作成](protecting-documents-policies.md#creating-watermarks)」を参照してください。

**透かしの更新**

透かしの属性を変更した後、透かしを更新する必要があります。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[透かしの作成](protecting-documents-policies.md#creating-watermarks)

### Java APIを使用した透かしの変更 {#modify-watermarks-using-the-java-api}

ドキュメントセキュリティAPI(Java)を使用して透かしを変更します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 変更する透かしを取得します。

   オブジェクトの `WatermarkManager` メソッドを呼び出し、透かしの名前を指定する文字列値を渡して、 `DocumentSecurityClient``getWatermarkManager` オブジェクトを作成します。 このメソッドは、変更する透かしを表す `Watermark` オブジェクトを返します。

1. 透かしの属性を設定します。

   オブジェクトの `Watermark``setOpacity` メソッドを呼び出し、不透明度レベルを指定する整数値を渡して、透かしの不透明度属性を設定します。 値を100に設定した場合、透かしは完全に不透明になり、値を0に設定した場合、透かしは完全に透明になります。

   >[!NOTE]
   >
   >次の例では、opacity属性のみを変更します。

1. 透かしを更新します。

   * オブジェクトの `WatermarkManager` メソッドを呼び出して透かしを更新し、属性が変更された `updateWatermark``Watermark` オブジェクトを渡します。

**コードの例**

ドキュメントセキュリティサービスを使用したコード例については、クイック開始（SOAPモード）を参照してください。 「Java API」セクションを使用した透かしの変更

### WebサービスAPIを使用した透かしの変更 {#modify-watermarks-using-the-web-service-api}

ドキュメントセキュリティAPI（Webサービス）を使用して透かしを変更します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `DocumentSecurityServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。


1. 変更する透かしを取得します。

   オブジェクトのメソッドを呼び出して、変更する透かし `DocumentSecurityServiceClient` を取得し `getWatermarkByName` ます。 透かしの名前を指定するstring値を渡します。 このメソッドは、変更する透かしを表す `WatermarkSpec` オブジェクトを返します。

1. 透かしの属性を設定します。

   * 更新する透かしのプロパティごとに、個別の `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。
   * キーの値を設定するには、 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` データメンバに値を割り当てます(例えば、 `WaterBackCmd:OPACITY)`)。
   * 値を設定するには、 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` データメンバーに値を割り当てます(例 `.50`)。
   * Create a `MyArrayOf_xsd_anyType` object. 各 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトに対して、 `MyArrayOf_xsd_anyType` オブジェクトの `Add` メソッドを呼び出します。 Pass the `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * オブジェクト `MyArrayOf_xsd_anyType` をオブジェクトの `WatermarkSpec``values` データメンバーに割り当てます。

1. 透かしを更新します。

   オブジェクトの `DocumentSecurityServiceClient` メソッドを呼び出し、変更する透かしを表す `updateWatermark``WatermarkSpec` オブジェクトを渡して、透かしを更新します。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM): WebサービスAPIを使用した透かしの変更」

## イベントの検索 {#searching-for-events}

Rights Managementサービスは、ドキュメントへのポリシーの適用、ポリシーで保護されたドキュメントの開封、ドキュメントへのアクセスの失効など、特定のアクションの発生時に追跡を行います。 Rights Managementサービスでイベント監査を有効にする必要があります。有効にしないと、イベントが追跡されません。

イベントは、次のいずれかのカテゴリに分類されます。

* 管理者イベントは、管理者に関連する操作（新しい管理者アカウントの作成など）です。
* ドキュメントイベントは、ポリシーで保護されたドキュメントを閉じるなど、ドキュメントに関連するアクションです。
* ポリシーイベントは、新しいポリシーの作成など、ポリシーに関連するアクションです。
* サービスイベントは、Rights Managementサービスに関連するアクション（ユーザーディレクトリとの同期など）です。

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

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**Rights Management Client APIオブジェクトの作成**

プログラムを使用してRights Managementサービスの操作を実行する前に、Rights Managementサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、 `DocumentSecurityClient` オブジェクトを作成します。 Rights Management WebサービスAPIを使用している場合は、 `DocumentSecurityServiceService` オブジェクトを作成します。

**検索するイベントの指定**

検索するイベントを指定する必要があります。 例えば、新しいポリシーが作成されたときに発生するポリシー作成イベントを検索できます。

**イベントの検索**

検索するイベントを指定した後、Rights Management Java APIまたはRights Management WebサービスAPIを使用してイベントを検索できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したイベントの検索 {#search-for-events-using-the-java-api}

Rights Management API(Java)を使用してイベントを検索します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. Rights Management Client APIオブジェクトの作成

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `DocumentSecurityClient``ServiceClientFactory` オブジェクトを作成します。

1. 検索するイベントの指定

   * オブジェクトの `EventManager` メソッドを呼び出して、 `DocumentSecurityClient` オブジェクトを作成 `getEventManager` します。 このメソッドは、 `EventManager` オブジェクトを返します。
   * コンストラクターを呼び出して、 `EventSearchFilter` オブジェクトを作成します。
   * オブジェクトの `EventSearchFilter` メソッドを呼び出し、検索対象のイベントを表す `setEventCode``EventManager` クラスに属する静的データメンバーを渡して、検索対象のイベントを指定します。 例えば、ポリシー作成イベントを検索するには、を渡し `EventManager.POLICY_CREATE_EVENT`ます。

   >[!NOTE]
   >
   >オブジェクトのメソッドを呼び出して、追加の検索条件を定義でき `EventSearchFilter` ます。 例えば、イベントに関連付けられたユーザーを指定するには、 `setUserName` メソッドを呼び出します。

1. イベントの検索

   オブジェクトの `EventManager` メソッドを呼び出し、イベントの検索条件を定義するオブジ `searchForEvents``EventSearchFilter` ェクトを渡して、イベントを検索します。 このメソッドは、 `Event` オブジェクトの配列を返します。

**コードの例**

Rights Managementサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(SOAP): Java APIを使用したイベントの検索»

### WebサービスAPIを使用したイベントの検索 {#search-for-events-using-the-web-service-api}

Rights Management API（Webサービス）を使用してイベントを検索します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. Rights Management Client APIオブジェクトの作成

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/RightsManagementService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `DocumentSecurityServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。


1. 検索するイベントの指定

   * Create an `EventSpec` object by using its constructor.
   * イベントが発生した開始を指定するには、 `EventSpec` オブジェクトの `firstTime.date``DataTime` データメンバに、イベントが発生した日付範囲の開始を表すインスタンスを設定します。
   * 値を `true` オブジェクトの `EventSpec``firstTime.dateSpecified` データメンバーに割り当てます。
   * イベントが発生した期間の終わりを指定します。その際には、 `EventSpec` オブジェクトの `lastTime.date``DataTime` データメンバに、イベントが発生した日付範囲の終わりを表すインスタンスを設定します。
   * 値を `true` オブジェクトの `EventSpec``lastTime.dateSpecified` データメンバーに割り当てます。
   * オブジェクトの `EventSpec``eventCode` データメンバに文字列値を割り当てて、検索するイベントを設定します。 次の表に、このプロパティに割り当てることができる数値を示します。

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

   オブジェクトのメソッドを呼び出し、検索対象のイベントを表す `DocumentSecurityServiceClient``searchForEvents``EventSpec` オブジェクトを渡し、検索結果の最大数を示すオブジェクトを渡して、イベントを検索します。 このメソッドは、各要素がインスタンスである `MyArrayOf_xsd_anyType` コレクションを返し `AuditSpec` ます。 インスタンスを使用して、イベントの発生時刻などの情報を取得でき `AuditSpec` ます。 この `AuditSpec` インスタンスには、この情報を指定する `timestamp` データメンバが含まれます。

**コードの例**

Rights Managementサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM): WebサービスAPIを使用したイベントの検索&quot;
* &quot;クイック開始(SwaRef): WebサービスAPIを使用したイベントの検索&quot;

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Wordドキュメントへのポリシーの適用 {#applying-policies-to-word-documents}

Rights Managementサービスは、PDFドキュメントに加えて、Microsoft Wordドキュメント（DOCファイル）やその他のMicrosoft Officeファイル形式などの追加のドキュメント形式もサポートします。 例えば、Wordドキュメントを保護するために、Wordアプリケーションにポリシーを適用できます。 Wordドキュメントにポリシーを適用すると、ドキュメントへのアクセスを制限できます。 ドキュメントが既にポリシーで保護されている場合は、ドキュメントにポリシーを適用できません。

ポリシーで保護されたWordドキュメントを配布した後、その使用を監視できます。 つまり、ドキュメントの使用状況と使用者を確認できます。 例えば、誰かがドキュメントを開いた日時を調べることができます。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-11}

Wordドキュメントにポリシーを適用するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. ポリシーが適用されているWordドキュメントを取得します。
1. 既存のポリシーをWordドキュメントに適用します。
1. ポリシーで保護されたWordドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムによってドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成する必要があります。

**Wordドキュメントの取得**

ポリシーを適用するには、Wordドキュメントを取得する必要があります。 Wordドキュメントにポリシーを適用すると、ドキュメントの使用時にユーザーが制限されます。 例えば、オフライン時にドキュメントを開くことをポリシーで有効にしていない場合、ドキュメントを開くには、ユーザーがオンラインである必要があります。

**既存のポリシーをWordドキュメントに適用する**

Wordドキュメントにポリシーを適用するには、既存のポリシーを参照し、ポリシーが属するポリシーセットを指定する必要があります。 接続プロパティを設定するユーザーは、指定したポリシーにアクセスできる必要があります。 そうでない場合は、例外が発生します。

**Wordドキュメントの保存**

ドキュメントセキュリティサービスがWordドキュメントにポリシーを適用した後、ポリシーで保護されたWordドキュメントをDOCファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ドキュメントへのアクセスの失効](protecting-documents-policies.md#revoking-access-to-documents)

### Java APIを使用したWordドキュメントへのポリシーの適用 {#apply-a-policy-to-a-word-document-using-the-java-api}

ドキュメントセキュリティAPI(Java)を使用してWordドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Wordドキュメントを取得します。

   * Wordドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。そのためには、コンストラクタを使用し、Wordドキュメントの場所を指定する文字列値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 既存のポリシーをWordドキュメントに適用します。

   * オブジェクトの `DocumentManager` メソッドを呼び出して、 `DocumentSecurityClient` オブジェクトを作成 `getDocumentManager` します。
   * オブジェクトの `DocumentManager` メソッドを呼び出し、次の値を渡して、Wordドキュメントにポリシーを適用し `protectDocument` ます。

      * ポリシーを適用するWordドキュメントを含む `com.adobe.idp.Document` オブジェクトです。
      * ドキュメントの名前を指定するstring値です。
      * ポリシーが属するポリシーセットの名前を指定するstring値です。 ポリシーセットを使用する結果として得られる `null` 値を指定でき `MyPolicies` ます。
      * ポリシー名を指定するstring値です。
      * ドキュメントのパブリッシャであるユーザーのUser Managerドメインの名前を表すstring値です。 このパラメーター値はオプションであり、nullにすることができます（このパラメーターがnullの場合、次のパラメーター値はnullにする必要があります）。
      * ドキュメントのパブリッシャであるUser Managerユーザーの正規名の名前を表すstring値です。 このパラメーターの値はオプションであり、値を指定できます `null` (このパラメーターが `null`の場合、前のパラメーターの値を指定する必要があり `null`ます)。
      * MS Officeテンプレートの選択に使用されるロケールを表す `com.adobe.livecycle.rightsmanagement.Locale` 。 このパラメーターの値はオプションで、指定でき `null`ます。

      ポリシーで保護されたWordドキュメントを含む `protectDocument``RMSecureDocumentResult` オブジェクトを返します。


1. Wordドキュメントを保存します。

   * オブジェクトの `RMSecureDocumentResult``getProtectedDoc` メソッドを呼び出して、ポリシーで保護されたWordドキュメントを取得します。 このメソッドは、 `com.adobe.idp.Document` オブジェクトを返します。
   * Create a `java.io.File` object and ensure that the file extension is DOC.
   * オブジェクトのメ `com.adobe.idp.Document` ソッドを呼び出して、 `copyToFile` オブジェクトの内容をファイルにコピーします(メソッドから返された `Document``Document``getProtectedDoc` オブジェクトを必ず使用してください)。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（SOAPモード）: Java APIを使用したWordドキュメントへのポリシーの適用»

### WebサービスAPIを使用してWordドキュメントにポリシーを適用する {#apply-a-policy-to-a-word-document-using-the-web-service-api}

ドキュメントセキュリティAPI（Webサービス）を使用してWordドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * Create a `DocumentSecurityServiceClient` object by using its default constructor.
   * Create a `DocumentSecurityServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `DocumentSecurityServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。


1. Wordドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、ポリシーが適用されるWordドキュメントを格納するために使用されます。
   * コンストラクターを呼び出し、Word `System.IO.FileStream` ドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 オブジェクトのプロパティを取得して、バイト配列のサイズ `System.IO.FileStream` を決定し `Length` ます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. 既存のポリシーをWordドキュメントに適用します。

   オブジェクトの `DocumentSecurityServiceClient` メソッドを呼び出し、次の値を渡して、Wordドキュメントにポリシーを適用し `protectDocument` ます。

   * ポリシーを適用するWordドキュメントを含む `BLOB` オブジェクトです。
   * ドキュメントの名前を指定するstring値です。
   * ポリシーが属するポリシーセットの名前を指定するstring値です。 ポリシーセットを使用する結果として得られる `null` 値を指定でき `MyPolicies` ます。
   * ポリシー名を指定するstring値です。
   * ドキュメントのパブリッシャであるユーザーのUser Managerドメインの名前を表すstring値です。 このパラメーターの値はオプションであり、nullにすることができます(このパラメーターがnullの場合、次のパラメーターの値にする必要があり `null`ます)。
   * ドキュメントのパブリッシャであるUser Managerユーザーの正規名の名前を表すstring値です。 このパラメーターの値はオプションであり、nullにすることができます(このパラメーターがnullの場合、前のパラメーターの値を `null`必ず指定してください)。
   * ロケール値を指定する `RMLocale` 値(例えば、 `RMLocale.en`)。
   * ポリシー識別子の値を保存するために使用される文字列出力パラメーターです。
   * ポリシーで保護された識別子の値の保存に使用される文字列出力パラメーターです。
   * MIMEタイプの格納に使用される文字列出力パラメーター(例： `application/doc`)。

   ポリシーで保護されたWordドキュメントを含む `protectDocument``BLOB` オブジェクトを返します。

1. Wordドキュメントを保存します。

   * コンストラクターを呼び出し、ポリシーで保護されたWordドキュメントーのファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトのデータ内容を格納するバイト配列を作成し `protectDocument` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をWordファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM): WebサービスAPIを使用してWordドキュメントにポリシーを適用する»

## Wordドキュメントからのポリシーの削除 {#removing-policies-from-word-documents}

ポリシーで保護されたWordドキュメントからポリシーを削除して、ドキュメントからセキュリティを削除できます。 つまり、ドキュメントをポリシーで保護したくない場合です。 ポリシーで保護されたWordドキュメントを新しいポリシーで更新する場合は、ポリシーを削除して更新されたポリシーを追加する代わりに、ポリシーを切り替える方が効率的です。

>[!NOTE]
>
>For more information about the Document Security service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-12}

ポリシーで保護されたWordドキュメントからポリシーを削除するには、次の手順を実行します。

1. プロジェクトファイルを含める
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. ポリシーで保護されたWordドキュメントを取得します。
1. Wordドキュメントからポリシーを削除します。
1. 保護されていないWordドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムを使用してドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成します。

**ポリシーで保護されたWordドキュメントの取得**

ポリシーを削除するには、ポリシーで保護されたWordドキュメントを取得する必要があります。 ポリシーで保護されていないWordドキュメントからポリシーを削除しようとすると、例外が発生します。

**Wordドキュメントからポリシーを削除します**

接続設定で管理者が指定されている場合は、ポリシーで保護されたWordドキュメントからポリシーを削除できます。 ポリシーがない場合は、Wordドキュメントからポリシーを削除するために、ドキュメントを保護するために使用されるポリシーに `SWITCH_POLICY` 権限が含まれている必要があります。 また、AEM Forms接続設定で指定したユーザーにも、その権限が必要です。 それ以外の場合は、例外が発生します。

**保護されていないWordドキュメントを保存する**

ドキュメントセキュリティサービスがWordドキュメントからポリシーを削除した後、保護されていないWordドキュメントをDOCファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Wordドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-word-documents)

### Java APIを使用したWordドキュメントからのポリシーの削除 {#remove-a-policy-from-a-word-document-using-the-java-api}

ドキュメントセキュリティAPI (Java)を使用して、ポリシーで保護されたWordドキュメントからポリシーを削除します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護されたWordドキュメントの取得

   * コンストラクターを使用し、Wordドキュメントーの場所を指定する文字列値を渡して、ポリシーで保護されたWordドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. Wordドキュメントからポリシーを削除します

   * オブジェクトの `DocumentManager` メソッドを呼び出して、 `RightsManagementClient` オブジェクトを作成 `getDocumentManager` します。
   * オブジェクトのドキュメントを呼び出し、ポリシーで保護されたWordドキュメントを含む `DocumentManager``removeSecurity``com.adobe.idp.Document` オブジェクトを渡すことで、Wordメソッドからポリシーを削除します。 このメソッドは、保護されていないWordドキュメントを含む `com.adobe.idp.Document` オブジェクトを返します。

1. 保護されていないWordドキュメントを保存する

   * Create a `java.io.File` object and ensure that the file extension is DOC.
   * オブジェクトのメ `Document` ソッドを呼び出して、 `copyToFile` オブジェクトの内容をファイルにコピーします(メソッドから返された `Document``Document``removeSecurity` オブジェクトを必ず使用してください)。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（SOAPモード）: Java APIを使用したWordドキュメントからのポリシーの削除»

### WebサービスAPIを使用してWordドキュメントからポリシーを削除する {#remove-a-policy-from-a-word-document-using-the-web-service-api}

ドキュメントセキュリティAPI （Webサービス）を使用して、ポリシーで保護されたWordドキュメントからポリシーを削除します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトの作成

   * Create a `RightsManagementServiceClient` object by using its default constructor.
   * Create a `RightsManagementServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/RightsManagementService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `RightsManagementServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `RightsManagementServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `RightsManagementServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。


1. ポリシーで保護されたWordドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、ポリシーが削除された、ポリシーで保護されたWordドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、Word `System.IO.FileStream` ドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. Wordドキュメントからポリシーを削除します

   オブジェクトのドキュメントを呼び出し、ポリシーで保護されたWordドキュメントを含む `RightsManagementServiceClient``removePolicySecurity``BLOB` オブジェクトを渡すことで、Wordメソッドからポリシーを削除します。 このメソッドは、保護されていないWordドキュメントを含む `BLOB` オブジェクトを返します。

1. 保護されていないWordドキュメントを保存する

   * コンストラクターを呼び出し、保護されていないWordドキュメントーのファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトのデータ内容を格納するバイト配列を作成し `removePolicySecurity` ます。 オブジェクトのフィールドの値を取得して、 `BLOB` バイト配列を設定し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM): WebサービスAPIを使用してWordドキュメントからポリシーを削除する」

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
