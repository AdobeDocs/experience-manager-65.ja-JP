---
title: AEM 6.5 における Forms リポジトリの再構築
description: AEM 6.5 for Formsの新しいリポジトリ構造への移行に必要な変更を加える方法について説明します。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: d555422e-dc97-4d45-9525-4299d22315e2
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 42%

---

# AEM 6.5 における Forms リポジトリの再構築{#forms-repository-restructuring-in-aem}

[AEM 6.5 におけるリポジトリの再構築](/help/sites-deploying/repository-restructuring.md)の親ページで説明しているように、AEM 6.5 にアップグレードする場合は、このページを参考に、AEM Forms ソリューションに影響を及ぼすリポジトリ変更に伴う作業量を評価する必要があります。一部の変更は AEM 6.5 アップグレードプロセス中に作業が必要ですが、それ以外は今後のアップグレードまで延期できます。

**6.5 へのアップグレード時におこなう変更**

* [その他](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**今後のアップグレードの前に**

* [EchoSign クラウドサービス設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [reCAPTCHA クラウドサービス設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [Typekit クラウドサービス設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [その他](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## 6.5 へのアップグレード時におこなう変更 {#with-upgrade}

### その他 {#misc}

| **以前の場所** | `/etc/clientlibs/fd/fp` |
|---|---|
| **新しい場所** | `/libs/fd/fp/components` |
| **再構築の手引き** | カスタムコード内で従来の場所を明示的に参照している場合は、新しい場所に更新する必要があります。 |
| **備考** | これらのクライアントライブラリは、編集または拡張しないでください。 |

| **以前の場所** | `/etc/clientlibs/fd/rte` |
|---|---|
| **新しい場所** | `/libs/fd/rte` |
| **再構築の手引き** | クライアントライブラリのリソースを絶対パスで参照できる場合は、新しいアセットで新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/af` |
|---|---|
| **新しい場所** | `/libs/fd/af/authoring/clientlibs` |
| **再構築の手引き** | クライアントライブラリのリソースを絶対パスで参照できる場合は、新しいアセットで新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **新しい場所** | `/libs/fd/xfaforms/clientlibs/` |
| **再構築の手引き** | クライアントライブラリのリソースを絶対パスで参照できる場合は、新しいアセットで新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/af` |
|---|---|
| **新しい場所** | `/libs/fd/af/runtime/clientlibs` |
| **再構築の手引き** | クライアントライブラリのリソースを絶対パスで参照できる場合は、新しいアセットで新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/af` |
|---|---|
| **新しい場所** | `/libs/fd/af/runtime/clientlibs` |
| **再構築の手引き** | クライアントライブラリのリソースを絶対パスで参照できる場合は、新しいアセットで新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **新しい場所** | `/libs/fd/expeditor/clientlibs` |
| **再構築の手引き** | クライアントライブラリのリソースを絶対パスで参照できる場合は、新しいアセットで新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **新しい場所** | `/libs/fd/fmaddon` |
| **再構築の手引き** | これらの clientlibs の変更は、推奨もサポートもされていませんでした。 これらの clientlib に変更が加えられている場合は、ロールバックしてAEM提供のコードを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/aep` |
|---|---|
| **新しい場所** | `/var/fd/content/annotations` |
| **再構築の手引き** | これらの clientlibs の変更は、推奨もサポートもされていませんでした。 これらの clientlib に変更が加えられている場合は、ロールバックしてAEM提供のコードを使用する必要があります。 |
| **備考** | 該当なし |

## 今後のアップグレードの前に {#prior-to-upgrade}

### EchoSign クラウドサービス設定 {#echosign-cloud-service-configuration}

| **以前の場所** | `/etc/cloudservices/echosign` |
|---|---|
| **新しい場所** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **再構築の手引き** | この [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md) Forms移行 UI からトリガーされるユーティリティ。 |
| **備考** | 該当なし |

### reCAPTCHA クラウドサービス設定 {#recaptcha-cloud-service-configurations}

| **以前の場所** | `/etc/cloudservices/recaptcha` |
|---|---|
| **新しい場所** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **再構築の手引き** | この [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md) Forms移行 UI からトリガーされるユーティリティ。 |
| **備考** | 該当なし |

### Typekit クラウドサービス設定 {#typekit-cloud-service-configurations}

| **以前の場所** | `/etc/cloudservices/typekit` |
|---|---|
| **新しい場所** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **再構築の手引き** | この [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md) Forms移行 UI からトリガーされるユーティリティ。 |
| **備考** | 該当なし |

### その他 {#misc-1}

| **以前の場所** | `/etc/cloudservices/fdm` |
|---|---|
| **新しい場所** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **再構築の手引き** | この [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md) Forms移行 UI からトリガーされるユーティリティ。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/designs/fd/fp` |
|---|---|
| **新しい場所** | `/libs/fd/fp` |
| **再構築の手引き** | /etc テンプレートへの参照をすべて、の参照を指すように更新します `/libs` 対応する。 |
| **備考** | 該当なし |
