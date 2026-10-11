---
title: ドラフトと送信に使用するストレージサービスの設定
description: ドラフトと送信に使用するストレージの設定方法について説明します
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 51ca2844-91f0-453a-9b39-b876399ebecb
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: fa155e29-cba2-5e77-9efd-4824be5ce4c8
    internal-label: Forms Portal
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 100%
---
# ドラフトと送信に使用するストレージサービスの設定 {#configuring-storage-services-for-drafts-and-submissions}

## 概要 {#overview}

AEM Forms では以下を格納できます。

* **ドラフト**：後で送信するためエンドユーザーが入力して保存した作業中のフォーム。

* **送信**：ユーザーが入力したデータが含まれている送信済みフォーム。

AEM Forms ポータルのデータサービスおよびメタデータサービスは、ドラフトと送信をサポートします。 データはデフォルトでパブリッシュインスタンスに格納されます。その後、設定したオーサーインスタンスにリバースレプリケートされ、他のパブリッシュインスタンスで使用できるようになります。

初期設定されている既存の方法では、個人情報（PII）を含めたすべてのデータがパブリッシュインスタンスに格納される点が懸念されます。

上記のデフォルトの方法のほか、フォームデータをローカルに保存するのではなく、直接処理にプッシュする代替実装も利用できます。 パブリッシュインスタンスに潜在的な機密データを格納したくない顧客は、データを処理サーバーに送信する代替実装を選択できます。 処理はオーサーインスタンスで実行されるので、通常はより安全なゾーンに存在します。

>[!NOTE]
>
>「フォームポータル」送信アクションを使用したり、アダプティブフォームでフォームポータルにデータを保存するオプションを有効にしたりすると、フォームデータは AEM リポジトリーに保存されます。 本番環境では、ドラフトまたは送信されたフォームデータを AEM リポジトリに保存しないことをお勧めします。 代わりに、ドラフトと送信コンポーネントをエンタープライズデータベースなどの安全なストレージと統合して、ドラフトと送信済みフォームデータを格納する必要があります。
>
>詳しくは、「[ドラフト&amp;送信コンポーネントとデータベースの統合](/help/forms/using/integrate-draft-submission-database.md)」を参照してください。

## フォームポータルのドラフトサービスおよび送信サービスの設定 {#configuring-forms-portal-drafts-and-submissions-services}

AEM web コンソール設定（`https://[host]:'port'/system/console/configMgr`）で、「**Forms Portal Draft and Submission Configuration**」をクリックし、編集モードで開きます。

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

AEM web コンソール設定（`https://[host]:'port'/system/console/configMgr`）で、「**AEM DS Settings Service**」をクリックし、編集モードで開きます。 AEM DS 設定サービスダイアログで、処理サーバーの URL、ユーザー名、パスワードを入力します。

>[!NOTE]
>
>ユーザーデータをデータベースに格納するためのサンプル実装も提供されます。 ユーザーデータを既存のデータベースに格納するデータサービスとメタデータサービスを設定する方法を理解するには、「[サンプル：ドラフトと送信コンポーネントのデータベースへの統合](/help/forms/using/integrate-draft-submission-database.md)」を参照してください。
