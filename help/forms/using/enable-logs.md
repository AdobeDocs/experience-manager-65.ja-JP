---
title: HTML5 フォーム内でのログの有効化
seo-title: HTML5 フォーム内でのログの有効化
description: ロガーユーティリティはフォームのログを可能にし、フォーム関連の問題のデバッグに役立ちます。
seo-description: ロガーユーティリティはフォームのログを可能にし、フォーム関連の問題のデバッグに役立ちます。
uuid: 322306ba-8ad7-463d-8a9d-4cea5a0c4b55
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 973806f8-fb44-4d52-ad3f-bfbf335f60a1
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 70%

---


# HTML5フォーム内でのログの有効化{#enable-logging-for-html-forms}

ロガーユーティリティを設定することで、HTML5フォームでログの作成を開始することができます。ロガーユーティリティにはいくつかのレベルがあり、要件に応じてレベルを設定することができます。HTML5フォームは、サーバーコンポーネントとクライアントコンポーネントから構成されています。両方のコンポーネントに対してログを設定できます。 

## サーバー側のログの設定 {#configuring-server-side-logging}

次の手順を実行して、サーバーサイドログを構成します。

1. `https://'[server]:[port]'/system/console/configMgr` にアクセスします。*Apace Slingロギングロガー設定*&#x200B;オプションを探して開きます。 ダイアログボックスが表示されます。

   ![ Apace Sling ロギングのロガー設定オプションのダイアログボックス](assets/logconfig.png)

   Apace Sling ロギングロガー設定オプション

1. **ログレベル**&#x200B;を&#x200B;**デバッグ**&#x200B;に変更します。 

1. **ログファイル**&#x200B;の名前とパスを指定します。

   >[!NOTE]
   >
   >HTML5 フォームログディレクトリ内にログを生成する場合は、ファイル名の前に ../logs/ を追加します。

1. **Logger**&#x200B;を&#x200B;**HTMLFormsPerfLogger**&#x200B;に変更します。 「**保存**」をクリックします。

## クライアントロギングの設定 {#configuring-client-logging}

次の方法により、HTML5 フォームのクライアント側のロギングを有効にできます。

* `log` という名前の要求パラメーターの使用
* CQ Configuration Manager の使用

### 要求パラメーターの使用によるログの有効化  {#enabling-logging-using-request-parameter}

この方法を使用して、特定の要求に対するログを生成できます。リクエストパラメータの名前は&#39;logです。 ログURLは次のとおりです。

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

ログの設定はログレベルとロガーカテゴリで構成されています。

#### ログの宛先 {#log-destination}

<table>
 <tbody>
  <tr>
   <th><strong>ログの宛先</strong></th>
   <th><strong>説明</strong></th>
  </tr>
  <tr>
   <td>1</td>
   <td>ログはブラウザーの<strong>コンソール</strong>に送信されます。</td>
  </tr>
  <tr>
   <td>2</td>
   <td>ログはクライアント側の JavaScript オブジェクトに収集され、<strong>サーバー</strong>にポストできます。 </td>
  </tr>
  <tr>
   <td>3</td>
   <td>両方の上記のオプション<br /> </td>
  </tr>
 </tbody>
</table>

#### ログのレベル {#log-levels}

<table>
 <tbody>
  <tr>
   <th>ログレベル</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>0</td>
   <td>OFF<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>FATAL<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>2</td>
   <td>ERROR<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>WARN<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>4</td>
   <td>INFO<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>5</td>
   <td>DEBUG<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>6</td>
   <td>TRACE<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>7</td>
   <td>ALL<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### ロガーカテゴリ  {#logger-categories}

<table>
 <tbody>
  <tr>
   <th>ログカテゴリ</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>がない場合、</td>
   <td>xfa （スクリプティングエンジン関連ログ）</td>
  </tr>
  <tr>
   <td>b</td>
   <td>xfaView （レイアウトエンジン関連ログ）<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>c</td>
   <td>xfaPerf （パフォーマンス関連ログ）<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### ログの設定 {#log-configuration}

ログ URL では、ログ設定クエリーの文字列パラメーターは次のとおりに定義します。

`{destination}-{a level}-{b level}-{c level}`

次に例を示します。

<table>
 <tbody>
  <tr>
   <th>ログの設定</th>
   <th>詳細</th>
  </tr>
  <tr>
   <td>2-a4-b5-c6<br type="_moz" /> </td>
   <td>保存場所：Server<br /> xfa レベル：INFO<br /> xfaView レベル：DEBUG<br /> xfaPerf レベル： TRACE</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>a（xfa）、b（xfaView）、および c（xfaPerf）のそれぞれのログカテゴリに対するデフォルトログレベルは 2（エラー）です。そのため、ログ設定 2-b6 では、異なるカテゴリのログレベルは：
>a (xfa):2（デフォルトのレベルERROR）
>b (xfaView):6(ユーザー指定TRACE)
>a (xfaPerf):2（デフォルトのレベルERROR）

### Configuration Manager の使用によるログの有効化 {#enabling-logging-using-configuration-manager}

ログを有効にするためにConfiguration Managerを使用する場合、ログが再び無効になるまで、すべてのレンダリング要求に対してログが生成されます。

1. `https://'[server]:[port]'/system/console/configMgr`でCQ Configuration Managerにログインし、管理者の資格情報を使用してログインします。
1. **「LC Forms Configurations」**&#x200B;を探してクリックします。
1. 「Debug Options」テキストボックスで、前のセクションで説明されたとおりにログ設定を入力します。例：**2-a4-b5-c6**

   ![Forms 設定](assets/forms_configuration.png)

   Forms 設定

## ログのアップロード {#uploading-logs}

宛先が 1 として設定されている場合、すべてのクライアントスクリプトのログメッセージはコンソールに送信されます。管理者がサーバーログと共にこれらのログを必要とする場合は、宛先レベルを2に設定します。 このレベルでは、すべてのログがクライアント側のJSオブジェクトに収集され、フォームがデフォルトのプロファイルでレンダリングされる場合、ツールバーの「**既存のフィールドをハイライト**」ボタンの左に「**ログを送信**」ボタンが表示されます。 ユーザーがリンクをクリックすると、収集されたすべてのログがサーバーに投稿され、サーバー上の設定済みのエラーログファイルに記録されます。

デフォルトでは、すべての情報が /crx-repository/logs/ ディレクトリに保存されている error.log ファイルに追加されます。

ログファイルの場所と名前を変更するには、次の操作を実行します。

1. 管理者として「Configuration Manager」にログインします。Configuration ManagerのデフォルトURLは`https://'[server]:[port]'/system/console/configMgr`です。
1. **「Apace Sling ロギングロガー設定」**&#x200B;をクリックします。ダイアログボックスが表示されます。

   ![logconfig-1](assets/logconfig-1.png)

1. **ログレベル**&#x200B;をデバッグに変更します。 

1. **ログファイル**&#x200B;のパスと名前を指定します。

   >[!NOTE]
   >
   >他のログファイルが保存されている同じディレクトリにログを作成するには、Log Files プロパティで ../logs/&lt;filename> を指定します。

1. **Logger**&#x200B;を&#x200B;**HTMLFormsPerfLogger**&#x200B;に変更し、**「保存**」をクリックします。
