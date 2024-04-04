---
title: Adobe Developer Console での JWT 資格情報の非推奨（廃止予定）
description: AEM の Adobe Developer Console での JWT 資格情報の非推奨（廃止予定）の影響について説明します。
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
source-git-commit: dec88af3b2345d142d0cc3bc27cfbc27804ab57e
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 53%

---

# Adobe Developer Console での JWT 資格情報の非推奨（廃止予定） {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM as a Cloud Service は、 [この記事](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html) を参照してください。

アドビのお客様は、[Adobe Developer Console](https://developer.adobe.com/console) を使用すると、様々な API へのアクセスを可能にする資格情報を生成できます。お客様は、OAuth サーバー間からシングルページアプリまで、様々な資格情報タイプから選択できます。これらの資格情報タイプの 1 つであるサービスアカウント（JWT）資格情報は、OAuth サーバー間資格情報に代わって非推奨（廃止予定）になりました。新しいサービスアカウント (JWT) 資格情報は 2024 年 6 月 3 日以降は作成できず、2025 年 1 月 27 日以降は既存の JWT 資格情報は機能しません。 非推奨（廃止予定）については、[こちら](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)を参照してください。

この記事では、AEM 6.5 のお客様による廃止の処理方法に関する追加のコンテキストを説明します。

現時点での主な留意点は、AEM の機能で新しい OAuth サーバー間資格情報がまだサポートされていないことです。最新の Service Pack 20 以前を実行している場合（Service Pack 21 以降が自動的に含まれる）、2024 年 4 月下旬までに、AEM 6.5 用にインストールする特別な互換性パッケージを通じて、サポートが提供される予定です。 JWT 格情報を移行する手順が記載されたメールが届いている可能性がありますが、AEM で新しい OAuth サーバー間資格情報タイプがサポートされるまで、資格情報の移行を保留しても問題ありません。

以下の節では、AEMが 4 月下旬にサポートした後に、サービスアカウント (JWT) 資格情報を OAuth サーバー間資格情報に置き換える（または置き換えない）必要があるシナリオについて説明します。 今後、資格情報を置き換える方法については、[こちら](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)を参照してください。

## AEM と他のアドビソリューションの統合 {#integrating-aem-with-other-adobe-solutions}

**アクション**:2024 年 4 月下旬 (AEMがサポートする場合 ) まで移行を待ちます。

**関連するAEMバージョン**:AdobeManaged Services（Service Pack 20 以前）。


AEM のお客様は、AEM オーサー UI を使用すると、他のすべてのアドビソリューション（例えば、Adobe Target、Adobe Analytics、Adobe Launch、AFCS など）との統合を設定できます。

![AEM と他のソリューションの統合](/help/sites-administering/assets/jwt-deprecation.png)

例えば、Adobe Target との統合を設定する手順については、[こちら](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=ja)を参照してください。の API キー [AEMでの IMS 設定の完了](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=ja#completing-the-ims-configuration-in-aem) AEMが 4 月下旬にこれらの資格情報をサポートするようになれば、セクションは OAuth サーバー間資格情報タイプに移行する必要があります。 これらの手順は、新しい OAuth サーバー間資格情報を適用するのに役立つよう、4 月下旬に更新されます。

## Cloud Manager API {#cloud-manager-apis}

**アクション**:2024 年 4 月下旬 (AEMがサポートする場合 ) まで移行を待ちます。

**関連するAEMバージョン**:AdobeManaged Services（Service Pack 20 以前）。

お客様は Adobe Developer Console プロジェクトを作成すると、[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/) を呼び出すことができます。AEM と Cloud Manager でサポートされたら、Adobe Developer プロジェクトの資格情報を OAuth サーバー間資格情報タイプに移行する必要があります。
