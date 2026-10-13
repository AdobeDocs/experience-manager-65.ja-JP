---
title: 設定プロパティの暗号化サポート
description: AEM で提供される設定プロパティの暗号化サポートについて説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
exl-id: 3c3db1c8-5b22-45dd-aeaf-5cf830a9486b
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c35bc059-fd80-4a01-91a6-e48da3c76758
    internal-label: Security practices
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 100%
---
# 設定プロパティの暗号化サポート{#encryption-support-for-configuration-properties}

## 概要 {#overview}

この機能を使用すると、すべての OSGI 設定プロパティをクリアテキストではなく保護された暗号化形式で保存できます。 Web コンソール UI のフォームは、システム全体の暗号化プライマリキーを使用して、クリアテキストから暗号化テキストを作成するために使用されます。

OSGi 設定プラグインのサポートは、サービスによって使用される前に、プロパティを復号化するために追加されました。

>[!NOTE]
>
>暗号化された値を予期するサービスは、値を復号化する前に IsProtected チェックを使用して、暗号化されているかどうかを確認する必要があります。

## 暗号化サポートの有効化 {#enabling-encryption-support}

これらの手順は、メールサービスの SMTP パスワードを暗号化する方法を示します。 暗号化する OSGI プロパティに対してこれらの手順を完了します。

1. AEM web コンソール（*https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*）にアクセスします。
1. 左上隅の **Main／Crypto Support** に移動します。

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. **Adobe Experience Manager web コンソール Crypto Support** ページが表示されます。

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. 「**Plain Text**」フィールドに保護する機密データのテキストを入力します。
1. 「**Protect**」を選択します。 保護されたテキストは暗号化されたテキストとして表示されます。

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. 手順 5 の保護テキストをコピーして OSGI フォーム値にペーストします。 この例では、暗号化された **SMTP パスワード** は *Day CQ Mail Service* に追加されます。

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. Day CQ Mail Service のプロパティを保存します。 SMTP パスワードは暗号化された値として送信されます。

## 復号化サポート {#decryption-support}

AEM は現在、設定プロパティを復号化するための設定プラグインを提供しています。 この AEM プラグインは自動的に復号化してクリアテキストプロパティを取得します。
