---
title: AEM Forms アプリの配布
seo-title: AEM Forms アプリの配布
description: Mobile Device Management（MDM）を使用すると、モバイルデバイスでアプリケーションの大規模なデプロイメントを実行できます。
seo-description: Mobile Device Management（MDM）を使用すると、モバイルデバイスでアプリケーションの大規模なデプロイメントを実行できます。
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# AEM Forms アプリの配布 {#distribute-aem-forms-app}

Mobile Device Management（MDM）により、モバイルデバイスでアプリケーションの大規模なデプロイメントを実行できます。

>[!NOTE]
>
>今回の公開は、iOS および Android デバイスのみ該当します。

## MDM ソリューションによって一般的に提供される主な機能： {#main-features-generally-provided-by-mdm-solutions}

* エンタープライズ環境でのデバイス登録の有効化
* デバイス設定の設定と更新の許可
* セキュリティコンプライアンスの執行
* 企業リソースへのモバイルアクセスの保護

MDM ソリューションと Mobile Application Management により、企業のモバイルデバイスにおける社内用、公共用、および購入済みのアプリケーションを管理できます。

MDM 管理者は ipa ファイルと apk ファイルの両方を MDM サーバーにアップロードし、ipa ファイルまたは apk ファイルにアクセスできるユーザーをコントロールできます。管理者は、各アプリケーションに対応するプロファイル設定を管理することもできます。

## AEM Forms アプリケーションに影響するプロファイル設定 {#profile-settings-affecting-the-aem-forms-app-br}

お使いのプロファイルの次の設定は、お使いのデバイスのAEM Formsアプリケーションの機能に影響します。

* 「**Device functionality**」セクションの「**Allow use of camera**」

「**Allow use of camera**」を無効にすると、[写真注釈](/help/forms/using/add-attachments.md)のカメラ機能は使えません。 アプリケーションでカメラを使用するには、このオプションを有効にする必要があります。

* 「Passcode policies」セクションの「**Require passcode on device**」

**アプリケーションデータの暗号化** を有効にするには、デバイスの **パスコード** を有効にすることをお勧めします。 デバイスでパスコードが設定されていないと、デバイスに保存されているアプリケーションデータは暗号化されません。
