---
title: Acrobat Reader DC Extensions で使用するタイムアウト値の設定
seo-title: Setting timeout values for use with Acrobat Reader DC extensions
description: Acrobat Reader DC Extensions で使用するタイムアウト値の設定方法について説明します。
seo-description: Learn how to set timeout values for use with Acrobat Reader DC extensions.
uuid: d6d072a0-0a30-417a-98b1-df8b4ff8f911
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a9aeeb89-45e9-4d5d-aa25-8145c89b64f2
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 100%

---

# Acrobat Reader DC Extensions で使用するタイムアウト値の設定  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

Acrobat Reader DC Extensions で多数の PDF ファイルを処理している場合は、以下のタイムアウト値を適切に設定して、ジョブがタイムアウトして失敗するのを防ぎます。

**ドキュメント廃棄タイムアウト：**

この値は管理コンソールで設定できます。設定／コアシステム設定／設定を選択し、「デフォルトのドキュメント廃棄タイムアウト」に値を指定します。

**User Manager AEM Forms のタイムアウト：**&#x200B;この値を設定するには、config.xml ファイルを編集してください。 管理コンソールで、設定／User Management／設定／既存の設定ファイルの読み込みと書き出しをクリックし、「書き出し」をクリックします。書き出された config.xml ファイルを開き、次の行を編集します。

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

config.xml ファイルを保存し、再び管理コンソールに読み込みます。

**アプリケーションサーバーセッションタイムアウト：**&#x200B;この値は、アプリケーションサーバーで設定できます。 詳しくは、アプリケーションサーバーに付属するマニュアルを参照してください。
