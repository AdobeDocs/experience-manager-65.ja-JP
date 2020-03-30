---
title: AEM Forms Workspace のトラブルシューティングガイドライン
seo-title: AEM Forms Workspace のトラブルシューティングガイドライン
description: ログを有効にし、ブラウザーでデバッガーを使用して AEM Forms Workspace をトラブルシューティングします。
seo-description: ログを有効にし、ブラウザーでデバッガーを使用して AEM Forms Workspace をトラブルシューティングします。
uuid: 07b8c8ed-f1ff-4be5-8005-251ff7b2ac85
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 5dae9ed9-77a3-44f5-a94d-ca5c355c8730
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# AEM Forms Workspace のトラブルシューティングガイドライン {#troubleshooting-guidelines-for-aem-forms-workspace}

この記事では、ログを有効にしてブラウザーでデバッガーを使用することによって、AEM Forms Workspace をデバッグする方法について説明します。また、AEM Forms Workspace および回避策を使用する場合に直面する共通の問題についても説明します。

## AEM Forms Workspace パッケージをインストールできない {#unable-to-install-aem-forms-workspace-package}

パッチをインストールした後、AEM Forms Workspace を開きます。If you encounter the No Resource Found error, open the CRX Package Manager, and reinstalling the `adobe-lc-workspace-pkg-<version>.zip` package.

While installling the package, if you encounter an error `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`, perform the following steps:

1. CRX DE Lite にログインします。The default url is `https://[localhost]:'port'/lc/crx/de/index.jsp`
1. 次のノードを削除します。

   `/home/groups/P/PERM_WORKSPACE_USER`

1. Package Manager に移動します。The default URL is `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. Search and install the `adobe-lc-workspace-pkg-[version].zip` package.
1. アプリケーションサーバーを再起動します。

## AEM Forms Workspace のログ {#aem-forms-workspace-nbsp-logging}

様々なレベルでログを生成することにより、エラーの最適なトラブルシューティングを行うことができます。たとえば、複合アプリケーションでは、コンポーネントレベルでログすると、特定のコンポーネントのデバッグおよびトラブルシューティングに役立ちます。

AEM Forms Workspace では次の操作が可能です。

* To get the logging information about a specific component file, append `/log/<ComponentFile>/<LogLevel>` in the URL, and press `Enter`. 特定のログレベルにおけるコンポーネントファイルのすべてのログ情報は、コンソールに印刷されます。

* To get logging information of all component files, append `/log/all/trace` in the URL, and press `Enter`.

* Log format: `<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>デフォルトでは、すべてのコンポーネントのログレベルは INFO に設定されます。

* ユーザーによって設定されたログレベルは、そのブラウザーセッションでのみ保持されます。ユーザーがページを更新すると、ログレベルはすべてのコンポーネントに対してその初期値に設定されます。

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

### AEM Forms Workspaceアプリで使用可能なログレベル {#log-levels-available-in-nbsp-aem-forms-workspace}

* FATAL
* ERROR
* WARN
* INFO
* DEBUG
* TRACE
* OFF

## ブラウザーへの情報のデバッグ {#debugging-information-for-browsers}

スクリプトおよびスタイルは異なるブラウザーにデバッグすることができます。

* **IEでのデバッグ**:IEでAEM Forms Workspaceをデバッグするには、次を参照してください。 [https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx](https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx)。

* **Chromeでのデバッグ**:Chromeでデバッガーを開くには、次のショートカットを使用します。Ctrl + Shift + I。詳しくは、次を参照してください。 [https://developer.chrome.com/extensions/tut_debugging.html](https://developer.chrome.com/extensions/tut_debugging.html)。

* **Firefox でのデバッグ**：複数のアドオンを Firefox でスクリプトおよびスタイルのデバッグに使用することができます。For example, Firebug is one such debugging utility ([https://getfirebug.com](https://getfirebug.com)).

## FAQ {#faqs}

1. Google Chrome で PDF フォームをレンダリングまたは送信することができません。

   1. Adobe® Reader® プラグインをインストールします。
   1. Chrome で、chrome://plugins を開いて使用可能なプラグインを表示します。
   1. Chrome PDF Viewer プラグインを無効にして Adobe Reader プラグインを有効にします。

1. Google Chrome で SWF フォームまたは Guide がレンダリングされません。

   1. Chrome で、chrome://plugins を開いて使用可能なプラグインを表示します。
   1. Adobe Flash® Player プラグインの詳細を参照してください。
   1. Adobe Flash Player プラグインの下で PepperFlash を無効にします。

1. AEM Forms Workspace をカスタマイズしましたが、変更を表示することができません。

   ブラウザーのキャッシュをクリアしてから AEM Forms Workspace にアクセスしてください。

1. デスクトップで開いたときにフォームを HTML にレンダリングされるようにするには、ユーザーは何をすればよいですか?

   Workbench を使用する際に、タスクの割り当て手順でデフォルトのプロファイルに HTML ラジオボタンを選択してください。

1. クリックしても添付ファイルが表示されません。

   添付ファイルを表示するには、ブラウザーのポップアップを有効にしてください。

1. ユーザーが Forms Application にログインしています。ユーザーが Workspace にログインしようとしても、ユーザーに Workspace 権限がない場合は、読み込まれません。

   他の Forms Application からログアウトしてから、Workspace にログインしてください。

1. デザインにプロセスプロパティを使用している HTML フォームを AEM Forms Workspace でレンダリングすると、フォーム内に「送信」ボタンが表示されます。

   フォームのデザイン中にプロセスプロパティを使用すると、フォーム内に「送信」ボタンが追加されます。AEM Forms Workspace で PDF としてレンダリングすると、「送信」ボタンはエンドユーザーに表示されなくなります。ただし、AEM Forms Workspace で HTML フォームとしてレンダリングすると、「送信」ボタンがエンドユーザーに表示されます。フォーム内で「送信」ボタンをクリックしても、いずれのアクションも開始されません。AEM Forms Workspace の下部（フォームの外側）にある「送信」ボタンをクリックすると、タスクは完了します。

[サポートへのお問い合わせ](https://www.adobe.com/account/sign-in.supportportal.html)
