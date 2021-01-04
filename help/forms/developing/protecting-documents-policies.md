---
title: ポリシーによるドキュメントの保護
seo-title: ポリシーによるドキュメントの保護
description: ドキュメントセキュリティサービスを使用すると、Adobe PDFドキュメントに機密設定を動的に適用し、ドキュメントの制御を維持できます。 また、ドキュメントセキュリティサービスを使用すると、受信者がポリシーで保護されたPDFドキュメントをどのように使用するかを制御できます。
seo-description: ドキュメントセキュリティサービスを使用すると、Adobe PDFドキュメントに機密設定を動的に適用し、ドキュメントの制御を維持できます。 また、ドキュメントセキュリティサービスを使用すると、受信者がポリシーで保護されたPDFドキュメントをどのように使用するかを制御できます。
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '15544'
ht-degree: 4%

---


# ポリシー{#protecting-documents-with-policies}でドキュメントを保護

**ドキュメントセキュリティサービスについて**

ドキュメントセキュリティサービスを使用すると、ユーザーは、Adobe PDFドキュメントに対して動的に機密設定を適用でき、ドキュメントがどの程度広く配布されているかに関わらず、管理を維持できます。

ドキュメントセキュリティサービスは、ユーザーがポリシーで保護されたPDFドキュメントを受信者がどのように使用するかを制御できるようにし、ユーザーの手の届く範囲を超えて情報が広がるのを防ぎます。 ユーザーは、ドキュメントを開くことのできるユーザーを指定し、そのユーザーがを使用する方法を制限し、配布後にドキュメントを監視できます。 また、ポリシーで保護されたドキュメントへのアクセスを動的に制御し、ドキュメントへのアクセスを動的に取り消すこともできます。

ドキュメントセキュリティサービスは、Microsoft Wordファイル（DOCファイル）など、他のファイルタイプも保護します。 ドキュメントセキュリティクライアントAPIを使用して、これらのファイルタイプを操作できます。 次のバージョンがサポートされています。

* Microsoft Office 2003ファイル（DOC、XLS、PPTファイル）
* Microsoft Office 2007ファイル（DOCX、XLSX、PPTXファイル）
* PTC Pro/Eファイル

次の2つの節で、Wordドキュメントの使い方を説明します。

* [Wordドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Wordドキュメントからのポリシーの削除](protecting-documents-policies.md#removing-policies-from-word-documents)

ドキュメントセキュリティサービスを使用して、次のタスクを実行できます。

* ポリシーの作成. 詳しくは、「[ポリシーの作成](protecting-documents-policies.md#creating-policies)」を参照してください。
* ポリシーを変更します。 詳しくは、[ポリシーの変更](protecting-documents-policies.md#modifying-policies)を参照してください。
* ポリシーの削除 詳しくは、[ポリシーの削除](protecting-documents-policies.md#deleting-policies)を参照してください。
* PDFドキュメントにポリシーを適用します。 詳しくは、[PDFドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)を参照してください。
* PDFドキュメントからポリシーを削除します。 詳しくは、[PDFドキュメントからのポリシーの削除](protecting-documents-policies.md#removing-policies-from-pdf-documents)を参照してください。
* Inspectのポリシーで保護されたドキュメント。 詳しくは、[ポリシーで保護されたPDFドキュメントの検査](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents)を参照してください。
* PDFドキュメントへのアクセス権限を失効させます。 詳しくは、[ドキュメントへのアクセスの失効](protecting-documents-policies.md#revoking-access-to-documents)を参照してください。
* 失効したドキュメントへのアクセス権限の復元。 詳しくは、[失効したドキュメントへのアクセス権限の復元](protecting-documents-policies.md#reinstating-access-to-revoked-documents)を参照してください。
* 透かしを作成します。 詳しくは、[透かしの作成](protecting-documents-policies.md#creating-watermarks)を参照してください。
* イベントを検索します。 詳しくは、[イベントの検索](protecting-documents-policies.md#searching-for-events)を参照してください。

>[!NOTE]
>
>ドキュメントセキュリティサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## ポリシーの作成{#creating-policies}

ドキュメントセキュリティJava APIまたはWebサービスAPIを使用して、プログラムによってポリシーを作成できます。 *ポリシー*&#x200B;は、ドキュメントのセキュリティ設定、許可されたユーザー、使用権限などの情報の集まりです。 様々な状況やユーザーに適したセキュリティ設定を使用して、任意の数のポリシーを作成および保存できます。

ポリシーを使用すると、次のタスクを実行できます。

* ドキュメントを開くことができるユーザーを指定します。 受信者は、組織に属するか、組織外に属することができます。
* 受信者がドキュメントを使用する方法を指定します。 AcrobatとAdobe Readerの異なる機能へのアクセスを制限できます。 これらの機能には、テキストの印刷とコピー、ドキュメントの追加、署名へのコメントの追加が含まれます。
* ポリシーで保護されたドキュメントを配布した後でも、いつでもアクセスおよびセキュリティの設定を変更できます。
* ドキュメントを配布した後、その使用状況を監視します。 ドキュメントの使用方法と使用者を確認できます。 例えば、誰かがドキュメントを開いた日時を調べることができます。

### Webサービス{#creating-a-policy-using-web-services}を使用したポリシーの作成

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
>ドキュメントセキュリティサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary-of-steps}の概要

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

これらのJARファイルの場所について詳しくは、「[AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

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

* **AES256**:256ビットキーを持つAES暗号化アルゴリズムを表します。
* **AES128**:128ビットキーを持つAES暗号化アルゴリズムを表します。
* **NoEncryption：暗号化なしを** 表します。

`NoEncryption`オプションを指定する場合、`PlaintextMetadata`オプションを`false`に設定することはできません。 これを行うと、例外が発生します。

>[!NOTE]
>
>設定可能なその他の属性については、『[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』の`Policy`インターフェイスの説明を参照してください。

**ポリシーエントリの作成**

ポリシーエントリは、プリンシパル（グループとユーザー、権限）をポリシーに添付します。 ポリシーには少なくとも1つのポリシーエントリが必要です。 例えば、次のタスクを実行するとします。

* ポリシーエントリを作成して登録します。このエントリを使用すると、オンライン時にグループがドキュメントを表示するだけで、受信者はポリシーエントリをコピーできなくなります。
* ポリシーエントリをポリシーに添付します。
* Acrobatを使用して、ポリシーでドキュメントを保護します。

これらの操作により、受信者はドキュメントをオンラインで表示することのみができ、コピーすることができません。 セキュリティが解除されるまで、ドキュメントはセキュリティで保護された状態のままです。

**ポリシーの登録**

新しいポリシーを使用するには、そのポリシーを登録する必要があります。 登録したポリシーは、ドキュメントの保護に使用できます。

### Java APIを使用したポリシーの作成{#create-a-policy-using-the-java-api}

ドキュメントセキュリティAPI(Java)を使用してポリシーを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーの属性を設定します。

   * `InfomodelObjectFactory`オブジェクトの静的`createPolicy`メソッドを呼び出して、`Policy`オブジェクトを作成します。 このメソッドは、`Policy`オブジェクトを返します。
   * `Policy`オブジェクトの`setName`メソッドを呼び出し、ポリシー名を指定する文字列値を渡して、ポリシーの名前属性を設定します。
   * `Policy`オブジェクトの`setDescription`メソッドを呼び出し、ポリシーの説明を指定する文字列値を渡して、ポリシーの説明を設定します。
   * `Policy`オブジェクトの`setPolicySetName`メソッドを呼び出し、ポリシーセット名を指定する文字列値を渡すことで、新しいポリシーが属するポリシーセットを設定します。 （このパラメーター値に`null`を指定すると、ポリシーが&#x200B;*My Policies*&#x200B;ポリシーセットに追加されます）。
   * `InfomodelObjectFactory`オブジェクトの静的`createValidityPeriod`メソッドを呼び出して、ポリシーの有効期間を作成します。 このメソッドは、`ValidityPeriod`オブジェクトを返します。
   * `ValidityPeriod`オブジェクトの`setRelativeExpirationDays`メソッドを呼び出し、日数を指定する整数値を渡すことで、ポリシーで保護されたドキュメントにアクセスできる日数を設定します。
   * `Policy`オブジェクトの`setValidityPeriod`メソッドを呼び出し、`ValidityPeriod`オブジェクトを渡して、ポリシーの有効期間を設定します。

1. ポリシーエントリを作成します。

   * `InfomodelObjectFactory`オブジェクトの静的`createPolicyEntry`メソッドを呼び出して、ポリシーエントリを作成します。 このメソッドは、`PolicyEntry`オブジェクトを返します。
   * `InfomodelObjectFactory`オブジェクトの静的`createPermission`メソッドを呼び出して、ポリシーの権限を指定します。 権限を表す`Permission`インターフェイスに属する静的データメンバーを渡します。 このメソッドは、`Permission`オブジェクトを返します。 例えば、ポリシーで保護されたPDFドキュメントーからのデータのコピーをユーザーに許可する権限を追加するには、`Permission.COPY`を渡します。 （追加する権限ごとに、この手順を繰り返します）。
   * 追加`PolicyEntry`オブジェクトの`addPermission`メソッドを呼び出し、`Permission`オブジェクトを渡すことによって、ポリシーエントリに対する権限です。 （作成した`Permission`オブジェクトごとに、この手順を繰り返します）。
   * `InfomodelObjectFactory`オブジェクトの静的`createSpecialPrincipal`メソッドを呼び出して、ポリシープリンシパルを作成します。 プリンシパルを表す`InfomodelObjectFactory`オブジェクトに属するデータメンバーを渡します。 このメソッドは、`Principal`オブジェクトを返します。 例えば、ドキュメントのパブリッシャーをプリンシパルとして追加するには、`InfomodelObjectFactory.PUBLISHER_PRINCIPAL`を渡します。
   * 追加`PolicyEntry`オブジェクトの`setPrincipal`メソッドを呼び出し、`Principal`オブジェクトを渡すことで、ポリシーエントリのプリンシパルを指定します。
   * 追加`Policy`オブジェクトの`addPolicyEntry`メソッドを呼び出し、`PolicyEntry`オブジェクトを渡すことで、ポリシーに対するポリシーエントリを指定します。

1. ポリシーを登録します。

   * `DocumentSecurityClient`オブジェクトの`getPolicyManager`メソッドを呼び出して、`PolicyManager`オブジェクトを作成します。
   * `PolicyManager`オブジェクトの`registerPolicy`メソッドを呼び出し、次の値を渡して、ポリシーを登録します。

      * 登録するポリシーを表す`Policy`オブジェクトです。
   * ポリシーが属するポリシーセットを表すstring値です。

   接続設定でAEM forms管理者アカウントを使用して`DocumentSecurityClient`オブジェクトを作成する場合は、`registerPolicy`メソッドの呼び出し時にポリシーセット名を指定します。 ポリシーセットの`null`値を渡すと、ポリシーは管理者&#x200B;*マイポリシー*&#x200B;ポリシーセットに作成されます。

   ドキュメントセキュリティユーザーを接続設定内で使用する場合は、ポリシーのみを受け入れるオーバーロードされた`registerPolicy`メソッドを呼び出すことができます。 つまり、ポリシーセット名を指定する必要はありません。 ただし、ポリシーは&#x200B;*マイポリシー*&#x200B;という名前のポリシーセットに追加されます。 このポリシーセットに新しいポリシーを追加しない場合は、`registerPolicy`メソッドを呼び出すときにポリシーセット名を指定します。

   >[!NOTE]
   >
   >ポリシーを作成する場合は、既存のポリシーセットを参照します。 存在しないポリシーセットを指定すると、例外が発生します。

ドキュメントセキュリティサービスを使用したコードの例については、次を参照してください。

* 「クイック開始（SOAPモード）:Java APIを使用したポリシーの作成»

### WebサービスAPI {#create-a-policy-using-the-web-service-api}を使用したポリシーの作成

ドキュメントセキュリティAPI（Webサービス）を使用してポリシーを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * `DocumentSecurityServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`DocumentSecurityServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `RightsManagementServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`RightsManagementServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`RightsManagementServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
   * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。


1. ポリシーの属性を設定します。

   * コンストラクタを使用して `PolicySpec` オブジェクトを作成します。
   * `PolicySpec`オブジェクトの`name`データメンバに文字列値を割り当てて、ポリシーの名前を設定します。
   * `PolicySpec`オブジェクトの`description`データメンバに文字列値を割り当てて、ポリシーの説明を設定します。
   * `PolicySpec`オブジェクトの`policySetName`データメンバに文字列値を割り当てて、ポリシーが属するポリシーセットを設定します。 既存のポリシーセット名を指定する必要があります。 （このパラメーター値に`null`を指定すると、ポリシーが&#x200B;*My Policies*&#x200B;に追加されます）。
   * `PolicySpec`オブジェクトの`offlineLeasePeriod`データメンバに整数値を割り当てて、ポリシーのオフラインリース期間を設定します。
   * `PolicySpec`オブジェクトの`policyXml`データメンバーに、PDRL XMLデータを表す文字列値を設定します。 このタスクを実行するには、コンストラクタを使用して.NET `StreamReader`オブジェクトを作成します。 ポリシーを表すPDRL XMLファイルの場所を`StreamReader`コンストラクターに渡します。 次に、`StreamReader`オブジェクトの`ReadLine`メソッドを呼び出し、戻り値を文字列変数に割り当てます。 `ReadLine`メソッドがnullを返すまで、`StreamReader`オブジェクトを繰り返し処理します。 文字列変数を`PolicySpec`オブジェクトの`policyXml`データメンバに割り当てます。

1. ポリシーエントリを作成します。

   ドキュメントセキュリティWebサービスAPIを使用してポリシーを作成する場合、ポリシーエントリを作成する必要はありません。 ポリシーエントリは、PDRLドキュメントで定義されます。

1. ポリシーを登録します。

   `DocumentSecurityServiceClient`オブジェクトの`registerPolicy`メソッドを呼び出し、次の値を渡して、ポリシーを登録します。

   * 登録するポリシーを表す`PolicySpec`オブジェクトです。
   * ポリシーが属するポリシーセットを表すstring値です。 `null`値を指定すると、ポリシーが&#x200B;*MyPolices*&#x200B;ポリシーセットに追加されます。

   接続設定でAEM forms管理者アカウントを使用して`DocumentSecurityClient`オブジェクトを作成する場合は、`registerPolicy`メソッドの呼び出し時にポリシーセット名を指定します。

   接続設定内でドキュメントのSecurityDocument Securityユーザーを使用する場合は、ポリシーのみを受け入れる、オーバーロードされた`registerPolicy`メソッドを呼び出すことができます。 つまり、ポリシーセット名を指定する必要はありません。 ただし、ポリシーは&#x200B;*マイポリシー*&#x200B;という名前のポリシーセットに追加されます。 このポリシーセットに新しいポリシーを追加しない場合は、`registerPolicy`メソッドを呼び出すときにポリシーセット名を指定します。

   >[!NOTE]
   >
   >ポリシーを作成し、ポリシーセットを指定する場合は、既存のポリシーセットを必ず指定してください。 存在しないポリシーセットを指定すると、例外が発生します。

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM):WebサービスAPIを使用したポリシーの作成」
* &quot;クイック開始(SwaRef):WebサービスAPIを使用したポリシーの作成」

## ポリシーの変更{#modifying-policies}

ドキュメントセキュリティJava APIまたはWebサービスAPIを使用して、既存のポリシーを変更できます。 既存のポリシーを変更するには、そのポリシーを取得し、変更してから、サーバー上のポリシーを更新します。 例えば、既存のポリシーを取得し、その有効期間を延長したとします。 変更を有効にする前に、ポリシーを更新する必要があります。

ビジネス要件が変更され、ポリシーにこれらの要件が反映されなくなった場合は、ポリシーを変更できます。 新しいポリシーを作成する代わりに、既存のポリシーを更新するだけで済みます。

Webサービス（例えば、JAX-WSで作成されたJavaプロキシクラスを使用）を使用してポリシー属性を変更するには、ポリシーがドキュメントセキュリティサービスに登録されていることを確認する必要があります。 その後、`PolicySpec.getPolicyXml`メソッドを使用して既存のポリシーを参照し、該当するメソッドを使用してポリシー属性を変更できます。 例えば、`PolicySpec.setOfflineLeasePeriod`メソッドを呼び出して、オフラインリース期間を変更できます。

>[!NOTE]
>
>ドキュメントセキュリティサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-1}の概要

既存のポリシーを変更するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. 既存のポリシーを取得します。
1. ポリシー属性を変更します。
1. ポリシーを更新します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムを使用してドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、`RightsManagementClient`オブジェクトを作成します。 ドキュメントセキュリティWebサービスAPIを使用している場合は、`RightsManagementServiceService`オブジェクトを作成します。

**既存のポリシーの取得**

既存のポリシーを変更するには、そのポリシーを取得する必要があります。 ポリシーを取得するには、ポリシー名とポリシーが属するポリシーセットを指定します。 ポリシーセット名に`null`値を指定した場合、ポリシーは&#x200B;*マイポリシー*&#x200B;ポリシーセットから取得されます。

**ポリシーの属性の設定**

ポリシーを変更するには、ポリシー属性の値を変更します。 変更できない唯一のポリシー属性はname属性です。 例えば、ポリシーのオフラインリース期間を変更するには、ポリシーのオフラインリース期間属性の値を変更します。

Webサービスを使用してポリシーのオフラインリース期間を変更する場合、`PolicySpec`インターフェイスの`offlineLeasePeriod`フィールドは無視されます。 オフラインリース期間を更新するには、PDRL XMLドキュメントの`OfflineLeasePeriod`要素を変更します。 次に、`PolicySpec`インターフェイスの`policyXML`データメンバを使用して、更新されたPDRL XMLドキュメントを参照します。

>[!NOTE]
>
>設定可能なその他の属性については、『[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』の`Policy`インターフェイスの説明を参照してください。

**ポリシーの更新**

ポリシーに対して行った変更を有効にする前に、ドキュメントセキュリティサービスを使用してポリシーを更新する必要があります。 ドキュメントを保護するポリシーに対する変更は、次回、ポリシーで保護されたドキュメントがドキュメントセキュリティサービスと同期されたときに更新されます。

### Java API {#modify-existing-policies-using-the-java-api}を使用して既存のポリシーを変更する

ドキュメントセキュリティAPI(Java)を使用して既存のポリシーを変更します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 既存のポリシーを取得します。

   * `RightsManagementClient`オブジェクトの`getPolicyManager`メソッドを呼び出して、`PolicyManager`オブジェクトを作成します。
   * `PolicyManager`オブジェクトの`getPolicy`メソッドを呼び出し、次の値を渡すことで、更新するポリシーを表す`Policy`オブジェクトを作成します。&quot;

      * ポリシーが属するポリシーセット名を表すstring値です。 `null`を指定すると、`MyPolicies`ポリシーセットが使用されます。
      * ポリシー名を表すstring値です。

1. ポリシーの属性を設定します。

   ビジネス要件に合わせてポリシーの属性を変更します。 例えば、ポリシーのオフラインリース期間を変更するには、`Policy`オブジェクトの`setOfflineLeasePeriod`メソッドを呼び出します。

1. ポリシーを更新します。

   `PolicyManager`オブジェクトの`updatePolicy`メソッドを呼び出して、ポリシーを更新します。 更新するポリシーを表す`Policy`オブジェクトを渡します。

**コードの例**

ドキュメントセキュリティサービスを使用したコード例については、クイック開始（SOAPモード）を参照してください。「Java API」セクションを使用してポリシーを変更する。

### WebサービスAPI {#modify-existing-policies-using-the-web-service-api}を使用して既存のポリシーを変更

ドキュメントセキュリティAPI （Webサービス）を使用して既存のポリシーを変更します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * `RightsManagementServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`RightsManagementServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `RightsManagementServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`RightsManagementServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`RightsManagementServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
   * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。


1. 既存のポリシーを取得します。

   `RightsManagementServiceClient`オブジェクトの`getPolicy`メソッドを呼び出し、次の値を渡して、変更するポリシーを表す`PolicySpec`オブジェクトを作成します。

   * ポリシーが属するポリシーセット名を指定するstring値です。 `null`を指定すると、`MyPolicies`ポリシーセットが使用されます。
   * ポリシーの名前を指定するstring値です。

1. ポリシーの属性を設定します。

   ビジネス要件に合わせてポリシーの属性を変更します。

1. ポリシーを更新します。

   `RightsManagementServiceClient`オブジェクトの`updatePolicyFromSDK`メソッドを呼び出し、更新するポリシーを表す`PolicySpec`オブジェクトを渡して、ポリシーを更新します。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM):WebサービスAPIを使用したポリシーの変更」
* &quot;クイック開始(SwaRef):WebサービスAPIを使用したポリシーの変更」

## ポリシーの削除{#deleting-policies}

ドキュメントセキュリティJava APIまたはWebサービスAPIを使用して、既存のポリシーを削除できます。 ポリシーを削除すると、ドキュメントの保護にポリシーを使用できなくなります。 ただし、ポリシーを使用している既存のポリシーで保護されたドキュメントは、引き続き保護されます。 新しいポリシーが利用可能になった場合は、ポリシーを削除できます。

>[!NOTE]
>
>ドキュメントセキュリティサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-2}の概要

既存のポリシーを削除するには、次の手順を実行します。

1. プロジェクトファイルを含める
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. ポリシーを削除します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムによってドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、`RightsManagementClient`オブジェクトを作成します。 ドキュメントセキュリティWebサービスAPIを使用している場合は、`RightsManagementServiceService`オブジェクトを作成します。

**ポリシーの削除**

ポリシーを削除するには、削除するポリシーと、そのポリシーが属するポリシーセットを指定します。 AEM Formsの呼び出しに使用される設定を持つユーザーは、ポリシーを削除する権限を持っている必要があります。それ以外の場合は、例外が発生します。 同様に、存在しないポリシーを削除しようとすると、例外が発生します。

### Java APIを使用したポリシーの削除{#delete-policies-using-the-java-api}

ドキュメントセキュリティAPI(Java)を使用してポリシーを削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーを削除します。

   * `RightsManagementClient`オブジェクトの`getPolicyManager`メソッドを呼び出して、`PolicyManager`オブジェクトを作成します。
   * `PolicyManager`オブジェクトの`deletePolicy`メソッドを呼び出し、次の値を渡して、ポリシーを削除します。

      * ポリシーが属するポリシーセット名を指定するstring値です。 `null`を指定すると、`MyPolicies`ポリシーセットが使用されます。
      * 削除するポリシーの名前を指定するstring値です。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（SOAPモード）:Java APIを使用したポリシーの削除」

### WebサービスAPI {#delete-policies-using-the-web-service-api}を使用したポリシーの削除

ドキュメントセキュリティAPI（Webサービス）を使用してポリシーを削除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * `RightsManagementServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`RightsManagementServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `RightsManagementServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`RightsManagementServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`RightsManagementServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
   * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。


1. ポリシーを削除します。

   `RightsManagementServiceClient`オブジェクトの`deletePolicy`メソッドを呼び出し、次の値を渡して、ポリシーを削除します。

   * ポリシーが属するポリシーセット名を指定するstring値です。 `null`を指定すると、`MyPolicies`ポリシーセットが使用されます。
   * 削除するポリシーの名前を指定するstring値です。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM):WebサービスAPIを使用したポリシーの削除」
* &quot;クイック開始(SwaRef):WebサービスAPIを使用したポリシーの削除」

## PDFドキュメントへのポリシーの適用{#applying-policies-to-pdf-documents}

ドキュメントを保護するために、PDFドキュメントにポリシーを適用できます。 ポリシーをPDFドキュメントに適用すると、ドキュメントへのアクセスを制限できます。 ドキュメントが既にポリシーで保護されている場合は、ドキュメントにポリシーを適用できません。

ドキュメントが開いている間は、テキストの印刷やコピー、変更、ドキュメントへの署名やコメントの追加など、AcrobatおよびAdobe Readerの機能へのアクセスを制限することもできます。 また、ドキュメントにアクセスしたくなくなった場合に、ポリシーで保護されたPDFドキュメントを無効にすることもできます。

ポリシーで保護されたドキュメントを配布した後、その使用を監視できます。 つまり、ドキュメントの使用状況と使用者を確認できます。 例えば、誰かがドキュメントを開いた日時を調べることができます。

>[!NOTE]
>
>ドキュメントセキュリティサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-3}の概要

PDFドキュメントにポリシーを適用するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. ポリシーが適用されるPDFドキュメントを取得します。
1. 既存のポリシーをPDFドキュメントに適用します。
1. ポリシーで保護されたPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムを使用してドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成します。 Java APIを使用している場合は、`DocumentSecurityClient`オブジェクトを作成します。 ドキュメントセキュリティWebサービスAPIを使用している場合は、`DocumentSecurityServiceService`オブジェクトを作成します。

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

### Java API {#apply-a-policy-to-a-pdf-document-using-the-java-api}を使用したPDFドキュメントへのポリシーの適用

ドキュメントセキュリティAPI(Java)を使用してPDFドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントを取得します。

   * PDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成するには、コンストラクターを使用します。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 既存のポリシーをPDFドキュメントに適用します。

   * `RightsManagementClient`オブジェクトの`getDocumentManager`メソッドを呼び出して、`DocumentManager`オブジェクトを作成します。
   * `DocumentManager`オブジェクトの`protectDocument`メソッドを呼び出し、次の値を渡して、PDFドキュメントにポリシーを適用します。

      * ポリシーが適用されるPDFドキュメントが含まれる`com.adobe.idp.Document`オブジェクトです。
      * ドキュメントの名前を指定するstring値です。
      * ポリシーが属するポリシーセットの名前を指定するstring値です。 `null`値を指定すると、`MyPolicies`ポリシーセットが使用されます。
      * ポリシー名を指定するstring値です。
      * ドキュメントのパブリッシャであるユーザーのUser Managerドメインの名前を表すstring値です。 このパラメーター値はオプションであり、nullにすることができます（このパラメーターがnullの場合、次のパラメーター値はnullにする必要があります）。
      * ドキュメントのパブリッシャであるUser Managerユーザーの正規名の名前を表すstring値です。 このパラメーターの値はオプションで、`null`に設定できます（このパラメーターがnullの場合、前のパラメーターの値は`null`に設定する必要があります）。
      * MS Officeテンプレートの選択に使用するロケールを表す`com.adobe.livecycle.rightsmanagement.Locale`。 このパラメーター値はオプションで、PDFドキュメントでは使用されません。 PDFドキュメントを保護するには、`null`を指定します。

      `protectDocument`メソッドは、ポリシーで保護されたPDFドキュメントを含む`RMSecureDocumentResult`オブジェクトを返します。


1. PDFドキュメントを保存します。

   * `RMSecureDocumentResult`オブジェクトの`getProtectedDoc`メソッドを呼び出して、ポリシーで保護されたPDFドキュメントを取得します。 このメソッドは、`com.adobe.idp.Document`オブジェクトを返します。
   * `java.io.File`オブジェクトを作成し、ファイル拡張子がPDFであることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`Document`オブジェクトの内容をファイルにコピーします（`getProtectedDoc`メソッドから返された`Document`オブジェクトを必ず使用してください）。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（EJBモード）:Java APIを使用したPDFドキュメントへのポリシーの適用」
* 「クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントへのポリシーの適用」

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}を使用したPDFドキュメントへのポリシーの適用

ドキュメントセキュリティAPI（Webサービス）を使用してPDFドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * `RightsManagementServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`RightsManagementServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをFormsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `RightsManagementServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`RightsManagementServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`RightsManagementServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
   * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。


1. PDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、ポリシーが適用されるPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定します。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。

1. 既存のポリシーをPDFドキュメントに適用します。

   `RightsManagementServiceClient`オブジェクトの`protectDocument`メソッドを呼び出し、次の値を渡して、PDFドキュメントにポリシーを適用します。

   * ポリシーが適用されるPDFドキュメントが含まれる`BLOB`オブジェクトです。
   * ドキュメントの名前を指定するstring値です。
   * ポリシーが属するポリシーセットの名前を指定するstring値です。 `null`値を指定すると、`MyPolicies`ポリシーセットが使用されます。
   * ポリシー名を指定するstring値です。
   * ドキュメントのパブリッシャであるユーザーのUser Managerドメインの名前を表すstring値です。 このパラメーターの値はオプションで、nullにすることができます（このパラメーターがnullの場合、次のパラメーターの値は`null`にする必要があります）。
   * ドキュメントのパブリッシャであるUser Managerユーザーの正規名の名前を表すstring値です。 このパラメーターの値はオプションで、nullにすることができます（このパラメーターがnullの場合、前のパラメーターの値は`null`にする必要があります）。
   * ロケール値を指定する`RMLocale`値（例：`RMLocale.en`）。
   * ポリシー識別子の値を保存するために使用される文字列出力パラメーターです。
   * ポリシーで保護された識別子の値の保存に使用される文字列出力パラメーターです。
   * MIMEタイプの格納に使用される文字列出力パラメーター（例：`application/pdf`）。

   `protectDocument`メソッドは、ポリシーで保護されたPDFドキュメントを含む`BLOB`オブジェクトを返します。

1. PDFドキュメントを保存します。

   * コンストラクターを呼び出し、ポリシーで保護されたPDFドキュメントのファイルの場所を表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `protectDocument`メソッドから返された`BLOB`オブジェクトのデータ内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM):WebサービスAPIを使用したPDFドキュメントへのポリシーの適用」
* &quot;クイック開始(SwaRef):WebサービスAPIを使用したPDFドキュメントへのポリシーの適用」

## PDFドキュメントからのポリシーの削除{#removing-policies-from-pdf-documents}

ポリシーで保護されたドキュメントからポリシーを削除して、ドキュメントからセキュリティを削除できます。 つまり、ドキュメントをポリシーで保護したくない場合です。 ポリシーで保護されたドキュメントを新しいポリシーで更新する場合は、ポリシーを削除して更新されたポリシーを追加する代わりに、ポリシーを切り替える方が効率的です。

>[!NOTE]
>
>ドキュメントセキュリティサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-4}の概要

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

接続設定で管理者が指定されている場合は、ポリシーで保護されたPDFドキュメントからポリシーを削除できます。 ポリシーがない場合は、PDFドキュメントからポリシーを削除するには、ドキュメントを保護するために使用されるポリシーに`SWITCH_POLICY`権限が含まれている必要があります。 また、AEM Forms接続設定で指定したユーザーにも、その権限が必要です。 それ以外の場合は、例外が発生します。

**保護されていないPDFドキュメントの保存**

ドキュメントセキュリティサービスがPDFドキュメントからポリシーを削除した後、保護されていないPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Java API {#remove-a-policy-from-a-pdf-document-using-the-java-api}を使用したPDFドキュメントからのポリシーの削除

ドキュメントセキュリティAPI(Java)を使用して、ポリシーで保護されたPDFドキュメントからポリシーを削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護されたPDFドキュメントを取得します。

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、ポリシーで保護されたPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ポリシーをPDFドキュメントから削除します。

   * `DocumentSecurityClient`オブジェクトの`getDocumentManager`メソッドを呼び出して、`DocumentManager`オブジェクトを作成します。
   * `DocumentManager`オブジェクトの`removeSecurity`メソッドを呼び出し、ポリシーで保護されたPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを渡すことで、PDFドキュメントからポリシーを削除します。 このメソッドは、保護されていないPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを返します。

1. 保護されていないPDFドキュメントを保存します。

   * `java.io.File`オブジェクトを作成し、ファイル拡張子がPDFであることを確認します。
   * `Document`オブジェクトの`copyToFile`メソッドを呼び出して、`Document`オブジェクトの内容をファイルにコピーします（`removeSecurity`メソッドから返された`Document`オブジェクトを必ず使用してください）。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントからのポリシーの削除»

### WebサービスAPI {#remove-a-policy-using-the-web-service-api}を使用したポリシーの削除

ドキュメントセキュリティAPI（Webサービス）を使用して、ポリシーで保護されたPDFドキュメントからポリシーを削除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * `DocumentSecurityServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`DocumentSecurityServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `DocumentSecurityServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
   * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。


1. ポリシーで保護されたPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、ポリシーが削除された、ポリシーで保護されたPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。

1. ポリシーをPDFドキュメントから削除します。

   `DocumentSecurityServiceClient`オブジェクトの`removePolicySecurity`メソッドを呼び出し、ポリシーで保護されたPDFドキュメントを含む`BLOB`オブジェクトを渡すことで、PDFドキュメントからポリシーを削除します。 このメソッドは、保護されていないPDFドキュメントを含む`BLOB`オブジェクトを返します。

1. 保護されていないPDFドキュメントを保存します。

   * コンストラクターを呼び出し、保護されていないPDFドキュメントーのファイルの場所を表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `removePolicySecurity`メソッドから返された`BLOB`オブジェクトのデータ内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`フィールドの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM):WebサービスAPIを使用したPDFドキュメントからのポリシーの削除」
* &quot;クイック開始(SwaRef):WebサービスAPIを使用したPDFドキュメントからのポリシーの削除」

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## ドキュメントへのアクセスの取り消し{#revoking-access-to-documents}

ポリシーで保護されたPDFドキュメントへのアクセスを無効にすると、そのドキュメントのすべてのコピーにユーザーからアクセスできなくなります。 失効したPDFドキュメントを開こうとすると、指定したURLにリダイレクトされ、変更されたドキュメントを表示できます。 ユーザーのリダイレクト先のURLは、プログラムで指定する必要があります。 ドキュメントへのアクセスを無効にすると、ポリシーで保護されたドキュメントを次回オンラインで開いたときに、ドキュメントセキュリティサービスとの同期が行われます。

ドキュメントへのアクセスを取り消す機能により、セキュリティが強化されます。 例えば、新しいバージョンのドキュメントが利用可能で、古いバージョンを表示するユーザーが不要になったとします。 この場合、古いドキュメントへのアクセスを取り消すことができ、アクセスを元に戻さない限り、誰もドキュメントに表示できません。

>[!NOTE]
>
>ドキュメントセキュリティサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-5}の概要

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

### Java API {#revoke-access-to-documents-using-the-java-api}を使用してドキュメントへのアクセスを取り消す

ドキュメントセキュリティAPI(Java)を使用して、ポリシーで保護されたPDFドキュメントへのアクセス権限を失効させます。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護されたPDFドキュメントの取得

   * コンストラクターを使用し、PDFドキュメントの場所を指定する文字列値を渡すことで、ポリシーで保護されたPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ポリシーで保護されたドキュメントの失効

   * `DocumentSecurityClient`オブジェクトの`getDocumentManager`メソッドを呼び出して、`DocumentManager`オブジェクトを作成します。
   * `DocumentManager`オブジェクトの`getLicenseId`メソッドを呼び出して、ポリシーで保護されたドキュメントのライセンス識別子の値を取得します。 ポリシーで保護されたドキュメントを表す`com.adobe.idp.Document`オブジェクトを渡します。 このメソッドは、ライセンス識別子の値を表すstring値を返します。
   * `DocumentSecurityClient`オブジェクトの`getLicenseManager`メソッドを呼び出して、`LicenseManager`オブジェクトを作成します。
   * `LicenseManager`オブジェクトの`revokeLicense`メソッドを呼び出し、次の値を渡して、ポリシーで保護されたドキュメントを取り消します。

      * ポリシーで保護されたドキュメントのライセンス識別子の値を指定するstring値（`DocumentManager`オブジェクトの`getLicenseId`メソッドの戻り値を指定）。
      * ドキュメントを取り消す理由を指定する、`License`インターフェイスの静的データメンバです。 例えば、`License.DOCUMENT_REVISED`を指定できます。
      * 改訂ドキュメントの場所を指定する`java.net.URL`値。 ユーザーを別のURLにリダイレクトしたくない場合は、`null`を渡すことができます。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（SOAPモード）:Java APIを使用したドキュメントの取り消し»

### WebサービスAPI {#revoke-access-to-documents-using-the-web-service-api}を使用してドキュメントへのアクセスを取り消す

ドキュメントセキュリティAPI（Webサービス）を使用して、ポリシーで保護されたPDFドキュメントへのアクセス権限を失効させます。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトの作成

   * `DocumentSecurityServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`DocumentSecurityServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `DocumentSecurityServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
   * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。


1. ポリシーで保護されたPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、失効したポリシーで保護されたPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、失効するポリシーで保護されたPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。

1. ポリシーで保護されたドキュメントの失効

   * `DocumentSecurityServiceClient`オブジェクトの`getLicenseID`メソッドを呼び出し、ポリシーで保護されたドキュメントを表す`BLOB`オブジェクトを渡すことで、ポリシーで保護されたドキュメントのライセンス識別子の値を取得します。 このメソッドは、ライセンス識別子を表すstring値を返します。
   * `DocumentSecurityServiceClient`オブジェクトの`revokeLicense`メソッドを呼び出し、次の値を渡して、ポリシーで保護されたドキュメントを取り消します。

      * ポリシーで保護されたドキュメントのライセンス識別子の値を指定するstring値（`DocumentSecurityServiceService`オブジェクトの`getLicenseId`メソッドの戻り値を指定）。
      * ドキュメントを取り消す理由を指定する、`Reason`列挙の静的データメンバです。 例えば、`Reason.DOCUMENT_REVISED`を指定できます。
      * 変更したドキュメントの場所のURLの場所を指定する`string`値。 ユーザーを別のURLにリダイレクトしたくない場合は、`null`を渡すことができます。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM):WebサービスAPIを使用したドキュメントの取り消し
* &quot;クイック開始(SwaRef):WebサービスAPIを使用したドキュメントの取り消し

**関連トピック**

[Wordドキュメントからのポリシーの削除](protecting-documents-policies.md#removing-policies-from-word-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 失効したドキュメントへのアクセスの復元{#reinstating-access-to-revoked-documents}

失効したPDFドキュメントへのアクセス権限を復元できるので、失効したドキュメントのすべてのコピーにユーザーがアクセスできます。 ユーザーが失効した復元済みドキュメントを開くと、そのドキュメントを表示できます。

>[!NOTE]
>
>ドキュメントセキュリティサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-6}の概要

失効したPDFドキュメントへのアクセス権限を復元するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. 失効したPDFドキュメントのライセンスIDを取得します。
1. 失効したPDFドキュメントへのアクセス権限を復元しました。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムによってドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、`DocumentSecurityClient`オブジェクトを作成します。 ドキュメントセキュリティWebサービスAPIを使用している場合は、`DocumentSecurityServiceService`オブジェクトを作成します。

**失効したPDFドキュメントのライセンスIDを取得します**

失効したPDFドキュメントを復元するには、失効したPDFドキュメントのライセンスIDを取得する必要があります。 ライセンス識別子の値を取得した後、失効したドキュメントを復元できます。 失効していないドキュメントを復元しようとすると、例外が発生します。

**失効したPDFドキュメントへのアクセス権限の復元**

失効したPDFドキュメントへのアクセス権限を復元するには、失効したドキュメントのライセンスIDを指定する必要があります。 失効していないPDFドキュメントへのアクセス権限を復元しようとすると、例外が発生します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[ドキュメントへのアクセスの失効](protecting-documents-policies.md#revoking-access-to-documents)

### Java API {#reinstate-access-to-revoked-documents-using-the-java-api}を使用した、失効したドキュメントへのアクセス権の復元

ドキュメントセキュリティAPI(Java)を使用して、失効したドキュメントへのアクセス権限を復元する：

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 失効したPDFドキュメントのライセンスIDを取得します。

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、失効したPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * `DocumentSecurityClient`オブジェクトの`getDocumentManager`メソッドを呼び出して、`DocumentManager`オブジェクトを作成します。
   * `DocumentManager`オブジェクトの`getLicenseId`メソッドを呼び出し、失効したドキュメントを表す`com.adobe.idp.Document`オブジェクトを渡して、失効したドキュメントのライセンス識別子の値を取得します。 このメソッドは、ライセンス識別子を表すstring値を返します。

1. 失効したPDFドキュメントへのアクセス権限を復元しました。

   * `DocumentSecurityClient`オブジェクトの`getLicenseManager`メソッドを呼び出して、`LicenseManager`オブジェクトを作成します。
   * `LicenseManager`オブジェクトの`unrevokeLicense`メソッドを呼び出し、取り消されたドキュメントのライセンス識別子の値を渡すことで、取り消されたPDFドキュメントへのアクセスを復元します。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（SOAPモード）:WebサービスAPIを使用した、失効したドキュメントへのアクセス権限の復元」

### WebサービスAPI {#reinstate-access-to-revoked-documents-using-the-web-service-api}を使用した、失効したドキュメントへのアクセス権の復元

ドキュメントセキュリティAPI（Webサービス）を使用して、失効したドキュメントへのアクセス権限を復元する：

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * `DocumentSecurityServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`DocumentSecurityServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `DocumentSecurityServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
   * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。


1. 失効したPDFドキュメントのライセンスIDを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、アクセス権限が復元された失効済みPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、失効したPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。

1. 失効したPDFドキュメントへのアクセス権限を復元しました。

   * `DocumentSecurityServiceClient`オブジェクトの`getLicenseID`メソッドを呼び出し、失効したドキュメントを表す`BLOB`オブジェクトを渡して、失効したドキュメントのライセンス識別子の値を取得します。 このメソッドは、ライセンス識別子を表すstring値を返します。
   * `DocumentSecurityServiceClient`オブジェクトの`unrevokeLicense`メソッドを呼び出し、取り消されたPDFドキュメントのライセンス識別子の値を指定する文字列値を渡すことで、取り消されたPDFドキュメントへのアクセスを復元します（`DocumentSecurityServiceClient`オブジェクトの`getLicenseId`メソッドの戻り値を渡します）。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM):WebサービスAPIを使用した、失効したドキュメントへのアクセス権限の復元」
* &quot;クイック開始(SwaRef):WebサービスAPIを使用した、失効したドキュメントへのアクセス権限の復元」

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## ポリシーで保護されたPDFドキュメントの検査{#inspecting-policy-protected-pdf-documents}

ドキュメントセキュリティサービスAPI（JavaおよびWebサービス）を使用して、ポリシーで保護されたPDFドキュメントを検査できます。 ポリシーで保護されたPDFドキュメントを検査すると、ポリシーで保護されたPDFドキュメントに関する情報が返されます。 例えば、ドキュメントの保護に使用されたポリシーや、ドキュメントの保護日を決定できます。

お使いのLiveCycleのバージョンが8.x以前の場合は、このタスクを実行できません。 ポリシーで保護されたドキュメントの検査のサポートはAEM Formsに追加されました。 LiveCycle8.x（またはそれ以前）を使用してポリシーで保護されたドキュメントを検査しようとすると、例外が発生します。

>[!NOTE]
>
>ドキュメントセキュリティサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-7}の概要

ポリシーで保護されたPDFドキュメントを検査するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. ポリシーで保護されたドキュメントを取得して検査します。
1. ポリシーで保護されたドキュメントに関する情報を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムを使用してドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成します。 Java APIを使用している場合は、`RightsManagementClient`オブジェクトを作成します。 ドキュメントセキュリティWebサービスAPIを使用している場合は、`RightsManagementServiceService`オブジェクトを作成します。

**ポリシーで保護されたドキュメントを取得して検査する**

ポリシーで保護されたドキュメントを検査するには、それを取得します。 ポリシーで保護されていないドキュメントや取り消された例外を検査しようとすると、例外が発生します。

**ドキュメントInspect**

ポリシーで保護されたドキュメントを取得したら、それを検査できます。

**ポリシーで保護されたドキュメントに関する情報の取得**

ポリシーで保護されたPDFドキュメントを検査した後、その情報を取得できます。 例えば、ドキュメントのセキュリティ保護に使用するポリシーを指定できます。

マイポリシーに属するポリシーでドキュメントを保護し、`RMInspectResult.getPolicysetName`または`RMInspectResult.getPolicysetId`を呼び出した場合、nullが返されます。

ポリシーセットに含まれるポリシー（マイポリシー以外）を使用してドキュメントが保護されている場合、`RMInspectResult.getPolicysetName`と`RMInspectResult.getPolicysetId`は有効な文字列を返します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したInspectポリシーで保護されたPDFドキュメント{#inspect-policy-protected-pdf-documents-using-the-java-api}

ドキュメントセキュリティサービスAPI(Java)を使用した、ポリシーで保護されたPDFドキュメントのInspect:

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護されたドキュメントを取得して検査します。

   * ポリシーで保護されたPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。作成するには、コンストラクターを使用します。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ドキュメントInspect。

   * `RightsManagementClient`オブジェクトの`getDocumentManager`メソッドを呼び出して、`DocumentManager`オブジェクトを作成します。
   * ポリシーで保護されたドキュメントをInspectに送信するには、`LicenseManager`オブジェクトの`inspectDocument`メソッドを呼び出します。 ポリシーで保護されたPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを渡します。 このメソッドは、ポリシーで保護されたドキュメントに関する情報を含む`RMInspectResult`オブジェクトを返します。

1. ポリシーで保護されたドキュメントに関する情報を取得します。

   ポリシーで保護されたドキュメントに関する情報を取得するには、`RMInspectResult`オブジェクトに属する適切なメソッドを呼び出します。 例えば、ポリシー名を取得するには、`RMInspectResult`オブジェクトの`getPolicyName`メソッドを呼び出します。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（SOAPモード）:Java APIを使用したポリシーで保護されたPDFドキュメントの検査»

### WebサービスAPI {#inspect-policy-protected-pdf-documents-using-the-web-service-api}を使用したInspectポリシーで保護されたPDFドキュメント

ドキュメントセキュリティサービスAPI（webサービス）を使用して、ポリシーで保護されたPDFドキュメントをInspectします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * `RightsManagementServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`RightsManagementServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `RightsManagementServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`RightsManagementServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`RightsManagementServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
   * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。


1. ポリシーで保護されたドキュメントを取得して検査します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、検査するPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 PDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。

1. ドキュメントInspect。

   ポリシーで保護されたドキュメントをInspectに送信するには、`RightsManagementServiceClient`オブジェクトの`inspectDocument`メソッドを呼び出します。 ポリシーで保護されたPDFドキュメントを含む`BLOB`オブジェクトを渡します。 このメソッドは、ポリシーで保護されたドキュメントに関する情報を含む`RMInspectResult`オブジェクトを返します。

1. ポリシーで保護されたドキュメントに関する情報を取得します。

   ポリシーで保護されたドキュメントに関する情報を取得するには、`RMInspectResult`オブジェクトに属する適切なフィールドの値を取得します。 例えば、ポリシー名を取得するには、`RMInspectResult`オブジェクトの`policyName`フィールドの値を取得します。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM):WebサービスAPIを使用したポリシーで保護されたPDFドキュメントの検査」
* &quot;クイック開始(SwaRef):WebサービスAPIを使用したポリシーで保護されたPDFドキュメントの検査」

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 透かしの作成{#creating-watermarks}

透かしは、ドキュメントを一意に識別し、著作権侵害を制御することで、ドキュメントのセキュリティを確保するのに役立ちます。 例えば、「機密」という内容の透かしを作成し、ドキュメントのすべてのページに配置することができます。 透かしを作成した後、その透かしをポリシーの一部として含めることができます。 つまり、新しく作成した透かしをポリシーの透かし属性に設定できます。 透かしを含むポリシーがドキュメントに適用されると、その透かしはポリシーで保護されたドキュメントに表示されます。

>[!NOTE]
>
>ドキュメントセキュリティの管理者権限を持つユーザーのみが、透かしを作成できます。 つまり、ドキュメントセキュリティサービスクライアントオブジェクトの作成に必要な接続設定を定義する場合は、このようなユーザーを指定する必要があります。

>[!NOTE]
>
>ドキュメントセキュリティサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-8}の概要

透かしを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. 透かしの属性を設定します。
1. 透かしをドキュメントセキュリティサービスに登録します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムによってドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、`RightsManagementClient`オブジェクトを作成します。 ドキュメントセキュリティWebサービスAPIを使用している場合は、`RightsManagementServiceService`オブジェクトを作成します。

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
   <td><p>この値がtrueの場合、カスタムテキストの値は<code>WaterBackCmd:SRCTEXT</code>を使用して指定する必要があります。</p></td>
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
   <td><p>この値を指定する場合は、<code>WaterBackCmd:IS_SIZE_ENABLED</code>が存在し、値をtrueに設定する必要があります。 この属性を指定しない場合、デフォルトの動作はページに合わせて調整されます。</p></td>
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
   <td><p>透かしのカスタムテキストを指定します。 この値が存在する場合は、<code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code>も存在し、trueに設定する必要があります。</p></td>
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

### Java APIを使用した透かしの作成{#create-watermarks-using-the-java-api}

ドキュメントセキュリティAPI(Java)を使用して透かしを作成します。

1. プロジェクトファイルを含めます。

   `adobe-rightsmanagement-client.jar`などのクライアントJARファイルをJavaプロジェクトのクラスパスに含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 透かしの属性の設定

   * `InfomodelObjectFactory`オブジェクトの静的`createWatermark`メソッドを呼び出して、`Watermark`オブジェクトを作成します。 このメソッドは、`Watermark`オブジェクトを返します。
   * `Watermark`オブジェクトの`setName`メソッドを呼び出し、ポリシー名を指定する文字列値を渡して、透かしの名前属性を設定します。
   * `Watermark`オブジェクトの`setBackground`メソッドを呼び出し、`true`を渡して、透かしの背景属性を設定します。 この属性を設定すると、透かしはドキュメントの背景に表示されます。
   * `Watermark`オブジェクトの`setCustomText`メソッドを呼び出し、透かしのテキストを表す文字列値を渡して、透かしのカスタムテキスト属性を設定します。
   * `Watermark`オブジェクトの`setOpacity`メソッドを呼び出し、不透明度レベルを指定する整数値を渡して、透かしの不透明度属性を設定します。 値を100に設定した場合、透かしは完全に不透明になり、値を0に設定した場合、透かしは完全に透明になります。

1. 透かしを登録します。

   * `RightsManagementClient`オブジェクトの`getWatermarkManager`メソッドを呼び出して、`WatermarkManager`オブジェクトを作成します。 このメソッドは、`WatermarkManager`オブジェクトを返します。
   * `WatermarkManager`オブジェクトの`registerWatermark`メソッドを呼び出し、登録する透かしを表す`Watermark`オブジェクトを渡して、透かしを登録します。 このメソッドは、透かしの識別値を表すstring値を返します。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（SOAPモード）:Java APIを使用した透かしの作成»

### WebサービスAPI {#create-watermarks-using-the-web-service-api}を使用した透かしの作成

ドキュメントセキュリティAPI（Webサービス）を使用して、透かしを作成します。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * `RightsManagementServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`RightsManagementServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `RightsManagementServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`RightsManagementServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`RightsManagementServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
   * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。


1. 透かしの属性を設定します。

   * `WatermarkSpec`コンストラクターを呼び出して、`WatermarkSpec`オブジェクトを作成します。
   * `WatermarkSpec`オブジェクトの`name`データメンバに文字列値を割り当てて、透かしの名前を設定します。
   * `WatermarkSpec`オブジェクトの`id`データメンバに文字列値を割り当てて、透かしの`id`属性を設定します。
   * 設定する透かしのプロパティごとに、個別の`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトを作成します。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`key`データメンバに値を割り当てて、キーの値を設定します（例：`WaterBackCmd:OPACITY)`）。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`value`データメンバに値を割り当てて値を設定します（例：`.25`）。
   * `MyArrayOf_xsd_anyType`オブジェクトを作成します。 各`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトに対して、`MyArrayOf_xsd_anyType`オブジェクトの`Add`メソッドを呼び出します。 `MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトを渡します。
   * `MyArrayOf_xsd_anyType`オブジェクトを`WatermarkSpec`オブジェクトの`values`データメンバに割り当てます。

1. 透かしを登録します。

   `RightsManagementServiceClient`オブジェクトの`registerWatermark`メソッドを呼び出し、登録する透かしを表す`WatermarkSpec`オブジェクトを渡して、透かしを登録します。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM):WebサービスAPIを使用した透かしの作成」
* &quot;クイック開始(SwaRef):WebサービスAPIを使用した透かしの作成」

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 透かしの変更{#modifying-watermarks}

ドキュメントセキュリティJava APIまたはWebサービスAPIを使用して、既存の透かしを変更できます。 既存の透かしを変更するには、その透かしを取得し、属性を変更して、サーバー上で更新します。 例えば、透かしを取得し、その不透明度属性を変更したとします。 変更を有効にする前に、透かしを更新する必要があります。

透かしを変更すると、その透かしが適用された後のドキュメントに影響します。 つまり、透かしを含む既存のPDFドキュメントは影響を受けません。

>[!NOTE]
>
>ドキュメントセキュリティの管理者権限を持つユーザーのみが、透かしを変更できます。 つまり、ドキュメントセキュリティサービスクライアントオブジェクトの作成に必要な接続設定を定義する場合は、このようなユーザーを指定する必要があります。

>[!NOTE]
>
>ドキュメントセキュリティサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-9}の概要

透かしを変更するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。
1. 変更する透かしを取得します。
1. 透かしの属性を設定します。
1. 透かしを更新します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**ドキュメントセキュリティクライアントAPIオブジェクトの作成**

プログラムによってドキュメントセキュリティサービスの操作を実行する前に、ドキュメントセキュリティサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、`DocumentSecurityClient`オブジェクトを作成します。 ドキュメントセキュリティWebサービスAPIを使用している場合は、`DocumentSecurityServiceService`オブジェクトを作成します。

**変更する透かしを取得する**

透かしを変更するには、既存の透かしを取得する必要があります。 透かしの名前を指定するか、識別子の値を指定することで、透かしを取得できます。

**透かしの属性の設定**

既存の透かしを変更するには、1つ以上の透かし属性の値を変更します。 Webサービスを使用してプログラムによって透かしを更新する場合は、値が変更されなくても、最初に設定されたすべての属性を設定する必要があります。 例えば、次の透かし属性が設定されているとします。`WaterBackCmd:IS_USERID_ENABLED`、`WaterBackCmd:IS_CUSTOMTEXT_ENABLED`、`WaterBackCmd:OPACITY`、`WaterBackCmd:SRCTEXT`。 変更したい属性は`WaterBackCmd:OPACITY`のみですが、他の値は適切に設定する必要があります。

>[!NOTE]
>
>Java APIを使用して透かしを変更する場合、すべての属性を指定する必要はありません。 変更する透かし属性を設定します。

>[!NOTE]
>
>透かしの属性名について詳しくは、「[透かしの作成](protecting-documents-policies.md#creating-watermarks)」を参照してください。

**透かしの更新**

透かしの属性を変更した後、透かしを更新する必要があります。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[透かしの作成](protecting-documents-policies.md#creating-watermarks)

### Java APIを使用した透かしの変更{#modify-watermarks-using-the-java-api}

ドキュメントセキュリティAPI(Java)を使用して透かしを変更します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 変更する透かしを取得します。

   `DocumentSecurityClient`オブジェクトの`getWatermarkManager`メソッドを呼び出して`WatermarkManager`オブジェクトを作成し、透かし名を指定する文字列値を渡します。 このメソッドは、変更する透かしを表す`Watermark`オブジェクトを返します。

1. 透かしの属性を設定します。

   `Watermark`オブジェクトの`setOpacity`メソッドを呼び出し、不透明度レベルを指定する整数値を渡して、透かしの不透明度属性を設定します。 値を100に設定した場合、透かしは完全に不透明になり、値を0に設定した場合、透かしは完全に透明になります。

   >[!NOTE]
   >
   >次の例では、opacity属性のみを変更します。

1. 透かしを更新します。

   * `WatermarkManager`オブジェクトの`updateWatermark`メソッドを呼び出して透かしを更新し、属性が変更された`Watermark`オブジェクトを渡します。

**コードの例**

ドキュメントセキュリティサービスを使用したコード例については、クイック開始（SOAPモード）を参照してください。「Java API」セクションを使用した透かしの変更

### WebサービスAPI {#modify-watermarks-using-the-web-service-api}を使用して透かしを変更

ドキュメントセキュリティAPI（Webサービス）を使用して透かしを変更します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * `DocumentSecurityServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`RightsManagementServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/DocumentSecurityService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `DocumentSecurityServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
   * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。


1. 変更する透かしを取得します。

   `DocumentSecurityServiceClient`オブジェクトの`getWatermarkByName`メソッドを呼び出して、変更する透かしを取得します。 透かしの名前を指定するstring値を渡します。 このメソッドは、変更する透かしを表す`WatermarkSpec`オブジェクトを返します。

1. 透かしの属性を設定します。

   * 更新する透かしのプロパティごとに、個別の`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトを作成します。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`key`データメンバに値を割り当てて、キーの値を設定します（例：`WaterBackCmd:OPACITY)`）。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`value`データメンバに値を割り当てて値を設定します（例：`.50`）。
   * `MyArrayOf_xsd_anyType`オブジェクトを作成します。 各`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトに対して、`MyArrayOf_xsd_anyType`オブジェクトの`Add`メソッドを呼び出します。 `MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトを渡します。
   * `MyArrayOf_xsd_anyType`オブジェクトを`WatermarkSpec`オブジェクトの`values`データメンバに割り当てます。

1. 透かしを更新します。

   `DocumentSecurityServiceClient`オブジェクトの`updateWatermark`メソッドを呼び出し、変更する透かしを表す`WatermarkSpec`オブジェクトを渡して、透かしを更新します。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM):WebサービスAPIを使用した透かしの変更」

## イベントの検索{#searching-for-events}

Rights Managementサービスは、ドキュメントへのポリシーの適用、ポリシーで保護されたドキュメントのオープン、ドキュメントへのアクセスの取り消しなど、発生する特定のアクションを追跡します。 Rights Managementサービスでイベント監査を有効にする必要があります。有効にしないと、イベントが追跡されません。

イベントは、次のいずれかのカテゴリに分類されます。

* 管理者イベントは、管理者に関連する操作（新しい管理者アカウントの作成など）です。
* ドキュメントイベントは、ポリシーで保護されたドキュメントを閉じるなど、ドキュメントに関連するアクションです。
* ポリシーイベントは、新しいポリシーの作成など、ポリシーに関連するアクションです。
* サービスイベントは、Rights Managementサービスに関連するアクション（ユーザーディレクトリとの同期など）です。

Rights ManagementのJava APIまたはWebサービスAPIを使用して、特定のイベントを検索できます。 イベントを検索することで、特定のイベントのログファイルの作成などのタスクを実行できます。

>[!NOTE]
>
>Rights Managementサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-10}の概要

Rights Managementイベントを検索するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Rights ManagementクライアントAPIオブジェクトを作成します。
1. 検索するイベントを指定します。
1. イベントを検索します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**Rights ManagementクライアントAPIオブジェクトの作成**

プログラムを使用してRights Managementサービスの操作を実行する前に、Rights Managementサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、`DocumentSecurityClient`オブジェクトを作成します。 Rights ManagementWebサービスAPIを使用している場合は、`DocumentSecurityServiceService`オブジェクトを作成します。

**検索するイベントの指定**

検索するイベントを指定する必要があります。 例えば、新しいポリシーが作成されたときに発生するポリシー作成イベントを検索できます。

**イベントの検索**

検索するイベントを指定した後、Rights ManagementJava APIまたはRights ManagementWebサービスAPIを使用してイベントを検索できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API {#search-for-events-using-the-java-api}を使用したイベントの検索

Rights ManagementAPI(Java)を使用してイベントを検索します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. Rights ManagementクライアントAPIオブジェクトの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`DocumentSecurityClient`オブジェクトを作成します。

1. 検索するイベントの指定

   * `DocumentSecurityClient`オブジェクトの`getEventManager`メソッドを呼び出して、`EventManager`オブジェクトを作成します。 このメソッドは、`EventManager`オブジェクトを返します。
   * コンストラクターを呼び出して、`EventSearchFilter`オブジェクトを作成します。
   * `EventSearchFilter`オブジェクトの`setEventCode`メソッドを呼び出し、検索するイベントを表す`EventManager`クラスに属する静的データメンバーを渡して、検索するイベントを指定します。 例えば、ポリシー作成イベントを検索するには、`EventManager.POLICY_CREATE_EVENT`を渡します。

   >[!NOTE]
   >
   >`EventSearchFilter`オブジェクトメソッドを呼び出すことで、追加の検索条件を定義できます。 例えば、`setUserName`メソッドを呼び出して、イベントに関連付けられたユーザーを指定します。

1. イベントの検索

   `EventManager`オブジェクトの`searchForEvents`メソッドを呼び出し、イベント検索条件を定義する`EventSearchFilter`オブジェクトを渡して、イベントを検索します。 このメソッドは、`Event`オブジェクトの配列を返します。

**コードの例**

Rights Managementサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(SOAP):Java APIを使用したイベントの検索»

### WebサービスAPI {#search-for-events-using-the-web-service-api}を使用したイベントの検索

Rights ManagementAPI（Webサービス）を使用してイベントを検索します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Rights ManagementクライアントAPIオブジェクトの作成

   * `DocumentSecurityServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`DocumentSecurityServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `DocumentSecurityServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
   * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。


1. 検索するイベントの指定

   * コンストラクターを使用して`EventSpec`オブジェクトを作成します。
   * `EventSpec`オブジェクトの`firstTime.date`データメンバーに、イベントが発生した日付範囲の開始を表す`DataTime`インスタンスを設定して、イベントが発生した開始を指定します。
   * 値`true`を`EventSpec`オブジェクトの`firstTime.dateSpecified`データメンバに割り当てます。
   * `EventSpec`オブジェクトの`lastTime.date`データメンバーに、イベントが発生した日付範囲の終了を表す`DataTime`インスタンスを設定して、イベントが発生した期間の終了を指定します。
   * 値`true`を`EventSpec`オブジェクトの`lastTime.dateSpecified`データメンバに割り当てます。
   * `EventSpec`オブジェクトの`eventCode`データメンバに文字列値を割り当てて、検索するイベントを設定します。 次の表に、このプロパティに割り当てることができる数値を示します。

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

   `DocumentSecurityServiceClient`オブジェクトの`searchForEvents`メソッドを呼び出し、検索対象のイベントと最大結果数を表す`EventSpec`オブジェクトを渡して、イベントを検索します。 このメソッドは、`MyArrayOf_xsd_anyType`コレクションを返します。各要素は`AuditSpec`インスタンスです。 `AuditSpec`インスタンスを使用して、イベントの発生時刻などの情報を取得できます。 `AuditSpec`インスタンスには、この情報を指定する`timestamp`データメンバが含まれています。

**コードの例**

Rights Managementサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM):WebサービスAPIを使用したイベントの検索&quot;
* &quot;クイック開始(SwaRef):WebサービスAPIを使用したイベントの検索&quot;

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Wordドキュメントへのポリシーの適用{#applying-policies-to-word-documents}

Rights Managementサービスは、PDFドキュメントに加えて、Microsoft Wordドキュメント（DOCファイル）やその他のMicrosoft Officeファイル形式などの追加のドキュメント形式もサポートします。 例えば、Wordドキュメントを保護するために、Wordアプリケーションにポリシーを適用できます。 Wordドキュメントにポリシーを適用すると、ドキュメントへのアクセスを制限できます。 ドキュメントが既にポリシーで保護されている場合は、ドキュメントにポリシーを適用できません。

ポリシーで保護されたWordドキュメントを配布した後、その使用を監視できます。 つまり、ドキュメントの使用状況と使用者を確認できます。 例えば、誰かがドキュメントを開いた日時を調べることができます。

>[!NOTE]
>
>ドキュメントセキュリティサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-11}の概要

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

### Java API {#apply-a-policy-to-a-word-document-using-the-java-api}を使用してWordドキュメントにポリシーを適用する

ドキュメントセキュリティAPI(Java)を使用してWordドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Wordドキュメントを取得します。

   * Wordドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。そのためには、コンストラクターを使用し、Wordドキュメントの場所を指定する文字列値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 既存のポリシーをWordドキュメントに適用します。

   * `DocumentSecurityClient`オブジェクトの`getDocumentManager`メソッドを呼び出して、`DocumentManager`オブジェクトを作成します。
   * `DocumentManager`オブジェクトの`protectDocument`メソッドを呼び出し、次の値を渡して、Wordドキュメントにポリシーを適用します。

      * ポリシーが適用されるWordドキュメントが含まれる`com.adobe.idp.Document`オブジェクトです。
      * ドキュメントの名前を指定するstring値です。
      * ポリシーが属するポリシーセットの名前を指定するstring値です。 `null`値を指定すると、`MyPolicies`ポリシーセットが使用されます。
      * ポリシー名を指定するstring値です。
      * ドキュメントのパブリッシャであるユーザーのUser Managerドメインの名前を表すstring値です。 このパラメーター値はオプションであり、nullにすることができます（このパラメーターがnullの場合、次のパラメーター値はnullにする必要があります）。
      * ドキュメントのパブリッシャであるUser Managerユーザーの正規名の名前を表すstring値です。 このパラメーターの値はオプションで、`null`に設定できます（このパラメーターが`null`の場合、前のパラメーターの値は`null`に設定する必要があります）。
      * MS Officeテンプレートの選択に使用するロケールを表す`com.adobe.livecycle.rightsmanagement.Locale`。 このパラメーターの値はオプションで、`null`を指定できます。

      `protectDocument`メソッドは、ポリシーで保護されたWordドキュメントを含む`RMSecureDocumentResult`オブジェクトを返します。


1. Wordドキュメントを保存します。

   * `RMSecureDocumentResult`オブジェクトの`getProtectedDoc`メソッドを呼び出して、ポリシーで保護されたWordドキュメントを取得します。 このメソッドは、`com.adobe.idp.Document`オブジェクトを返します。
   * `java.io.File`オブジェクトを作成し、ファイル拡張子がDOCであることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`Document`オブジェクトの内容をファイルにコピーします（`getProtectedDoc`メソッドから返された`Document`オブジェクトを必ず使用してください）。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（SOAPモード）:Java APIを使用したWordドキュメントへのポリシーの適用»

### WebサービスAPI {#apply-a-policy-to-a-word-document-using-the-web-service-api}を使用してWordドキュメントにポリシーを適用する

ドキュメントセキュリティAPI（Webサービス）を使用してWordドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトを作成します。

   * `DocumentSecurityServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`DocumentSecurityServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/DocumentSecurityService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `DocumentSecurityServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`DocumentSecurityServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
   * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。


1. Wordドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、ポリシーが適用されるWordドキュメントを格納するために使用します。
   * コンストラクターを呼び出し、Wordドキュメントーのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定します。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。

1. 既存のポリシーをWordドキュメントに適用します。

   `DocumentSecurityServiceClient`オブジェクトの`protectDocument`メソッドを呼び出し、次の値を渡して、Wordドキュメントにポリシーを適用します。

   * ポリシーが適用されるWordドキュメントが含まれる`BLOB`オブジェクトです。
   * ドキュメントの名前を指定するstring値です。
   * ポリシーが属するポリシーセットの名前を指定するstring値です。 `null`値を指定すると、`MyPolicies`ポリシーセットが使用されます。
   * ポリシー名を指定するstring値です。
   * ドキュメントのパブリッシャであるユーザーのUser Managerドメインの名前を表すstring値です。 このパラメーターの値はオプションで、nullにすることができます（このパラメーターがnullの場合、次のパラメーターの値は`null`にする必要があります）。
   * ドキュメントのパブリッシャであるUser Managerユーザーの正規名の名前を表すstring値です。 このパラメーターの値はオプションで、nullにすることができます（このパラメーターがnullの場合、前のパラメーターの値は`null`にする必要があります）。
   * ロケール値を指定する`RMLocale`値（例：`RMLocale.en`）。
   * ポリシー識別子の値を保存するために使用される文字列出力パラメーターです。
   * ポリシーで保護された識別子の値の保存に使用される文字列出力パラメーターです。
   * MIMEタイプの格納に使用される文字列出力パラメーター（例：`application/doc`）。

   `protectDocument`メソッドは、ポリシーで保護されたWordドキュメントを含む`BLOB`オブジェクトを返します。

1. Wordドキュメントを保存します。

   * コンストラクターを呼び出し、ポリシーで保護されたWordドキュメントーのファイルの場所を表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `protectDocument`メソッドから返された`BLOB`オブジェクトのデータ内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をWordファイルに書き込みます。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM):WebサービスAPIを使用してWordドキュメントにポリシーを適用する»

## Wordドキュメントからのポリシーの削除{#removing-policies-from-word-documents}

ポリシーで保護されたWordドキュメントからポリシーを削除して、ドキュメントからセキュリティを削除できます。 つまり、ドキュメントをポリシーで保護したくない場合です。 ポリシーで保護されたWordドキュメントを新しいポリシーで更新する場合は、ポリシーを削除して更新されたポリシーを追加する代わりに、ポリシーを切り替える方が効率的です。

>[!NOTE]
>
>ドキュメントセキュリティサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-12}の概要

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

接続設定で管理者が指定されている場合は、ポリシーで保護されたWordドキュメントからポリシーを削除できます。 そうでない場合は、ドキュメントを保護するために使用されるポリシーに`SWITCH_POLICY`権限が含まれていないと、Wordドキュメントからポリシーを削除できません。 また、AEM Forms接続設定で指定したユーザーにも、その権限が必要です。 それ以外の場合は、例外が発生します。

**保護されていないWordドキュメントの保存**

ドキュメントセキュリティサービスがWordドキュメントからポリシーを削除した後、保護されていないWordドキュメントをDOCファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Wordドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-word-documents)

### Java API {#remove-a-policy-from-a-word-document-using-the-java-api}を使用してWordドキュメントからポリシーを削除する

ドキュメントセキュリティAPI (Java)を使用して、ポリシーで保護されたWordドキュメントからポリシーを削除します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-rightsmanagement-client.jarなどのクライアントJARファイルを含めます。

1. ドキュメントセキュリティクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護されたWordドキュメントの取得

   * コンストラクターを使用し、Wordドキュメントーの場所を指定する文字列値を渡すことで、ポリシーで保護されたWordドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. Wordドキュメントからポリシーを削除します

   * `RightsManagementClient`オブジェクトの`getDocumentManager`メソッドを呼び出して、`DocumentManager`オブジェクトを作成します。
   * `DocumentManager`オブジェクトの`removeSecurity`メソッドを呼び出し、ポリシーで保護されたWordドキュメントを含む`com.adobe.idp.Document`オブジェクトを渡すことで、Wordドキュメントからポリシーを削除します。 このメソッドは、保護されていないWordドキュメントを含む`com.adobe.idp.Document`オブジェクトを返します。

1. 保護されていないWordドキュメントの保存

   * `java.io.File`オブジェクトを作成し、ファイル拡張子がDOCであることを確認します。
   * `Document`オブジェクトの`copyToFile`メソッドを呼び出して、`Document`オブジェクトの内容をファイルにコピーします（`removeSecurity`メソッドから返された`Document`オブジェクトを必ず使用してください）。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始（SOAPモード）:Java APIを使用したWordドキュメントからのポリシーの削除»

### WebサービスAPI {#remove-a-policy-from-a-word-document-using-the-web-service-api}を使用してWordドキュメントからポリシーを削除する

ドキュメントセキュリティAPI （Webサービス）を使用して、ポリシーで保護されたWordドキュメントからポリシーを削除します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. ドキュメントセキュリティクライアントAPIオブジェクトの作成

   * `RightsManagementServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`RightsManagementServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/RightsManagementService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `RightsManagementServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`RightsManagementServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`RightsManagementServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
   * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。


1. ポリシーで保護されたWordドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、ポリシーが削除された、ポリシーで保護されたWordドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、Wordドキュメントーのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。

1. Wordドキュメントからポリシーを削除します

   `RightsManagementServiceClient`オブジェクトの`removePolicySecurity`メソッドを呼び出し、ポリシーで保護されたWordドキュメントを含む`BLOB`オブジェクトを渡すことで、Wordドキュメントからポリシーを削除します。 このメソッドは、保護されていないWordドキュメントを含む`BLOB`オブジェクトを返します。

1. 保護されていないWordドキュメントの保存

   * コンストラクターを呼び出し、保護されていないWordドキュメントーのファイルの場所を表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `removePolicySecurity`メソッドから返された`BLOB`オブジェクトのデータ内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`フィールドの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。

**コードの例**

ドキュメントセキュリティサービスを使用したコードの例については、次のクイック開始を参照してください。

* 「クイック開始(MTOM):WebサービスAPIを使用してWordドキュメントからポリシーを削除する」

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
