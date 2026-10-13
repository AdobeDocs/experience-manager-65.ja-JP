---
title: オフラインモードの使用
description: AEM Forms のネットワーク圏外や、完全オフラインモードでモバイルデバイスを使用して、AEM Forms アプリケーションで作業する
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: ba4ceef1-510d-41ef-94b8-4834fb7de804
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 97%
---
# オフラインモードの使用 {#working-in-the-offline-mode}

>[!NOTE]
>
>AEM Forms アプリは現在、非推奨です。 質問またはヘルプについては、[aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com)までお問い合わせください。

AEM Forms アプリケーションのオフラインモードを使用すると、アプリケーションがオフラインになってもシームレスに作業を続けることができます。 ネットワーク接続を必要とせずにフォームを開いたり、更新したり、送信したりすることができます。

AEM Forms アプリケーションで作業を開始する際は、まずアプリケーションを AEM Forms サーバーと同期します。 ユーザーに割り当てられているフォームすべてが、ユーザーのアプリケーションにダウンロードされます。 JEE 上の AEM Forms の場合、タスクは「タスク」タブで取得され、スタートポイントに関連付けられているフォームおよびその他のフォームは「フォーム」タブで取得されます。 OSGi 上の AEM Forms の場合、AEM Forms のみが「フォーム」タブに読み込まれます。

アプリケーションを同期する方法について詳しくは、[アプリケーションの同期](/help/forms/using/sync-app.md)を参照してください。

## Forms をオフラインで使用可能にする {#making-forms-available-offline}

アプリケーションを AEM Forms サーバーと同期すると、フォームがモバイルデバイス上にダウンロードされます。 ただし、デフォルトでは、フォームに関連付けられた添付ファイルはダウンロードされません。 このことは、オンラインになったときに添付ファイルを表示できることを意味します。 ただし、オフラインモードで添付ファイルを表示できるようにするには、アプリケーションのデフォルト設定を変更します。

各フォームに関連付けられた添付ファイルをダウンロードするには、「添付ファイルの取得」を ON に設定します。 詳しくは、[一般設定の更新](/help/forms/using/update-general-settings.md)を参照してください。

モバイルデバイスへデータをダウンロードすると処理能力に影響を与えるため、デフォルトでは、「添付ファイルの取得」オプションは「オフ」に設定されています。 これらの設定を「有効」に更新すると、タスクがサーバーからダウンロードされる際に添付ファイルもデバイスにダウンロードされます。 オフラインモードでは、「**添付ファイルを取得する**」オプションを「有効」に設定することで、デバイスにダウンロードされるタスクすべてが作業可能になります。

## AEM Forms アプリケーションのオフラインサービスの設定 {#configuring-offline-service-for-aem-forms-app-br}

AEM Forms アプリケーションオフラインサービスでは、フォームで使用するリソースを認識します。 AEM Forms アプリケーションは、フォームの依存関係に関する情報を取得する際に、このサービスに依存しています。 フォームの依存関係に関する情報は、オフライン機能を有効にするために必要です。 AEM Forms アプリケーションのオフラインサービスでは、フォームで使用されるリソースのパスや URL をキャッシュに保存します。 キャッシュは、フォームに加えられた変更やオフラインサービスに設定された有効期間に基づいて更新されます。 フォームで使用されるリソースのパスや URL をキャッシュに保存することで、サーバーサイドのパフォーマンスが向上します。

AEM Forms アプリケーションでサーバー側のオフラインコンポーネントの設定は、次のように行います。

1. オーサーインスタンスで、**Adobe Experience Manager**／**ツール**／**Forms**／**Forms アプリケーションオフラインサービスを設定**&#x200B;に移動します。

   URL：`https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. 一般設定で、以下を実行します。

   * **キャッシュの消去**：フォームの依存関係に関するサーバー側のキャッシュをクリアします。
   * **設定のリセット**：AEM Forms アプリケーションのオフライン設定をリセットします。
   * **キャッシュの有効性**：サーバー側のオフラインキャッシュの有効期間を指定します。
   * **リソース監視パス**：オフラインサービスによるリソースの変更監視パスを指定します。 指定されたパスに何らかの変更が発生した場合は、依存関係に関するオフラインキャッシュもすべて更新されます （例：`/etc/clientlibs/fd,/content/dam/images`）。

1. 「**手動のリソースキャッシュ**」タブで、オフラインサービスでは認識できないフォームの依存性を設定します。 JavaScript 内で読み込まれた画像などのリソースを指定することができます。 AEM Forms アプリケーションは、オフラインモード用にこれらのリソースもダウンロードします。
