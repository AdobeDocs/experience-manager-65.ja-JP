---
title: ドラフトと送信コンポーネントとデータベースの統合のサンプル
seo-title: ドラフトと送信コンポーネントとデータベースの統合のサンプル
description: ドラフトと送信コンポーネントをデータベースに統合するためのカスタマイズされたデータサービスおよびメタデータサービスのリファレンス実装
seo-description: ドラフトと送信コンポーネントをデータベースに統合するためのカスタマイズされたデータサービスおよびメタデータサービスのリファレンス実装
uuid: ccdb900e-2c2e-4ed3-8a88-5c97aa0092a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: da96d3d8-a338-470a-8d20-55ea39bd15bf
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# ドラフトと送信コンポーネントとデータベースの統合のサンプル {#sample-for-integrating-drafts-submissions-component-with-database}

## サンプルｎ概要 {#sample-overview}

AEM Forms ポータルのドラフトと送信コンポーネントにより、フォームをドラフトとして保存し、任意のデバイスから後で送信することができます。また、ポータルにて送信済みのフォームを表示することもできます。この機能を有効にするため、AEM Forms では、ユーザーによってフォームに入力されたデータおよびドラフトおよび送信済みフォームに関連するメタデータを保存する、データおよびメタデータサービスを提供しています。このデータは、デフォルトで CRX レポジトリに格納されます。ただし、ユーザーが AEM のパブリッシュインスタンスを通じてフォームとやり取りを行うのは通常企業のファイアウォールの外側であるため、組織によっては、よりセキュアで信頼性のあるデータストレージが必要となる場合もあります。

このドキュメントで取り上げるサンプルは、ドラフト&amp;送信コンポーネントをデータベースに統合するためのカスタマイズされたデータサービスおよびメタデータサービスのリファレンス実装です。サンプル実装で使用されているデータベースは **MySQL 5.6.24** ですが、ドラフト&amp;送信コンポーネントは、あらゆるデータベースに統合することができます。

>[!NOTE]
>
>* このドキュメントで説明されている例および設定は、MySQL 5.6.24 に基づいているため、お使いのデータベースシステムに合わせてそれらを適切に置き換える必要があります。
>* 最新バージョンの AEM Forms のアドオンパッケージをインストールしていることを確認してください。使用可能なパッケージのリストについては、[AEM Forms リリース](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)の記事を参照してください。
>



## サンプルのセットアップおよび設定 {#set-up-and-configure-the-sample}

すべての作成者インスタンスと発行インスタンスで次の手順を実行し、サンプルをインストールして設定します。

1. パッケージ **aem-fp-db-integration-sample-pkg-6.1.2.zip** をファイルシステムにダウンロードします。

   データベース統合のサンプルパッケージ

   [ファイルを入手](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. Go to AEM package manager at https://[*host*]:[*port*]/crx/packmgr/.
1. 「**[!UICONTROL パッケージをアップロード]**」をクリックします。

1. パッケージ **aem-fp-db-integration-sample-pkg-6.1.2.zip** を参照して選択し、「**[!UICONTROL OK]**」をクリックします。
1. パッケージの隣にある「**[!UICONTROL インストール]**」をクリックし、パッケージをインストールします。
1. **[!UICONTROL AEM Web Console Configuration]**&#x200B;ページ(https://[*host*]:[*port*]/system/console/configMgr)に移動します。
1. **[!UICONTROL Forms Portal Draft and Submission Configuration]** をクリックし、編集モードで開きます。

1. 次の表の説明に従って、プロパティの値を指定します。

   | **プロパティ** | **説明** | **値** |
   |---|---|---|
   | フォームポータル ドラフトデータサービス | ドラフトデータサービスの識別子 | formsportal.sampledataservice |
   | フォームポータル ドラフトメタデータサービス | ドラフトメタデータサービス の識別子 | formsportal.samplemetadataservice |
   | フォームポータル 送信データサービス | 送信データサービス の識別子 | formsportal.sampledataservice |
   | フォームポータル 送信メタデータサービス | 送信メタデータサービス の識別子 | formsportal.samplemetadataservice |
   | フォームポータル 保留中署名データサービス | 保留中の署名データサービスの識別子 | formsportal.sampledataservice |
   | フォームポータル 保留中署名メタデータサービス | 保留中の署名メタデータサービスの識別子 | formsportal.samplemetadataservice |

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
   **注意**:テーブル名を変更する場合は、フォームポータル設定で指定します。

1. 他の設定はそのままにし、「**[!UICONTROL 保存]**」をクリックします。

1. データベース接続は、Apache Sling接続プールされたデータソースを介して行うことができます。
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
   <td>jdbc:mysql://[<em>ホスト</em>]:[<em>ポート</em>]/[<em>スキーマ名</em>]</td>
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

## mysql-connector-java-5.1.39-bin.jar ファイルのインストール {#install-mysql-connector-java-bin-jar-file}

すべてのオーサーインスタンスとパブリッシュインスタンスで、次の手順を実行し、mysql-connector-java-5.1.39-bin.jar ファイルをインストールします。

1. com.mysql.jdbc `https://'[server]:[port]'/system/console/depfinder` パッケージに移動し、検索します。
1. 「次による書き出し」列で、パッケージがバンドルで書き出されているかどうかを確認します。

   パッケージがバンドルで書き出されていない場合は、先に進みます。

1. に移動し、「イン `https://'[server]:[port]'/system/console/bundles` ストール/更 **[!UICONTROL 新」をクリックしま]**&#x200B;す。
1. Click **[!UICONTROL Choose File]** and browse to select the mysql-connector-java-5.1.39-bin.jar file. Also, select **[!UICONTROL Start Bundle]** and **[!UICONTROL Refresh Packages]** checkboxes.
1. Click **[!UICONTROL Install or Update]**. 完了したら、サーバーを再起動します。
1. (*Windows only*) Turn off the system firewall for your operating system.

## フォームポータルデータおよびメタデータサービスのサンプルコード {#sample-code-for-forms-portal-data-and-metadata-service}

次の zip ファイルには、データおよびメタデータサービスインターフェイスの `FormsPortalSampleDataServiceImpl` および `FormsPortalSampleMetadataServiceImpl`（実装クラス）が含まれます。また、上記で述べた実装クラスのコンパイルに必要なすべてのクラスが含まれます。

[ファイルを入手](assets/sample_package.zip)

## ファイル名の長さの検証  {#verify-length-of-the-file-name}

フォームポータルのデータベース実装では、追加のメタデータテーブルを使用します。このテーブルには、テーブルのキーと ID 列に基づいた複合プライマリキーが含まれます。MySQL を使用すれば、プライマリキーの長さを最大 255 文字にすることができます。次のクライアントサイドの検証スクリプトを使用して、ファイルウィジェットに添付されたファイル名の長さを検証できます。この検証は、ファイルが添付されているときに実行されます。次の手順で提供されているスクリプトでは、ファイル名が拡張子を含めて 150 文字を超えるとメッセージが表示されます。スクリプトを変更して、異なる文字数でチェックできます。

次の手順を実行して[クライアントライブラリ](/help/sites-developing/clientlibs.md)を作成し、次のスクリプトを使用します。

1. CRXDE にログインし、/etc/clientlibs/ に移動します。
1. **cq:ClientLibraryFolder** タイプのノードを作成して、ノードの名前を入力します。例えば、次のように入力します。`validation`

   「**[!UICONTROL すべて保存]**」をクリックします。

1. ノードを右クリックして「**[!UICONTROL 新しいファイルを作成]**」をクリックし、.txt の拡張子を付けてファイルを作成します。例えば、`js.txt` です。新しく作成した .txt ファイルに次のコードを追加して、「**[!UICONTROL すべて保存]**」をクリックします。

   ```
   #base=util
    util.js
   ```

   上記コードの場合、`util` はフォルダーの名前で、`util.js` フォルダーにあるファイルの `util` 名です。The `util` folder and `util.js` file are created in suceeeding steps.

1. 手順 2 で作成した `cq:ClientLibraryFolder` ノードを右クリックし、「作成／フォルダーの作成」を選択します。Create a folder named `util`. 「**[!UICONTROL すべて保存]**」をクリックします。`util` フォルダーを右クリックし、「作成／ファイルを作成」を選択します。Create a file named `util.js`. 「**[!UICONTROL すべて保存]**」をクリックします。

1. util.js ファイルに次のコードを追加して、「**[!UICONTROL すべて保存]**」をクリックします。ファイル名の検証長のコード。

   ```
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

1. Navigate to `/libs/fd/af/runtime/clientlibs/guideRuntime`and append the `fp.validation` value to the embed property.

1. Navigate to /libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA and append the `fp.validation` value to embed property.

   >[!NOTE]
   >
   >guideRuntimeおよびguideRuntimeWithXfaクライアントライブラリの代わりにカスタムクライアントライブラリを使用する場合は、カテゴリ名を使用して、この手順で作成したクライアントライブラリを実行時に読み込むカスタムライブラリに埋め込みます。

1. 「**[!UICONTROL すべて保存」をクリックします。]** 現在は、ファイル名が150文字（拡張子を含む）を超える場合、メッセージが表示されます。

