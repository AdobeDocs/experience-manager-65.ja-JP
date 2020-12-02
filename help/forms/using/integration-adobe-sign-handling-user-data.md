---
title: Adobe Sign との統合| ユーザーデータの処理
seo-title: Adobe Sign との統合| ユーザーデータの処理
description: Adobe Sign との統合| ユーザーデータの処理
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 70%

---


# Adobe Sign との統合| ユーザーデータの処理 {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] を と統合すると、アダプティブフォームで電子署名ワークフローが有効になり、法務、販売、給与、人事管理のワークフローのフォームまたは契約書を処理することができます。[!DNL  Adobe Sign]これにより、1 人のユーザーおよび複数ユーザーの署名、連続署名および並列署名のワークフロー、匿名ユーザーまたはログインしたユーザーでの署名フォームなど、様々なユーザー認証方法が可能になります。

署名者または複数の署名者がアダプティブフォームに署名して送信すると、[!DNL Adobe Sign]契約が生成され、署名者に関する情報が含まれます。

[!DNL AEM Forms]と[!DNL Adobe Sign]の統合について詳しくは、[アダプティブフォームでのAdobe Signの使用](/help/forms/using/working-with-adobe-sign.md)を参照してください。

## ユーザーデータとデータストア {#data}

[!DNL Adobe Sign] 対応のアダプティブフォームには署名者に関する情報が含まれています。これにはアダプティブフォームで収集された他のユーザーのデータが含まれている場合があります。[!DNL Adobe Sign]サービスは、ユーザーデータを契約内の署名と共に保存します。 契約書は、[!DNL AEM Forms]クラウドサービスで設定された[!DNL Adobe Sign]サーバーに保存されます。 さらに、Forms Portal の送信アクションを使用するようにアダプティブフォームが構成されている場合、契約書のデータはフォームデータとともに Forms Portal のデータストアに格納されます。

## ユーザーデータへのアクセスと削除  {#access-and-delete-user-data}

ユーザーデータは契約書内で収集されますが、いずれのサービステーブルにも保存されません。[!DNL Adobe Sign] を使用すると、管理者はサービスで管理する管理データを自身で選択できます。[!DNL Adobe Sign]サービスのプライバシー管理者は、要求者の電子メールアドレスに基づいて、契約のリストや削除を行うことができます。

[!DNL Adobe Sign] は、参加者による契約書の検索、および必要に応じて契約書の削除を実行できる Web アプリケーションを提供しています。詳しくは、[Adobe Sign — 機能：ユーザー情報を削除](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html)。

Forms Portal の送信アクションを使用するように構成されているアダプティブフォームの契約書データも、Forms Portal のデータストアに格納されます。Forms Portal のデータストアにアクセスしてデータを削除する方法については、「[Forms Portal | ユーザーデータの処理](/help/forms/using/forms-portal-handling-user-data.md)」を参照してください。
