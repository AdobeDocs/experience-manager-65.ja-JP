---
title: AEM ポータルとポートレット
description: AEM as a portal の設定と管理の方法、およびポートレットでAEMコンテンツを設定および表示する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: b5f3d3a6-39c0-4aa5-8562-3cc6fa2b9e46
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '6093'
ht-degree: 26%

---

# AEM ポータルとポートレット{#aem-portals-and-portlets}

このドキュメントは次の内容について説明します。

* AEM Portal のアーキテクチャ
* AEM as a portal の管理と設定
* AEMをポータルとして使用する
* ポートレット（例えば、web サーバーなど）内の AEM コンテンツのインストール、設定、表示

## AEM Portal のアーキテクチャ {#aem-portal-architecture}

AEM portal アーキテクチャには、ポータルとポートレットの定義が含まれます。

### ポータルとは {#what-is-a-portal}

ポータルとは、パーソナライゼーション、シングルサインオン、様々なソースからのコンテンツ統合を提供し、情報システムのプレゼンテーションレイヤーをホストする Web アプリケーションです。

AEM では JSR 286 準拠のポートレットを実行できます。ポートレットコンポーネントによって、ページにポートレットを埋め込むことができます。[AEM コンテンツポートレットの管理](#administeringthecqcontentportlet)を参照してください。

### ポートレットとは {#what-is-a-portlet}

ポートレットとは、動的コンテンツを生成するコンテナ内にデプロイされる Web コンポーネントです。 ポートレットインターフェイスはパッケージ化され、ポートレットコンテナ内の.war ファイルとしてデプロイされます。 AEMをポータルとして実行している場合は、ポートレットの.war ファイルを使用してポートレットを実行する必要があります。

ポータルに表示されるAEMコンテンツを設定するには、 [ポートレットでのAEMのインストール、設定、使用](#installingconfiguringandusingcqinaportlet).

### AEM Portal Director {#aem-portal-director}

>[!CAUTION]
>
>AEM Portal Directorは、AEM 6.4 で非推奨（廃止予定）となりました。詳しくは、 [廃止および削除された機能](https://helpx.adobe.com/jp/experience-manager/6-4/release-notes/deprecated-removed-features.html).

## AEM Content Portlet の管理 {#administering-the-aem-content-portlet}

AEMコンテンツポートレットを使用すると、ポータルにAEMコンテンツを表示できます。 このポートレットは `/crx-quickstart/opt/portal` にあり、様々な方法でカスタマイズできます。例えば、AEMがデフォルトの動作を上書きするために必要な認証情報を生成する独自の認証サービスをデプロイすることで、SSO/認証処理をカスタマイズできます。 プラグインは、定義された API を使用し、API に対してプラグインを作成することで、独自の機能を追加できます。 プラグインは、実行中のポートレットにデプロイできます。 適切に機能させるには、起動時に表示するコンテンツパスと共に、AEMオーサーインスタンスとパブリッシュインスタンスの設定が必要です。

一部の設定はポートレット環境設定によって変更できますが、その他の設定の変更は OSGi サービス設定で行います。設定の変更には、**config** ファイルまたは OSGi Web コンソールを使用します。

### ポートレット環境設定 {#portlet-preferences}

ポータルの環境設定は、ポータルサーバーでのデプロイ時に設定するか、 **WEB-INF/portlet.xml** ファイルを作成してから、ポートレット Web アプリケーションをデプロイします。 デフォルトでは portlet.xml ファイルは次のようになります。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<portlet-app xmlns="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd /opt/SUNWps/dtd/portlet.xsd"
             version="1.0">
   <portlet>
      <portlet-name>RSSWeatherPortlet</portlet-name>
      <portlet-class>org.jboss.portlet.weather.WeatherPortlet</portlet-class>
      <init-param>
         <name>default_zipcode</name>
         <value>05673</value>
      </init-param>
      <init-param>
         <name>RSS_XSL</name>
         <value>/WEB-INF/Rss.xsl</value>
      </init-param>
      <init-param>
         <name>base_url</name>
         <value>https://xml.weather.yahoo.com/forecastrss?p=</value>
      </init-param>
      <expiration-cache>180</expiration-cache>
      <supports>
         <mime-type>text/html</mime-type>
         <portlet-mode>VIEW</portlet-mode>
         <portlet-mode>EDIT</portlet-mode>
      </supports>
      <portlet-info>
         <title>Weather Portlet</title>
      </portlet-info>
      <portlet-preferences>
         <preference>
            <name>expires</name>
            <value>180</value>
         </preference>
         <preference>
            <name>RssXml</name>
            <value>https://xml.weather.yahoo.com/forecastrss?p=33145</value>
            <read-only>false</read-only>
         </preference>
      </portlet-preferences>
   </portlet>
</portlet-app>
```

ポートレットは、次の環境設定を使用して設定できます。

<table>
 <tbody>
  <tr>
   <td>startPath</td>
   <td><p>これはポートレットの開始パスで、最初に表示されるコンテンツを定義します。</p> <p><strong>重要</strong>：ポートレットが、次のコンテキストパスで実行されているAEMオーサーインスタンスとパブリッシュインスタンスに接続するように設定されている場合は、<strong> /</strong>、強制を有効にする必要があります <strong>CQUrlInfo</strong> これらのAEMインスタンスの Html Library Manager 設定（例えば、Felix Webconsole を使用）では、編集が機能せず、環境設定ダイアログは表示されません。</p> </td>
  </tr>
  <tr>
   <td>htmlSelector</td>
   <td>各 URL に追加されるセレクター。 デフォルトでは <strong>portlet</strong> であり、HTML ページへのすべてのリクエストが、<strong>.portlet.html で終わる URL を使用します。</strong> これにより、AEM内でカスタムスクリプトを使用してポートレットのレンダリングを行うことができます。</td>
  </tr>
  <tr>
   <td>addCssToPortalHeader</td>
   <td><p>デフォルトでは、AEMのHTMLページに含まれる CSS ファイルがポートレットに含まれます。 このオプションを無効にすると、デフォルトの CSS ファイルは除外されます。</p> <p>このオプションを有効にすると、ポータルの動作に応じて、CSS ファイルが html ページの先頭に追加されるか、html ページに埋め込まれます。</p> </td>
  </tr>
  <tr>
   <td>includeToolbar</td>
   <td>デフォルトでは、管理機能用のツールバーがコンテンツポートレット内にレンダリングされます。 このオプションを無効にすると、ツールバーはレンダリングされません。</td>
  </tr>
  <tr>
   <td>urlParameterNames</td>
   <td><p>ポートレットに対して表示する新しいコンテンツ URL を含む可能性のある代替 URL パラメーター名のリスト。 リストは上から下へと処理され、値を含む最初のパラメーターが使用されます。 URL が見つからない場合は、デフォルトの URL パラメーターが使用されます。 指定された URL は、そのまま使用され、それ以上変更はありません。</p> <p>この設定は、デプロイ済みのポートレットごとにおこなわれます。また、「Day Portal Director Portlet Bridge」の OSGi 設定で、一部の URL パラメーターをグローバルに設定することもできます。</p> </td>
  </tr>
  <tr>
   <td>preferenceDialog</td>
   <td>AEMの環境設定ダイアログへのパス。空のままにした場合は、組み込みの環境設定ダイアログが使用されます。 デフォルト値は/libs/portal/content/prefs.htmlです。</td>
  </tr>
  <tr>
   <td>initialRedirect</td>
   <td>デフォルトでは、ポートレットは最初の呼び出し時にポータルページ全体の JavaScript リダイレクトを実行します。 これは、最新のポータルサーバーのドラッグ&amp;ドロップシナリオをサポートするためです。 実稼動環境では、このリダイレクトはほとんど必要とされないので、この環境設定をに設定してオフにすることができます。 <em>false</em>.</td>
  </tr>
 </tbody>
</table>

#### OSGi Web コンソール {#osgi-web-console}

ポータルサーバーがホスト localhost、ポート 8080 で実行され、AEM ポートレット Web アプリケーションが Web アプリケーションコンテキスト *cqportlet* にマウントされていると想定すると、Web コンソールの URL は `https://localhost:8080/cqportlet/cqbridge/system/console` になります。デフォルトのユーザーとパスワードはです。 **admin**.

を開きます。 **設定** 「 」タブで「 」を選択します。 **Portal Directory CQ Server Configuration**. ここでオーサーインスタンスおよびパブリッシュインスタンスのベース URL を指定します。この手順については、[ポートレットの設定](#configuring-the-portlet)で説明します。

>[!NOTE]
>
>OSGi Web コンソールは、開発（またはテスト）中に設定を変更する目的でのみ使用します。 実稼動システムのコンソールへのリクエストを必ずブロックしてください。

### 設定の指定 {#providing-configurations}

自動デプロイメントと設定プロビジョニングをサポートするために、AEMコンテンツポートレットには組み込みの設定サポートがあり、ポートレットアプリケーションに提供されるクラスパスから設定を読み込もうとします。

起動時に、システムプロパティ **com.day.cq.portet.config** は、現在の環境を検出するために読み取られます。 通常、このプロパティの値は **dev**, **prod**, **テスト** など。 環境が設定されていない場合、設定は読み取られません。

環境を設定している場合、クラスパス **com/day/cq/portlet/{env}.config** で config ファイルが検索されます（**env** はその環境の実際の値に置き換えられます）。このファイルには、この環境のすべての設定ファイルが一覧表示されます。 これらのファイルは、設定ファイルの場所を基準に検索されます。 例えば、ファイルに `my.service.xml,` 行が含まれている場合、 このファイルは、クラスパス `com/day/cq/portlet/my.service.config.` から読み取られます。ファイルの名前は、サービスの永続性 ID に **.config** を付けたものになります。 先ほどの例では、永続性 ID は **my.service** です。設定ファイルの形式は、Apache Sling OSGi インストーラーによって使用されている形式と同じです。

つまり、各環境に対して、対応する設定ファイルを追加する必要があります。 すべての環境に適用する設定は、これらのすべてのファイルに入力する必要があります。単一の環境の場合は、そのファイルに入力するだけです。 このメカニズムにより、どの環境でどの設定が読み取られるかを完全に制御できます。

異なるシステムプロパティを使用して環境を検出できます。 システムプロパティを指定します。 **com.day.cq.portet.configproperty** の代わりに使用するシステムプロパティの名前を含む **com.day.cq.portet.config**.

#### キャッシュとキャッシュの無効化 {#caching-and-caching-invalidation}

ポートレットは、デフォルト設定で、AEM WCM から受け取った応答をユーザー固有のキャッシュにキャッシュします。 パブリッシュインスタンスのコンテンツで変更が発生した場合、キャッシュを無効にする必要があります。 この目的で、AEM WCM では、オーサーインスタンス上にレプリケーションエージェントを設定する必要があります。 キャッシュは手動でフラッシュすることもできます。 この項では、これらの両方の手順について説明します。

ポートレットには独自のキャッシュを設定できるので、AEMへのアクセス権を必要とせずに、ポートレット内のコンテンツを表示できます。 ポータルは、/libs/portal/director 内のコンテンツとして使用できます。 コンテンツにアクセスするには、AEM インスタンスを起動して、CRXDE Lite または WebDav を使用してその場所からファイルをダウンロードします。

このバンドルは実行時にデプロイするか、デプロイ前にポートレット Web アプリケーションの `WEB-INF/lib/resources/bundles` に追加します。

キャッシュがデプロイされた後は、ポートレットによってパブリッシュインスタンスからコンテンツがキャッシュされます。ポートレットのキャッシュは、AEMから Dispatcher をフラッシュして無効化できます。 ポートレットが独自のキャッシュを使用するように設定するには、次の手順を実行します。

1. ポータルサーバーをターゲットにするオーサー環境でレプリケーションエージェントを設定します。
1. ポータルサーバーがホスト **localhost**、ポート 8080 で実行され、AEM ポートレット Web アプリケーションがコンテキスト **cqportlet** にマウントされていると想定すると、キャッシュをフラッシュするための URL は `https://localhost:8080/cqportlet/cqbridge/cqpcache?Path=$(path)` になります。GET メソッドを使用してください。
   **注意：**&#x200B;要求パラメーターを使用する代わりに、**Path** という名前の http ヘッダーを送信できます。

#### レプリケーションエージェントによるキャッシュのフラッシュ {#flushing-the-cache-via-replication-agent}

通常の Dispatcher の無効化と同様に、レプリケーションエージェントを設定して、ポータルのAEMポートレットキャッシュをターゲットに設定できます。 レプリケーションエージェントを設定した後、通常のページアクティベーションのたびにポータルのキャッシュがフラッシュされます。

AEMポートレットを実行する複数のポータルノードを操作する場合は、この手順で説明するように、各ノードにエージェントを作成する必要があります。

ポータルのレプリケーションエージェントを設定するには、次の手順に従います。

1. オーサーインスタンスにログインします。
1. 「Web サイト」タブで、「*ツール*」タブをクリックします。
1. レプリケーションエージェントの&#x200B;**新規**&#x200B;メニューで、「**新しいページ**」をクリックします。

   ![screen_shot_2012-02-15at40647pm](assets/screen_shot_2012-02-15at40647pm.png)

1. 「*テンプレート*」で、「*レプリケーションエージェント*」を選択し、エージェントの名前を入力します。「*作成*」をクリックします。

   ![screen_shot_2012-02-15at40817pm](assets/screen_shot_2012-02-15at40817pm.png)

1. 作成したレプリケーションエージェントをダブルクリックします。 まだ設定されていないので、無効と表示されます。

   ![screen_shot_2012-02-15at41001pm](assets/screen_shot_2012-02-15at41001pm.png)

1. 「**編集**」をクリックします。
1. 「**設定**」タブで、「**有効**」チェックボックスを選択し、シリアル化の種類として「**Dispatcher Flush**」を選択し、再試行のタイムアウト値（例：60000）を入力します。

   ![screen_shot_2012-02-15at42101pm](assets/screen_shot_2012-02-15at42101pm.png)

1. 「**トランスポート**」タブをクリックします。
1. 「**URI**」フィールドに、ポートレットのフラッシュ URI（URL）を入力します。URL は次の形式です。

   ```xml
   https://<wps-host>:<port>/<wps-context>/<cq5-portlet-context>/cqbridge/cqpcache
   ```

   ![screen_shot_2012-02-15at42322pm](assets/screen_shot_2012-02-15at42322pm.png)

1. 「**拡張**」タブをクリックします。

   ![screen_shot_2012-02-15at42515pm](assets/screen_shot_2012-02-15at42515pm.png)

1. 「**HTTP メソッド**」フィールドに 「**GET**」 と入力します。
1. 「**HTTP ヘッダー**」フィールドで **+** をクリックし、新しいエントリおよびタイプとして **Path: {path}** を追加します。
1. 必要に応じて、「**プロキシ**」タブをクリックし、エージェントのプロキシ情報を入力します。
1. 「**OK**」をクリックして、変更を保存します。
1. 接続をテストするには、「**接続をテスト**」リンクをクリックします。レプリケーションテストが成功したかどうかを示すログメッセージが表示されます。 次に例を示します。

   ![screen_shot_2012-02-15at42639pm](assets/screen_shot_2012-02-15at42639pm.png)

#### ポートレットのキャッシュの手動フラッシュ {#manually-flushing-the-portlet-cache}

レプリケーションエージェント用に設定されたのと同じ URL にアクセスして、ポートレットのキャッシュを手動でフラッシュできます。 詳しくは、 [キャッシュのフラッシュ](#flushing-the-cache-via-replication-agent) を URL の形式に設定します。 また、フラッシュ対象を示すには、URL パラメーターの Path=&lt;path> を使用してこの URL を拡張する必要があります。

次に例を示します。

`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=*` キャッシュ全体をフラッシュします。 キャッシュから`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=/content/mypage/xyz`が`/content/mypage/xyz`をフラッシュします。

### ポータルセキュリティ {#portal-security}

ポータルは、駆動認証メカニズムです。 技術ユーザー、ポータルユーザー、グループなどを使用してAEMにログインできます。 ポートレットにはポータル内のユーザーのパスワードへのアクセス権がないので、ポートレットがユーザーに正常にログインするためのすべての資格情報を知らない場合は、SSO ソリューションを使用する必要があります。 この場合、AEMポートレットは必要な情報をすべてAEMに転送し、次にこの情報を基になるAEMリポジトリに転送します。 この動作はプラグ可能で、カスタマイズ可能です。

### 公開時の認証 {#authentication-on-publish}

この節では、ポートレットが基になるAEM WCM インスタンスとの通信で使用できる認証モードについて説明します。

デフォルトでは、AEMのパブリッシュインスタンスにユーザー情報は送信されません。コンテンツは、常に匿名ユーザーとして表示されます。 ユーザー固有の情報をAEMから配信する場合、または公開用のユーザー認証が必要な場合は、これをオンにする必要があります。

#### ポートレットの認証設定へのアクセス {#accessing-the-portlet-s-authentication-configuration}

ポートレットがAEM WCM インスタンスで使用する認証設定オプションは、Web コンソール（OSGi 設定）で使用できます。

>[!NOTE]
>
>AEMを操作する場合、OSGi サービス（コンソールまたはリポジトリノード）の設定を管理する方法がいくつかあります。
>
>詳しくは、 [OSGi の設定](/help/sites-deploying/configuring-osgi.md) を参照してください。

ポートレットの認証設定にアクセスするには、次の手順に従います。

1. 次の URL で Web コンソールにアクセスします。

   `https://localhost:8080/cqportlet/cqbridge/system/console`

   デフォルト設定での例：

   `https://wps-host:10040/wps/PA_CQ5_Portlet/cqbridge/system/console`

1. Web コンソールにログインします。デフォルトの資格情報は、`admin/admin` です。
1. コンソールで、「**Configuration**」を選択します。
1. **Configuration** メニューで、設定する特定のサービスを選択します。サービスは、OSGi フレームワーク内のポートレットによって提供されます。

   | サービス名 | 説明 |
   |---|---|
   | Day Portal Director Authenticator | AEM WCM インスタンスに使用する認証モードを設定します。 選択したモードに応じて、技術ユーザーまたは SSO Cookie の名前を指定できます。 また、AEM WCM パブリッシュインスタンスの認証を有効にすることもできます。 |
   | Day Portal Director File Cache | ポートレットがAEM WCM インスタンスから受け取った応答をキャッシュする方法のパラメーターを設定します。 |
   | Day Portal Director HTTP Client Service | ポートレットが基になるAEM WCM インスタンスに HTTP 経由で接続する方法を設定します。 例えば、プロキシサーバーを指定できます。 |
   | Day Portal Director Locale Handler | ポートレットがサポートするロケールを設定します。 AEM WCM インスタンスへのリクエストはユーザーのロケールに基づいています。例えば、ユーザーの言語が「ドイツ語」の場合、`/content/geometrixx/de/` にリクエストされます。 |
   | Day Portal Director Privilege Manager | 現在ログインしているユーザーに基づいて、ポートレットで「Web サイト」タブをテストするかどうかを設定します。 |
   | Day Portal Director Toolbar Renderer | ポートレットのツールバーのレンダリングをカスタマイズします。 |

1. さらに、Web コンソールとログサービスを設定できます。 例えば、Apache Felix OSGi Management Console リンクをクリックして、Web コンソールの管理者資格情報を変更できます。

#### テクニカルユーザーモード {#technical-user-mode}

デフォルトモードでは、AEM WCM オーサーインスタンスのポートレットによって発行されたすべてのリクエストは、現在のポータルユーザーに関係なく、同じテクニカルユーザーを使用して認証されます。 テクニカルユーザーモードは、デフォルトで有効になっています。 このモードは、OSGi 管理コンソールのそれぞれの設定画面で有効または無効にします。

指定されたテクニカルユーザーは AEM WCM オーサーインスタンスに存在する必要があり、**公開時の認証**&#x200B;が有効な場合は、パブリッシュインスタンスにも存在する必要があります。オーサリング作業に十分なユーザーアクセス権限を与えてください。

#### SSO {#sso}

ポートレットでは、AEMを初期状態で使用する場合に SSO をサポートします。 オーセンティケーターサービスが SSO を使用し、現在のポータルユーザーを `cqpsso` という cookie として **Basic** 形式で AEM に送信するように設定することができます。AEM は、パス / に対して SSO 認証ハンドラーを使用するように設定する必要があります。cookie 名をもここで設定する必要があります。

それに従って、AEM リポジトリの `crx-quickstart/repository/repository.xml` も次のように設定する必要があります。

```xml
<LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
  ...
  <param name="trust_credentials_attribute" value="TrustedInfo"/>
  <param name="anonymous_principal" value="anonymous"/>
</LoginModule>
```

#### SSO 認証モード {#sso-authentication-mode}

ポートレットは、シングルサインオン (SSO) スキームを使用してAEM WCM を認証できます。 このモードでは、現在ポータルにログインしているユーザーは、SSO Cookie の形式でAEM WCM に転送されます。 SSO モードを使用する場合、AEMポートレットにアクセスできるすべてのポータルユーザーは、基になるAEM WCM インスタンスに対して認識される必要があります。最も一般的には、AEM WCM が LDAP に接続されている形で、事前にユーザーを手動で作成しておく必要があります。 また、ポートレット内で SSO を有効にする前に、基盤の AEM WCM オーサーインスタンス（および&#x200B;**公開時の認証**&#x200B;が有効な場合のパブリッシュインスタンス）を、SSO ベースのリクエストを受け入れるように設定しておく必要もあります。

ポートレットで SSO 認証モードを使用するように設定するには、次の手順を実行します（次の節で詳しく説明）。

* AEM WCM のリポジトリが信頼された資格情報を受け入れるようにします。
* AEM WCM で SSO 認証を有効にします。
* AEMポートレットで SSO 認証を有効にします。

#### AEM WCM のリポジトリーが信頼できる資格情報を受け入れることを有効にする {#enabling-aem-wcm-s-repository-to-accept-trusted-credentials}

AEM WCM で SSO を有効にする前に、AEM WCM から提供される信頼済みの資格情報を受け入れるように基になるリポジトリを設定する必要があります。 これをおこなうには、AEM repository.xml を設定します。

1. AEM WCM がインストールされているファイルシステムで、次のファイルを開きます。

   `//crx-quickstart/repository/repository.xml`

1. この XML ファイル内で **LoginModule** のエントリを探し、その設定に対して trust_credentials_attribute を追加します。

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
     <param name="anonymous_principal" value="anonymous"/>
   </LoginModule>
   ```

1. 変更を有効にするには、AEM WCM を再起動します。

#### AEM WCM での SSO 認証の有効化 {#enabling-sso-authentication-in-the-aem-wcm}

AEM WCM で SSO を有効にするには、AEM WCM の Apache Felix Web Management Console(OSGi) で関連する設定エントリにアクセスします。

1. URI の https://&lt;AEM-host>:&lt;port>/system/console を使用してコンソールにアクセスします。
1. 「構成」メニューで、「SSO 認証ハンドラ」を選択します。 この例では、SSO ハンドラーはAEMポートレットが提供する Cookie に基づいて、すべてのパスに対する SSO リクエストを受け付けます。 設定は異なる場合があります。

   | パス | ／ | すべてのリクエストに対して SSO ハンドラーを有効にします |
   |---|---|---|
   | Cookie 名 | cqpsso | ポートレットの OSGi コンソールで設定した、ポートレットによって提供される Cookie の名前。 |

1. クリック **保存** SSO を有効にします。 SSO がプライマリ認証スキームになりました。

AEM WCM が受け取るリクエストごとに、まず SSO ベースの認証が試行されます。 失敗した場合は、通常の基本認証スキームへのフォールバックが実行されます。 そのため、SSO を使用しないAEM WCM への通常の接続は引き続き可能です。

#### AEMポートレットでの SSO 認証の有効化 {#enabling-sso-authentication-in-a-aem-portlet}

基になるAEM WCM インスタンスが SSO リクエストを受け入れるには、ポートレットの認証モードを次のように切り替える必要があります。 **技術** から **SSO**.

AEM ポートレットで SSO 認証を有効にするには：

1. URI の https://&lt;aem-host>:&lt;port>/system/console を使用してコンソールにアクセスします。
1. [Configuration] メニューで、利用可能な設定の一覧から [Day Portal Director Authenticator] を選択します。
1. 「モード」で「SSO」を選択します。 その他のパラメーターはデフォルト値のままにします。

   ![chlimage_1-135](assets/chlimage_1-135.png)

1. 「Save」をクリックして、ポートレットの SSO を有効にします。

   テストの目的で、管理者権限を持つAEM WCM で同じユーザーを作成した後、ポータルの管理者ユーザーでポートレットにアクセスします。

この手順を実行した後、リクエストは SSO を使用して認証されます。 HTTP 通信の一般的なスニペットにより、次の SSO およびポートレット固有のヘッダーが表示されます。

```xml
C-12-#001898 -> [GET /mynet/en/_jcr_content/par/textimage/image.img.png HTTP/1.1 ]
C-12-#001963 -> [cq5:locale: en ]
C-12-#001979 -> [cq5:used-locale: en ]
C-12-#002000 -> [cq5:locales: en,en_US ]
C-12-#002023 -> [cqp:user: wpadmin ]
C-12-#002042 -> [cqp:portal: IBM WebSphere Portal/6.1 ]
C-12-#002080 -> [cqp:windowid: 7_CGAH47L000CE302V2KFNOG0084 ]
C-12-#002124 -> [cqp:windowstate: normal ]
C-12-#002149 -> [cqp:portletmode: view ]
C-12-#002172 -> [User-Agent: Jakarta Commons-HttpClient/3.1 ]
C-12-#002216 -> [Host: 10.0.0.68:4502 ]
C-12-#002238 -> [Cookie: $Version=0; cqpsso=Basic+d3BhZG1pbg%3D%3D ]
C-12-#002289 -> [ ]
```

### PIN 認証を有効にする {#enabling-pin-authentication}

AEMコンテンツポートレットのデフォルトのインライン編集機能を使用せず、ポータル外のポートレットのオーサリングと管理の一部をAEMオーサーインスタンスで直接使用する場合は、PIN 認証を有効にする必要があります。 また、管理ボタンの設定を変更する必要があります。

Web サイト管理ページを開く、またはポートレットからページを編集する場合、AEMコンテンツポートレットでは新しい PIN 認証が使用されます。 デフォルトでは、ピン認証は無効になっているので、AEMで次の設定変更を行う必要があります。

1. repository.xml ファイルに信頼できる情報を追加することで、AEMで信頼できる認証を有効にします。

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
   </LoginModule>
   ```

1. OSGi 設定コンソール（デフォルトの場所は https://localhost:4502/system/console/configMgr）で、ドロップダウンメニューから「**CQ PIN Authentication Handler**」を選択します。
1. を編集します。 **URL ルートパス** 単一の値のみを含むためのパラメーター **/**.

### 権限 {#privileges}

ポートレットの一部の機能は、特権によって保護されます。 現在のユーザーがこの関数にアクセスするには、この権限が必要です。 次の権限が事前に定義されています。

* &quot;toolbar&quot; ：ポートレット内のツールバーを表示または使用するための一般的な権限です。
* prefs ：ユーザーがこの権限を持っている場合、ポートレットの環境設定の表示/変更が許可されます。
* &quot;cq-author:edit&quot; ：この権限を持つユーザーは、コンテンツの編集ビューを呼び出すことができます。
* &quot;cq-author:preview&quot; ：この権限を持つユーザーは、プレビューを表示できます。
* &quot;cq-author:siteadmin&quot; ：この権限を持つユーザーは、AEM内で siteadmin を開くことができます。

権限を管理する最善の方法は、ポータルの役割を使用し、これらの権限に役割を割り当てることです。 これは、OSGi 設定を通じておこなうことができます。 「Day Portal Director Privilege Manager」は、権限ごとに一連の役割を設定できます。 ユーザーがいずれかの役割を持っている場合、ユーザーは対応する権限を持ちます。

また、ポートレットインスタンスごとのベースに基づいて、このロールのアクセス権を定義することもできます。 ポートレットの環境設定ダイアログには、上記の権限ごとに入力フィールドが含まれます。 権限ごとに、ポートレットの役割のコンマ区切りリストを設定できます。 値が設定されている場合、これは「Day Portal Director Privilege Manager」サービスのグローバル設定を上書きし、役割が結合されないので、このグローバル設定から同じ役割を追加する必要が生じる場合があります。 値を指定しない場合は、グローバル設定が使用されます。

### AEMポートレットアプリケーションのカスタマイズ {#customizing-the-aem-portlet-application}

指定されたAEMポートレットアプリケーションは、AEMと同様に、Web アプリケーション内で OSGi コンテナを開始します。 このアーキテクチャを使用すると、OSGi の次の利点をすべて活用できます。

* 更新と拡張が容易
* ポータルサーバーと通信せずに、ポートレットのホットアップデートを実行できる
* ポートレットのカスタマイズが容易

### ツールバーボタン {#toolbar-buttons}

ツールバーとそのボタンは設定可能で、カスタマイズできます。 ツールバーに独自のボタンを追加したり、どのモードで表示されるボタンを定義したりできます。 各ボタンは、OSGi 設定を通じて設定できる OSGi サービスです。

OSGi Web コンソールには、 **設定** タブをクリックします。 ボタンごとに、このボタンを表示するモードを定義できます。 これにより、例えばすべてのモードを削除して、ボタンを無効にすることができます。

デフォルトでは、AEMコンテンツポートレットはインライン編集機能を使用します。 ただし、編集のためにAEMオーサーインスタンスに切り替える場合は、 **SiteAdmin ボタン** そして **コンテンツファインダーボタン**&#x200B;を無効にします。 **編集ボタン**. この場合、AEM で PIN 認証を適切に設定してください。

ポートレットの Felix Web コンソールを介してバンドルをインストールすると、ポートレットのツールバーレイアウトをカスタマイズできます。このコンソールには、事前に定義された場所にカスタムの CSS/HTMLが含まれています。

#### バンドル構造 {#bundle-structure}

次に、バンドル構造の例を示します。

```xml
$ jar tvf target/toolbarlayout-0.0.1-SNAPSHOT.jar | awk '{print $8}'
META-INF/
META-INF/MANIFEST.MF
/com/day/cq/portlet/toolbar/layout/
/com/day/cq/portlet/toolbar/layout/author.gif
/com/day/cq/portlet/toolbar/layout/back.gif
/com/day/cq/portlet/toolbar/layout/button.html
/com/day/cq/portlet/toolbar/layout/edit.gif
/com/day/cq/portlet/toolbar/layout/manage.html
/com/day/cq/portlet/toolbar/layout/publish.html
/com/day/cq/portlet/toolbar/layout/refresh.gif
/com/day/cq/portlet/toolbar/layout/siteadmin.gif
/com/day/cq/portlet/toolbar/layout/toolbar.css
```

META-INF フォルダーには、OSGi でバンドルとして識別するために必要な MANIFEST.MF ファイルが含まれます。 次のように表示されます。

```xml
Manifest-Version: 1.0
Built-By: djaeggi
Created-By: Apache Maven Bundle Plugin
Import-Package: com.day.cq.portlet.toolbar.layout
Bnd-LastModified: 1234178347159
Export-Package: com.day.cq.portlet.toolbar.layout
Bundle-Version: 0.0.1.SNAPSHOT
Bundle-Name: Company CQ5 Portal Director Portlet Toolbar Layout
Bundle-Description: This bundle provides a custom layout for the CQ5 P
 ortal Director Portlet Toolbar.
Build-Jdk: 1.5.0_16
Bundle-ManifestVersion: 2
Bundle-SymbolicName: com.day.cq.portlet.company.toolbarlayout
Tool: Bnd-0.0.255
```

HTML/CSS/画像が/com/day/cq/portlet/toolbar/layout フォルダー内にあることは、ポートレットによって必須となり、変更できません。 同様に、MANIFEST.MF の Import-Package ヘッダーと Export-Package ヘッダーも/com/day/cq/portlet/toolbar/layout と呼ばれる必要があります。 Bundle-SymbolicName は、一意の完全修飾パッケージ名である必要があります。

Maven などのツールを使用してビルドするか、この節で示すように、関連するヘッダーを設定して jar ファイルを手動で作成できます。

#### ポートレットツールバービュー {#portlet-toolbar-views}

ポートレットのツールバーには、基本的に 2 つのビュー状態があります。 各ビューおよび関連するボタンは、それぞれのボタンファイルを使用してHTMLできます。

#### 公開ビュー {#publish-view}

公開ビューには、ツールバーを管理ビューに切り替えるボタンが 1 つだけあります。 公開ビューは、 [前のバンドル](/help/sites-deploying/configuring-osgi.md#bundles). HTMLでは、次のプレースホルダーを使用できます。プレースホルダーは、レンダリング時にポートレットに置き換えられ、それぞれのコンテンツに置き換えられます。

#### 公開ビューのプレースホルダー {#publish-view-placeholders}

| プレースホルダー文字列 | 説明 |
|---|---|
| {buttonManage} | プレースホルダーが「**管理**」ボタンに置き換えられます。管理ボタンは、ポートレットの状態を管理状態に切り替えます。 |

#### ビューを管理 {#manage-view}

管理ビューには、編集、Web サイトタブ、更新、戻るの 4 つのボタンがあります。 管理ビューは、 [前のバンドル](/help/sites-deploying/configuring-osgi.md#bundles). HTMLでは、次のプレースホルダーを使用できます。プレースホルダーは、レンダリング時にポートレットに置き換えられ、それぞれのコンテンツに置き換えられます。

#### [ 管理 ] [ ビュープレースホルダ ] {#manage-view-placeholders}

| プレースホルダー文字列 | 説明 |
|---|---|
| {buttonEdit} | プレースホルダーが「**編集**」ボタンに置き換えられます。編集ボタンは、現在のページを含む新しいウィンドウを AEM の編集モードで開きます。 |
| {buttonWeb サイトタブ } | AEM WCM の「Web サイト」タブを開くボタンに置き換えられるプレースホルダー。 |
| {buttonRefresh} | 現在のビューを更新します。 |
| {buttonBack} | ポートレットをパブリッシュビューに切り替えます。 |

#### ボタン {#buttons}

ボタンは、どの表示に対しても、button.html で定義されているのと同じ共通HTMLを使用します。

HTMLでは、次のプレースホルダーを使用できます。プレースホルダーは、レンダリング時にポートレットに置き換えられ、それぞれのコンテンツに置き換えられます。

#### 「管理」および「公開」ビューボタン {#manage-and-publish-view-buttons}

| プレースホルダー文字列 | 説明 |
|---|---|
| {name} | ボタンの名前（例：author、back、refresh など）。 |
| {id} | ボタンの CSS ID。 |
| {URL} | ボタンのターゲットの URL。 |
| {text} | ボタンのラベル。 |
| {onclick} | JavaScript **onclick** 関数（次を含む） {url}) をクリックします。 |

button.html ファイルの例を次に示します。

```xml
<div class="cqp_button">

 <a href="#" onclick="{onclick}">

 <img src="/wps/PA_CQ5_Portlet/cqbridge/static/{id}.gif" alt="{text}"
title="{text}"/>

 </a>
</div>
```

#### カスタムレイアウトのインストール {#installing-a-custom-layout}

カスタムレイアウトをインストールするには、ポートレットの OSGI Web コンソールの「**Bundles**」セクションにアクセスして、バンドルをアップロードします。

#### パッケージ {#packages}

インストール用のパッケージをアップロードまたは作成する必要がある場合は、詳しい説明について AEM ドキュメントのパッケージマネージャーを参照してください。

### リンクの処理 {#link-handling}

すべてのリンクは、ポータルコンテキスト内で動作するように書き換えられます。 デフォルトでは、レンダリングパラメータを持つリンクが使用されます。 Portal DirectorHTMLの書き換えは、代わりにアクションリンクを使用するように設定できます。

また、コンテンツパスを表示するために問い合わせられる追加のリクエストパラメーターを定義することもできます。これは、例えば外部から特定のコンテンツへのリンクがある場合に便利です。

さらに、Portal Director HTML Rewriter に、リンクの書き換え除外を定義するための正規表現のリストを設定することができます。例えば、外部システムへの相対リンクがある場合、それらのリンクをこの除外リストに追加する必要があります。

### ローカライゼーション {#localization}

AEMコンテンツポートレットには、AEMのコンテンツが正しい言語で表示されるように、ローカライゼーション機能が組み込まれています。

これは、次の 2 つの手順でおこないます。

1. ポータルディレクトリのロケール検出は、ポータルからロケール設定を取得することで、ポータルユーザーのロケールを検出します。 このサービスは、AEMで使用可能な言語のリストを使用して設定する必要があります。
1. Portal Director Locale Handler は、現在の要求のローカライゼーションを処理します。 リクエストされたコンテンツのパスを取得します。例： `/content/geometrixx/en/company.html`設定に従って、 **en** ユーザーの実際のロケールを使用します。

Portal Director Locale Handler には、ロケール情報をチェックするためのパスを設定できます。通常、この設定には `/content` 以下のすべてと、パス内のロケール情報の位置が含まれます。Portal Director Locale Handler はデフォルトで、AEM 内の多言語サイトの推奨構造に従います。

パス内のロケール情報を処理するための厳格なルールがないサイトの場合は、ロケールハンドラーを独自の実装に置き換えることが可能です。

### オプションの OSGi サービス {#optional-osgi-services}

オプションの OSGi サービスを実装して、ポートレットの様々な部分をカスタマイズできます。 各サービスは Java インターフェイスに対応しています。 このインターフェイスを実装して、バンドルによってポートレットにデプロイすることができます。

<table>
 <tbody>
  <tr>
   <td>RequestTracker</td>
   <td>ポートレットによってコンテンツが表示されるたびに、リクエストトラッカーに通知が届きます。 これにより、ポートレットの呼び出しを追跡し続けることができます。</td>
  </tr>
  <tr>
   <td>InvocationContextListener</td>
   <td>ポートレットへの各リクエストの開始時と終了時に呼び出されるリスナー。 このリスナーを使用して、現在のリクエストの情報を変更または追加できます。<br /> </td>
  </tr>
  <tr>
   <td>ErrorHandler</td>
   <td>レンダリングフェーズ中のエラーに対するカスタムエラーハンドラ。</td>
  </tr>
  <tr>
   <td>HttpProcessor</td>
   <td>このサービスを使用して、AEMに対する各 HTTP 呼び出しに情報を追加できます。</td>
  </tr>
  <tr>
   <td>PortletAction</td>
   <td>ポートレットに独自のアクションを追加します。このアクションは、ポートレットアクションリンクを介して呼び出すことができます。</td>
  </tr>
  <tr>
   <td>PortletDecoratorService</td>
   <td>このサービスを使用して、ポートレットのコンテンツを修飾できます。</td>
  </tr>
  <tr>
   <td>ResourceProvider</td>
   <td>独自のリソースプロバイダーを追加して、ポートレットリソースリンクを介して一部のリソースをクライアントに配信します。</td>
  </tr>
  <tr>
   <td>TextMapper</td>
   <td>後処理のHTML、CSS および JavaScript ファイルを作成できます。</td>
  </tr>
  <tr>
   <td>ToolbarButton</td>
   <td>ツールバーに独自のボタンを追加します。</td>
  </tr>
  <tr>
   <td>UrlMapper</td>
   <td>カスタム URL マッピングまたは書き換えを適用するサービスを追加します。</td>
  </tr>
  <tr>
   <td>UserInfoProvider</td>
   <td>ユーザーに関する独自の情報を追加します。 このサービスを使用して、ポータルからポートレットに情報を取得できます。</td>
  </tr>
 </tbody>
</table>

#### デフォルトのサービスの置き換え {#replacing-default-services}

次のサービスは、（対応する Java インターフェイスと共に）コンテンツポートレットにデフォルトの実装を持っています。 カスタマイズするには、新しいサービス実装を含むバンドルをポートレットアプリケーションにデプロイする必要があります。

このようなサービスを実装する場合は、必ず **service.ranking** プロパティを正の値に設定します。 デフォルトの実装ではランク 0 が使用され、ポートレットは最もランキングの高いサービスを使用します。

| **名前** | **説明** | **デフォルトの動作** |
|---|---|---|
| Authenticator | 認証情報をAEMに提供します | オーサーとパブリッシュの両方に設定可能なテクニカルユーザーを使用します。 または、SSO を使用できます。 |
| HTMLRewriter | リンクや画像などを書き換えます。 | AEMリンクをポータルリンクに書き換えます。UrlMapper と TextMapper を使用して拡張できます。 |
| HttpClientService | すべての HTTP 接続を処理します | 標準的な実装 |
| LocaleHandler | ロケール情報を処理します | ロケールに従ってコンテンツへのリンクを書き換えます。 |
| LocaleDetector | ユーザーのロケールを検出します。 | ポータルが提供するロケールを使用します。 |
| PrivilegeManager | ユーザー権限を確認します | ユーザーがコンテンツの編集を許可されている場合は、オーサーインスタンスへのアクセスを確認します |
| ToolbarRenderer | ツールバーをレンダリング | ツールバー機能を追加します |

### ポートレットイベント {#portlet-events}

ポートレット API(JSR-286) は、ポートレットイベントを指定します。 AEMコンテンツポートレットには統合ブリッジがあり、AEMポートレット用のポートレットイベントが OSGi イベントとして配信されるので、ポートレットイベントの処理がプラグ可能です。

特定のイベントを処理する場合は、デプロイメント記述子でイベントを受け取るものとして宣言し（またはポータルサーバーを介して設定します）、EventHandler インターフェイスを宣言する OSGi サービスを実装します（ OSGi EventAdmin の仕様を参照）。

ポートレットイベントが発生するたびに、特定の OSGi イベントが送信され、ハンドラーを呼び出します。 ハンドラーはすべてのコンテキスト情報を取得し、それに応じてポートレットのステータスを更新したり、新しいイベントを送信したりできます。 基本的に、handle メソッド内ではポートレットイベントフェーズのすべての機能を使用できます。

## AEM as a Portal の使用 {#using-aem-as-a-portal}

ポートレットコンポーネントを使用して、ポートレットウィンドウをAEMページに追加します。 アプリケーションサーバーにインストールする共有ライブラリを使用すると、ポートレットコンポーネントはデプロイ済みのポートレットアプリケーションを検出できます。

AEMをポータルとして使用するには、次のタスクを実行します。

1. ポートレットコンポーネントと共有ライブラリをインストールします。
1. ポートレットコンポーネントをSidekickに追加します。
1. ポータルコンポーネントに表示するポートレットを含む Web アプリケーションを設定およびデプロイします。
1. ポートレットコンポーネントをページに追加し、表示するポートレットを選択します。

>[!NOTE]
>
>ポートレットコンポーネントは、AEMが Web アプリケーションとしてデプロイされている場合にのみ使用できます。 ([Installing AEM With an Application Server を参照してください。](/help/sites-deploying/application-server-install.md).)

### ポートレットコンポーネントのインストール {#installing-the-portlet-component}

AEM Quickstart JAR ファイルには、ポートレットコンポーネントファイルが含まれています。 ファイル（cq-portlet-components.zip）を取得するには、Quickstart を実行するか、その内容を抽出します。

1. Quickstart JAR ファイルを実行するかその内容を抽出して、次の場所にある cq-portlet-components.zip ファイルを特定します。

   * クイックスタートを実行： crx-quickstart/opt/portal
   * クイックスタートの内容を抽出：static/opt/portal

1. アプリケーションサーバーにデプロイされている CQ5 オーサーインスタンスのパッケージマネージャーを開きます(https://*appserverhost*:*port*/cq5author/crx/packmgr)。

1. パッケージマネージャーを使用して、cq-portlets-components.zip パッケージを[アップロードし、インストールします](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system)。

   このパッケージによって、リポジトリ内の /libs/portal/director フォルダーに cq-portlet-director-sharedlibs-x.x.x.jar がインストールされます。

1. cq-portlet-director-sharedlibs-x.x.x.jar をハードドライブにコピーします。 ファイルを取得するには、FileVault や WebDAV クライアントなどの任意の方法を使用します。
1. cq-portlet-director-sharedlibs.x.x.x.jar ファイルをアプリケーションサーバーの共有ライブラリフォルダーに移動し、デプロイされたポートレットアプリケーションでクラスを使用できるようにします。

### ポートレットコンポーネントのSidekickへの追加 {#adding-the-portlet-component-to-sidekick}

作成者が使用できるように、ポートレットコンポーネントを段落システムに追加します。

1. サイドキックで、定規アイコンをクリックしてデザインモードに切り替えます。
1. 最初の段落の上にある`Design of par`ヘッダーの横の「**編集**」をクリックします。

1. 「**一般**」コンポーネントカテゴリで、ポートレットコンポーネントの横にあるチェックボックスをオンにして「OK」をクリックします。

![chlimage_1-25](assets/chlimage_1-25.jpeg)

### ポートレットアプリケーションの設定とデプロイ {#configuring-and-deploying-your-portlet-applications}

ポートレットをアプリケーションサーバーの Web コンテナにデプロイして、ポータルコンポーネントで使用できるようにします。 ポートレットアプリケーションをデプロイする前に、このアプリケーションが AEM ポータルコンテナサーブレットを読み込むように設定する必要があります。この設定によって、ポートレットコンポーネントがポートレットにアクセスできるようになります。

1. ポートレットアプリケーションの WAR ファイルの内容を抽出します。

   **ヒント：** jar xf *nameofapp*.war コマンドによってファイルを抽出します。

1. web.xml ファイルをテキストエディターで開きます。
1. 次のサーブレット設定を web-app 要素内に追加します。

   ```xml
   <servlet>
           <servlet-name>slingportal</servlet-name>
           <servlet-class>org.apache.sling.portal.container.api.ContainerServlet</servlet-class>
           <load-on-startup>1</load-on-startup>
   </servlet>
   <servlet-mapping>
           <servlet-name>slingportal</servlet-name>
           <url-pattern>/SlingPortletInvoker</url-pattern>
   </servlet-mapping>
   ```

1. web.xml ファイルを保存し、WAR ファイルを再度パッケージ化します。

   **ヒント：** `jar cvf nameofapp.war *`コマンドにより、現在のディレクトリの内容を nameofapp.war ファイルに追加します。

1. ポートレットアプリケーションをアプリケーションサーバーにデプロイします。 詳しくは、使用しているアプリケーションサーバーのドキュメントを参照してください。

### AEMページへのポートレットの追加 {#adding-portlets-to-your-aem-page}

ポータルコンポーネントを使用して、ポートレットウィンドウを Web ページに追加します。 コンポーネントのプロパティを使用して、表示するポートレットを指定します。

1. Web ページで、 **ポートレット** コンポーネントを「一般」グループからSidekickに

   >[!NOTE]
   >
   >コンポーネントをページにドラッグした後、ページを再読み込みして、正しく機能することを確認します。

1. コンポーネントをダブルクリックして、ポートレットのプロパティを開きます。
1. Adobe Analytics の **ポートレットエンティティ** ドロップダウンメニューから、リストからポートレットを選択します。
1. ポートレットのタイトルバーを表示するかどうかに応じて、「タイトルバーを隠す」チェックボックスをオンまたはオフにします。
1. Adobe Analytics の **ポートレットウィンドウ** 必要に応じて、一意のポートレットウィンドウ ID を入力します。

   >[!NOTE]
   >
   >同じページで同じポートレットを複数回使用する場合は、各ポートレットに異なるウィンドウ ID を付けます。

1. 「**OK**」をクリックします。ポートレットがAEMページに表示されます。

   ![chlimage_1-136](assets/chlimage_1-136.png)

## ポートレットでのAEMのインストール、設定、使用 {#installing-configuring-and-using-aem-in-a-portlet}

AEM WCM が提供するコンテンツにアクセスするには、ポータルサーバーがAEM Portal Directorポートレットに適合している必要があります。 これをおこなうには、この節で説明する手順に従って、ポートレットをインストール、設定、ポータルページに追加します。

デフォルトでは、ポートレットは localhost:4503 のパブリッシュインスタンスに接続し、localhost:4502 のオーサーインスタンスに接続します。 これらの値は、ポートレットのデプロイ時に変更できます。 ポータルディレクタは、リポジトリ内の/libs/portal/directory の下にコンテンツとして表示されます。 使用する前に、アプリケーションの war ファイルをダウンロードする必要があります。

### WAR ファイルのダウンロード {#downloading-the-war-file}

1. WebDAV または CRXDE Lite を使用して、/libs/portal/director に移動します。

1. *cq-portlet-webapp.war* をダウンロードします。

>[!NOTE]
>
>これらの手順では、Websphere ポータルを例として使用しますが、可能な限り一般的なものです。他の Web ポータルでは手順が異なることに注意してください。 手順は基本的にすべての Web ポータルで同じですが、特定の Web ポータルの手順を再利用する必要があります。

#### ポートレットのインストール {#installing-the-portlet}

ポートレットをインストールするには：

1. 管理者権限でポータルにログインします。
1. Web ポータルのポートレット管理部分に移動します。
1. 「インストール」をクリックし、ダウンロードしたAEMポートレットアプリケーション (cq-portlet-webapp.war) を参照して、そのポートレットに関するその他の重要な情報を入力します。

   他のポートレット基本情報については、デフォルト値を使用するか、値を変更します。デフォルト値を使用する場合、ポートレットのアドレスは https://&lt;wps-host>:&lt;port>/wps/PA_CQ5_Portlet になります。ポートレットによって提供される OSGi 管理コンソールのアドレスは https://&lt;wps-host>:&lt;port>/wps/ PA_CQ5_Portlet/cqbridge/system/console になります（デフォルトのユーザー名とパスワードは admin/admin です）。

1. ポートレットアプリケーションが自動的に開始するようにするには、そのオプションまたはチェックボックスをオンにし、変更を保存します。 インストールが成功したことを示すメッセージが表示されます。

#### ポートレットの設定 {#configuring-the-portlet}

ポートレットをインストールした後、基になるAEMインスタンス（オーサーおよびパブリッシュ）の URL を知るように設定する必要があります。 また、他のオプションも設定できます。

ポートレットを設定するには：

1. アプリサーバーのポータル管理ウィンドウで、ポートレット管理に移動します。すべてのポートレットが表示され、AEM Portal Directorポートレットを選択します。
1. 必要に応じて、ポートレットを設定します。 例えば、オーサーインスタンスとパブリッシュインスタンスの URL と、開始パスの URL を変更する必要が生じる場合があります。 デフォルトの設定については、[ポートレット環境設定](/help/sites-administering/aem-as-portal.md#portlet-preferences)を参照してください。

   >[!NOTE]
   >
   >ポートレットが、** /**とは異なるコンテキストパスで実行されているAEMオーサーインスタンスとパブリッシュインスタンスに接続するように設定されている場合は、強制を有効にする必要があります。 **CQUrlInfo** これらのAEMインスタンスの Html Library Manager 設定（例えば、Felix Webconsole を使用）では、編集が機能せず、環境設定ダイアログは表示されません。

1. アプリケーションサーバーで設定の変更を保存します。

1. ポートレットの OSGI 管理コンソールに移動します。デフォルトの場所は `https://<wps-host>:<port>/wps/PA_CQ5_Portlet/cqbridge/system/console/configMgr` です。デフォルトのユーザー名とパスワードは **admin/admin** です。

1. 「**Day Portal Director CQ Server Configuration**」設定を選択し、次の値を編集します。

   * **オーサーのベース URL**:AEMオーサーインスタンスのベース URL。
   * **ベース URL を公開**:AEMパブリッシュインスタンスのベース URL。
   * **Author Is Used As Publish**：オーサーインスタンスが（開発用に）パブリッシュインスタンスとして
使用されているかどうかを指定します。

   ![chlimage_1-137](assets/chlimage_1-137.png)

1. 「**保存**」をクリックします。これで、ポートレットをポータルページに追加してポータルを使用できるようになりました。

### コンテンツの URL {#content-urls}

AEMからコンテンツが要求されると、ポートレットは現在の表示モード（パブリッシュまたはオーサー）と現在のパスを使用して、完全な URL を組み立てます。 デフォルト値を使用した場合の最初の URL は `https://localhost:4503/content/geometrixx/en.portlet.html` です。`htmlSelector` の値が URL の拡張子の前に自動的に追加されます。

ポートレットがヘルプモードに切り替えられ、`appendHelpViewModeAsSelector` が選択された場合は、同じように `help` セレクターが付加されます（例：`https://localhost:4503/content/geometrixx/en.portlet.html.help`）。ポートレットウィンドウが最大化され、`appendMaxWindowStateAsSelector` が選択された場合は、同じようにそのセレクターが付加されます（例：`https://localhost:4503/content/geometrixx/en.portlet.max.help`）。

セレクターはAEMで評価でき、異なるセレクターに対しては異なるテンプレートを使用できます。

### AEMでのコンテンツ URL マップの使用 {#using-a-content-url-map-in-aem}

通常、開始パスはAEM内のコンテンツを直接指します。 ポートレット環境設定ではなく AEM 内で開始パスを管理する場合は、開始パスが AEM 内のコンテンツマップを示すように設定できます（例：`/var/portlets`）。この場合、AEMで実行するスクリプトは、ポートレットから送信された情報を使用して、開始 URL を決定できます。 正しい URL にリダイレクトする必要があります。

#### ポータルページへのポートレットの追加 {#adding-the-portlet-to-the-portal-page}

ポートレットをポータルページに追加するには、次の手順を実行します。

1. アプリサーバーの管理ウィンドウにいることを確認し、ページを管理する場所に移動します。 ( 例えば、WebSphere 6.1 では、 **ページを管理**) をクリックします。
1. ポートレットの名前を選択し、既存のページを選択するか、ページを作成します。
1. ページレイアウトを編集します。
1. ポートレットを選択し、コンテナに追加します。
1. 変更を保存します。

#### ポートレットの使用 {#using-the-portlet}

ポートレットに追加したページにアクセスするには、次の手順を実行します。

1. ポートレットのパーソナライゼーションメニューで、ポータルでの設定と同じようにポートレットを設定します。
1. 設定を開き（ポートレットには、ポートレットの設定で設定された公開開始 URL が表示されます）、必要に応じて編集を行い、保存します。
