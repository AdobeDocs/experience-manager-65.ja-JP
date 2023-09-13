---
title: AEM Forms アプリの配布
description: モバイルデバイスでのアプリの大規模なデプロイメントには、モバイルデバイス管理 (MDM) を使用します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 22%

---

# AEM Forms アプリの配布 {#distribute-aem-forms-app}

モバイルデバイス管理 (MDM) を使用すると、モバイルデバイスでのアプリの大規模なデプロイメントを可能にします。

>[!NOTE]
>
>この配布は、iOSおよび Android™デバイスにのみ適用されます。

## MDM ソリューションが提供する主な機能： {#main-features-generally-provided-by-mdm-solutions}

* エンタープライズ環境でのデバイス登録の有効化
* デバイス設定の設定と更新の許可
* セキュリティコンプライアンスの執行
* 企業リソースへのモバイルアクセスの保護

MDM ソリューションとモバイルアプリケーション管理を組み合わせることで、企業内のモバイルデバイス全体で、社内、公開、購入したアプリを管理できます。

MDM 管理者は、ipa ファイルと apk ファイルの両方を MDM サーバーにアップロードし、ipa ファイルまたは apk ファイルにアクセスできるユーザーを制御できます。 管理者は、各アプリケーションに対応するプロファイル設定を制御することもできます。

## AEM Forms アプリケーションに影響するプロファイル設定 {#profile-settings-affecting-the-aem-forms-app-br}

デバイスでの次のプロファイル設定は、デバイスでのAEM Formsアプリの機能に影響します。

* **カメラの使用を許可** （内） **デバイスの機能** セクション

を無効にした場合、 **カメラの使用を許可**（のカメラ機能） [写真注釈](/help/forms/using/add-attachments.md) は機能しません。 アプリでカメラを使用するには、このオプションを有効にします。

* **デバイスでのパスコードの要求** 「Passcode policies」セクションの

**アプリケーションデータの暗号化** を有効にするには、デバイスの **パスコード** を有効にすることをお勧めします。デバイスにパスコードが設定されていない場合、デバイスに保存されているアプリケーションデータは暗号化されません。
