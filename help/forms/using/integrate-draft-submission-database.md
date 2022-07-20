---
title: ドラフトと送信コンポーネントとデータベースの統合のサンプル
seo-title: Sample for integrating drafts & submissions component with database
description: ドラフトと送信コンポーネントをデータベースに統合するためのカスタマイズされたデータサービスおよびメタデータサービスのリファレンス実装
seo-description: Reference implementation of customized data and metadata services to integrate drafts and submissions component with a database.
uuid: ccdb900e-2c2e-4ed3-8a88-5c97aa0092a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: da96d3d8-a338-470a-8d20-55ea39bd15bf
exl-id: 2e4f8f51-df02-4bbb-99bb-30181facd1e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1467'
ht-degree: 100%

---

# ドラフトと送信コンポーネントとデータベースの統合のサンプル {#sample-for-integrating-drafts-submissions-component-with-database}

## サンプルの概要 {#sample-overview}

AEM Forms ポータルのドラフトと送信コンポーネントにより、フォームをドラフトとして保存し、任意のデバイスから後で送信することができます。また、ポータルにて送信済みのフォームを表示することもできます。この機能を有効にするため、AEM Forms では、ユーザーによってフォームに入力されたデータおよびドラフトおよび送信済みフォームに関連するメタデータを保存する、データおよびメタデータサービスを提供しています。このデータは、デフォルトで CRX レポジトリに格納されます。ただし、ユーザーが AEM のパブリッシュインスタンスを通じてフォームとやり取りを行うのは通常企業のファイアウォールの外側であるため、組織によっては、よりセキュアで信頼性のあるデータストレージが必要となる場合もあります。

このドキュメントで取り上げるサンプルは、ドラフト&amp;送信コンポーネントをデータベースに統合するためのカスタマイズされたデータサービスおよびメタデータサービスのリファレンス実装です。サンプル実装で使用されているデータベースは **MySQL 5.6.24** ですが、ドラフト&amp;送信コンポーネントは、あらゆるデータベースに統合することができます。

>[!NOTE]
>
>* このドキュメントで説明されている例および設定は、MySQL 5.6.24 に基づいているため、お使いのデータベースシステムに合わせてそれらを適切に置き換える必要があります。
>* 最新バージョンの AEM Forms のアドオンパッケージをインストールしていることを確認してください。使用可能なパッケージのリストについては、[AEM Forms リリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)の記事を参照してください。
>* サンプルパッケージは、アダプティブフォーム送信アクションでのみ機能します。


## サンプルのセットアップおよび設定 {#set-up-and-configure-the-sample}

すべてのオーサーインスタンスとパブリッシュインスタンスで、次の手順を実行し、サンプルをインストールして設定します。

1. パッケージ **aem-fp-db-integration-sample-pkg-6.1.2.zip** をファイルシステムにダウンロードします。

   データベース統合のサンプルパッケージ

[ファイルを入手](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. AEM パッケージマネージャー（https://[*host*]:[*port*]/crx/packmgr/）に移動します。
1. 「**[!UICONTROL パッケージをアップロード]**」をクリックします。

1. パッケージ **aem-fp-db-integration-sample-pkg-6.1.2.zip** を参照して選択し、「**[!UICONTROL OK]**」をクリックします。
1. パッケージの隣にある「**[!UICONTROL インストール]**」をクリックし、パッケージをインストールします。
1. **[!UICONTROL AEM web コンソール設定]**
ページ（https://[*host*]:[*port*]/system/console/configMgr）に移動します。
1. **[!UICONTROL Forms Portal Draft and Submission Configuration]** をクリックし、編集モードで開きます。

1. 次の表の説明に従って、プロパティの値を指定します。

   | **プロパティ** | **説明** | **値** |
   |---|---|---|
   | フォームポータル ドラフトデータサービス | ドラフトデータサービスの識別子 | formsportal.sampledataservice |
   | フォームポータル ドラフトメタデータサービス | ドラフトメタデータサービスの識別子 | formsportal.samplemetadataservice |
   | フォームポータル 送信データサービス | 送信データサービスの識別子 | formsportal.sampledataservice |
   | フォームポータル 送信メタデータサービス | 送信メタデータサービスの識別子 | formsportal.samplemetadataservice |
   | フォームポータル 保留中署名データサービス | 保留中署名データサービスの識別子 | formsportal.sampledataservice |
   | フォームポータル 保留中署名メタデータサービス | 保留中署名メタデータサービスの識別子 | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >サービスは、`aem.formsportal.impl.prop` キーの値として以下に記述されている名前によって解決されます。

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   データテーブルおよびメタデータテーブルの名前は変更できます。

   メタデータテーブルに別の名前を設定するには、以下の手順を実行してください。

   * Web コンソール設定で、「Forms Portal Metadata Service Sample Implementation」を見つけてクリックします。データソース、メタデータ／追加メタデータのテーブル名の値は変更できます。

   データテーブルに別の名前を設定するには、以下の手順を実行してください。

   * Web コンソール設定で、「Forms Portal Data Service Sample Implementation」を見つけてクリックします。データソースおよびデータテーブル名の値は変更できます。
   >[!NOTE]
   >
   >テーブル名を変更する場合は、テーブル名をフォームポータル設定に入力してください。

1. 他の設定はそのままにし、「**[!UICONTROL 保存]**」をクリックします。

1. データベース接続は、Apache Sling Connection Pooled Data Source 経由で実行できます。
1. Apache Sling 接続の場合は、Web コンソール設定で「**[!UICONTROL Apache Sling Connection Pooled DataSource]**」を見つけてクリックし、編集モードで開きます。次の表の説明に従って、プロパティの値を指定します。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>値</strong></td>
  </tr>
  <tr>
   <td>データソース名</td>
   <td><p>データソースプールからドライバーをフィルターするためのデータソース名</p> <p><strong>注意：</strong><em>サンプルでは、データソース名として「FormsPortal」を使用しています。</em></p> </td>
  </tr>
  <tr>
   <td>JDBC ドライバークラス</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>JDBC 接続 URI<br /> </td>
   <td>jdbc:mysql://[<em>host</em>]:[<em>port</em>]/[<em>schema_name</em>]</td>
  </tr>
  <tr>
   <td>ユーザー名</td>
   <td>データベース表でのアクションを認証・実行するためのユーザー名</td>
  </tr>
  <tr>
   <td>パスワード</td>
   <td>ユーザー名に関連するパスワード</td>
  </tr>
  <tr>
   <td>トランザクションの分離</td>
   <td>READ_COMMITTED</td>
  </tr>
  <tr>
   <td>最大アクティブ接続数</td>
   <td>1000</td>
  </tr>
  <tr>
   <td>最大アイドル接続数</td>
   <td>100</td>
  </tr>
  <tr>
   <td>最小アイドル接続数</td>
   <td>10</td>
  </tr>
  <tr>
   <td>初期サイズ</td>
   <td>10</td>
  </tr>
  <tr>
   <td>最大待機時間</td>
   <td>100000</td>
  </tr>
  <tr>
   <td>Test on Borrow</td>
   <td>チェック</td>
  </tr>
  <tr>
   <td>Test while Idle</td>
   <td>チェック</td>
  </tr>
  <tr>
   <td>検証クエリ</td>
   <td>値の例：SELECT 1（mySQL）、select 1 from dual（Oracle）、SELECT 1（MS SQL Server）（validationQuery）</td>
  </tr>
  <tr>
   <td>検証クエリタイムアウト</td>
   <td>10000</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> * MySQL 向けの JDBC ドライバーは、サンプルでは提供されていません。これに対してのプロビジョニングを行い、JDBC 接続プールの設定に必要な情報を提供してください。
> * オーサーインスタンスとパブリッシュインスタンスで同じデータベースを使用するよう指定します。JDBC 接続の URI フィールドの値は、すべてのオーサーインスタンスとパブリッシュインスタンスで同じである必要があります。
   >


1. 他の設定はそのままにし、「**[!UICONTROL 保存]**」をクリックします。

1. データベーススキーマにすでにテーブルがある場合は、次のステップに進んでください。

   データベーススキーマにテーブルがまだない場合は、次の SQL ステートメントを実行し、データベーススキーマ内にデータ、メタデータ、および追加メタデータ用に別々のテーブルを作成します。

   >[!NOTE]
   >
   >オーサーインスタンスとパブリッシュインスタンスで異なるデータベースは必要はありません。すべてのオーサーインスタンスとパブリッシュインスタンスで同じデータベースを使用します。

   **データ表用の SQL ステートメント**

   ```sql
   CREATE TABLE `data` (
   `owner` varchar(255) DEFAULT NULL,
   `data` longblob,
   `metadataId` varchar(45) DEFAULT NULL,
   `id` varchar(45) NOT NULL,
   PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **メタデータ表用の SQL ステートメント**

   ```sql
   CREATE TABLE `metadata` (
   `formPath` varchar(1000) DEFAULT NULL,
   `formType` varchar(100) DEFAULT NULL,
   `description` text,
   `formName` varchar(255) DEFAULT NULL,
   `owner` varchar(255) DEFAULT NULL,
   `enableAnonymousSave` varchar(45) DEFAULT NULL,
   `renderPath` varchar(1000) DEFAULT NULL,
   `nodeType` varchar(45) DEFAULT NULL,
   `charset` varchar(45) DEFAULT NULL,
   `userdataID` varchar(45) DEFAULT NULL,
   `status` varchar(45) DEFAULT NULL,
   `formmodel` varchar(45) DEFAULT NULL,
   `markedForDeletion` varchar(45) DEFAULT NULL,
   `showDorClass` varchar(255) DEFAULT NULL,
   `sling:resourceType` varchar(1000) DEFAULT NULL,
   `attachmentList` longtext,
   `draftID` varchar(45) DEFAULT NULL,
   `submitID` varchar(45) DEFAULT NULL,
   `id` varchar(60) NOT NULL,
   `profile` varchar(255) DEFAULT NULL,
   `submitUrl` varchar(1000) DEFAULT NULL,
   `xdpRef` varchar(1000) DEFAULT NULL,
   `agreementId` varchar(255) DEFAULT NULL,
   `nextSigners` varchar(255) DEFAULT NULL,
   `eSignStatus` varchar(45) DEFAULT NULL,
   `pendingSignID` varchar(45) DEFAULT NULL,
   `agreementDataId` varchar(255) DEFAULT NULL,
   `enablePortalSubmit` varchar(45) DEFAULT NULL,
   `submitType` varchar(45) DEFAULT NULL,
   `dataType` varchar(45) DEFAULT NULL,
   `jcr:lastModified` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`id`),
   UNIQUE KEY `ID_UNIQUE` (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **追加メタデータテーブル用の SQL ステートメント**

   ```sql
   CREATE TABLE `additionalmetadatatable` (
   `value` text,
   `key` varchar(255) NOT NULL,
   `id` varchar(60) NOT NULL,
   PRIMARY KEY (`id`,`key`),
   CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **コメントテーブル用の SQL ステートメント**

   ```sql
   CREATE TABLE `commenttable` (
   `commentId` varchar(255) DEFAULT NULL,
   `comment` text DEFAULT NULL,
   `ID` varchar(255) DEFAULT NULL,
   `commentowner` varchar(255) DEFAULT NULL,
   `time` varchar(255) DEFAULT NULL);
   ```

1. データベーススキーマにテーブル（data、metadata、および additionalmetadatatable）がすでにある場合は、テーブルクエリーの後に次を実行します。

   **データテーブルを変更する SQL ステートメント**

   ```sql
   ALTER TABLE `data` CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **メタデータテーブルを変更する SQL ステートメント**

   ```sql
   ALTER TABLE metadata add markedForDeletion varchar(45) DEFAULT NULL
   ```

   >[!NOTE]
   >
   >ALTER TABLE metadata add クエリがすでに実行済みで、markedfordeletion 列がテーブルにある場合は、このクエリを実行すると失敗します。

   ```sql
   ALTER TABLE metadata add agreementId varchar(255) DEFAULT NULL,
   add nextSigners varchar(255) DEFAULT NULL,
   add eSignStatus varchar(45) DEFAULT NULL,
   add pendingSignID varchar(45) DEFAULT NULL,
   add agreementDataId varchar(255) DEFAULT NULL,
   add enablePortalSubmit varchar(45) DEFAULT NULL,
   add submitType varchar(45) DEFAULT NULL,
   add dataType varchar(45) DEFAULT NULL;
   ```

   ```sql
   ALTER TABLE `metadata` CHANGE `formPath` `formPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formType` `formType` VARCHAR(100) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `description` `description` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formName` `formName` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `renderPath` `renderPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `showDorClass` `showDorClass` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `sling:resourceType` `sling:resourceType` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `profile` `profile` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `submitUrl` `submitUrl` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `xdpRef` `xdpRef` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **additionalmetadatatable テーブルを変更する SQL ステートメント**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

データおよびメタデータをデータベースに保存しながら、ドラフトと送信をリスト表示するために使用できるサンプル実装が設定されました。サンプルでデータサービスとメタデータサービスがどのように設定されているか見てみましょう。

## mysql-connector-java-5.1.39-bin.jar ファイルをインストールする {#install-mysql-connector-java-bin-jar-file}

すべてのオーサーインスタンスとパブリッシュインスタンスで、次の手順を実行し、mysql-connector-java-5.1.39-bin.jar ファイルをインストールします。

1. `https://'[server]:[port]'/system/console/depfinder` にアクセスして com.mysql.jdbc パッケージを検索します。
1. 「次による書き出し」列で、パッケージがバンドルで書き出されているかどうかを確認します。

   パッケージがバンドルで書き出されていない場合は、先に進みます。

1. `https://'[server]:[port]'/system/console/bundles` に移動して「**[!UICONTROL Install/Update]**」をクリックします。
1. 「**[!UICONTROL ファイルを選択]**」をクリックし、mysql-connector-java-5.1.39-bin.jar を探して選択します。また、「**[!UICONTROL Start Bundle]**」チェックボックスと「**[!UICONTROL Refresh Packages]**」チェックボックスを選択します。
1. 「**[!UICONTROL Install」または「Update]**」をクリックします。完了したら、サーバーを再起動します。
1. （*Windows のみ*）オペレーティングシステムのシステムファイアウォールをオフにします。

## フォームポータルデータおよびメタデータサービスのサンプルコード {#sample-code-for-forms-portal-data-and-metadata-service}

次の zip ファイルには、データおよびメタデータサービスインターフェイスの `FormsPortalSampleDataServiceImpl` および `FormsPortalSampleMetadataServiceImpl`（実装クラス）が含まれます。また、上記で述べた実装クラスのコンパイルに必要なすべてのクラスが含まれます。

[ファイルを入手](assets/sample_package.zip)

## ファイル名の長さの検証  {#verify-length-of-the-file-name}

フォームポータルのデータベース実装では、追加のメタデータテーブルを使用します。このテーブルには、テーブルのキーと ID 列に基づいた複合プライマリキーが含まれます。MySQL を使用すれば、プライマリキーの長さを最大 255 文字にすることができます。次のクライアントサイドの検証スクリプトを使用して、ファイルウィジェットに添付されたファイル名の長さを検証できます。この検証は、ファイルが添付されているときに実行されます。次の手順で提供されているスクリプトでは、ファイル名が拡張子を含めて 150 文字を超えるとメッセージが表示されます。スクリプトを変更して、異なる文字数でチェックできます。

次の手順を実行して[クライアントライブラリ](/help/sites-developing/clientlibs.md)を作成し、次のスクリプトを使用します。

1. CRXDE にログインし、/etc/clientlibs/ に移動します。
1. **cq:ClientLibraryFolder** タイプのノードを作成して、ノードの名前を入力します。（例：`validation`）。

   「**[!UICONTROL すべて保存]**」をクリックします。

1. ノードを右クリックして「**[!UICONTROL 新しいファイルを作成]**」をクリックし、.txt の拡張子を付けてファイルを作成します。例えば、`js.txt` です。新しく作成した .txt ファイルに次のコードを追加して、「**[!UICONTROL すべて保存]**」をクリックします。

   ```javascript
   #base=util
    util.js
   ```

   上記コードの場合、`util` はフォルダーの名前で、`util.js` フォルダーにあるファイルの `util` 名です。`util` フォルダーと `util.js` ファイルはこの後に続く手順で作成されます。

1. 手順 2 で作成した `cq:ClientLibraryFolder` ノードを右クリックし、「作成／フォルダーの作成」を選択します。`util` という名前のフォルダーを作成します。「**[!UICONTROL すべて保存]**」をクリックします。`util` フォルダーを右クリックし、「作成／ファイルを作成」を選択します。`util.js` という名前のファイルを作成します。「**[!UICONTROL すべて保存]**」をクリックします。

1. util.js ファイルに次のコードを追加して、「**[!UICONTROL すべて保存]**」をクリックします。このコードでファイル名の長さを検証します。

   ```javascript
   /*
    * ADOBE CONFIDENTIAL
    * ___________________
    *
    * Copyright 2016 Adobe Systems Incorporated
    * All Rights Reserved.
    *
    * NOTICE:  All information contained herein is, and remains
    * the property of Adobe Systems Incorporated and its suppliers,
    * if any.  The intellectual and technical concepts contained
    * herein are proprietary to Adobe Systems Incorporated and its
    * suppliers and may be covered by U.S. and Foreign Patents,
    * patents in process, and are protected by trade secret or copyright law.
    * Dissemination of this information or reproduction of this material
    * is strictly forbidden unless prior written permission is obtained
    * from Adobe Systems Incorporated.
    *
    */
   (function () {
       var connectWithGuideBridge = function (gb) {
           gb.connect(function () {
               //For first time load
               window.guideBridge.on("elementValueChanged" , function(event, payload) {
           var component = payload.target; // Field whose value has changed
                   if(component.name == 'fileAttachment' && component.parent) {
                       var fileItems = $('#'+payload.target.parent.id).find(".guide-fu-fileItem");
                       for (i = 0;i<fileItems.length;i++) {
                           var filename = $(fileItems[i]).find(".guide-fu-fileName").text();
                           //check whether it is previously attached file or a newly  attached one
                           if(filename.length > 150 && filename.indexOf("fp.attach.jsp") < 0) {
                               window.alert("filename is larger than 150 : "+filename);
                                $(fileItems[i]).find(".guide-fu-fileClose.close").click();
                           }
                       }
                   }
   
      });
           });
       };
   
       if (window.guideBridge) {
           connectWithGuideBridge(window.guideBridge);
       } else {
           window.addEventListener("bridgeInitializeStart", function (event) {
               connectWithGuideBridge(event.detail.guideBridge);
           });
       }
   })();
   ```

   >[!NOTE]
   >
   >スクリプトは、初期設定済み（OOTB）の添付ウィジェットコンポーネントです。カスタマイズした OOTB 添付ウィジェットがある場合は、上記のスクリプトを変更して個々の変更を組み込みます。

1. 次のプロパティを手順 2 で作成したフォルダーに追加し、「**[!UICONTROL すべて保存]**」をクリックします。

   * **[!UICONTROL 名前：]** categories

   * **[!UICONTROL タイプ：]** String

   * **[!UICONTROL 値：]** fp.validation

   * **[!UICONTROL マルチオプション：]** Enabled

1. `/libs/fd/af/runtime/clientlibs/guideRuntime` に移動し、`fp.validation` 値を embed プロパティに追加します。

1. /libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA に移動し、`fp.validation` 値を embed プロパティに追加します。

   >[!NOTE]
   >
   >guideRuntime および guideRuntimeWithXfa クライアントライブラリの代わりにカスタムクライアントライブラリを使用している場合、カテゴリ名を使用してこの手順で作成したクライアントライブラリを、実行時にロードしたカスタムライブラリに埋め込みます。

1. 「**[!UICONTROL すべて保存」をクリックします。]** ここで、ファイル名が拡張子を含めて 150 文字を超えるとメッセージが表示されます。
