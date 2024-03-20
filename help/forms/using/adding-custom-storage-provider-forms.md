---
title: ドラフトと送信コンポーネントのカスタムストレージ
description: ドラフトと送信用のユーザーデータの保存場所をカスタマイズする方法を説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
feature: Forms Portal
exl-id: b1300eeb-2653-4bb5-b2fd-88048c9c43b9
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 100%

---

# ドラフトと送信コンポーネントのカスタムストレージ {#custom-storage-for-drafts-and-submissions-component}

## 概要 {#overview}

AEM Forms ではフォームをドラフトとして保存できます。ドラフト機能により、作業中のフォームを維持できるようになります。任意のデバイスから後でフォームを完成させて、送信できます。

デフォルトでは、AEM Forms はフォームのドラフトと送信に関連付けられたユーザーデータをパブリッシュインスタンスの `/content/forms/fp` ノードに保存します。さらに、AEM Forms ポータルコンポーネントではデータサービスを使用でき、これを使用するとドラフトと送信のユーザーデータの保存の実装をカスタマイズできます。例えば、ユーザーデータをデータストアに保存できます。

## 前提条件  {#prerequisites}

* [フォームポータルコンポーネント](/help/forms/using/enabling-forms-portal-components.md)を有効にする
* [フォームポータルページ](/help/forms/using/creating-form-portal-page.md)を作成する
* [フォームポータル用アダプティブフォーム](/help/forms/using/draft-submission-component.md)を有効にする
* [カスタムストレージの実装の詳細](/help/forms/using/draft-submission-component.md#customizing-the-storage)を学ぶ

## ドラフトデータサービス {#draft-data-service}

ドラフトのユーザーデータの保存場所をカスタマイズするには、`DraftDataService` インターフェイスのすべてのメソッドを実装する必要があります。次のサンプルコードでメソッドと引数を説明します。

```java
/**
 * DraftDataService service will get/delete/save user data (attachments and form data) filled with a draft instance of Form
 */

public interface DraftDataService {

    /**
     * To save/modify user data for this userDataID, it will be null if there is creation
     * @param draftDataID: unique identifier associated with the form data
     * @param formName: name of the form whose draft is being saved
     * @param formData: user data associated with this draft
     * @return userdataID corresponding to which user data has been stored and which can be used later to retrieve this user data
     * @throws FormsPortalException
     */
    public String saveData (String draftDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Returns the user data stored against the ID passed as the argument
     * @param userDataID: unique data id for user data associated with a draft
     * @return user data associated with this data ID
     * @throws FormsPortalException
     */

    public byte[] getData (String userDataID) throws FormsPortalException;

    /**
     * To delete data associated with this draft
     * @param userDataID: unique data id for data associated with a draft
     * @return status of delete operation on data associated with this draft
     * @throws FormsPortalException
     */

    public boolean deleteData (String userDataID) throws FormsPortalException;

    /**
     * Saves the attachment for current form instance
     * @param attachmentsBytes: byte array of the attachment to be saved
     * @return unique id (attachmentID) for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment (byte[] attachmentBytes) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

>[!NOTE]
>
>ドラフト ID フィールドの長さの最小値は 26 文字です。アドビでは、ドラフト ID の長さを 26 文字以上に設定することをお勧めします。

## 送信データサービス {#submission-data-service}

送信用のユーザーデータの保存場所をカスタマイズするには、`SubmitDataService` インターフェイスのすべてのメソッドを実装する必要があります。次のサンプルコードでメソッドと引数を説明します。

```java
/**
 * SubmitDataService service will get/delete/submit user data (attachments and form data) filled with a submission of Form
 */
public interface SubmitDataService {

    /**
     * Submits the user data passed in argument map
     * @param userDataID, unique identifier associated with this user data
     * @param formName, name of the form whose draft is being submitted
     * @param formData, user data associated with this submission
     * @return userdataID, corresponding to which the user data has been stored and which can be used later to retrieve this data
     * @throws FormsPortalException
     */
    public String saveData (String userDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Submits the user data provided as byte array
     * @param id
     * @param data
     * @return id corresponding to saved data
     * @throws FormsPortalException
     */
    public String saveData (String id, byte[] data) throws FormsPortalException;

    /** Submits the user data provided as byte array asynchronously for the user name provided in the options map
     * @param data data to be saved in bytes
     * @param options map containing options that affect this save
     * @return id of the saved data instance
     */
    public String saveDataAsynchronusly(byte[] data, Map<String, Object> options) throws FormsPortalException;

    /**
     * Gets the user data stored against the ID passed as argument
     * @param userDataID: unique id associated with this user data for this submission
     * @return user data associated with this submission
     * @throws FormsPortalException
     */
    public byte[] getData(String userDataID) throws FormsPortalException;

    /**
     * Deletes user data stored against the userDataID
     * @param userDataID: unique id associated with this user data for this submission
     * @return status of the delete operation on this submission
     * @throws FormsPortalException
     */

    public boolean deleteData(String userDataID) throws FormsPortalException;

    /**
     * Submits the attachment bytes passed as argument
     * @param attachmentsBytes: would expect byte array of the attachment for this submission
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment(byte[] attachmentBytes) throws FormsPortalException;

    /** Submits the attachment bytes passed as argument asynchronously for the user id provided in options map.
     * @param attachmentBytes would expect byte array of the attachment for this submission
     * @param options map containing options that affect this save
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachmentAsynchronously(byte[] attachmentBytes, Map<String, Object> options) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: Unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

フォームポータルでは、ユニバーサル固有識別子（UUID）の概念を使用して、ドラフトや送信済みフォームそれぞれに一意の ID を生成します。独自の一意の ID を作成することもできます。FPKeyGeneratorService インターフェースを実装して、メソッドをオーバーライドし、カスタムの論理を開発してドラフトや送信済みフォームそれぞれに一意の ID を生成することができます。また、カスタム ID 生成の実装のサービスランクを 0 より高く設定します。これにより、デフォルトの実装ではなくカスタムの実施が確実に使用されるようになります。

```java
public interface FPKeyGeneratorService {
    /**
     * returns a unique id for draft and submission
     *
     * @param none
     * @return unique id in string format as per the implementation
     * @throws FormsPortalException
     */
    public String getUniqueId() throws FormsPortalException;
}
```

上記のコードを使用して生成したカスタム ID のサービスの順位付けを上げるには、以下の注釈を使用します。

`@Properties(value = { @Property(name = "service.ranking", intValue = 15) } )`

上記の注釈を使用するには、以下をプロジェクトにインポートします。  

```java
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
```
