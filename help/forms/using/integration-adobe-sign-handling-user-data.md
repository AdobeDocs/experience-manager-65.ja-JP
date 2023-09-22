---
title: Adobe Sign との統合| ユーザーデータの処理
description: Adobe Sign との統合| ユーザーデータの処理
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Acrobat Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: f7b24617dec77c6907798b1615debdc2329c9d80
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 58%

---

# Adobe Sign との統合| ユーザーデータの処理 {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] を と統合すると、アダプティブフォームで電子署名ワークフローが有効になり、法務、販売、給与、人事管理のワークフローのフォームまたは契約書を処理することができます。[!DNL  Adobe Sign]これにより、1 人のユーザーおよび複数ユーザーの署名、連続署名および並列署名のワークフロー、匿名ユーザーまたはログインしたユーザーでの署名フォームなど、様々なユーザー認証方法が可能になります。

1 人または複数の署名者がアダプティブフォームに署名をして送信するときに、署名者に関する情報を含む [!DNL Adobe Sign] の契約書が生成されます。

[!DNL AEM Forms] の [!DNL Adobe Sign] との統合について詳しくは、[アダプティブフォームで Adobe Sign を使用する](/help/forms/using/working-with-adobe-sign.md)を参照してください。

## ユーザーデータとデータストア {#data}

[!DNL Adobe Sign] 対応のアダプティブフォームには署名者に関する情報が含まれています。これにはアダプティブフォームで収集された他のユーザーのデータが含まれている場合があります。[!DNL Adobe Sign] サービスは、契約書内の署名を使用してユーザーデータを格納します。契約は [!DNL Adobe Sign] サーバーが次の場所で設定されています： [!DNL AEM Forms] クラウドサービス。 さらに、Formsポータルの送信アクションを使用するようにアダプティブフォームが設定されている場合、契約データはフォームデータと共にFormsポータルのデータストアに保存されます。

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

ユーザーデータは契約内で収集されますが、どのサービステーブルにも保存されません。 [!DNL Adobe Sign] を使用すると、管理者は、サービスで制御するデータの管理に関して独自に選択できます。 [!DNL Adobe Sign] サービスのプライバシー管理者は、依頼者のメールアドレスに基づいて契約書のリストの作成または削除を行うことができます。

[!DNL Adobe Sign] は、参加者による契約の検索を可能にし、必要に応じて削除する Web アプリケーションを提供します。 詳しくは、[Adobe Sign - 機能：ユーザー情報の削除](https://helpx.adobe.com/jp/sign/help/adobesign_gdpr_user_deletion.html)を参照してください。

Formsポータル送信アクションを使用するように設定されたアダプティブフォームの契約データも、Formsポータルデータストアに保存されます。 Forms Portal データストアにアクセスして削除する方法については、 [Forms Portal |ユーザーデータの処理](/help/forms/using/forms-portal-handling-user-data.md).
