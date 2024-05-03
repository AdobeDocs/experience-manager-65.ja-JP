---
title: AEM Forms アプリの配布
description: モバイルデバイス管理（MDM）を使用すると、モバイルデバイスでアプリケーションの大規模なデプロイメントを実行できます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 100%

---

# AEM Forms アプリの配布 {#distribute-aem-forms-app}

モバイルデバイス管理（MDM）により、モバイルデバイスでアプリケーションの大規模なデプロイメントを実行できます。

>[!NOTE]
>
>今回の公開は、iOS および Android™ デバイスのみ該当します。

## MDM ソリューションによって提供される主な機能： {#main-features-generally-provided-by-mdm-solutions}

* エンタープライズ環境でのデバイス登録の有効化
* デバイス設定の設定と更新の許可
* セキュリティコンプライアンスの執行
* 企業リソースへのモバイルアクセスの保護

MDM ソリューションとモバイルアプリケーション管理により、企業のモバイルデバイスにおける社内用、公共用、および購入済みのアプリケーションを管理できます。

MDM 管理者は ipa ファイルと apk ファイルの両方を MDM サーバーにアップロードし、ipa ファイルまたは apk ファイルにアクセスできるユーザーを管理できます。管理者は、各アプリケーションに対応するプロファイル設定を管理することもできます。

## AEM Forms アプリケーションに影響するプロファイル設定 {#profile-settings-affecting-the-aem-forms-app-br}

お使いのデバイスにおける次のプロファイル設定は、デバイスの AEM Forms アプリケーションの機能に影響を与えます。

* 「**Device functionality**」セクションの「**Allow use of camera**」

「**Allow use of camera**」を無効にすると、[写真注釈](/help/forms/using/add-attachments.md)のカメラ機能は使えません。アプリでカメラを使用するには、このオプションを有効にします。

* 「Passcode policies」セクションの「**Require passcode on device**」

**アプリケーションデータの暗号化** を有効にするには、デバイスの **パスコード** を有効にすることをお勧めします。デバイスでパスコードが設定されていないと、デバイスに保存されているアプリケーションデータは暗号化されません。
