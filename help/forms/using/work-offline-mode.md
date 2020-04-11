---
title: オフラインモードの使用
seo-title: オフラインモードの使用
description: AEM Forms のネットワーク圏外や、完全オフラインモードでモバイルデバイスを使用して、AEM Forms アプリケーションで作業する
seo-description: AEM Forms のネットワーク圏外や、完全オフラインモードでモバイルデバイスを使用して、AEM Forms アプリケーションで作業する
uuid: b900a0f8-90ce-486a-bde6-6cdf11bd2801
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9a3c6ab4-8bb9-40c7-8c56-59153b364887
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# オフラインモードの使用 {#working-in-the-offline-mode}

AEM Formsアプリケーションのオフラインモードを使用すると、アプリケーションがオフラインになった場合でも、シームレスに作業を行うことができます。 ネットワーク接続を必要とせずにフォームを開いたり、更新したり、送信したりすることができます。

開始がAEM Formsアプリケーションで作業を行う際に、アプリケーションをAEM Formsサーバーと同期します。 ユーザーに割り当てられているフォームすべてが、ユーザーのアプリケーションにダウンロードされます。JEE 上の AEM Forms の場合、タスクは「タスク」タブで取得され、スタートポイントに関連付けられているフォームおよびその他のフォームは「フォーム」タブで取得されます。OSGi 上の AEM Forms の場合、フォームのみが「フォーム」タブに読み込まれます。

アプリケーションを同期する方法について詳しくは、「[アプリケーションの同期](/help/forms/using/sync-app.md)」を参照してください。

## Forms をオフラインで使用可能にする {#making-forms-available-offline}

アプリケーションを AEM Forms サーバーと同期すると、フォームがモバイルデバイス上にダウンロードされます。ただし、デフォルトでは、フォームに関連付けられた添付ファイルはダウンロードされません。このことは、オンラインになったときに添付ファイルを表示できることを意味します。ただし、オフラインモードで添付ファイルを表示できるようにするには、アプリケーションのデフォルト設定を変更します。

各フォームに関連付けられた添付ファイルをダウンロードするには、「添付ファイルの取得」を「有効」に設定します。詳しくは、「[一般設定の更新](/help/forms/using/update-general-settings.md)」を参照してください。

モバイルデバイスへデータをダウンロードすると処理能力に影響を与えるため、デフォルトでは、「添付ファイルの取得」オプションは「オフ」に設定されています。これらの設定を「有効」に変更すると、タスクがサーバーからダウンロードされる際に添付ファイルもデバイスにダウンロードされます。In the offline mode, a user can then work on all tasks that are downloaded to device after setting the **Fetch attachments** options to ON.

## AEM Forms アプリケーションに対してオフラインサービスを設定する {#configuring-offline-service-for-aem-forms-app-br}

AEM Forms アプリケーションオフラインサービスでは、フォームで使用するリソースを認識します。AEM Formsアプリケーションは、このサービスを利用して、フォームの依存関係に関する情報を取得します。 フォームの依存関係に関する情報は、オフライン機能を有効にするために必要です。AEM Forms アプリケーションのオフラインサービスでは、フォームで使用されるリソースのパスや URL をキャッシュに保存します。キャッシュは、フォームに加えられた変更やオフラインサービスに設定された有効期間に基づいて更新されます。フォームで使用されるリソースのパスや URL をキャッシュに保存することで、サーバー側のパフォーマンスが向上します。

AEM Forms アプリケーションでサーバー側のオフラインコンポーネントの設定は、次のように行います。

1. In the author instance, navigate to **Adobe Experience Manager** >**Tools** > **Forms** > **Configure Forms App Offline Service**.

   URL: `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. 一般設定で、以下を実行します。

   * **キャッシュの消去**：フォームの依存関係に関するサーバ側のキャッシュをクリアします。
   * **設定のリセット**:AEM Formsアプリケーションのオフライン設定をリセットします。
   * **キャッシュの有効性**：サーバー側のオフラインキャッシュの有効期間を指定します。
   * **リソース監視パス**：オフラインサービスによるリソースの変更監視パスを指定します。指定されたパスに何らかの変更が発生した場合は、依存関係に関するオフラインキャッシュもすべて更新されます。例： `/etc/clientlibs/fd,/content/dam/images`

1. 「**手動のリソースキャッシュ**」タブで、オフラインサービスでは認識できないフォームの依存性を設定します。JavaScript 内で読み込まれた画像などのリソースを指定することができます。AEM Forms アプリケーションは、オフラインモードに向けてこれらのリソースもダウンロードします。
