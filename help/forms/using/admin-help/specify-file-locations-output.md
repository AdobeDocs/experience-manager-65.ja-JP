---
title: Output のファイルの場所の指定
description: 特定のタイプのファイルに対して、Output のファイルの場所を指定する方法について説明します。例えば、コンテンツルート URI、XCI 設定ファイル、キャッシュ、デフォルトなどです。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 620c69d6-4fe1-46d6-b5d4-3b562142e547
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 100%

---

# Output のファイルの場所の指定 {#specify-file-locations-for-output}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

Output で必要な、特定のタイプのファイルを検索する場所を指定できます。

1. 管理コンソールで、サービス／Output をクリックします。
1. 「場所」で、適切なオプションを指定します。
1. 「保存」をクリックします。

## 場所の設定 {#locations-settings}

**コンテンツルート URI：**&#x200B;フォームの取得元であるリポジトリの URI または絶対位置。この値と、API 経由で指定された sForm パラメーターを連結して、フォームの取得元である絶対パスが作られます。この値で参照できるのは、特定のディレクトリまたは HTTP でアクセス可能な web 上の場所です。

デフォルト値は空の文字列です。

**XCI 設定ファイル：** Output サービスがレンダリングで使用する XCI 設定ファイルの相対位置または絶対位置です。相対パスの場合は、AEM Forms のデプロイ可能な EAR ファイル内に XCI ファイルが保存されていることが前提となります。

デフォルト値は `com/adobe/formServer/PA/pa_output.xci` です。

**キャッシュの場所：** Output ディスクキャッシュの場所を指定します。この設定を変更すると、現在の場所の既存のキャッシュ情報すべてがリセットされ、新しいキャッシュが新しい場所に作成されます。次のいずれかのオプションを選択します。

**デフォルトの場所：** これはデフォルトの選択です。このオプションを選択すると、次のように使用しているアプリケーションサーバーによって決まる場所にキャッシュが作成されます。

* **JBoss:** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic:** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[Forms Server name]\Output\Cache`
* **WebSphere:** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**LC の一時ディレクトリ：**&#x200B;キャッシュは、AEM Forms の一時ディレクトリのサブディレクトリ（管理コンソールの、設定／コアシステム設定／設定／一時ディレクトリの場所で指定）に作成されます。サブディレクトリの名前は `adobeoutput_[servername]` です。

>[!NOTE]
>
>一時クリーニングユーティリティを使用している場合、これらのディレクトリの削除は機能に影響しませんが、新しいキャッシュが作成されるまで、短期間パフォーマンスが大きく低下する可能性があります。このような問題を回避するには、AEM Forms の一時ディレクトリの消去中、これらのディレクトリを削除しないでください。
