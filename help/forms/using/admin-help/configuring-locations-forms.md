---
title: Forms の場所の設定
seo-title: Forms の場所の設定
description: Forms の場所の設定方法について説明します。
seo-description: Forms の場所の設定方法について説明します。
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Forms の場所の設定 {#configuring-locations-for-forms}

Web ルート、検索対象フォームの場所、PDFForm 変換で使用するシード PDF ファイル、キャッシュの場所などの属性の URL、URI およびファイルの場所を指定できます。

1. 管理コンソールで、サービス／Forms をクリックします。
1. 「場所」で、適切なオプションを指定します。オプションについては後述します。
1. 「保存」をクリックします。

## 場所の設定 {#locations-settings}

**ベースURL:** 画像やスクリプトなどのフォームリソースが配置されるベースURLです。 HTML 変換に画像やスクリプトなどの外部依存の HREF 参照が含まれている場合は、この値が必須となります。このようなスクリプトの 1 つに xfasubset.js があります。xfasubset.js は HTML フォームで XFA インテリジェンスを実行するのに必要です。この値は HTTP 形式のコンテンツルート URI である必要があります。

>[!NOTE]
>
>Base URL では HTTP プロトコルまたはリポジトリプロトコルのみがサポートされています。file:/// のようなプロトコルはサポートされていません。カスタム CSS またはデジタル署名 URI などのリソースにアクセスする必要がある場合は、適切な API パラメーターの値を使用して絶対位置を指定します。

依存パスが絶対パスのとき、ベース URL 値は無視されます。それ以外の場合、依存パスはベース URL と連結されます。

デフォルト値は空の文字列です。

次の例は、（コンテンツルート URI とベース URL を使用して）同じコンテンツを指しています。

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**FS Web Root URI:** Forms WebアプリケーションのURL。 Forms Web アプリケーションとクライアントアプリケーションを同じアプリケーションサーバーにデプロイする場合は、このボックスを空白のままにしておくことができます。その場合は Forms API Web ルート URL が使用されます。

Forms Web アプリケーションとクライアントアプリケーションを同じアプリケーションサーバーにデプロイしない場合は、次の例に示すように、このボックスに Forms Web アプリケーションの URL を入力する必要があります。

`https://<host name>:<port>/FormServer`

`host name` と `port` には、それぞれ Forms Web アプリケーションをホストするサーバーのサーバー名とポート番号を入力します。

デフォルト値は空の文字列です。

**WebルートURI:** アプリケーションのWebルート。 この値と、AEM Forms SDK を介して指定された sTargetURL パラメーターを連結して（sTargetURL が相対 URL の場合）、アプリケーション固有の Web コンテンツにアクセスするための絶対 URL が作成されます。

デフォルト値は空の文字列です。

**コンテンツルートURI:** フォームの取得元のURIまたは絶対位置。 この値と、API 経由で指定された sFormQuery パラメーターを連結して、フォームの取得先である絶対パスが作られます。この値で参照できるのは、特定のディレクトリか、HTTP でアクセス可能な Web 上の場所です。

デフォルト値は空の文字列です。

**XCI Configuration URI:** レンダリングに使用するXCIファイルの相対パスまたは絶対パスが見つかります。 相対パスの場合は、デプロイ可能な AEM Forms EAR ファイル内に XCI ファイルが保存されていることが前提となります。

デフォルト値は `com/adobe/formServer/PA/pa.xci` です。

**Font Map URI:** フォントマッピングファイルの相対パスまたは絶対パスです。 相対パスの場合は、デプロイ可能な AEM Forms EAR ファイル内にこのファイルが保存されていることが前提となります。

フォントマップファイルによってフォーム内に HTML 変換のためのカスタムフォントマップが作成されます。こうすると、クライアントコンピューターに存在しないフォントを別のフォントに置き換えるように指定することができます。

デフォルト値は `com/adobe/formServer/client-font-map.properties` です。

次のエントリは、フォントマップファイル内のエントリの例です。

`Arial=Arial,Helvetica,sans-serif`

**シードPDFファイル：** 配信を最適化するためにPDFForm変換で使用される初期PDFファイルです。 シード PDF ファイルで指定する特別な PDF ファイル（XFA ストリーム、画像およびフォントリソースのみを含む）にフォームのデザインとデータが付加されます。このフォームは Acrobat バージョン 7 以降でレンダリングされ、PDFForm 変換に適用されます。

デフォルト値は空の文字列です。

**キャッシュの場所：** Formsディスクキャッシュの場所を指定します。 この設定を変更すると、現在の場所の既存のキャッシュ情報すべてがリセットされ、新しいキャッシュが新しい場所に作成されます。次のいずれかのオプションを選択します。

**デフォルトの場所：** これはデフォルトの選択です。 このオプションを選択すると、次のように使用しているアプリケーションサーバーによって決まる場所にキャッシュが作成されます。

* **JBoss:**[JBoss Home]\server\[install type]\svcdata\FormServer\Cache
* **WebLogic:**[WebLogic Home]\user_projects\domains\[aem-forms Domain Name]\adobe\[forms server name]\FormServer\Cache
* **WebSphere:**[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**LC Temp Directory:** キャッシュは、AEM forms一時ディレクトリのサブディレクトリに作成されます。このサブディレクトリは、管理コンソールのSettings/Core System Settings/Configurations/Location of Temp Directoryで指定されます。 The subdirectory is named adobeform_[servername].

>[!NOTE]
>
>一時クリーニングユーティリティを使用している場合、これらのディレクトリを削除しても機能に影響を与えませんが、新しいキャッシュが作成されるまで、短期間パフォーマンスが大きく低下する可能性があります。このような問題を回避するには、AEM Forms 一時ディレクトリの消去中、これらのディレクトリを削除しないでください。

