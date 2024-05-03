---
title: AEM Forms Workspace のトラブルシューティングガイドライン
description: ログを有効にし、ブラウザーでデバッガーを使用して AEM Forms Workspace のトラブルシューティングを行います。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a054b60a-5e89-4c98-87bc-35669988d160
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 100%

---

# AEM Forms Workspace のトラブルシューティングガイドライン {#troubleshooting-guidelines-for-aem-forms-workspace}

この記事では、ログを有効にしブラウザーでデバッガーを使用して AEM Forms Workspace をデバッグする方法について説明します。また、AEM Forms Workspace の使用時に発生する可能性のある一般的な問題とその回避策についても説明します。

## AEM Forms Workspace パッケージをインストールできない {#unable-to-install-aem-forms-workspace-package}

パッチをインストールした後、AEM Forms Workspace を開きます。「リソースが見つかりません」というエラーが発生した場合は、CRX Package Manager を開いて、`adobe-lc-workspace-pkg-<version>.zip` パッケージを再インストールします。

パッケージをインストールするときに、「`javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`」というエラーが発生した場合は、次の手順を実行します。

1. CRXDE Lite にログインします。デフォルトの URL は、`https://[localhost]:'port'/lc/crx/de/index.jsp` です。
1. 次のノードを削除します。

   `/home/groups/P/PERM_WORKSPACE_USER`

1. Package Manager に移動します。デフォルトの URL は、`https://[localhost]:'port'/lc/crx/packmgr/index.jsp.` です。
1. `adobe-lc-workspace-pkg-[version].zip` パッケージを検索してインストールします。
1. アプリケーションサーバーを再起動します。

>[!NOTE]
>
> SDK を再起動するには、「Ctrl + C」コマンドを使用することをお勧めします。Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。

## AEM Forms Workspace のログ {#aem-forms-workspace-nbsp-logging}

様々なレベルでログを生成することにより、エラーの最適なトラブルシューティングを行うことができます。例えば、複合アプリケーションでは、コンポーネントレベルでログすると、特定のコンポーネントのデバッグおよびトラブルシューティングに役立ちます。

AEM Forms Workspace では次の操作が可能です。

* 特定のコンポーネントファイルについてのログ情報を取得するには、URL に `/log/<ComponentFile>/<LogLevel>` を付け加えて `Enter` キーを押します。特定のログレベルにおけるコンポーネントファイルのすべてのログ情報は、コンソールに印刷されます。

* すべてのコンポーネントファイルについてのログ情報を取得するには、URL に `/log/all/trace` を付け加えて `Enter` キーを押します。

* ログ形式：`<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>デフォルトでは、すべてのコンポーネントのログレベルは INFO に設定されています。

* ユーザーが設定したログレベルは、そのブラウザーセッションでのみ保持されます。ユーザーがページを更新すると、すべてのコンポーネントのログレベルが初期値に設定されます。

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

* FATAL
* ERROR
* WARN
* INFO
* DEBUG
* TRACE
* OFF

## ブラウザーのデバッグ情報 {#debugging-information-for-browsers}

スクリプトとスタイルは、様々なブラウザーでデバッグできます。

* **IE でのデバッグ**：IE でAEM Forms Workspace をデバッグするには、[https://learn.microsoft.com/ja-jp/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie](https://learn.microsoft.com/ja-jp/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie) を参照してください。

* **Chrome でのデバッグ**：Chrome でデバッガーを開くには、Ctrl+Shift+I ショートカットキーを使用します。詳しくは、[https://developer.chrome.com/docs/extensions/mv3/tut_debugging/](https://developer.chrome.com/docs/extensions/mv3/tut_debugging/) を参照してください。

* **Firefox でのデバッグ**：複数のアドオンを Firefox でスクリプトおよびスタイルのデバッグに使用することができます。例えば、Firebug はデバッグユーティリティの 1 つです（[https://getfirebug.com](https://getfirebug.com)）。

## FAQ {#faqs}

1. Google Chrome で PDF フォームをレンダリングまたは送信できない。

   1. Adobe® Reader® プラグインをインストールします。
   1. Chrome で、chrome://plugins を開いて使用可能なプラグインを表示します。
   1. Chrome PDF Viewer プラグインを無効にし、Adobe Reader プラグインを有効にします。

1. Google Chrome で SWF フォームまたは Guide がレンダリングされない。

   1. Chrome で、chrome://plugins を開いて使用可能なプラグインを表示します。
   1. Adobe Flash® Player プラグインの詳細を参照してください。
   1. Adobe Flash Player プラグインで PepperFlash を無効にします。

1. AEM Forms Workspace をカスタマイズしたが、変更が表示されない。

   ブラウザーのキャッシュをクリアしてから AEM Forms Workspace にアクセスしてください。

1. フォームをデスクトップで開いたときに HTML でレンダリングされるようにするには？

   Workbench を使用する際、タスクを割り当てステップで、デフォルトプロファイルの HTML ラジオボタンを選択します。

1. 添付ファイルをクリックしても表示されない。

   添付ファイルを表示するには、ブラウザーのポップアップを有効にします。

1. Forms アプリケーションにログインしているユーザーが Workspace にログインしようとすると、Workspace の権限がない場合、読み込まれないことがある。

   他の Forms アプリケーションからログアウトしたあと、Workspace にログインします。

1. プロセスプロパティを使用して HTMLフォームをデザインし、AEM Forms Workspace でレンダリングすると、フォーム内に「送信」ボタンが表示される。

   フォームをデザインする際にプロセスプロパティを使用すると、フォーム内に「送信」ボタンが追加されます。AEM Forms Workspace で PDF としてレンダリングすると、「送信」ボタンはエンドユーザーに表示されなくなります。ただし、AEM Forms Workspace で HTML フォームとしてレンダリングすると、「送信」ボタンがエンドユーザーに表示されます。フォーム内でこの「送信」ボタンをクリックしても、アクションは開始されません。AEM Forms Workspace の下部（フォームの外側）にある「送信」ボタンをクリックすると、タスクは完了します。
