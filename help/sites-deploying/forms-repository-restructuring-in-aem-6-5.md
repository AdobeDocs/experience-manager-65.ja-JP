---
title: AEM 6.5 における Forms リポジトリの再構築
seo-title: AEM 6.5 における Forms リポジトリの再構築
description: AEM 6.5 for Forms の新しいリポジトリ構造に移行するために必要な変更を加える方法について説明します。
seo-description: AEM 6.5 for Forms の新しいリポジトリ構造に移行するために必要な変更を加える方法について説明します。
uuid: e60830d4-23ca-4be9-941a-ee4abe4786a6
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 1ce9a622-5968-407f-a74b-d325a2bff669
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 83%

---


# AEM 6.5 における Forms リポジトリの再構築{#forms-repository-restructuring-in-aem}

AEM 6.5](/help/sites-deploying/repository-restructuring.md)の親ページ[リポジトリの再構築に関する説明に従い、AEM 6.5にアップグレードしたお客様は、このページを使用して、AEM Forms・ソリューションに影響を与えるリポジトリの変更に関連する作業量を評価する必要があります。 一部の変更ではAEM 6.5のアップグレードプロセス中に作業が必要になり、残りの変更は将来のアップグレードまで延期できます。

**6.5 へのアップグレード時におこなう変更**

* [その他](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**今後のアップグレードの前**

* [EchoSign クラウドサービス設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [reCAPTCHA クラウドサービス設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [Typekit クラウドサービス設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [その他](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## 6.5 へのアップグレード時におこなう変更 {#with-upgrade}

### その他 {#misc}

| **以前の場所** | `/etc/clientlibs/fd/fp` |
|---|---|
| **新しい場所** | `/libs/fd/fp/components` |
| **再構築の手引き** | カスタムコードから「従来の」の場所への明示的な参照は、「新しい」の場所に更新する必要があります。 |
| **備考** | これらのクライアントライブラリは、変更したり拡張したりしないでください。 |

| **以前の場所** | `/etc/clientlibs/fd/rte` |
|---|---|
| **新しい場所** | `/libs/fd/rte` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットでは新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/af` |
|---|---|
| **新しい場所** | `/libs/fd/af/authoring/clientlibs` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットでは新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **新しい場所** | `/libs/fd/xfaforms/clientlibs/` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットでは新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/af` |
|---|---|
| **新しい場所** | `/libs/fd/af/runtime/clientlibs` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットでは新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/af` |
|---|---|
| **新しい場所** | `/libs/fd/af/runtime/clientlibs` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットでは新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **新しい場所** | `/libs/fd/expeditor/clientlibs` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットでは新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **新しい場所** | `/libs/fd/fmaddon` |
| **再構築の手引き** | これらのクライアントライブラリを変更することは推奨されず、サポートもされていません。変更された場合は、AEM 提供のコードを使用するようにクライアントライブラリをロールバックしてください。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/aep` |
|---|---|
| **新しい場所** | `/var/fd/content/annotations` |
| **再構築の手引き** | これらのクライアントライブラリを変更することは推奨されず、サポートもされていません。変更された場合は、AEM 提供のコードを使用するようにクライアントライブラリをロールバックしてください。 |
| **備考** | 該当なし |

## 将来のアップグレードの前{#prior-to-upgrade}

### EchoSign クラウドサービス設定 {#echosign-cloud-service-configuration}

| **以前の場所** | `/etc/cloudservices/echosign` |
|---|---|
| **新しい場所** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **再構築の手引き** | [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md)ユーティリティを Forms 移行 UI からトリガーします。 |
| **備考** | 該当なし |

### reCAPTCHA クラウドサービス設定  {#recaptcha-cloud-service-configurations}

| **以前の場所** | `/etc/cloudservices/recaptcha` |
|---|---|
| **新しい場所** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **再構築の手引き** | [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md)ユーティリティを Forms 移行 UI からトリガーします。 |
| **備考** | 該当なし |

### Typekit クラウドサービス設定  {#typekit-cloud-service-configurations}

| **以前の場所** | `/etc/cloudservices/typekit` |
|---|---|
| **新しい場所** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **再構築の手引き** | [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md)ユーティリティを Forms 移行 UI からトリガーします。 |
| **備考** | 該当なし |

### その他  {#misc-1}

| **以前の場所** | `/etc/cloudservices/fdm` |
|---|---|
| **新しい場所** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **再構築の手引き** | [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md)ユーティリティを Forms 移行 UI からトリガーします。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/designs/fd/fp` |
|---|---|
| **新しい場所** | `/libs/fd/fp` |
| **再構築の手引き** | /etcテンプレートへの参照は、最終的に`/libs`に対応するを指すように更新される必要があります。 |
| **備考** | 該当なし |

