---
title: システム情報サービス API
seo-title: システム情報サービス API
description: このドキュメントは、システムシステムシステムが提供するAPIに関する詳細な情報を提供します。情報サービス
seo-description: このドキュメントは、システムシステムシステムが提供するAPIに関する詳細な情報を提供します。情報サービス
uuid: 7f624216-56e6-4d49-b9a1-3c9af045dabe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79fccce2-d090-4b50-9c58-3f2a00e651b2
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# システム情報サービス API {#system-information-service-apis}

システム情報サービスは情報取得のために REST API のセットを提供します。次のテーブルは API に関する詳細を提供します。

<table>
 <thead>
  <tr>
   <th><p>名前</p></th>
   <th><p>URL</p></th>
   <th><p>説明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>SystemInfo.properties</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.properties'</p></td>
   <td><p>この API は <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">system.getProperties</a> Java API のラッパーです。それは現在の作業環境の設定を取得します。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[サーバー]:[ポート]'/rest/services/ SystemInfo.envVar</p></td>
   <td><p>ホストのオペレーティングシステムにおけるすべての環境変数を取得します。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[サーバー]:[ポート]'/rest/services/ SystemInfo.logs</p></td>
   <td><p>アプリケーションのサーバーログを含む zip ファイルをダウンロードします。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[サーバー]:[ポート]'/rest/services/ SystemInfo.config</p></td>
   <td><p>config.xml ファイルのすべてのコンテンツを取得します。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://'[サーバー]:[ポート]'/rest/services/ SystemInfo.services</p></td>
   <td><p>AEM Forms サービスのステータスと設定パラメーターを取得します。</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[サーバー]:[ポート]'/rest/services/ SystemInfo.vitalDetails</p></td>
   <td><p>サーバー稼働時間、JVM 引数、システムメモリ、ヒープサイズ、オペレーティングシステム名、アクティブなスレッド数、およびスレッド数を取得します。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://'[サーバー]:[ポート]'/rest/services/ SystemInfo.coreSettings</p></td>
   <td><p>次のプロパティの値を取得します。</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>CustomerFontDir</p></li>
     <li><p>GlobalDocumentStorageRootDir</p></li>
     <li><p>DefaultDocumentMaxInlineSize</p></li>
     <li><p>DefaultDocumentDisposalTimeout</p></li>
     <li><p>EnableDocumentDBStorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>EnableFIPS</p></li>
     <li><p>EnableWSDL</p></li>
     <li><p>DataServicesConfigFile </p></li>
     <li><p>EnableRDS</p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.database</p></td>
   <td><p>https://'[サーバー]:[ポート]'/rest/services/ SystemInfo.database</p></td>
   <td><p>データベースに関する詳細を取得します。</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td>
   <td><p>https://'[サーバー]:[ポート]'/rest/services/ SystemInfo.licenseInfo</p></td>
   <td><p>インストールされている AEM Forms コンポーネントのバージョンとライセンス情報を取得します。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[サーバー]:[ポート]'/rest/services/ SystemInfo.serverConfig</p></td>
   <td><p>ホストのアプリケーションサーバーの設定ファイルをダウンロードします。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://'[サーバー]:[ポート]'/rest/services/ SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>アクティブなスレッドの数とスタックトレースを取得します。次のパラメーターを受け取ります。</p>
    <ul>
     <li><p>iterations= [n]: 繰り返し回数を指定します。n を数字と置き換えます。 </p></li>
     <li><p>Delay= [n]: 次の回数を始める前に待機するミリ秒の数値を指定します。 </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[サーバー]:[ポート]'/rest/services/ SystemInfo.info</p></td>
   <td><p>この API はすべてのシステム情報サービス API のラッパーです。内部的に、それはすべてのシステム情報 API を実行し、情報を zip 形式でダウンロードします。 </p><p><i><strong>注意</strong>：SystemInfo.info はアクティブなスレッドの数とスタックトレースを提供しません。 </i></p></td>
  </tr>
 </tbody>
</table>

