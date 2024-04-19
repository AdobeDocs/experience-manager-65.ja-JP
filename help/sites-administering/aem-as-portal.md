---
title: AEM ポータルとポートレット
description: AEM をポータルとして設定および管理する方法と、AEM コンテンツをポートレットに設定および表示する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: b5f3d3a6-39c0-4aa5-8562-3cc6fa2b9e46
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '6073'
ht-degree: 99%

---

# AEM ポータルとポートレット{#aem-portals-and-portlets}

このドキュメントでは次の内容について説明します。

* AEM ポータルのアーキテクチャ
* AEM のポータルとしての管理と設定
* AEM のポータルとしての使用
* ポートレット（例えば、web サーバーなど）内の AEM コンテンツのインストール、設定、表示

## AEM ポータルのアーキテクチャ {#aem-portal-architecture}

AEM ポータルのアーキテクチャには、ポータルおよびポートレットの定義が含まれます。

### ポータルとは {#what-is-a-portal}

ポータルとは、パーソナライズ機能、シングルサインオン、様々なソースからのコンテンツ統合の機能を備え、情報システムのプレゼンテーションレイヤーをホストする web アプリケーションです。

AEM では JSR 286 準拠のポートレットを実行できます。ポートレットコンポーネントによって、ページにポートレットを埋め込むことができます。[AEM コンテンツポートレットの管理](#administeringthecqcontentportlet)を参照してください。

### ポートレットとは {#what-is-a-portlet}

ポートレットとは、動的コンテンツを生成するコンテナ内部にデプロイされる web コンポーネントです。ポートレットインターフェイスは .war ファイルとしてパッケージ化され、ポートレットコンテナ内にデプロイされます。AEM をポータルとして実行している場合、ポートレットを実行するには、そのポートレットの .war ファイルが必要になります。

ポータルに表示するように AEM コンテンツを設定するには、[ポートレットでの AEM のインストール、設定および使用](#installingconfiguringandusingcqinaportlet)を参照してください。

### AEM Portal Director {#aem-portal-director}

>[!CAUTION]
>
>AEM Portal Director は、AEM 6.4 以降では使用されなくなりました。[廃止される機能および削除された機能](https://helpx.adobe.com/jp/experience-manager/6-4/release-notes/deprecated-removed-features.html)を参照してください。

## AEM コンテンツポートレットの管理 {#administering-the-aem-content-portlet}

AEM コンテンツポートレットでは、ポータル内に AEM コンテンツを表示できます。このポートレットは `/crx-quickstart/opt/portal` にあり、様々な方法でカスタマイズできます。例えば、必要な AEM の認証情報を生成する独自の認証サービスをデプロイしてデフォルトの動作を上書きすることで、SSO／認証処理をカスタマイズできます。プラグインで定義済みの API を使用し、この API に対してプラグインを作成して、独自の機能を追加できます。プラグインは実行中のポートレットにデプロイできます。適切に機能させるには、AEM オーサーインスタンスとパブリッシュインスタンスの設定と、起動時に表示するコンテンツパスが必要になります。

一部の設定はポートレット環境設定によって変更できますが、その他の設定の変更は OSGi サービス設定で行います。設定の変更には、**config** ファイルまたは OSGi Web コンソールを使用します。

### ポートレット環境設定 {#portlet-preferences}

ポートレット環境設定は、ポータルサーバー内へのデプロイ時に設定するか、ポートレット web アプリケーションのデプロイ前に **WEB-INF/portlet.xml** ファイルを編集して設定することができます。デフォルトでは portlet.xml ファイルは次のようになります。

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

ポートレットは次の環境設定を使用して設定できます。

<table>
 <tbody>
  <tr>
   <td>startPath</td>
   <td><p>ポートレットの開始パス。最初に表示されるコンテンツを定義します。</p> <p><strong>重要</strong>：ポートレットを <strong>/</strong> 以外のコンテキストパスで実行している AEM オーサーインスタンスおよびパブリッシュインスタンスに接続するように設定する場合は、（Felix Web コンソールなどを使用して）これらの AEM インスタンスの HTML ライブラリマネージャー設定で強制 <strong>CQUrlInfo</strong> を有効にする必要があります。そうしなければ、編集が機能せず、環境設定ダイアログが表示されません。</p> </td>
  </tr>
  <tr>
   <td>htmlSelector</td>
   <td>各 URL に追加されるセレクター。デフォルトでは <strong>portlet</strong> であり、HTML ページへのすべてのリクエストが、<strong>.portlet.html で終わる URL を使用します。</strong>このセレクター設定により、ポートレットのレンダリングのために、AEM 内でカスタムスクリプトを使用できるようになります。</td>
  </tr>
  <tr>
   <td>addCssToPortalHeader</td>
   <td><p>デフォルトでは、AEM からの HTML ページにインクルードされる CSS ファイルが、ポートレットにインクルードされます。このオプションを無効にすると、デフォルトの CSS ファイルはインクルードされません。</p> <p>このオプションを有効にすると、ポータルの状態に応じて、CSS ファイルが HTML ページの head 部に追加されるか、HTML ページ内に埋め込まれます。</p> </td>
  </tr>
  <tr>
   <td>includeToolbar</td>
   <td>デフォルトで、管理機能用のツールバーがコンテンツポートレット内部にレンダリングされます。このオプションを無効にすると、ツールバーがレンダリングされなくなります。</td>
  </tr>
  <tr>
   <td>urlParameterNames</td>
   <td><p>ポートレット用に表示する新しいコンテンツ URL を含む代替 URL パラメーター名のリスト。このリストは上から順に処理され、値が格納された最初のパラメーターが使用されます。URL が見つからない場合は、デフォルトの URL パラメーターが使用されます。指定した URL は、それ以上変更されずに指定したとおりに使用されます。</p> <p>この設定はデプロイされたポートレットごとの設定ですが、OSGi 設定で「Day Portal Director Portlet Bridge」に対して一部の URL パラメーターをグローバルに設定することもできます。</p> </td>
  </tr>
  <tr>
   <td>preferenceDialog</td>
   <td>AEM 内の環境設定ダイアログへのパス。空白の場合、組み込みの環境設定ダイアログが使用されます。ダイアログのデフォルトは、/libs/portal/content/prefs.html です。</td>
  </tr>
  <tr>
   <td>initialRedirect</td>
   <td>デフォルトでは、ポートレットは最初の呼び出し時にポータルページ全体の JavaScript リダイレクトを実行します。これは、最新型ポータルサーバーのドラッグ＆ドロップシナリオに対応するための設定です。実稼動環境ではこのリダイレクトはほとんど必要ないので、この環境設定を <em>false</em> に設定してオフにすることができます。</td>
  </tr>
 </tbody>
</table>

#### OSGi eb コンソール {#osgi-web-console}

ポータルサーバーがホスト localhost、ポート 8080 で実行され、AEM ポートレット Web アプリケーションが Web アプリケーションコンテキストにマウントされていると仮定します *cqportlet*、Web コンソールの URL はです。 `https://localhost:8080/cqportlet/cqbridge/system/console`. デフォルトのユーザー名とパスワードは **admin** です。

「**設定**」タブを開き、「**Portal Directory CQ Server Configuration**」を選択します。ここでオーサーインスタンスおよびパブリッシュインスタンスのベース URL を指定します。この手順については、[ポートレットの設定](#configuring-the-portlet)で説明します。

>[!NOTE]
>
>OSGi web コンソールの使用は、開発中（またはテスト中）の設定を変更する場合のみを想定しています。実稼働システムでは、このコンソールへのリクエストをブロックするようにしてください。

### 設定の指定 {#providing-configurations}

自動的なデプロイおよび設定のプロビジョニングをサポートするために、AEM コンテンツポートレットには、ポートレットアプリケーションに指定されたクラスパスから設定を読み取る設定補助機能が組み込まれています。

起動時に、システムプロパティの **com.day.cq.portet.config** が読み取られ、現在の環境が検出されます。通常、このプロパティの値は **dev**、**prod**、**test** などになります。環境を設定していない場合、設定は読み取られません。

環境を設定している場合、クラスパス **com/day/cq/portlet/{env}.config** で config ファイルが検索されます（**env** はその環境の実際の値に置き換えられます）。このファイルに、その環境のすべての設定ファイルを一覧で指定しておく必要があります。これらのファイルは、config ファイルからの相対位置として検索されます。例えば、ファイルに `my.service.xml,` 行が含まれている場合、 このファイルは、クラスパス `com/day/cq/portlet/my.service.config.` から読み取られます。ファイルの名前は、サービスの永続性 ID に **.config** を付けたものになります。 先ほどの例では、永続性 ID は **my.service** です。設定ファイルの形式は、Apache Sling OSGi インストーラーによって使用されている形式と同じです。

つまり、環境ごとに、対応する config ファイルを追加する必要があります。すべての環境に適用される設定については、これらすべてのファイルに入力する必要があります。1 つの環境にのみ適用される設定については、そのファイルだけに入力します。このメカニズムによって、どの環境でどの設定を読み取るのかを完全に管理できます。

環境を検出するために、異なるシステムプロパティを使用することも可能です。そのためには、システムプロパティ **com.day.cq.portet.configproperty** を指定し、このプロパティに、**com.day.cq.portet.config** の代わりに使用するシステムプロパティ名を設定します。

#### キャッシュおよびキャッシュの無効化 {#caching-and-caching-invalidation}

ポートレットは、デフォルト設定の場合、AEM WCM から受け取ったレスポンスをユーザー固有のキャッシュ内にキャッシュします。パブリッシュインスタンスのコンテンツ内で変更が行われた場合、このキャッシュを無効にする必要があります。この目的で、AEM WCM ではオーサーインスタンス上でレプリケーションエージェントを設定する必要があります。キャッシュは手動でフラッシュすることもできます。ここでは、これらの手順について説明します。

ポートレットには独自のキャッシュを設定でき、それによって AEM にアクセスしなくてもポートレット内のコンテンツを表示できます。ポータルは /libs/portal/director 内にコンテンツとして配置されます。コンテンツにアクセスするには、AEM インスタンスを起動して、CRXDE Lite または WebDav を使用してその場所からファイルをダウンロードします。

このバンドルは実行時にデプロイするか、デプロイ前にポートレット Web アプリケーションの `WEB-INF/lib/resources/bundles` に追加します。

キャッシュがデプロイされた後は、ポートレットによってパブリッシュインスタンスからコンテンツがキャッシュされます。ポートレットのキャッシュは、AEM から Dispatcher をフラッシュすることで無効にすることができます。独自のキャッシュを使用するようにポートレットを設定するには：

1. ポータルサーバーをターゲットとするオーサーインスタンス内で、レプリケーションエージェントを設定します。
1. ポータルサーバーがホスト **localhost**、ポート 8080 で実行され、AEM ポートレット Web アプリケーションがコンテキスト **cqportlet** にマウントされていると想定すると、キャッシュをフラッシュするための URL は `https://localhost:8080/cqportlet/cqbridge/cqpcache?Path=$(path)` になります。GET メソッドを使用してください。
   **注意：**&#x200B;要求パラメーターを使用する代わりに、**Path** という名前の http ヘッダーを送信できます。

#### レプリケーションエージェントによるキャッシュのフラッシュ {#flushing-the-cache-via-replication-agent}

通常の Dispatcher の無効化と同様に、レプリケーションエージェントもポータルの AEM ポートレットキャッシュをターゲットとするように設定できます。レプリケーションエージェントの設定後、通常のページのアクティベートが行われるたびにポータルのキャッシュがフラッシュされます。

AEM ポートレットを実行する複数のポータルノードを運用している場合、この手順で示すとおりノードごとにエージェントを作成する必要があります。

ポータルのレプリケーションエージェントを設定するには：

1. オーサーインスタンスにログインします。
1. 「Web サイト」タブで、「*ツール*」タブをクリックします。
1. レプリケーションエージェントの&#x200B;**新規**&#x200B;メニューで、「**新しいページ**」をクリックします。

   ![screen_shot_2012-02-15at40647pm](assets/screen_shot_2012-02-15at40647pm.png)

1. 「*テンプレート*」で、「*レプリケーションエージェント*」を選択し、エージェントの名前を入力します。「*作成*」をクリックします。

   ![screen_shot_2012-02-15at40817pm](assets/screen_shot_2012-02-15at40817pm.png)

1. 作成したレプリケーションエージェントをダブルクリックします。まだ設定されていないので、無効と表示されます。

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
1. 接続をテストするには、「**接続をテスト**」リンクをクリックします。レプリケーションのテストが成功したかを示すログメッセージが表示されます。例：

   ![screen_shot_2012-02-15at42639pm](assets/screen_shot_2012-02-15at42639pm.png)

#### ポートレットのキャッシュの手動フラッシュ {#manually-flushing-the-portlet-cache}

レプリケーションエージェントに対して設定したものと同じ URL にアクセスして、ポートレットのキャッシュを手動でフラッシュすることができます。URL の形式については、[キャッシュのフラッシュ](#flushing-the-cache-via-replication-agent)を参照してください。また、フラッシュ対象を示すには、URL パラメーターの Path=&lt;path> を使用してこの URL を拡張する必要があります。

例：

`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=*` キャッシュ全体をフラッシュします。 キャッシュから`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=/content/mypage/xyz`が`/content/mypage/xyz`をフラッシュします。

### ポータルのセキュリティ {#portal-security}

ポータルが認証メカニズムを主導します。AEM には、テクニカルユーザー、ポータルユーザー、グループなどを使用してログインできます。ポートレットにはポータル内のユーザーのパスワードにアクセスする権限がないので、ユーザーを正常にログインさせるためのすべての資格情報をポートレットで把握できない場合は、SSO ソリューションを使用する必要があります。この場合、AEM ポートレットは必要なすべての情報を AEM に転送し、さらに AEM がこの情報を基盤の AEM リポジトリに転送します。この動作はプラガブルで、カスタマイズ可能です。

### 公開時の認証 {#authentication-on-publish}

この節では、基盤の AEM WCM インスタンスとの通信時にポートレットで使用できる認証モードについて説明します。

デフォルトでは、AEM のパブリッシュインスタンスにはユーザー情報が送信されません。コンテンツは常に匿名ユーザーとして表示されます。ユーザー固有の情報が AEM から配信される場合、または公開用のユーザー認証が必要な場合は、その設定をオンにする必要があります。

#### ポートレットの認証設定へのアクセス {#accessing-the-portlet-s-authentication-configuration}

ポートレットが AEM WCM インスタンス内で使用する認証設定オプションは、web コンソール（OSGi 設定）で設定できます。

>[!NOTE]
>
>AEM で作業をする際に、OSGi サービスの設定を管理する方法がいくつかあります（コンソールまたはリポジトリノード）。
>
>詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

ポートレットの認証設定にアクセスするには：

1. 次の URL にある web コンソールにアクセスします。

   `https://localhost:8080/cqportlet/cqbridge/system/console`

   デフォルト設定での例：

   `https://wps-host:10040/wps/PA_CQ5_Portlet/cqbridge/system/console`

1. Web コンソールにログインします。デフォルトの資格情報は、`admin/admin` です。
1. コンソールで、「**Configuration**」を選択します。
1. **Configuration** メニューで、設定する特定のサービスを選択します。サービスは、OSGi フレームワーク内のポートレットによって提供されます。

   | サービス名 | 説明 |
   |---|---|
   | Day Portal Director Authenticator | AEM WCM インスタンスに対して使用する認証モードを設定します。選択したモードに応じて、テクニカルユーザーまたは SSO cookie の名前を指定できます。また、AEM WCM パブリッシュインスタンスに対する認証を有効にすることができます。 |
   | Day Portal Director File Cache | ポートレットが AEM WCM インスタンスから受け取ったレスポンスをどのようにキャッシュするかに関するパラメーターを設定します。 |
   | Day Portal Director HTTP Client Service | ポートレットが基盤の AEM WCM インスタンスに HTTP 接続する方法を設定します。例えば、プロキシサーバーを指定できます。 |
   | Day Portal Director Locale Handler | ポートレットがサポートするロケールを設定します。AEM WCM インスタンスへのリクエストはユーザーのロケールに基づいています。例えば、ユーザーの言語が「ドイツ語」の場合、`/content/geometrixx/de/` にリクエストされます。 |
   | Day Portal Director Privilege Manager | ポートレットで、現在ログインしているユーザーに基づいて「Web サイト」タブの検証を行うかどうかを設定します。 |
   | Day Portal Director Toolbar Renderer | ポートレットのツールバーのレンダリング方法をカスタマイズします。 |

1. さらに、web コンソールとログサービスを設定できます。例えば、「Apache Felix OSGi 管理コンソール」リンクをクリックして、web コンソールの管理者の資格情報を変更できます。

#### テクニカルユーザーモード {#technical-user-mode}

デフォルトのモードでは、現在のポータルユーザーに関係なく、AEM WCM オーサーインスタンスに対してポートレットから発行されたすべてのリクエストが、同じテクニカルユーザーを使用して認証されます。テクニカルユーザーモードはデフォルトで有効です。OSGi 管理コンソールの該当する設定画面で、このモードを有効または無効にすることができます。

指定されたテクニカルユーザーは AEM WCM オーサーインスタンスに存在する必要があり、**公開時の認証**&#x200B;が有効な場合は、パブリッシュインスタンスにも存在する必要があります。オーサリング用の十分なアクセス権限をそのユーザーに付与するようにしてください。

#### SSO {#sso}

ポートレットでは、AEM によって SSO が標準でサポートされます。オーセンティケーターサービスが SSO を使用し、現在のポータルユーザーを `cqpsso` という cookie として **Basic** 形式で AEM に送信するように設定することができます。AEM は、パス / に対して SSO 認証ハンドラーを使用するように設定する必要があります。cookie 名をもここで設定する必要があります。

それに従って、AEM リポジトリの `crx-quickstart/repository/repository.xml` も次のように設定する必要があります。

```xml
<LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
  ...
  <param name="trust_credentials_attribute" value="TrustedInfo"/>
  <param name="anonymous_principal" value="anonymous"/>
</LoginModule>
```

#### SSO 認証モード {#sso-authentication-mode}

ポートレットでは、シングルサインオン（SSO）スキームを使用して AEM WCM の認証を行うことができます。このモードでは、ポータルに現在ログインしているユーザーが SSO cookie の形式で AEM WCM に転送されます。SSO モードを使用する場合、AEM ポートレットへのアクセス権を持つすべてのポータルユーザーの情報が基盤の AEM WCM インスタンスに存在している必要があります。通常は、AEM WCM が LDAP に接続する形式をとるか、事前にユーザーを手動で作成します。また、ポートレット内で SSO を有効にする前に、基盤の AEM WCM オーサーインスタンス（および&#x200B;**公開時の認証**&#x200B;が有効な場合のパブリッシュインスタンス）を、SSO ベースのリクエストを受け入れるように設定しておく必要もあります。

ポートレットが SSO 認証モードを使用するように設定するには、次の手順を実行します（各手順については、以降の節で詳しく説明します）。

* AEM WCM のリポジトリで信頼された資格情報を受け入れるようにします。
* AEM WCM で SSO 認証を有効にします。
* AEM ポートレットで SSO 認証を有効にします。

#### AEM WCM のリポジトリで信頼された資格情報を受け入れる設定にする {#enabling-aem-wcm-s-repository-to-accept-trusted-credentials}

AEM WCM で SSO を有効にする前に、AEM WCM から提供される信頼済みの資格情報を受け入れるように、基になるリポジトリを設定する必要があります。これを行うには、AEM の repository.xml を設定します。

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

#### AEM WCM での SSO 認証を有効にする {#enabling-sso-authentication-in-the-aem-wcm}

AEM WCM で SSO を有効にするには、AEM WCM の Apache Felix Web 管理コンソール（OSGi）で関連する設定エントリにアクセスします。

1. URI の https://&lt;AEM-host>:&lt;port>/system/console を使用してコンソールにアクセスします。
1. Configuration メニューで、「SSO Authentication Handler」を選択します。この例では、SSO ハンドラーは AEM ポートレットが提供する cookie に基づいて、すべてのパスに対する SSO リクエストを受け入れます。実際の設定はこれとは異なる可能性があります。

   | パス | ／ | すべてのリクエストに対して SSO ハンドラーを有効にする |
   |---|---|---|
   | cookie 名 | cqpsso | ポートレットの OSGi コンソールで設定した、ポートレットによって提供される cookie の名前。 |

1. 「**Save**」をクリックして SSO を有効にします。SSO が主要な認証スキームになりました。

AEM WCM で受け取るすべてのリクエストに対して、最初に SSO ベースの認証が試行されます。認証に失敗した場合は、通常の基本認証スキームへのフォールバックが実行されます。このように、SSO を使用しない通常の AEM WCM への接続も引き続き可能です。

#### AEM ポートレットでの SSO 認証の有効化 {#enabling-sso-authentication-in-a-aem-portlet}

基盤の AEM WCM インスタンスが SSO リクエストを受け入れるようにするために、ポートレットの認証モードを「**Technical**」から「**SSO**」に切り替える必要があります。

AEM ポートレットで SSO 認証を有効にするには：

1. URI の https://&lt;aem-host>:&lt;port>/system/console を使用してコンソールにアクセスします。
1. Configuration メニューで、利用可能な設定のリストから「Day Portal Director Authenticator」を選択します。
1. 「Mode」で「SSO」を選択します。その他のパラメーターはデフォルト値のままにします。

   ![chlimage_1-135](assets/chlimage_1-135.png)

1. 「Save」をクリックして、ポートレットの SSO を有効にします。

   検証用に、ポータルの管理者ユーザーでポートレットにアクセスします（AEM WCM で管理者権限を持つ同じユーザーを作成しておきます）。

この手順を実行した後、リクエストは SSO を使用して認証されるようになります。HTTP 通信の一般的なスニペットを見ると、次のような SSO およびポートレット固有のヘッダーが表示されています。

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

### PIN 認証の有効化 {#enabling-pin-authentication}

AEM コンテンツポートレットのデフォルトのインライン編集機能を使用せず、ポータルの外部でポートレットのオーサリングと管理部分を直接 AEM オーサーインスタンスで行う場合は、PIN 認証を有効にする必要があります。また、管理ボタンの設定を変更する必要があります。

Web サイト管理ページを開く場合、またはポートレットからページを編集する場合、AEM コンテンツポートレットでは新しい PIN 認証が使用されます。デフォルトでは、PIN 認証は無効になっているので、AEM で次の設定変更を行う必要があります。

1. repository.xml ファイルに信頼できる情報を追加することで、AEM で信頼できる認証を有効にします。

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
   </LoginModule>
   ```

1. OSGi 設定コンソール（デフォルトの場所は https://localhost:4502/system/console/configMgr）で、ドロップダウンメニューから「**CQ PIN Authentication Handler**」を選択します。
1. 「**URL Root Path**」パラメーターを編集し、「**/**」という 1 つの値だけを入力します。

### 権限 {#privileges}

ポートレットの一部の機能は権限によって保護されます。現在のユーザーがこの関数にアクセスするには、この権限が必要です。次の権限が事前に定義されています。

* toolbar：これは、ポートレットでツールバーを表示または使用するための一般的な権限です。
* prefs：この権限を持つユーザーは、ポートレットの環境設定を表示または変更できます。
* cq-author:edit：この権限を持つユーザーは、コンテンツの編集ビューを起動できます。
* cq-author:preview：この権限を持つユーザーは、プレビュー表示を行えます。
* cq-author:siteadmin：この権限を持つユーザーは、AEM 内で siteadmin を開くことができます。

権限の管理方法として最適なのは、ポータルの役割を使用して、役割をそれらの権限に割り当てることです。これは OSGi 設定によって実行できます。「Day Portal Director Privilege Manager」に、権限ごとの一連の役割を設定できます。ユーザーがその役割のいずれかを持っている場合、対応する権限を持っていることになります。

さらに、この役割ベースのアクセス権をポートレットのインスタンスごとに定義することも可能です。ポートレットの環境設定ダイアログに、上記の権限のそれぞれに関する入力フィールドが表示されます。権限ごとに、ポートレットの役割をコンマ区切りで指定したリストを設定できます。値を設定したら、その値が「Day Portal Director Privilege Manager」サービスのグローバル設定よりも優先されます。また、役割がマージされないので、場合によっては、このグローバル設定と同じ役割を追加する必要があります。値を指定しない場合は、グローバル設定が使用されます。

### AEM ポートレットアプリケーションのカスタマイズ {#customizing-the-aem-portlet-application}

指定した AEM ポートレットアプリケーションによって、AEM と同様に、eb アプリケーション内部で OSGi コンテナが開始されます。このアーキテクチャによって、次のような OSGi の利点をすべて活かすことができます。

* 更新、拡張しやすい
* ポータルサーバーと通信せずに、ポートレットのホットアップデートを実行できる
* ポートレットをカスタマイズしやすい

### ツールバーのボタン {#toolbar-buttons}

ツールバーとそのボタンは設定可能で、カスタマイズできます。ツールバーに独自のボタンを追加したり、各モードで表示するボタンを定義したりすることができます。各ボタンは、OSGi 設定を通じて設定できる OSGi サービスです。

OSGi web コンソールの「**Configuration**」タブに、すべてのボタンの設定が一覧表示されます。ボタンごとに、このボタンを表示するモードを定義できます。例えばすべてのモードを削除して、ボタンを無効にすることができます。

デフォルトでは、AEM コンテンツポートレットではインライン編集機能を使用します。AEM オーサーインスタンスに切り替えて編集したい場合は、「**SiteAdmin Button**」と「**ContentFinder Button**」を有効にして、「**Edit Button**」を無効にします。この場合、AEM で PIN 認証を適切に設定してください。

ポートレットの Felix web コンソールからバンドルをインストールして、ポートレットのツールバーレイアウトをカスタマイズできます。このバンドル内の定義済みの場所に、カスタムの CSS/HTML があります。

#### バンドル構造 {#bundle-structure}

バンドル構造の例を次に示します。

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

META-INF フォルダーには、バンドルとして識別するために OSGi によって要求される MANIFEST.MF ファイルが含まれています。このファイルの内容は次のとおりです。

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

HTML、CSS または画像が /com/day/cq/portlet/toolbar/layout フォルダー内にあるということはポートレットの必須条件とされており、変更することはできません。同じように、MANIFEST.MF の Import-Package ヘッダーと Export-Package ヘッダーでも /com/day/cq/portlet/toolbar/layout を指定する必要があります。Bundle-SymbolicName は、一意の完全修飾パッケージ名である必要があります。

Maven などのツールを使用してこのバンドルをビルドするか、ここで説明する関連ヘッダーを含む JAR ファイルを手動で作成することができます。

#### ポートレットのツールバーのビュー {#portlet-toolbar-views}

ポートレットのツールバーには、基本的に 2 つのビューの状態があります。それぞれのビューと関連するボタンは、対応する各 HTML ファイルでカスタマイズできます。

#### 公開ビュー {#publish-view}

公開ビューには、ツールバーを管理ビューに切り替える 1 つのボタンだけがあります。公開ビューは、[以前のバンドル](/help/sites-deploying/configuring-osgi.md#bundles)内の publish.html ファイルによって表されます。この HTML では、次のプレースホルダーを使用できます。プレースホルダーは、レンダリング時にポートレットによって、対応するコンテンツに置き換えられます。

#### 公開ビューのプレースホルダー {#publish-view-placeholders}

| プレースホルダー文字列 | 説明 |
|---|---|
| {buttonManage} | プレースホルダーが「**管理**」ボタンに置き換えられます。管理ボタンは、ポートレットの状態を管理状態に切り替えます。 |

#### 管理ビュー {#manage-view}

管理ビューには、「編集」、「「Web サイト」タブ」、「更新」および「戻る」の 4 つのボタンがあります。管理ビューは、[以前のバンドル](/help/sites-deploying/configuring-osgi.md#bundles)内の manage.html ファイルによって表されます。この HTML では、次のプレースホルダーを使用できます。プレースホルダーは、レンダリング時にポートレットによって、対応するコンテンツに置き換えられます。

#### 管理ビューのプレースホルダー {#manage-view-placeholders}

| プレースホルダー文字列 | 説明 |
|---|---|
| {buttonEdit} | プレースホルダーが「**編集**」ボタンに置き換えられます。編集ボタンは、現在のページを含む新しいウィンドウを AEM の編集モードで開きます。 |
| {buttonWebsites tab} | AEM WCM の「Web サイト」タブを開くボタンに置き換えられるプレースホルダーです。 |
| {buttonRefresh} | 現在のビューを更新します。 |
| {buttonBack} | ポートレットを公開ビューに戻します。 |

#### ボタン {#buttons}

表示されるビューを問わず、ボタンには button.html に定義された同じ共通の HTML が使用されます。

この HTML では、次のプレースホルダーを使用できます。プレースホルダーは、レンダリング時にポートレットによって、対応するコンテンツに置き換えられます。

#### 管理ビューおよび公開ビューのボタン {#manage-and-publish-view-buttons}

| プレースホルダー文字列 | 説明 |
|---|---|
| {name} | ボタンの名前（**author、back、refresh** など）。 |
| {id} | ボタンの CSS ID。 |
| {url} | ボタンのターゲット URL。 |
| {text} | ボタンのラベル。 |
| {onclick} | JavaScript の **onclick** 関数（{url} が含まれる）。 |

button.html ファイルの例：

```xml
<div class="cqp_button">

 <a href="#" onclick="{onclick}">

 <img src="/wps/PA_CQ5_Portlet/cqbridge/static/{id}.gif" alt="{text}"
title="{text}"/>

 </a>
</div>
```

#### カスタムレイアウトのインストール {#installing-a-custom-layout}

カスタムレイアウトをインストールするには、ポートレットの OSGI Web コンソールの「**Bundles**」セクションにアクセスしてバンドルをアップロードします。

#### パッケージ {#packages}

インストール用のパッケージをアップロードまたは作成する必要がある場合は、詳しい説明について AEM ドキュメントのパッケージマネージャーを参照してください。

### リンクの処理 {#link-handling}

すべてのリンクは、ポータルのコンテキスト内で動作するように書き換えられます。デフォルトで、レンダリングパラメーターを含むリンクが使用されます。代わりにアクションリンクを使用するように Portal Director HTML Rewriter を設定することもできます。

また、コンテンツパスを表示するために問い合わせられる追加のリクエストパラメーターを定義することもできます。これは、例えば外部から特定のコンテンツへのリンクがある場合に便利です。

さらに、Portal Director HTML Rewriter に、リンクの書き換え除外を定義するための正規表現のリストを設定することができます。例えば、外部システムへの相対リンクがある場合、それらのリンクをこの除外リストに追加する必要があります。

### ローカライゼーション {#localization}

AEM コンテンツポートレットにはローカライゼーション機能が組み込まれています。この機能によって、AEM のコンテンツが適切な言語で表示されるようになります。

ローカライゼーションは次の 2 つの手順で実行されます。

1. Portal Directory Locale Detector がポータルのロケール設定を取得して、ポータルユーザーのロケールを検出します。このサービスには、AEM で使用可能な言語のリストを設定しておく必要があります。
1. Portal Director Locale Handler が現在のリクエストのローカライゼーションを処理します。リクエストされたコンテンツのパス（例：`/content/geometrixx/en/company.html`）を取得し、設定に従って、**en** を実際のユーザーのロケールに書き換えます。

Portal Director Locale Handler には、ロケール情報をチェックするためのパスを設定できます。通常、この設定には `/content` 以下のすべてと、パス内のロケール情報の位置が含まれます。Portal Director Locale Handler はデフォルトで、AEM 内の多言語サイトの推奨構造に従います。

パス内のロケール情報を処理するための厳格なルールがないサイトの場合は、ロケールハンドラーを独自の実装に置き換えることが可能です。

### オプションの OSGi サービス {#optional-osgi-services}

オプションの OSGi サービスを実装して、ポートレットの様々な部分をカスタマイズできます。各サービスが 1 つの Java インターフェイスに対応します。このインターフェイスを実装して、バンドルによってポートレットにデプロイすることができます。

<table>
 <tbody>
  <tr>
   <td>RequestTracker</td>
   <td>リクエストトラッカーは、ポートレットによってコンテンツが表示されるときに常に通知を受けます。リクエストトラッカーを使用して、ポートレットの呼び出しを追跡できます。</td>
  </tr>
  <tr>
   <td>InvocationContextListener</td>
   <td>ポートレットへの各リクエストの最初と最後に呼び出されるリスナー。このリスナーを使用して、現在のリクエストの情報を変更したり追加したりすることができます。<br /> </td>
  </tr>
  <tr>
   <td>ErrorHandler</td>
   <td>レンダリングフェーズでのエラーを処理するカスタムエラーハンドラー。</td>
  </tr>
  <tr>
   <td>HttpProcessor</td>
   <td>このサービスを使用して、AEM への各 HTTP 呼び出しに情報を追加できます。</td>
  </tr>
  <tr>
   <td>PortletAction</td>
   <td>ポートレットに独自のアクションを追加します。このアクションは、ポートレットのアクションリンクから呼び出すことができます。</td>
  </tr>
  <tr>
   <td>PortletDecoratorService</td>
   <td>このサービスを使用して、ポートレットのコンテンツを修飾することができます。</td>
  </tr>
  <tr>
   <td>ResourceProvider</td>
   <td>独自のリソースプロバイダーを追加して、ポートレットのリソースリンク経由で何らかのリソースをクライアントに送信します。</td>
  </tr>
  <tr>
   <td>TextMapper</td>
   <td>HTML、CSS および JavaScript ファイルの後処理ができます。</td>
  </tr>
  <tr>
   <td>ToolbarButton</td>
   <td>ツールバーに独自のボタンを追加します。</td>
  </tr>
  <tr>
   <td>UrlMapper</td>
   <td>カスタム URL マッピングまたは書き換えを適用するためのサービスを追加します。</td>
  </tr>
  <tr>
   <td>UserInfoProvider</td>
   <td>ユーザーに関する独自の情報を追加します。このサービスを使用して、ポータルからポートレットに渡す情報を取得できます。</td>
  </tr>
 </tbody>
</table>

#### デフォルトサービスの置き換え {#replacing-default-services}

次のサービスには、コンテンツポートレット内にデフォルト実装（と対応する Java インターフェイス）があります。カスタマイズするには、新しいサービス実装を含むバンドルをポートレットアプリケーションにデプロイする必要があります。

そのサービスを実装する際に、サービスの **service.ranking** プロパティに正の値を必ず設定するようにしてください。デフォルトの実装ではランク 0 が使用され、ポートレットは最もランキングの高いサービスを使用します。

| **名前** | **説明** | **デフォルトの動作** |
|---|---|---|
| Authenticator | AEM に認証情報を提供します。 | オーサーとパブリッシュの両方に対して、設定可能なテクニカルユーザーを使用します。または、SSO を使用できます。 |
| HTMLRewriter | リンクと画像を書き換え | AEM リンクをポータルリンクに書き換えます。UrlMapper と TextMapper を使用して拡張できます。 |
| HttpClientService | すべての HTTP 接続を処理します。 | 標準実装です。 |
| LocaleHandler | ロケール情報を処理します。 | ロケールに従ってコンテンツへのリンクを書き換えます。 |
| LocaleDetector | ユーザーのロケールを検出します。 | ポータルで指定されたロケールを使用します。 |
| PrivilegeManager | ユーザー権限を確認します。 | ユーザーがコンテンツの編集を許可されている場合は、オーサーインスタンスへのアクセス権を確認します。 |
| ToolbarRenderer | ツールバーをレンダリングします。 | ツールバー機能を追加します。 |

### ポートレットイベント {#portlet-events}

ポートレット API（JSR-286）で、ポートレットイベントについて指定します。AEM コンテンツポートレットには統合ブリッジがあり、AEM ポートレットのポートレットイベントを OSGi イベントとして配信します。これにより、ポートレットイベントの処理はプラグイン可能になります。

特定のイベントを処理する場合は、デプロイメント記述子でこれらのイベントを受信イベントとして宣言し（またはポータルサーバーを介して設定し）、EventHandler インターフェイスを宣言する OSGi サービスを実装します（OSGi EventAdmin の仕様を参照してください）。

ポートレットイベントが発生するたびに、特定の OSGi イベントが送信され、ハンドラーを呼び出します。ハンドラーはすべてのコンテキスト情報を取得し、それに応じてポートレットのステータスを更新したり、新しいイベントを送信したりできます。基本的に、handle メソッド内ではポートレットイベントフェーズのすべての機能を使用できます。

## AEM のポータルとしての使用 {#using-aem-as-a-portal}

ポートレットコンポーネントを使用して、ポートレットウィンドウを AEM ページに追加します。アプリケーションサーバーにインストールする共有ライブラリを使用すると、ポートレットコンポーネントでデプロイ済みのポートレットアプリケーションを検出できます。

AEM をポータルとして使用するには、次のタスクを実行します。

1. ポートレットコンポーネントと共有ライブラリをインストールします。
1. ポートレットコンポーネントをサイドキックに追加します。
1. ポータルコンポーネントに表示するポートレットを含む web アプリケーションを設定およびデプロイします。
1. ポートレットコンポーネントをページに追加し、表示するポートレットを選択します。

>[!NOTE]
>
>ポートレットコンポーネントは、AEM が web アプリケーションとしてデプロイされている場合にのみ使用できます（[AEM をアプリケーションサーバーと共にインストール](/help/sites-deploying/application-server-install.md)を参照してください）。

### ポートレットコンポーネントのインストール {#installing-the-portlet-component}

AEM Quickstart JAR ファイルには、ポートレットコンポーネントファイルが含まれています。ファイル（cq-portlet-components.zip）を取得するには、Quickstart を実行するか、その内容を抽出します。

1. Quickstart JAR ファイルを実行するかその内容を抽出して、次の場所にある cq-portlet-components.zip ファイルを特定します。

   * クイックスタートを実行：crx-quickstart/opt/portal
   * クイックスタートの内容を抽出：static/opt/portal

1. アプリケーションサーバーにデプロイされている CQ5 オーサーインスタンスのパッケージマネージャーを開きます(https://*appserverhost*:*port*/cq5author/crx/packmgr)。

1. パッケージマネージャーを使用して、cq-portlets-components.zip パッケージを[アップロードし、インストールします](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system)。

   このパッケージによって、リポジトリ内の /libs/portal/director フォルダーに cq-portlet-director-sharedlibs-x.x.x.jar がインストールされます。

1. cq-portlet-director-sharedlibs-x.x.x.jar をハードドライブにコピーします。FileVault や WebDAV クライアントなど、任意の方法でファイルを取得できます。
1. cq-portlet-director-sharedlibs.x.x.x.jar ファイルをアプリケーションサーバーの共有ライブラリフォルダーに移動し、デプロイされたポートレットアプリケーションでクラスを使用できるようにします。

### サイドキックへのポートレットコンポーネントの追加 {#adding-the-portlet-component-to-sidekick}

ポートレットコンポーネントを段落システムに追加して、作成者が使用できるようにします。

1. サイドキックで、定規アイコンをクリックしてデザインモードに切り替えます。
1. 最初の段落の上にある`Design of par`ヘッダーの横の「**編集**」をクリックします。

1. 「**一般**」コンポーネントカテゴリで、ポートレットコンポーネントの横にあるチェックボックスをオンにして「OK」をクリックします。

![chlimage_1-25](assets/chlimage_1-25.jpeg)

### ポートレットアプリケーションの設定とデプロイ {#configuring-and-deploying-your-portlet-applications}

アプリケーションサーバーの web コンテナにポートレットをデプロイして、ポータルコンポーネントから使用できるようにします。ポートレットアプリケーションをデプロイする前に、このアプリケーションが AEM ポータルコンテナサーブレットを読み込むように設定する必要があります。この設定によって、ポートレットコンポーネントがポートレットにアクセスできるようになります。

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

1. ポートレットアプリケーションをアプリケーションサーバーにデプロイします。詳しくは、アプリケーションサーバーのドキュメントを参照してください。

### AEM ページへのポートレットの追加 {#adding-portlets-to-your-aem-page}

ポータルコンポーネントを使用して、ポートレットウィンドウを web ページに追加します。コンポーネントのプロパティを使用して、表示するポートレットを指定します。

1. Web ページで、サイドキックの一般グループの&#x200B;**ポートレット**&#x200B;コンポーネントをページにドラッグします。

   >[!NOTE]
   >
   >コンポーネントをページにドラッグした後、ページを再度読み込んで、適切に動作することを確認します。

1. コンポーネントをダブルクリックして、ポートレットのプロパティを開きます。
1. **ポートレットエンティティ**&#x200B;ドロップダウンメニューで、リストからポートレットを選択します。
1. ポートレットのタイトルバーを表示するかどうかに応じて、「タイトルバーを隠す」チェックボックスをオンまたはオフにします。
1. 「**ポートレットウィンドウ**」フィールドに、必要に応じて一意のポートレットウィンドウ ID を入力します。

   >[!NOTE]
   >
   >同じページで同じポートレットを複数使用する場合は、それぞれのポートレットに異なるウィンドウ ID を設定してください。

1. 「**OK**」をクリックします。ポートレットが AEM ページに表示されます。

   ![chlimage_1-136](assets/chlimage_1-136.png)

## ポートレットでの AEM のインストール、設定、使用 {#installing-configuring-and-using-aem-in-a-portlet}

AEM WCM によって提供されるコンテンツにアクセスするには、ポータルサーバーに AEM Portal Director Portlet を取り付ける必要があります。そのためには、このセクションで説明する手順を使用して、ポートレットをインストールおよび設定し、ポータルページに追加します。

デフォルトで、ポートレットは localhost:4503 でパブリッシュインスタンスに接続し、localhost:4502 でオーサーインスタンスに接続します。これらの値は、ポートレットのデプロイ時に変更できます。ポータルディレクターは、リポジトリ内の /libs/portal/directory 以下にコンテンツとして存在します。ポータルディレクターを使用する前に、アプリケーション WAR ファイルをダウンロードします。

### WAR ファイルのダウンロード {#downloading-the-war-file}

1. WebDAV または CRXDE Lite を使用して、/libs/portal/director に移動します。

1. *cq-portlet-webapp.war* をダウンロードします。

>[!NOTE]
>
>ここで紹介する手順では、WebSphere ポータルを例として使用します。できる限り汎用的な手順を説明しますが、他の web ポータルでは手順が異なります。すべての web ポータルで手順はほぼ同一ですが、お使いの web ポータルに合わせて手順を変更する必要があります。

#### ポートレットのインストール {#installing-the-portlet}

ポートレットをインストールするには、以下の手順を実行します。

1. 管理者権限でポータルにログインします。
1. Web ポータルのポートレット管理画面に移動します。
1. 「インストール」をクリックして、ダウンロードした AEM ポートレットアプリケーション（cq-portlet-webapp.war）を参照し、ポートレットに関するその他の重要な情報を入力します。

   他のポートレット基本情報については、デフォルト値を使用するか、値を変更します。デフォルト値を使用する場合、ポートレットのアドレスは https://&lt;wps-host>:&lt;port>/wps/PA_CQ5_Portlet になります。ポートレットによって提供される OSGi 管理コンソールのアドレスは https://&lt;wps-host>:&lt;port>/wps/ PA_CQ5_Portlet/cqbridge/system/console になります（デフォルトのユーザー名とパスワードは admin/admin です）。

1. そのオプションまたはチェックボックスを選択してポートレットアプリケーションが自動起動することを確認し、変更を保存します。インストールが成功したことを示すメッセージが表示されます。

#### ポートレットの設定 {#configuring-the-portlet}

ポートレットのインストール後、基盤の AEM インスタンス（オーサーおよびパブリッシュ）の URL を認識できるようにポートレットを設定する必要があります。また、その他のオプションも設定できます。

ポートレットを設定するには、以下の手順を実行します。

1. アプリケーションサーバーのポータル管理ウィンドウで、ポートレット管理に移動します。この画面にすべてのポートレットが一覧表示され、AEM Portal Director ポートレットを選択します。
1. 必要に応じて、ポートレットを設定します。例えば、オーサーインスタンスとパブリッシュインスタンスの URL や開始パスの URL を変更する必要がある場合があります。デフォルトの設定については、[ポートレット環境設定](/help/sites-administering/aem-as-portal.md#portlet-preferences)を参照してください。

   >[!NOTE]
   >
   >ポートレットを **/** 以外のコンテキストパスで実行している AEM オーサーインスタンスおよびパブリッシュインスタンスに接続するように設定する場合は、（Felix Web コンソールなどを使用して）これらの AEM インスタンスの HTML ライブラリマネージャー設定で強制 **CQUrlInfo** を有効にする必要があります。そうしなければ、編集が機能せず、環境設定ダイアログが表示されません。

1. アプリケーションサーバーで設定の変更を保存します。

1. ポートレットの OSGI 管理コンソールに移動します。デフォルトの場所は `https://<wps-host>:<port>/wps/PA_CQ5_Portlet/cqbridge/system/console/configMgr` です。デフォルトのユーザー名とパスワードは **admin/admin** です。

1. 「**Day Portal Director CQ Server Configuration**」設定を選択し、次の値を編集します。

   * **オーサーベース URL**：AEM オーサーインスタンスのベース URL です。
   * **パブリッシュベース URL**：AEM パブリッシュインスタンスのベース URL です。
   * **Author Is Used As Publish**：オーサーインスタンスが（開発用に）パブリッシュインスタンスとして
使用されているかどうかを指定します。

   ![chlimage_1-137](assets/chlimage_1-137.png)

1. 「**保存**」をクリックします。これで、ポートレットをポータルページに追加してポータルを使用できるようになりました。

### コンテンツの URL {#content-urls}

コンテンツが AEM からリクエストされると、ポートレットにより、現在の表示モード（パブリッシュまたはオーサー）と現在のパスから完全な URL が作成されます。デフォルト値を使用した場合の最初の URL は `https://localhost:4503/content/geometrixx/en.portlet.html` です。`htmlSelector` の値が URL の拡張子の前に自動的に追加されます。

ポートレットがヘルプモードに切り替えられ、`appendHelpViewModeAsSelector` が選択された場合は、同じように `help` セレクターが付加されます（例：`https://localhost:4503/content/geometrixx/en.portlet.html.help`）。ポートレットウィンドウが最大化され、`appendMaxWindowStateAsSelector` が選択された場合は、同じようにそのセレクターが付加されます（例：`https://localhost:4503/content/geometrixx/en.portlet.max.help`）。

セレクターは AEM で評価され、セレクターごとに様々なテンプレートを使用できます。

### AEM でのコンテンツ URL マップの使用 {#using-a-content-url-map-in-aem}

通常、開始パスは直接 AEM 内のコンテンツを示しますが、ポートレット環境設定ではなく AEM 内で開始パスを管理する場合は、開始パスが AEM 内のコンテンツマップを示すように設定できます（例：`/var/portlets`）。この場合、AEM で実行されるスクリプトでは、ポートレットから送信された情報を使用して、どの URL が開始 URL であるかを判断することができます。このスクリプトは、正しい URL へのリダイレクトを発行する必要があります。

#### ポータルページへのポートレットの追加 {#adding-the-portlet-to-the-portal-page}

ポートレットをポータルページに追加するには、以下の手順を実行します。

1. アプリケーションサーバーの管理者ウィンドウで、ページ管理画面に移動します（例えば、WebSphere 6.1 では、「**ページを管理**」をクリックします）。
1. ポートレットの名前を選択し、既存のページを選択するかページを作成します。
1. ページレイアウトを編集します。
1. ポートレットを選択し、コンテナに追加します。
1. 変更を保存します。

#### ポートレットの使用 {#using-the-portlet}

ポートレットに追加したページにアクセスするには：

1. ポートレットのパーソナライズ機能メニューで、ポータル内で設定したとおりにポートレットを設定します。
1. その設定を開き（ポートレットに、ポートレットの設定で指定した公開用の開始 URL が表示されます）、必要に応じて編集を行い、保存します。
