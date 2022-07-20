---
title: ドラフトと送信に使用するストレージサービスの設定
seo-title: Configuring storage services for drafts and submissions
description: ドラフトと送信に使用するストレージの設定方法を学習します
seo-description: Learn how to configure storage for drafts and submissions
uuid: 2f4efc07-312c-4908-8c91-84f4e6c5ad25
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6ebb6420-68b6-4abc-b298-c252db038416
exl-id: 51ca2844-91f0-453a-9b39-b876399ebecb
source-git-commit: 8ef957d1f4efd00c48395cb5a51024ea63649eea
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 100%

---

# ドラフトと送信に使用するストレージサービスの設定 {#configuring-storage-services-for-drafts-and-submissions}

## 概要 {#overview}

AEM Forms では以下を格納できます。

* **ドラフト**：後で送信するためエンドユーザーが入力して保存した作業中のフォーム。

* **送信**：ユーザーが入力したデータが含まれている送信済みフォーム。

AEM Forms ポータルのデータサービスおよびメタデータサービスは、ドラフトと送信をサポートします。データはデフォルトでパブリッシュインスタンスに格納されます。その後、設定したオーサーインスタンスに逆複製され、他のパブリッシュインスタンスで使用できるようになります。

初期設定されている既存の方法では、個人情報（PII）を含めたすべてのデータがパブリッシュインスタンスに格納される点が懸念されます。

上記のデフォルトの方法のほか、ローカルに保存する代わりにフォームデータを「処理」に直接発行するといった代替処理を行うこともできます。パブリッシュインスタンスに機密データを格納したくない顧客は、データを「処理」サーバーに送信する代替処理を選択できます。「処理」はオーサーインスタンスで実行されるため、通常、より安全なゾーンに存在します。

>[!NOTE]
>
>「フォームポータル」送信アクションを使用したり、アダプティブフォームでフォームポータルにデータを保存するオプションを有効にしたりすると、フォームデータは AEM リポジトリーに保存されます。実稼働環境では、ドラフトまたは送信されたフォームデータを AEM リポジトリーに保存しないことをお勧めします。代わりに、ドラフトと送信コンポーネントをエンタープライズデータベースなどの安全なストレージと統合して、ドラフトと送信済みフォームデータを格納する必要があります。
>
>詳しくは、「[ドラフト&amp;送信コンポーネントとデータベースの統合](/help/forms/using/integrate-draft-submission-database.md)」を参照してください。

## フォームポータルのドラフトサービスおよび送信サービスの設定 {#configuring-forms-portal-drafts-and-submissions-services}

AEM Web Console Configuration（`https://[host]:'port'/system/console/configMgr`）で、「**Forms Portal Draft and Submission Configuration**」をクリックし、編集モードで開きます。

以下の説明に従い、要件に基づいてプロパティの値を指定します。

### パブリッシュインスタンスにデータを格納する初期設定済みサービス {#out-of-the-box-services-to-store-data-on-publish-instance}

データは設定したオーサーインスタンスに逆複製されます。

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>値</th>
  </tr>
  <tr>
   <td>フォームポータル ドラフトデータサービス（ドラフトデータサービス（<strong>draft.data.service</strong>）の識別子）</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>フォームポータル ドラフトメタデータサービス（ドラフトメタデータサービス（<strong>draft.metadata.service</strong>）の識別子）</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>フォームポータル 送信データサービス（送信データサービス（<strong>submit.data.service</strong>）の識別子）</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>フォームポータル 送信メタデータサービス（送信メタデータサービス（<strong>submit.metadata.service</strong>）の識別子）</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### リモート処理用インスタンスにデータを格納する初期設定済みボックスサービス {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

データは設定したリモートインスタンスに直接プッシュされます。

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>値</th>
  </tr>
  <tr>
   <td>フォームポータル ドラフトデータサービス（ドラフトデータサービス（<strong>draft.data.service</strong>）の識別子）</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>フォームポータル ドラフトメタデータサービス（ドラフトメタデータサービス（<strong>draft.metadata.service</strong>）の識別子）</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>フォームポータル 送信データサービス（送信データサービス（<strong>submit.data.service</strong>）の識別子）</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>フォームポータル 送信メタデータサービス（送信メタデータサービス（<strong>submit.metadata.service</strong>）の識別子）</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

上記に示した設定のほか、設定したリモート処理用インスタンスの情報を入力します。

AEM Web Console Configuration（`https://[host]:'port'/system/console/configMgr`）で、「**AEM DS Settings Service**」をクリックし、編集モードで開きます。AEM DS Settings Service ダイアログで、処理サーバーの URL、ユーザー名、パスワードを入力します。

>[!NOTE]
>
>ユーザーデータをデータベースに格納するためのサンプル実装も提供されます。ユーザーデータを既存のデータベースに格納するデータサービスとメタデータサービスを設定する方法を理解するには、「[サンプル：ドラフトと送信コンポーネントのデータベースへの統合](/help/forms/using/integrate-draft-submission-database.md)」を参照してください。
