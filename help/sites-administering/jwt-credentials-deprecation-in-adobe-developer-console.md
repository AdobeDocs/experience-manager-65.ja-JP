---
title: Adobe Developer Console での JWT 資格情報の廃止
description: AEM の Adobe Developer Console での JWT 資格情報の非推奨（廃止予定）の影響について説明します。
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 36c95ea717a0abcb0b6ef9b0796a94d7b0f66329
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 69%

---

# Adobe Developer Console での JWT 資格情報の廃止 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM as a Cloud Service のお客様は、[この記事](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html?lang=ja)を参照して詳細を確認してください。

アドビのお客様は、[Adobe Developer Console](https://developer.adobe.com/console) を使用すると、様々な API へのアクセスを可能にする資格情報を生成できます。お客様は、OAuth サーバー間からシングルページアプリまで、様々な資格情報タイプから選択できます。これらの資格情報タイプの 1 つであるサービスアカウント（JWT）資格情報は、OAuth サーバー間資格情報に代わって非推奨（廃止予定）になりました。新しいサービスアカウント（JWT）資格情報は 2024年6月3日（PT）以降は作成できなくなり、既存の JWT 資格情報は 2025年1月27日（PT）以降は機能しなくなります。非推奨（廃止予定）については、[こちら](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)を参照してください。

この記事では、AEM 6.5 のお客様が非推奨（廃止予定）にどのように対処する必要があるかについて、追加のコンテキストを提供します。

現時点での主な留意点は、AEM の機能で新しい OAuth サーバー間資格情報がまだサポートされていないことです。近日中にサポートを予定しています。最新のサービスパック 20 以前（サービスパック 21 以降には自動的に含まれます）を実行している場合は、AEM 6.5 用のインストールする特別な互換性パッケージを通じて、2024 年 5 月中旬までにサポートを開始します。 JWT 格情報を移行する手順が記載されたメールが届いている可能性がありますが、AEM で新しい OAuth サーバー間資格情報タイプがサポートされるまで、資格情報の移行を保留しても問題ありません。

以下では、AEMが 5 月中旬にサービスアカウント（JWT）資格情報をサポートした後で、お客様がサービスアカウント（JWT）資格情報を OAuth サーバー間資格情報に置き換える必要がある（または置き換えてはならない場合がある）シナリオを示します。 今後、資格情報を置き換える方法については、[こちら](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)を参照してください。

## AEM と他のアドビソリューションの統合 {#integrating-aem-with-other-adobe-solutions}

**アクション**:AEMでサポートされる 2024 年 5 月中旬以降まで、移行を待ちます。

**関連する AEM バージョン**：Adobe Managed Services（サービスパック 20 以前）。


AEM のお客様は、AEM オーサー UI を使用すると、他のすべてのアドビソリューション（例えば、Adobe Target、Adobe Analytics、Adobe Launch、AFCS など）との統合を設定できます。

![AEM と他のソリューションの統合](/help/sites-administering/assets/jwt-deprecation.png)

例えば、Adobe Target との統合を設定する手順については、[こちら](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/sites/administering/integration/integration-target-ims)を参照してください。の API キー [AEMでの IMS 設定の完了](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/sites/administering/integration/integration-target-ims#completing-the-ims-configuration-in-aem) AEMが 5 月中旬にこれらの資格情報をサポートしたら、セクションを OAuth サーバー間資格情報タイプに移行する必要があります。 これらの手順は、5 月中旬に改訂される予定で、新しい OAuth サーバー間資格情報の適用に役立つ予定です。

## Cloud Manager API {#cloud-manager-apis}

**アクション**:AEMでサポートされる 2024 年 5 月中旬以降まで、移行を待ちます。

**関連する AEM バージョン**：Adobe Managed Services（サービスパック 20 以前）。

お客様は Adobe Developer Console プロジェクトを作成すると、[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/) を呼び出すことができます。AEM と Cloud Manager でサポートされたら、Adobe Developer プロジェクトの資格情報を OAuth サーバー間資格情報タイプに移行する必要があります。
