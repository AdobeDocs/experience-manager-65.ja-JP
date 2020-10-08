---
title: グローバル設定の読み込みと書き出し
seo-title: グローバル設定の読み込みと書き出し
description: Workspace の検索テンプレート定義とグローバル設定は、読み込んだり書き出したりすることができます。
seo-description: Workspace の検索テンプレート定義とグローバル設定は、読み込んだり書き出したりすることができます。
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 72%

---


# グローバル設定の読み込みと書き出し {#importing-and-exporting-global-settings}

Workspace の検索テンプレート定義とグローバル設定は、読み込んだり書き出したりすることができます。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

例えば、検索テンプレート定義とグローバル設定を、ある環境から書き出して別の環境に読み込むことにより、開発環境から実稼働環境に移行することができます。

グローバル設定ファイルを書き出したら、設定を XML エディターまたはテキストエディターで変更できます。ただし、編集が必要になる可能性があるのは JChannelConnectionProperties、formViewOnly、および specialRoutes の設定だけです。詳しくは、[Workspace グローバル設定](importing-exporting-global-settings.md#workspace-global-settings)を参照してください。


>[!NOTE]
>
>グローバル設定ファイルのイベントプロパティを変更した場合は、サーバーを再起動する必要があります。

## 検索テンプレート定義の読み込み {#import-a-search-template-definition}

1. 管理コンソールで、サービス／Workspace／グローバル管理をクリックします。
1. 「検索テンプレート定義を読み込む」ボックスで、「ファイルを選択」をクリックし、検索テンプレートを選択します。読み込むことができるのは、Workspace のインスタンスから書き出された検索テンプレート定義だけです。
1. 「読み込み」をクリックします。

## 検索テンプレート定義の書き出し {#export-a-search-template-definition}

1. グローバル管理ページの「検索テンプレート定義を書き出し」で、「すべてを一覧表示」をクリックします。
1. 検索テンプレートのリストで、書き出すテンプレートを選択します。

   >[!NOTE]
   >
   >複数のテンプレートを選択できますが、最後に選択したテンプレートだけが書き出されます。

1. 「書き出し」をクリックし、ファイルを、使用しているコンピューターに保存します。

## グローバル設定の読み込み {#import-global-settings}

1. グローバル管理ページの「グローバル設定を読み込む」で、「ファイルを選択」をクリックし、グローバル設定ファイルを選択します。グローバル設定ファイルは、XML 形式である必要があります。
1. 「読み込み」をクリックします。

## グローバル設定の書き出し {#export-global-settings}

1. グローバル管理ページの「グローバル設定を書き出し」で、「書き出し」をクリックします。
1. ファイルを、使用しているコンピューターに保存します。

## Workspace グローバル設定 {#workspace-global-settings}

グローバル設定ファイルは変更できます。ただし、編集が必要になる可能性があるのは JChannelConnectionProperties、formViewOnly、および specialRoutes の設定だけです。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

Workspace グローバル設定ファイルには、次の設定が含まれます。

### specialRoutes 設定 {#specialroutes-settings}

*specialRoutes* 設定では、Workspace での特別なルート、承認および拒否のプロパティを指定します。場合によっては、Workspace のタスクカードにこれらのルートのボタンが表示され、ユーザーがフォームを開かずにルートを選択できます。グローバル設定ファイルで specialRoutes 設定を変更して、承認または拒否の対象となるカスタマイズされた名前を追加したり、追加ルートを作成したりすることができます。

**client_specialRoutes_routes_approve_style:** Workspaceテーマで検索されるスタイルの名前です。このテーマは、承認ボタンアイコンを識別します。 スタイルには、有効になっているアイコンと無効になっているアイコンの値を含める必要があります。カスタムボタンのスタイルを定義するには、次のテンプレートを使用する必要があります。` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }`Workspace の CSS ファイルは workspace-theme.swf ファイルに埋め込まれます。このファイルは、adobe-workspace-client.ear の adobe-workspace-client.war ファイル内にあります。Workspace の外観を変更するには、workspace-theme.swf ファイルを再コンパイルする必要があります。

**client_specialRoutes_routes_deny_names:** 「拒否」と解釈されるためにWorkbenchユーザーが使用できる様々な文字列です。 これらの文字列では、大文字と小文字が区別されます。例えば、デフォルト値は「deny」です。Workbench ユーザーのプロセスで「Deny」という単語が使用された場合、この単語は認識されません。ルートボタンをカスタマイズしたり、ルートボタンにスタイルを適用したりするには、「Deny」という単語をこの設定に追加する必要があります。

**client_specialRoutes_routes_deny_style:** Workspaceテーマファイル内にあるスタイルの名前です。これにより、拒否ボタンアイコンを識別します。 スタイルには、有効になっているアイコンと無効になっているアイコンの値を含める必要があります。カスタムボタンのスタイルを定義するには、次のテンプレートを使用する必要があります。
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_specialRoutes_routes_approve_names:** 「承認」として解釈されるためにWorkbenchユーザーが使用できる様々な文字列です。 これらの文字列では、大文字と小文字が区別されます。例えば、デフォルト値は、「approve」です。Workbench ユーザーのプロセスで「Approve」という単語が使用された場合、この単語は認識されません。ルートボタンをカスタマイズしたり、ルートボタンにスタイルを適用したりするには、「Approve」という単語をこの設定に追加する必要があります。

**client_specialRoutes_names:** リソースファイルからカスタマイズされた文字列値を検索するために使用されるキーです。 この設定の各エントリには、名前およびスタイルの値を含める必要があります。

### JGroup 設定 {#jgroup-settings}

これらの設定は、Adobe LiveCycle ES 2.5 またはそれより前のバージョンからアップグレードした場合のみ表示されます。

**server_remoteevents_ClientTimeoutMilliseconds:** JGroupがイベントメッセージを待機する最大時間です。 この設定は変更しないでください。

**server_remoteevents_ServerTimeoutMilliseconds:** サーバーでJGroupメッセージを受信するためのタイムアウトです。 このオプションで、サーバーからクライアントにメッセージを送信する際の遅延を設定します。

**server_remoteevents_JChannelConnectionProperties:** (サービスイベントがRemoteEventサービスによって処理される)サーバーとWorkspaceのすべてのインスタンスとの通信に使用されるJGroupの接続プロパティです。

マルチキャスト IP アドレス（mcast_addr）、マルチキャスト IP ポート（mcast_port）およびマルチキャストパケットの TTL（ip_ttl）について、UDP 値を変更する必要がある場合があります。デフォルトでは、マルチキャスト IP アドレスとポートの値は、任意の順序で生成され、通常、これらの値を変更する必要はありません。ただし、会社にマルチキャスト IP アドレスに対する特定のマルチキャストの範囲に関するネットワークポリシーがある場合は、これらの値の変更が必要になることがあります。

>[!NOTE]
>
>TTL は、クラスター内のサーバー間のネットワークスイッチの数よりも大きくする必要があります。ただし、この値の設定が大きすぎると、マルチキャストパケットがサブネットに送信され、そこで破棄される可能性があります。

この設定の残りのプロパティは変更しないでください。

**server_remoteevents_JGroupName:** リモートイベント通信に使用するJGroupの名前です。 この値は、ランダムに生成され、クラスター内の競合を回避します。この値は変更しないでください。

JGroups および Workspace について詳しくは、「[JGroups と AEM Forms Workspace - 説明](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html)」を参照してください。

### formView 設定 {#formview-settings}

**client_formView_openFormInFullScreen:** Workspaceですべてのフォームをフルスクリーンモードで表示するには、このオプションをtrueに設定します。 このオプションのデフォルトは false に設定されており、フォームはフルスクリーンモードで表示されません。User サービスには、タスクと関連付けられたドキュメントをフルスクリーンモードで開くオプションがあります。このオプションを使用すると、プロセスごとに表示を制御できます。

**client_routes_formViewOnly:** Trueに設定すると、ルートはWorkspaceのカード表示またはリスト表示に表示されません。 デフォルト値は False で、ルートはカード表示およびリスト表示に表示されます。

### その他の設定 {#other-settings}

**client_mimeTypes_openOutsideBrowser:** Workspaceブラウザーインスタンスの外部で開くドキュメントのMIMEタイプです。 組織のプロセスに追加の MIME タイプが必要な場合はここで指定します。デフォルト値は次のとおりです。

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching:** カスタムタスクユーザーインターフェイスをキャッシュします。

**server_debugLevel:** この設定は変更しないでください。

**client_pollingInterval:** 新しいタスクおよび変更されたを検出するために、(JEE上のAEM formsでは廃止されています)Flexワークスペースで使用されるポーリング間隔（秒）を設定します。 デフォルト値は 3 秒です。これは AEM Forms Workspace では動作しません。

**client_systemContext_name:** AEM Formsワークスペースのタスクの添付ファイルに対して（「添付ファイル」タブの）「追加者」フィールドに表示するカスタム名（例：市民）を指定します。

カスタム名を定義するには：

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>Demo アプリケーションでは、デフォルトの表示名は&#x200B;**市民**&#x200B;です。作成するカスタムアプリケーションでは、デフォルトの表示名は「**システムコンテキストアカウント**」です。
>
>**client_idleTimeout:** ユーザーが特定の時間非アクティブのままの場合、AEM Formsワークスペースセッションの有効期限が切れます。 この機能を有効にするには、グローバル設定&lt;client_idleTimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idleTimeout>にエントリを追加します。 値0を指定すると、アイドルタイムアウトが無効になります。 時間は秒単位で指定します。
