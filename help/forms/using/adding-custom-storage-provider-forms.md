---
title: ドラフトと送信コンポーネントのカスタムストレージ
seo-title: ドラフトと送信コンポーネントのカスタムストレージ
description: ドラフトおよび送信用のユーザーデータの保存場所をカスタマイズする方法を説明します。
seo-description: ドラフトおよび送信用のユーザーデータの保存場所をカスタマイズする方法を説明します。
uuid: ac2e80ee-a9c7-44e6-801e-fe5a840cb7f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 154255e7-468a-42e6-a33d-eee691cf854d
translation-type: tm+mt
source-git-commit: 615b0db6da0986d7a74c42ec0d0e14bad7ede168
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 70%

---


# ドラフトと送信コンポーネントのカスタムストレージ {#custom-storage-for-drafts-and-submissions-component}

## 概要 {#overview}

AEM Forms ではフォームをドラフトとして保存できます。ドラフト機能により、作業中のフォームを維持できるようになります。任意のデバイスから後でフォームを完成させて、送信できます

By default, AEM Forms stores the user data associated with the draft and submission of a form in the `/content/forms/fp` node on the Publish instance. さらに、AEM Forms ポータルコンポーネントではデータサービスを使用でき、これを使用するとドラフトと送信のユーザーデータの保存の実装をカスタマイズできます。例えば、ユーザーデータをデータストアに保存できます。

## 前提条件  {#prerequisites}

* フ [ォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md)
* Create a [forms portal page](/help/forms/using/creating-form-portal-page.md)
* フォームポータルでの [アダプティブフォームの有効化](/help/forms/using/draft-submission-component.md)
* カスタムストレージの [導入の詳細を知る](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## ドラフトデータサービス {#draft-data-service}

ドラフトのユーザーデータの保存場所をカスタマイズするには、`DraftDataService` インターフェイスのすべてのメソッドを実装する必要があります。次のサンプルコードでメソッドと引数を説明します。

```java
/**
 * DraftDataService service will get/delete/save user data (attachments and form data) filled with a draft instance of Form
 */

public interface DraftDataService {

    /**
     * To save/modify user data for this userDataID, it will be null in case of creation
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
>ドラフトIDフィールドの長さの最小値は26文字です。 Adobeでは、ドラフトIDの長さを26文字以上に設定することをお勧めします。

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

フォームポータルでは、UUID（Universally Unique Identifier）の概念を使用して、ドラフトや送信済みフォームそれぞれに一意の ID を生成します。自分の一意の ID を作成することもできます。インターフェイスFPKeyGeneratorServiceを実装し、そのメソッドを上書きし、カスタムロジックを開発して、すべてのドラフトおよび送信済みフォームに対してカスタムの一意のIDを生成できます。 また、カスタム ID 生成の実装のサービスランクを 0 より高く設定します。これにより、デフォルトの実装ではなくカスタムの実施が確実に使用されるようになります。

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

上記の注釈を使用するには、次をプロジェクトに読み込みます。

```java
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
```

