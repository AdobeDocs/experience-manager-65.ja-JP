---
title: Adobe Developer Console での JWT 資格情報の廃止
description: AEM の Adobe Developer Console での JWT 資格情報の非推奨（廃止予定）の影響について説明します。
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 3aa55b88f589749fb49d5ff46340b0912d490157
workflow-type: ht
source-wordcount: '362'
ht-degree: 100%

---

# Adobe Developer Console での JWT 資格情報の廃止 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM as a Cloud Service のお客様は、[AEMaaCS バージョンの同等の記事](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html?lang=ja)を参照して詳細を確認してください。

アドビのお客様は、[Adobe Developer Console](https://developer.adobe.com/console) を使用すると、様々な API へのアクセスを可能にする資格情報を生成できます。お客様は、OAuth サーバー間からシングルページアプリまで、様々な資格情報タイプから選択できます。これらの資格情報タイプの 1 つであるサービスアカウント（JWT）資格情報は、OAuth サーバー間資格情報に代わって非推奨（廃止予定）になりました。新しいサービスアカウント（JWT）資格情報は 2024年6月3日（PT）以降は作成できなくなり、既存の JWT 資格情報は 2025年1月27日（PT）以降は機能しなくなります。非推奨（廃止予定）については、[こちら](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)を参照してください。

この記事では、Adobe Experience Manager（AEM）6.5 のお客様が非推奨（廃止予定）にどのように対処する必要があるかを説明した追加のコンテキストを提供します。

主なポイントは、AEM で AEM の新しい OAuth サーバー間資格情報をサポートするようになったということです。JWT 資格情報を移行する手順が記載されたメールを受信した場合は、この移行を今すぐ実行できます。

以下の節では、AEM でサポートするようになり、お客様がサービスアカウント（JWT）資格情報を OAuth サーバー間資格情報に置き換える必要がある（場合によっては置き換えてはいけない）シナリオを示します。資格情報を移行する方法については、[こちら](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)を参照してください。

## AEM と他のアドビソリューションの統合 {#integrating-aem-with-other-adobe-solutions}

**アクション**：AEM で OAuth 資格情報をサポートするようになったので、設定を移行します。

**関連する AEM バージョン**：Adobe Managed Services（サービスパック 21 以降）。

AEM のお客様は、AEM を使用して他のすべてのアドビソリューションとの統合を設定します。例えば、Adobe Target、Adobe Analytics などです。

![AEM と他のソリューションの統合](/help/sites-administering/assets/jwt-deprecation.png)

次の方法について詳しくは、[AEM の IMS 統合の設定](/help/sites-administering/setting-up-ims-integrations-for-aem.md)を参照してください。

* OAuth 資格情報を使用した設定の作成
* JWT 資格情報を使用して作成された設定を移行した、OAuth 資格情報の使用

## Cloud Manager API {#cloud-manager-apis}

**アクション**：JWT 資格情報から OAuth 資格情報に移行できるタイミングを確認します。

**関連する AEM バージョン**：Adobe Managed Services（サービスパック 21 以降）。

お客様は Adobe Developer Console プロジェクトを作成すると、[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/) を呼び出すことができます。非推奨の JWT 資格情報の有効期限が 2025年1月に切れる前に、Adobe Developer プロジェクトの資格情報を OAuth サーバー間資格情報タイプに移行する必要があります。
