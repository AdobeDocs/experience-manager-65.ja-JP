---
title: ドラフトおよび送信データサービスのカスタマイズ
seo-title: ドラフトおよび送信データサービスのカスタマイズ
description: デフォルトでは、AEM Forms はドラフトと送信済みのアダプティブフォームをパブリッシュインスタンスのデフォルトのノードに保存します。ただし、AEM Forms のドラフトと送信データサービスを設定することにより、ドラフトおよび送信済みアダプティブフォームのストレージをカスタマイズできます。
seo-description: デフォルトでは、AEM Forms はドラフトと送信済みのアダプティブフォームをパブリッシュインスタンスのデフォルトのノードに保存します。ただし、AEM Forms のドラフトと送信データサービスを設定することにより、ドラフトおよび送信済みアダプティブフォームのストレージをカスタマイズできます。
uuid: c3ec1708-3b11-4142-93f0-1cffb6643f34
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 602fd6a9-9a65-411c-8475-a4082a3fdee0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 80%

---


# ドラフトおよび送信データサービスのカスタマイズ {#customizing-draft-and-submission-data-services}

## 概要 {#overview}

AEM Forms ではアダプティブフォームをドラフトとして保存できます。ドラフト機能により、ユーザーは作業中のフォームを維持することができます。これにより、ユーザーはデバイスを問わずいつでもフォームに記入および送信できます。

By default, AEM Forms stores the user data associated with the draft and submission on the Publish instance in the `/content/forms/fp` node.

ただし、AEM Forms ポータルコンポーネントは、ドラフトおよび送信用のユーザーデータの保存の実装をカスタマイズするデータサービスを提供します。例えば、組織に現在実装されているデータストアにデータを保存することができます。

ユーザーデータのストレージをカスタマイズするには、[ドラフトデータ](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p)および[送信データ](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p)サービスを参照してください。

## 前提条件 {#prerequisites}

* [Formsポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md)
* Create a [forms portal page](/help/forms/using/creating-form-portal-page.md)
* フォームポータルでの [アダプティブフォームの有効化](/help/forms/using/draft-submission-component.md)
* カスタムストレージの [導入の詳細を知る](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## ドラフトデータサービス {#draft-data-service}

ユーザーのドラフトデータのストレージをカスタマイズするには、`DraftAFDataService` インターフェイスのすべてのメソッドに対して実装を指定する必要があります。

メソッドとその引数の説明を、次のインターフェイスのコードサンプルに示します。

```java
public interface DraftAFDataService {

 /**
  * Deletes the user data stored against the ID passed as the argument
  *
  * @param draftDataID
  * @return status for the just occurred delete draft UserData operation
  * @throws FormsPortalException
  */
 public Boolean deleteAFDraftUserData (String draftDataID) throws FormsPortalException;

 /**
  * Saves user data provided in the argument map
  *
  * @param draftUserDataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID") in case of update
  * @return userData ID would be returned which needs to be saved in metadata node
  * @throws FormsPortalException
  */
 public String saveAFUserData (Map<String, Object> draftUserDataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as the argument
  *
  * @param Draft DataID
  * @return guideState (which would then be populated in adaptive form to reload the draft) which is stored against draftDataID
  * @throws FormsPortalException
  */
 public byte[] getAFDraftUserData(String draftDataID) throws FormsPortalException;

 /**
  * Saves the attachments for current adaptive form instance
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String saveAttachments(byte[] attachmentBytes) throws FormsPortalException;
}
```

## 送信データサービス {#submission-data-service}

To customize the storage of user submission data, you need to provide implementation for all the methods of the `SubmittedAFDataService` interface.

メソッドとその引数の説明を、次のインターフェイスのコードサンプルに示します。

```java
public interface SubmittedAFDataService {

 /**
  * Submits the user data passed in argument map
  *
  * @param submittedAFUserdataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID")
  * @return userData ID is returned that needs to be saved in the metadata node
  * @throws FormsPortalException
  */
 public String submitAFUserData (Map<String, Object> submittedAFUserdataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as argument
  *
  * @param submitDataID
  * @return guideState which would be used to open DOR
  * @throws FormsPortalException
  */
 public byte[] getSubmittedAFUSerData(String submitDataID) throws FormsPortalException;

 /**
  * Deletes user data stored against the ID passed as argument
  *
  * @param Submit DataID
  * @return status of the delete operation on Submitted User data
  * @throws FormsPortalException
  */

 public Boolean deleteSubmittedAFUserData(String submitDataID) throws FormsPortalException;

 /**
  * Submits the attachment bytes passed as argument
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String submitAttachments(Object attachmentBytes) throws FormsPortalException;

}
```

