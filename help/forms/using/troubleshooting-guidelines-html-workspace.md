---
title: AEM Forms Workspace のトラブルシューティングガイドライン
seo-title: Troubleshooting guidelines for AEM Forms workspace
description: ログを有効にし、ブラウザーで Debugger を使用してAEM Forms Workspace のトラブルシューティングをおこなう。
seo-description: Enable logs and use debugger in browser to troubleshoot AEM Forms workspace.
uuid: 07b8c8ed-f1ff-4be5-8005-251ff7b2ac85
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 5dae9ed9-77a3-44f5-a94d-ca5c355c8730
exl-id: a054b60a-5e89-4c98-87bc-35669988d160
source-git-commit: d3923e5e693e7426ee57e81e203f31964a23af3a
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 19%

---

# AEM Forms Workspace のトラブルシューティングガイドライン {#troubleshooting-guidelines-for-aem-forms-workspace}

この記事では、ログを有効にし、ブラウザーで debugger を使用してAEM Forms Workspace をデバッグする方法について説明します。 また、AEM Forms Workspace とその回避策を使用する際に発生する可能性のある一般的な問題についても説明します。

## AEM Forms Workspace パッケージをインストールできません {#unable-to-install-aem-forms-workspace-package}

パッチをインストールしたら、AEM Forms Workspace を開きます。 「リソースが見つかりません」というエラーが発生した場合は、CRX Package Manager を開いて、`adobe-lc-workspace-pkg-<version>.zip` パッケージを再インストールします。

パッケージをインストールするときに、「`javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`」というエラーが発生した場合は、次の手順を実行します。

1. CRXDE Lite にログインします。
デフォルトの URL は、`https://[localhost]:'port'/lc/crx/de/index.jsp` です。
1. 次のノードを削除します。

   `/home/groups/P/PERM_WORKSPACE_USER`

1. Package Manager に移動します。デフォルトの URL は、`https://[localhost]:'port'/lc/crx/packmgr/index.jsp.` です。
1. `adobe-lc-workspace-pkg-[version].zip` パッケージを検索してインストールします。
1. アプリケーションサーバーを再起動します。

## AEM Forms workspace ログ {#aem-forms-workspace-nbsp-logging}

様々なレベルでログを生成し、エラーの最適なトラブルシューティングを可能にします。 例えば、複雑なアプリケーションでは、コンポーネントレベルでログを記録すると、特定のコンポーネントのデバッグとトラブルシューティングに役立ちます。

AEM Forms Workspace の場合：

* 特定のコンポーネントファイルについてのログ情報を取得するには、URL に `/log/<ComponentFile>/<LogLevel>` を付け加えて `Enter` キーを押します。特定のログレベルにおけるコンポーネントファイルのすべてのログ情報は、コンソールに印刷されます。

* すべてのコンポーネントファイルについてのログ情報を取得するには、URL に `/log/all/trace` を付け加えて `Enter` キーを押します。

* ログ形式：`<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>デフォルトでは、すべてのコンポーネントのログレベルは「情報」(INFO) に設定されています。

* ユーザーが設定したログレベルは、そのブラウザーセッションでのみ維持されます。 ユーザーがページを更新すると、すべてのコンポーネントのログレベルが初期値に設定されます。

### AEM Forms Workspace のコンポーネントファイルのリスト {#list-of-component-files-in-nbsp-aem-forms-workspace}

<table>
 <tbody>
  <tr>
   <td><p>allcategoryModel</p> </td>
   <td><p>processinstanceModel</p> </td>
   <td><p>tasklistModel</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationModel</p> </td>
   <td><p>processInstanceView</p> </td>
   <td><p>tasklistView</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationView</p> </td>
   <td><p>processnamelistModel</p> </td>
   <td><p>taskModel</p> </td>
  </tr>
  <tr>
   <td><p>categorylistModel</p> </td>
   <td><p>processnamelistView</p> </td>
   <td><p>taskView</p> </td>
  </tr>
  <tr>
   <td><p>categorylistView</p> </td>
   <td><p>processnameModel</p> </td>
   <td><p>teamqueuesView</p> </td>
  </tr>
  <tr>
   <td><p>categoryModel</p> </td>
   <td><p>processnameView</p> </td>
   <td><p>todoView</p> </td>
  </tr>
  <tr>
   <td><p>categoryView</p> </td>
   <td><p>searchtemplatedetailsView</p> </td>
   <td><p>trackingView</p> </td>
  </tr>
  <tr>
   <td><p>favoritecategoryModel</p> </td>
   <td><p>sharequeueModel</p> </td>
   <td><p>uisettingsModel</p> </td>
  </tr>
  <tr>
   <td><p>filterlistView</p> </td>
   <td><p>sharequeueView</p> </td>
   <td><p>uisettingsView</p> </td>
  </tr>
  <tr>
   <td><p>filterView</p> </td>
   <td><p>startpointlistModel</p> </td>
   <td><p>userinfoModel</p> </td>
  </tr>
  <tr>
   <td><p>outofofficeModel</p> </td>
   <td><p>startpointlistView</p> </td>
   <td><p>userinfoView</p> </td>
  </tr>
  <tr>
   <td><p>outofofficeView</p> </td>
   <td><p>startpointModel</p> </td>
   <td><p>usersearchModel</p> </td>
  </tr>
  <tr>
   <td><p>preferencesView</p> </td>
   <td><p>startpointView</p> </td>
   <td><p>usersearchView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancehistoryView</p> </td>
   <td><p>startProcessView</p> </td>
   <td><p>wserrorModel</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistModel</p> </td>
   <td><p>startprocessView</p> </td>
   <td><p>wserrorView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistView</p> </td>
   <td><p>taskdetailsView</p> </td>
   <td><p>wsmessageView</p> </td>
  </tr>
 </tbody>
</table>

### AEM Forms Workspace で使用可能なログレベル {#log-levels-available-in-nbsp-aem-forms-workspace}

* 致命的
* ERROR
* WARN
* INFO
* DEBUG
* TRACE
* OFF

## ブラウザーのデバッグ情報 {#debugging-information-for-browsers}

スクリプトとスタイルは、異なるブラウザーでデバッグできます。

* **IE でのデバッグ**:IE でAEM Forms Workspace をデバッグするには、以下を参照してください。 [https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie](https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie).

* **Chrome でのデバッグ**:Chrome でデバッガーを開くには、次のショートカットを使用します。Ctrl + Shift + I。詳しくは、以下を参照してください。 [https://developer.chrome.com/docs/extensions/mv3/tut_debugging/](https://developer.chrome.com/docs/extensions/mv3/tut_debugging/).

* **Firefox でのデバッグ**：複数のアドオンを Firefox でスクリプトおよびスタイルのデバッグに使用することができます。例えば、Firebug はデバッグユーティリティの 1 つです（[https://getfirebug.com](https://getfirebug.com)）。

## FAQ {#faqs}

1. PDFフォームがGoogle Chrome でレンダリングまたは送信されません。

   1. Adobe®Reader®プラグインをインストールします。
   1. Chrome で、chrome://pluginsを開いて使用可能なプラグインを表示します。
   1. ChromePDFビューアプラグインを無効にし、Adobe Readerプラグインを有効にします。

1. SWFフォームまたはガイドがGoogle Chrome でレンダリングされません。

   1. Chrome で、chrome://pluginsを開いて使用可能なプラグインを表示します。
   1. AdobeFlash® Player プラグインの詳細を参照してください。
   1. AdobeFlash Playerプラグインの PepperFlash を無効にします。

1. AEM Forms Workspace をカスタマイズしましたが、変更が表示されません。

   ブラウザーのキャッシュをクリアして、AEM Forms Workspace にアクセスします。

1. デスクトップで開いたときにフォームをHTMLでレンダリングできるようにするには、ユーザーは何をおこなう必要がありますか？

   Workbench の使用中に、タスクの割り当て手順でデフォルトプロファイルのHTMLラジオボタンを選択します。

1. 添付ファイルをクリックしても表示されません。

   添付ファイルを表示するには、ブラウザーでポップアップを有効にします。

1. ユーザーが Forms アプリケーションにログインしている。 ユーザーが Workspace にログインしようとすると、Workspace 権限を持たない場合は、読み込まれない可能性があります。

   他の Forms アプリケーションからログアウトし、Workspace にログインします。

1. HTMLフォームは、デザインでプロセスプロパティを使用し、AEM Forms Workspace でレンダリングされると、フォーム内に「送信」ボタンを表示します。

   フォームをデザインする際に、プロセスのプロパティを使用すると、フォーム内に「送信」ボタンが追加されます。 AEM Forms Workspace でPDFとしてレンダリングされた場合、送信ボタンはエンドユーザーには表示されません。 ただし、AEM Forms Workspace でHTMLフォームとしてレンダリングする場合は、エンドユーザーに「送信」ボタンが表示されます。 フォーム内でこの「送信」ボタンをクリックしても、アクションは開始されません。 AEM Formsワークスペースの下部（フォームの外側）にある「送信」ボタンをクリックすると、タスクが完了します。
