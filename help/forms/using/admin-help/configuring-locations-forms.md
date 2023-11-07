---
title: Forms の場所の設定
description: AEM Form の場所を設定する方法を説明します。 属性のファイルの場所、フォームの場所、シードPDFファイルおよびキャッシュの場所を指定できます。
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
exl-id: 0d9eb7fe-28a6-444e-957d-023687158c61
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 45%

---

# Forms の場所の設定 {#configuring-locations-for-forms}

属性の URL、URI、ファイルの場所 (Web ルート、取得するフォームの場所、PDFForm 変換で使用されるシードPDFファイル、キャッシュの場所など ) を指定できます。

1. 管理コンソールで、サービス／Forms をクリックします。
1. 「場所」で、適切なオプションを指定します。 オプションについては、以下で説明します。
1. 「保存」をクリックします。

## 場所の設定 {#locations-settings}

**ベース URL：**&#x200B;画像やスクリプトなどのフォームリソースが置かれるベース URL です。この値は、画像やスクリプトなど、外部のHTMLへの HREF 参照を含む依存関係変換に必要です。 このようなスクリプトの 1 つに xfasubset.js があります。これは、HTMLフォームが XFA インテリジェンスを実行するために必要です。 この値は、コンテンツルート URI と同等の HTTP 値である必要があります。

>[!NOTE]
>
>ベース URL は、HTTP プロトコルまたはリポジトリプロトコルのみをサポートします。 file:///などのプロトコルはサポートされていません。 カスタム CSS やデジタル署名 URI などのリソースにアクセスする必要がある場合は、適切な API パラメーター値を使用して絶対位置を指定します。

依存パスが絶対パスの場合、ベース URL の値は無視されます。 それ以外の場合は、依存パスとベース URL が結合されます。

デフォルト値は空の文字列です。

次の例では、同じコンテンツを指します（コンテンツルート URI とベース URL を使用）。

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**FS Web ルート URI：** Forms Web アプリケーションの URL です。Forms Web アプリケーションとクライアントアプリケーションが同じアプリケーションサーバーにデプロイされている場合は、このボックスを空のままにできます。Forms API Web ルート URL が使用されます。

Forms Web アプリケーションとクライアントアプリケーションが同じアプリケーションサーバーにデプロイされていない場合は、次の例に示すように、このボックスにForms Web アプリケーションの URL を指定します。

`https://<host name>:<port>/FormServer`

`host name` と `port` には、それぞれ Forms Web アプリケーションをホストするサーバーのサーバー名とポート番号を入力します。

デフォルト値は空の文字列です。

**Web ルート URI：**&#x200B;アプリケーションの Web ルートです。この値と、AEM Forms SDK を介して指定された sTargetURL パラメーターを連結して（sTargetURL が相対 URL の場合）、アプリケーション固有の Web コンテンツにアクセスするための絶対 URL が作成されます。

デフォルト値は空の文字列です。

**コンテンツルート URI：**&#x200B;フォームの取得元である URI または絶対パスです。この値と、API を介して指定された sFormQuery パラメーターを連結して、フォームの取得先となる絶対パスが作成されます。この値は、HTTP を使用してアクセス可能なディレクトリまたは Web の場所を参照できます。

デフォルト値は空の文字列です。

**XCI 設定 URI：**&#x200B;レンダリング用 XCI ファイルがある場所の相対パスまたは絶対パスです。相対パスの場合は、デプロイ可能な AEM Forms EAR ファイル内に XCI ファイルが保存されていることが前提となります。

デフォルト値は `com/adobe/formServer/PA/pa.xci` です。

**フォントマップ URI：** フォントマップファイルの場所の相対パスまたは絶対パスです。相対値の場合は、デプロイ可能なAEM forms EAR ファイル内にこのファイルが存在することが前提となります。

フォントマッピングファイルは、フォーム内のHTML変換に対するカスタムフォントマッピングの作成に使用されるので、クライアントのコンピューター上でフォントが使用できない場合に置き換えるフォントを指定できます。

デフォルト値は `com/adobe/formServer/client-font-map.properties` です。

次のエントリは、フォントマップファイル内のエントリの例です。

`Arial=Arial,Helvetica,sans-serif`

**シード PDF ファイル：** PDFForm 変換で配信を最適化するために使用する初期 PDF ファイルです。シードPDFファイルでは、フォームデザインとデータに追加されるカスタマイズされたPDFファイル（XFA ストリーム、画像、フォントリソースのみを含む）を指定します。 フォームはAcrobat 7以降でレンダリングされ、PDFForm 変換に適用されます。

デフォルト値は空の文字列です。

**キャッシュの場所：** Forms ディスクキャッシュの場所を指定します。この設定を変更すると、現在の場所の既存のキャッシュ情報がすべてリセットされ、新しいキャッシュが新しい場所に作成されます。 次のいずれかのオプションを選択します。

**デフォルトの場所：** これはデフォルトの選択です。このオプションを選択すると、次のように使用しているアプリケーションサーバーによって決まる場所にキャッシュが作成されます。

* **JBoss：** [JBoss ホーム]\server\[install type]\svcdata\FormServer\Cache
* **WebLogic：** [WebLogic ホーム]\user_projects\domains\[aem-forms Domain Name]\adobe\[forms server name]\FormServer\Cache
* **WebSphere：** [IBM ホーム]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**LC の一時ディレクトリ：**&#x200B;キャッシュは、AEM Forms の一時ディレクトリのサブディレクトリ（管理コンソールの、設定／コアシステム設定／設定／一時ディレクトリの場所で指定）に作成されます。サブディレクトリの名前は、adobeform_[[servername]] です。

>[!NOTE]
>
>一時クリーニングユーティリティを使用している場合、これらのディレクトリを削除しても機能に影響はありませんが、新しいキャッシュが作成されるまで、短時間の間、パフォーマンスに大きな影響が及ぶ可能性があります。 この問題を回避するには、AEM forms の一時ディレクトリをクリアする際に、これらのディレクトリを削除しないでください。
