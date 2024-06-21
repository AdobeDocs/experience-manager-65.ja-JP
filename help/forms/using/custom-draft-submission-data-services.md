---
title: ドラフトおよび送信データサービスのカスタマイズ
description: デフォルトでは、AEM Forms はドラフトと送信済みのアダプティブフォームをパブリッシュインスタンスのデフォルトのノードに保存します。ただし、AEM Forms のドラフトと送信データサービスを設定することにより、ドラフトおよび送信済みアダプティブフォームのストレージをカスタマイズできます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: ed10ef8c-7b9c-43cf-bea8-7cf9742a8cac
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 100%

---

# ドラフトおよび送信データサービスのカスタマイズ {#customizing-draft-and-submission-data-services}

## 概要 {#overview}

AEM Forms ではアダプティブフォームをドラフトとして保存できます。ドラフト機能により、ユーザーは作業中のフォームを維持できます。これにより、ユーザーはデバイスを問わずいつでもフォームに記入して送信できます。

デフォルトでは、AEM Forms はドラフトと送信に関連付けられたユーザーデータを `/content/forms/fp` ノードのパブリッシュインスタンスに保存します。

ただし、AEM Forms ポータルコンポーネントは、ドラフトおよび送信用のユーザーデータの保存の実装をカスタマイズするデータサービスを提供します。例えば、組織に現在実装されているデータストアにデータを保存できます。

ユーザーデータのストレージをカスタマイズするには、[ドラフトデータ](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p)および[送信データ](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p)サービスを参照してください。

## 前提条件 {#prerequisites}

* [フォームポータルコンポーネント](/help/forms/using/enabling-forms-portal-components.md)を有効にする
* [フォームポータルページ](/help/forms/using/creating-form-portal-page.md)を作成する
* [フォームポータル用アダプティブフォーム](/help/forms/using/draft-submission-component.md)を有効にする
* [カスタムストレージの実装の詳細](/help/forms/using/draft-submission-component.md#customizing-the-storage)を学ぶ

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
  * @param draftUserDataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID") if there is update
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

ユーザーの送信データのストレージをカスタマイズするには、`SubmittedAFDataService` インターフェイスのすべてのメソッドに対して実装を指定する必要があります。

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
