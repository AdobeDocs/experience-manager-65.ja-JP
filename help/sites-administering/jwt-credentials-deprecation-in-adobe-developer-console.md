---
title: Adobe Developer Console での JWT 資格情報の廃止
description: AEM の Adobe Developer Console での JWT 資格情報の非推奨（廃止予定）の影響について説明します。
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 36c95ea717a0abcb0b6ef9b0796a94d7b0f66329
workflow-type: ht
source-wordcount: '456'
ht-degree: 100%

---

# Adobe Developer Console での JWT 資格情報の廃止 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM as a Cloud Service のお客様は、[この記事](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html?lang=ja)を参照して詳細を確認してください。

アドビのお客様は、[Adobe Developer Console](https://developer.adobe.com/console) を使用すると、様々な API へのアクセスを可能にする資格情報を生成できます。お客様は、OAuth サーバー間からシングルページアプリまで、様々な資格情報タイプから選択できます。これらの資格情報タイプの 1 つであるサービスアカウント（JWT）資格情報は、OAuth サーバー間資格情報に代わって非推奨（廃止予定）になりました。新しいサービスアカウント（JWT）資格情報は 2024年6月3日（PT）以降は作成できなくなり、既存の JWT 資格情報は 2025年1月27日（PT）以降は機能しなくなります。非推奨（廃止予定）については、[こちら](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)を参照してください。

この記事では、AEM 6.5 のお客様が非推奨（廃止予定）にどのように対処する必要があるかについて、追加のコンテキストを提供します。

現時点での主な留意点は、AEM の機能で新しい OAuth サーバー間資格情報がまだサポートされていないことです。最新のサービスパック 20 以前（サービスパック 21 以降には自動的に含まれます）を実行している場合、サポートは、まもなく（2024年5 月中旬までに）AEM 6.5 にインストールする特別な互換性パッケージを通じて提供される予定です。お客様には JWT 資格情報を移行する手順が記載されたメールが届いているかもしれませんが、AEM で新しい OAuth サーバー間資格情報タイプがサポートされるまで、資格情報の移行を保留してください。

以下の節では、AEM で 5月中旬にサポートされた後、お客様がサービスアカウント（JWT）資格情報を OAuth サーバー間資格情報に置き換える必要がある（場合によっては置き換えてはいけない）シナリオを示します。今後、資格情報を置き換える方法については、[こちら](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)を参照してください。

## AEM と他のアドビソリューションの統合 {#integrating-aem-with-other-adobe-solutions}

**アクション**：AEM でサポートが開始する 2024年5月中旬以降まで移行を待ちます。

**関連する AEM バージョン**：Adobe Managed Services（サービスパック 20 以前）。


AEM のお客様は、AEM オーサー UI を使用すると、他のすべてのアドビソリューション（例えば、Adobe Target、Adobe Analytics、Adobe Launch、AFCS など）との統合を設定できます。

![AEM と他のソリューションの統合](/help/sites-administering/assets/jwt-deprecation.png)

例えば、Adobe Target との統合を設定する手順については、[こちら](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/sites/administering/integration/integration-target-ims)を参照してください。[AEM での IMS 設定の完了](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/sites/administering/integration/integration-target-ims#completing-the-ims-configuration-in-aem)の節に記載されている API キーは、5月下旬に AEM でこれらの資格情報がサポートされ次第、OAuth サーバー間資格情報タイプに移行する必要があります。これらの手順は、新しい OAuth サーバー間資格情報を適用できるように、5月中旬に改訂される予定です。

## Cloud Manager API {#cloud-manager-apis}

**アクション**：AEM でサポートが開始する 2024年5月中旬以降まで移行するのを待ちます。

**関連する AEM バージョン**：Adobe Managed Services（サービスパック 20 以前）。

お客様は Adobe Developer Console プロジェクトを作成すると、[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/) を呼び出すことができます。AEM と Cloud Manager でサポートされたら、Adobe Developer プロジェクトの資格情報を OAuth サーバー間資格情報タイプに移行する必要があります。