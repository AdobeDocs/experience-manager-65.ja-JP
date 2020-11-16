---
title: Acrobat Reader DC Extensions で使用するタイムアウト値の設定
seo-title: Acrobat Reader DC Extensions で使用するタイムアウト値の設定
description: Acrobat Reader DC Extensions で使用するタイムアウト値の設定方法について説明します。
seo-description: Acrobat Reader DC Extensions で使用するタイムアウト値の設定方法について説明します。
uuid: d6d072a0-0a30-417a-98b1-df8b4ff8f911
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a9aeeb89-45e9-4d5d-aa25-8145c89b64f2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 85%

---


# Acrobat Reader DC Extensions で使用するタイムアウト値の設定  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

Acrobat Reader DC Extensions で多数の PDF ファイルを処理している場合は、以下のタイムアウト値を適切に設定して、ジョブがタイムアウトして失敗するのを防ぎます。

**ドキュメント廃棄タイムアウト：**

この値は管理コンソールで設定できます。設定／コアシステム設定／設定を選択し、「デフォルトのドキュメント廃棄タイムアウト」に値を指定します。

**User Manager AEM formsタイムアウト：** この値は、config.xmlファイルを編集することで設定できます。 管理コンソールで、設定／User Management／設定／既存の設定ファイルの読み込みと書き出しをクリックし、「書き出し」をクリックします。書き出された config.xml ファイルを開き、次の行を編集します。

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

config.xml ファイルを保存し、再び管理コンソールに読み込みます。

**アプリケーションサーバーセッションタイムアウト：** この値は、アプリケーションサーバーで設定できます。 詳しくは、アプリケーションサーバーに付属するマニュアルを参照してください。
