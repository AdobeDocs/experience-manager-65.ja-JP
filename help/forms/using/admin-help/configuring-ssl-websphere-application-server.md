---
title: WebSphere Application Server に対する SSL の設定
description: WebSphere Application Server の SSL を構成する方法を学習します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b0786b52-879e-4a24-9cc9-bd9dcb2473cc
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 100%

---

# WebSphere Application Server に対する SSL の設定 {#configuring-ssl-for-websphere-application-server}

このセクションには、IBM WebSphere アプリケーションサーバーで SSL を構成するための次の手順が含まれています。

## WebSphere でのローカルユーザーアカウントの作成 {#creating-a-local-user-account-on-websphere}

SSL を有効にするには、WebSphere は、システムを管理する権限を持つローカル OS ユーザーレジストリ内のユーザーアカウントにアクセスする必要があります。

* （Windows）Administrators グループの一員であり、オペレーティングシステムの一部として機能する権限を持つ Windows ユーザーを作成します（[WebSphere 用 Windows ユーザーの作成](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere)を参照）。
* （Linux、UNIX）ユーザーは、root ユーザーまたは root 権限を持つ別のユーザーにすることができます。WebSphere で SSL を有効にする場合は、このユーザーのサーバー ID とパスワードを使用します。

### WebSphere 用 Linux または UNIX ユーザーを作成する {#create-a-linux-or-unix-user-for-websphere}

1. root ユーザーとしてログインします。
1. コマンドプロンプトに次のコマンドを入力してユーザーを作成します。

   * （Linux および Sun Solaris）`useradd`
   * （IBM AIX）`mkuser`

1. コマンドプロンプトで `passwd` と入力して、新しいユーザーのパスワードを設定します。
1. （Linux および Solaris）コマンドプロンプトでパラメーターを付けずに `pwconv` と入力して、シャドーパスワードファイルを作成します。

   >[!NOTE]
   >
   >（Linux および Solaris）WebSphere Application Server のローカル OS セキュリティレジストリが機能するには、シャドーパスワードファイルが存在している必要があります。シャドーパスワードファイルは通常、**/etc/shadow** という名前で、/etc/passwd ファイルを基にして作成されます。シャドーパスワードファイルが存在しない場合、グローバルセキュリティを有効にしてユーザーレジストリをローカル OS として設定するとでエラーが発生します。

1. /etc ディレクトリにあるグループファイルをテキストエディターで開きます。
1. 手順 2 で作成したユーザーを `root` グループに追加します。
1. ファイルを保存して閉じます。
1. （SSL が有効な UNIX）WebSphere を root ユーザーとして起動および停止します。

### WebSphere 用 Windows ユーザーを作成する {#create-a-windows-user-for-websphere}

1. 管理者アカウントを使用して管理コンソールにログインします。
1. **スタート／コントロールパネル／管理ツール／コンピュータ管理／ローカルユーザーとグループ**&#x200B;を選択します。
1. 「ユーザー」を右クリックして「**新規ユーザー**」を選択します。
1. 適切なボックスにユーザー名とパスワードを入力し、残りのボックスに必要なその他の情報を入力します。
1. 「**ユーザーは次回ログイン時にパスワードを変更する必要がある**」の選択を解除し、「**作成**」をクリックしてから、「**閉じる**」をクリックします。
1. 「**ユーザー**」をクリックし、作成したユーザーを右クリックして、「**プロパティ**」を選択します。
1. 「**メンバー**」タブをクリックし、「**追加**」をクリックします。
1. 「選択するオブジェクト名を入力」ボックスに `Administrators` と入力し、「名前の確認」をクリックしてグループ名が正しいことを確認します。
1. 「**OK**」をクリックしてから、「**OK**」を再びクリックします。
1. **スタート／コントロールパネル／管理ツール／ローカルセキュリティポリシー／ローカルポリシー**&#x200B;を選択します。
1. 「ユーザー権利の割り当て」をクリックし、「オペレーティングシステムの一部として機能」を右クリックして、「プロパティ」を選択します。
1. 「**ユーザーまたはグループを追加**」をクリックします。
1. 「選択するオブジェクト名を入力してください」ボックスに、手順 4 で作成したユーザーの名前を入力し、「**名前を確認**」をクリックして名前が正しいことを確認し、「**OK**」をクリックします。
1. 「**OK**」をクリックして、「オペレーティングシステムの一部として機能するプロパティ」ダイアログボックスを閉じます。

### 新しく作成したユーザーを管理者として使用するように WebSphere を構成する {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. WebSphere が実行されていることを確認します。
1. WebSphere 管理コンソールで、**セキュリティ／グローバルセキュリティ**&#x200B;を選択します。
1. 管理セキュリティで、「**管理ユーザーの役割**」を選択します。
1. 「追加」をクリックして次の操作を行います。

   1. 検索ボックスに「**&amp;ast;**」と入力し、「検索」をクリックします。
   1. 役割の下にある「**管理者**」をクリックします。
   1. 新しく作成したユーザーを「Mapped to role」に追加し、管理者にマップします。

1. 「**OK**」をクリックして、変更を保存します。
1. WebSphere プロファイルを再起動します。

## 管理セキュリティを有効にする {#enable-administrative-security}

1. WebSphere 管理コンソールで、**セキュリティ／グローバルセキュリティ**&#x200B;を選択します。
1. 「**セキュリティ構成ウィザード**」をクリックします。
1. 「**アプリケーションセキュリティを有効にする**」チェックボックスが有効になっていることを確認します。「**次へ**」をクリックします。
1. 「**統合リポジトリ**」を選択して、「**次**」をクリックします。
1. 設定する認証情報を指定し、「**次**」をクリックします。
1. 「**終了**」をクリックします。
1. WebSphere プロファイルを再起動します。

   WebSphere は、デフォルトのキーストアとトラストストアの使用を開始します。

## SSL（カスタムキーとトラストストア）を有効にする {#enable-ssl-custom-key-and-truststore}

信頼ストアとキーストアは ikeyman ユーティリティまたは管理コンソールを使用して作成できます。ikeyman を正しく動作させるには、WebSphere のインストール パスに括弧が含まれていないことを確認してください。

1. WebSphere 管理コンソールで、**セキュリティ／SSL 証明書とキーの管理**&#x200B;を選択します。
1. 関連項目の下にある「**キーストアと証明書**」をクリックします。
1. **キーストアの使用法**&#x200B;ドロップダウンで、「**SSL キーストア**」が選択されていることを確認します。「**新規**」をクリックします。
1. 論理名と説明を入力します。
1. キーストアを作成する場所のパスを指定します。ikeyman を通じてキーストアをすでに作成している場合は、キーストアファイルへのパスを指定します。
1. パスワードを指定して確認します。
1. キーストアのタイプを選択して、「**適用する**」をクリックします。
1. マスター設定を保存します。
1. 「**個人証明書**」をクリックします。
1. ikeyman を使用して既に作成されたキーストアを追加した場合は、証明書が表示されます。それ以外の場合は、次の手順を実行して、新しい自己署名証明書を追加する必要があります。

   1. **作成／自己署名証明書**&#x200B;を選択します。
   1. 証明書フォームに適切な値を指定します。エイリアスと共通名をマシンの完全修飾ドメイン名として保持していることを確認してください。
   1. 「**適用**」をクリックします。

1. 手順 2 ～ 10 を繰り返して、トラストストアを作成します。

## カスタムキーストアとトラストストアをサーバーに適用 {#apply-custom-keystore-and-truststore-to-the-server}

1. WebSphere 管理コンソールで、**セキュリティ／SSL 証明書とキー管理**&#x200B;を選択します。
1. 「**エンドポイントのセキュリティ設定を管理**」をクリックします。ローカルトポロジマップが開きます。
1. 「受信」で、ノードの直接の子を選択します。
1. 「関連項目」で、「**SSL設定**」を選択します。
1. 「**NodeDefaultSSLSetting**」を選択します。
1. トラストストア名とキーストア名のドロップダウンリストから、作成したカスタムトラストストアとキーストアを選択します。
1. 「**適用**」をクリックします。
1. マスター設定を保存します。
1. WebSphere プロファイルを再起動します。

   これで、プロファイルは SSL 設定と証明書の上で実行されます。

## AEM Forms ネイティブのサポートの有効化 {#enabling-support-for-aem-forms-natives}

1. WebSphere 管理コンソールで、**セキュリティ／グローバルセキュリティ**&#x200B;を選択します。
1. 「認証」セクションで、**RMI/IIOP セキュリティ**&#x200B;を展開して、「**CSIv2 インバウンド通信**」をクリックします。
1. トランスポートドロップダウンリストで「**SSL サポート**」が選択されていることを確認します。
1. WebSphere プロファイルを再起動します。

## https で始まる URL を変換するように WebSphere を設定 {#configuring-websphere-to-convert-urls-that-begins-with-https}

https で始まる URL を変換するには、その URL の署名者証明書を WebSphere サーバーに追加します。

**https 対応サイトの署名者証明書を作成**

1. WebSphere が実行されていることを確認します。
1. WebSphere 管理コンソールで、「署名者証明書」に移動し、セキュリティ／SSL 証明書とキー管理／キーストアと証明書／NodeDefaultTrustStore／署名者証明書をクリックします。
1. 「ポートから取得」をクリックして、次のタスクを実行します。

   * 「ホスト」ボックスに URL を入力します。例えば、`www.paypal.com` と入力します。
   * 「ポート」ボックスに、`443` と入力します。このポートはデフォルトの SSL ポートです。
   * 「エイリアス」ボックスにエイリアスを入力します。

1. 「署名者情報を取得」をクリックし、情報が取得されたことを確認します。
1. 「適用」をクリックし、「保存」をクリックします。

証明書が追加されたサイトからの HTML から PDF への変換は、Generate PDF サービスから機能するようになります。

>[!NOTE]
>
>アプリケーションが WebSphere 内から SSL サイトに接続するには、署名者証明書が必要です。これは、SSL ハンドシェイク中に接続のリモートサイドから送信された証明書を検証するために Java Secure Socket Extensions（JSSE）によって使用されます。

## 動的なポートの設定 {#configuring-dynamic-ports}

IBM WebSphere では、グローバルセキュリティが有効な場合、ORB.init() への複数の呼び出しは許可されません。永続的な制限については、https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704 を参照してください。

次の手順を実行してポートを動的に設定し、問題を解決します。

1. WebSphere 管理コンソールで、**サーバー**／**サーバーの種類**／**WebSphere アプリケーションサーバー**&#x200B;を選択します。
1. 「環境設定」セクションでサーバーを選択します。
1. 「**設定**」タブの「**通信**」セクションで、**ポート**&#x200B;を展開し、「**詳細**」をクリックします。
1. 以下のポート名をクリックし、**ポート番号**&#x200B;を 0 にして、「**OK**」をクリックします。

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## sling.properties ファイルを設定します。 {#configure-the-sling-properties-file}

1. 編集用に `[aem-forms_root]`\crx-repository\launchpad\sling.properties ファイルを開きます。
1. `sling.bootdelegation.ibm` プロパティを見つけてその値フィールドに `com.ibm.websphere.ssl.*` を追加します。更新されたフィールドは次のようになります。

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. ファイルを保存し、サーバーを再起動します。
