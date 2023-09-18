---
title: Acrobat Reader DC Extensions で使用するタイムアウト値の設定
description: Acrobat Reader DC Extensions で使用するタイムアウト値を設定する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 24%

---

# Acrobat Reader DC Extensions で使用するタイムアウト値の設定  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

Acrobat Reader DC Extensions で多くのPDFファイルを操作する場合は、ジョブのタイムアウトと失敗を防ぐために、次のタイムアウト値が適切に設定されていることを確認してください。

**ドキュメント廃棄タイムアウト：**

この値は管理コンソールで設定できます。 設定/コアシステム設定/設定をクリックし、「デフォルトのドキュメント廃棄タイムアウト」の値を指定します。

**User Manager AEM Forms のタイムアウト：**&#x200B;この値を設定するには、config.xml ファイルを編集してください。管理コンソールで、設定/User Management/設定/設定/設定ファイルの読み込みと書き出しをクリックし、「書き出し」をクリックします。 書き出された config.xml ファイルを開き、次の行を編集します。

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

config.xml ファイルを保存し、管理コンソールに再度読み込みます。

**アプリケーションサーバーセッションタイムアウト：**&#x200B;この値は、アプリケーションサーバーで設定できます。詳しくは、アプリケーションサーバーに付属するマニュアルを参照してください。
