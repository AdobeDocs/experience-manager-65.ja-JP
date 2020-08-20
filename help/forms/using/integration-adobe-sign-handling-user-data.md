---
title: Adobe Sign との統合| ユーザーデータの処理
seo-title: Adobe Sign との統合| ユーザーデータの処理
description: 'null'
seo-description: 'null'
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
translation-type: tm+mt
source-git-commit: 4e0709031aca030e50840811a9b3717f3cb20340
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 69%

---


# Adobe Sign との統合| ユーザーデータの処理 {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] を と統合すると、アダプティブフォームで電子署名ワークフローが有効になり、法務、販売、給与、人事管理のワークフローのフォームまたは契約書を処理することができます。[!DNL  Adobe Sign]これにより、1 人のユーザーおよび複数ユーザーの署名、連続署名および並列署名のワークフロー、匿名ユーザーまたはログインしたユーザーでの署名フォームなど、様々なユーザー認証方法が可能になります。

When a signer or multiple signers sign and submit an adaptive form, an [!DNL Adobe Sign] agreement is generated that includes information about the signers.

For more information about [!DNL AEM Forms] integration with [!DNL Adobe Sign], see [Using Adobe Sign in an adaptive form](/help/forms/using/working-with-adobe-sign.md).

## ユーザーデータとデータストア {#data}

[!DNL Adobe Sign] 対応のアダプティブフォームには署名者に関する情報が含まれています。これにはアダプティブフォームで収集された他のユーザーのデータが含まれている場合があります。The [!DNL Adobe Sign] service saves user data with the signature within the agreement. The agreement is saved on [!DNL Adobe Sign] server configured in [!DNL AEM Forms] cloud services. さらに、Forms Portal の送信アクションを使用するようにアダプティブフォームが構成されている場合、契約書のデータはフォームデータとともに Forms Portal のデータストアに格納されます。

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

ユーザーデータは契約書内で収集されますが、いずれのサービステーブルにも保存されません。[!DNL Adobe Sign] を使用すると、管理者はサービスで管理する管理データを自身で選択できます。Privacy administrators on the [!DNL Adobe Sign] service can list or remove agreements based on the email address of a requestor.

[!DNL Adobe Sign] は、参加者による契約書の検索、および必要に応じて契約書の削除を実行できる Web アプリケーションを提供しています。詳しくは、 [Adobe Sign — 機能：ユーザー情報の削除](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html)。

Forms Portal の送信アクションを使用するように構成されているアダプティブフォームの契約書データも、Forms Portal のデータストアに格納されます。Forms Portal のデータストアにアクセスしてデータを削除する方法については、「[Forms Portal | ユーザーデータの処理](/help/forms/using/forms-portal-handling-user-data.md)」を参照してください。
