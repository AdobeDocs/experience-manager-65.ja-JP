---
title: ドラフトと送信に使用するストレージサービスの設定
description: ドラフトと送信に使用するストレージの設定方法について説明します
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 51ca2844-91f0-453a-9b39-b876399ebecb
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 100%

---

# ドラフトと送信に使用するストレージサービスの設定 {#configuring-storage-services-for-drafts-and-submissions}

## 概要 {#overview}

AEM Forms では以下を格納できます。

* **ドラフト**：後で送信するためエンドユーザーが入力して保存した作業中のフォーム。

* **送信**：ユーザーが入力したデータが含まれている送信済みフォーム。

AEM Forms ポータルのデータサービスおよびメタデータサービスは、ドラフトと送信をサポートします。データはデフォルトでパブリッシュインスタンスに格納されます。その後、設定したオーサーインスタンスにリバースレプリケートされ、他のパブリッシュインスタンスで使用できるようになります。

初期設定されている既存の方法では、個人情報（PII）を含めたすべてのデータがパブリッシュインスタンスに格納される点が懸念されます。

上記のデフォルトの方法のほか、フォームデータをローカルに保存するのではなく、直接処理にプッシュする代替実装も利用できます。パブリッシュインスタンスに潜在的な機密データを格納したくない顧客は、データを処理サーバーに送信する代替実装を選択できます。処理はオーサーインスタンスで実行されるので、通常はより安全なゾーンに存在します。

>[!NOTE]
>
>「フォームポータル」送信アクションを使用したり、アダプティブフォームでフォームポータルにデータを保存するオプションを有効にしたりすると、フォームデータは AEM リポジトリーに保存されます。実稼働環境では、ドラフトまたは送信されたフォームデータを AEM リポジトリーに保存しないことをお勧めします。代わりに、ドラフトと送信コンポーネントをエンタープライズデータベースなどの安全なストレージと統合して、ドラフトと送信済みフォームデータを格納する必要があります。
>
>詳しくは、「[ドラフト&amp;送信コンポーネントとデータベースの統合](/help/forms/using/integrate-draft-submission-database.md)」を参照してください。

## フォームポータルのドラフトサービスおよび送信サービスの設定 {#configuring-forms-portal-drafts-and-submissions-services}

AEM Web Console Configuration（`https://[host]:'port'/system/console/configMgr`）で、「**Forms Portal Draft and Submission Configuration**」をクリックし、編集モードで開きます。

以下の説明に従い、要件に基づいてプロパティの値を指定します。

### パブリッシュインスタンスにデータを格納する標準のサービス {#out-of-the-box-services-to-store-data-on-publish-instance}

データは設定したオーサーインスタンスにリバースレプリケートされます。

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>値</th>
  </tr>
  <tr>
   <td>フォームポータルドラフトデータサービス（ドラフトデータサービス（<strong>draft.data.service</strong>）の識別子）</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>フォームポータルドラフトメタデータサービス（ドラフトメタデータサービス（<strong>draft.metadata.service</strong>）の識別子）</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>フォームポータル送信データサービス（送信データサービス（<strong>submit.data.service</strong>）の識別子）</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>フォームポータル送信メタデータサービス（送信メタデータサービス（<strong>submit.metadata.service</strong>）の識別子）</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### リモート処理用インスタンスにデータを格納する標準のサービス {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

データは設定したリモートインスタンスに直接プッシュされます。

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>値</th>
  </tr>
  <tr>
   <td>フォームポータルドラフトデータサービス（ドラフトデータサービス（<strong>draft.data.service</strong>）の識別子）</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>フォームポータルドラフトメタデータサービス（ドラフトメタデータサービス（<strong>draft.metadata.service</strong>）の識別子）</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>フォームポータル送信データサービス（送信データサービス（<strong>submit.data.service</strong>）の識別子）</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>フォームポータル送信メタデータサービス（送信メタデータサービス（<strong>submit.metadata.service</strong>）の識別子）</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

上記に示した設定のほか、設定したリモート処理用インスタンスの情報を入力します。

AEM Web Console Configuration（`https://[host]:'port'/system/console/configMgr`）で、「**AEM DS Settings Service**」をクリックし、編集モードで開きます。AEM DS 設定サービスダイアログで、処理サーバーの URL、ユーザー名、パスワードを入力します。

>[!NOTE]
>
>ユーザーデータをデータベースに格納するためのサンプル実装も提供されます。ユーザーデータを既存のデータベースに格納するデータサービスとメタデータサービスを設定する方法を理解するには、「[サンプル：ドラフトと送信コンポーネントのデータベースへの統合](/help/forms/using/integrate-draft-submission-database.md)」を参照してください。
