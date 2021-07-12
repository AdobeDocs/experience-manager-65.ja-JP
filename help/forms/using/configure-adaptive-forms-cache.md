---
title: アダプティブフォームのキャッシュの設定
seo-title: アダプティブフォームのキャッシュの設定
description: 'アダプティブフォームのキャッシュは、アダプティブフォームおよびアダプティブドキュメント向けに設計されています。これは、クライアント側のアダプティブフォームまたはドキュメントのレンダリングの時間を短縮する目的で、アダプティブフォームとアダプティブドキュメントをキャッシュします。 '
seo-description: 'アダプティブフォームのキャッシュは、アダプティブフォームおよびアダプティブドキュメント向けに設計されています。これは、クライアント側のアダプティブフォームまたはドキュメントのレンダリングの時間を短縮する目的で、アダプティブフォームとアダプティブドキュメントをキャッシュします。 '
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
role: Admin
exl-id: 153986f0-b6ff-4278-8bb6-70c320a4e539
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 53%

---

# アダプティブフォームのキャッシュの設定 {#configure-adaptive-forms-cache}

キャッシュは、データへのアクセスにかかる時間を短縮し、遅延を削減して I／O 速度を改善するメカニズムです。アダプティブフォームのキャッシュは、アダプティブフォームの HTML コンテンツと JSON の構造のみを保存し、事前入力されたデータは保存しません。これにより、クライアント上でのアダプティブフォームのレンダリングに要する時間を短縮できます。 これは、アダプティブフォーム専用に設計されています。

## オーサーインスタンスとパブリッシュインスタンスでアダプティブフォームのキャッシュを設定する {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. `https://[server]:[port]/system/console/configMgr` の AEM Web コンソール設定マネージャーに移動します。
1. 「**[!UICONTROL アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定]**」をクリックして、設定値を編集します。
1. [!UICONTROL 設定値を編集]ダイアログで、AEM [!DNL Forms] サーバーのインスタンスでキャッシュできるフォームまたはドキュメントの最大数を「**[!UICONTROL アダプティブフォームの数]**」フィールドに指定します。デフォルト値は 100 です。

   >[!NOTE]
   >
   >キャッシュを無効にするには、「アダプティブフォームの数」フィールドの値を **0** に設定します。キャッシュ設定を無効にしたり変更したりすると、キャッシュがリセットされ、すべてのフォームとドキュメントがキャッシュから削除されます。

   ![アダプティブフォームの HTML キャッシュの設定ダイアログ](assets/cache-configuration-edit.png)

1. 「**[!UICONTROL 保存]**」をクリックして、設定を保存します。

環境は、アダプティブフォームと関連アセットをキャッシュするように設定されています。


## （オプション）Dispatcherでのアダプティブフォームのキャッシュの設定 {#configure-the-cache}

また、Dispatcherでのアダプティブフォームのキャッシュを設定して、パフォーマンスを向上させることもできます。

### 前提条件 {#pre-requisites}

* [クライアントでのデータの結合または事前入力](prepopulate-adaptive-form-fields.md#prefill-at-client)オプションを有効にします。これは、事前入力されたフォームの各インスタンスの一意のデータを結合するのに役立ちます。

### Dispatcher上のアダプティブフォームをキャッシュする際の考慮事項 {#considerations}

* アダプティブフォームのキャッシュを使用する場合は、AEM [!DNL Dispatcher]を使用してアダプティブフォームのクライアントライブラリ（CSSとJavaScript）をキャッシュします。
* カスタムコンポーネントの開発時には、開発に使用されるサーバー上でアダプティブフォームのキャッシュを無効にしておく必要があります。
* 拡張子のない URL はキャッシュされません。例えば、パターン `/content/forms/[folder-structure]/[form-name].html` の URL はキャッシュされ、パターン `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content` の URL は無視されます。したがって、キャッシュのメリットを活用するには、拡張子が付いた URL を使用します。
* ローカライズされたアダプティブフォームに関する考慮事項：
   * アダプティブフォームのローカライズ版をリクエストする場合は、URL形式`http://host:port/content/forms/af/<afName>.<locale>.html`を使用します（`http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`の代わりに）。
   * [](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) 形式の URL に対するブラウザーロケール`http://host:port/content/forms/af/<adaptivefName>.html`の使用を無効にします。
   * Configuration ManagerでURL形式`http://host:port/content/forms/af/<adaptivefName>.html`を使用し、**[!UICONTROL ブラウザーのロケール]**&#x200B;を使用を無効にすると、ローカライズされていないバージョンのアダプティブフォームが提供されます。 ローカライズされていない言語は、アダプティブフォームの開発時に使用される言語です。 使用しているブラウザー（ブラウザーのロケール）に設定されたロケールは考慮されず、アダプティブフォームのローカライズされていないバージョンが提供されます。
   * URL形式`http://host:port/content/forms/af/<adaptivefName>.html`を使用し、Configuration Managerで「**[!UICONTROL ブラウザーのロケール]**&#x200B;を使用」が有効になっている場合は、ローカライズ版のアダプティブフォームが提供されます（使用可能な場合）。 ローカライズされたアダプティブフォームの言語は、お使いのブラウザーに設定されているロケール（ブラウザーのロケール）に基づきます。 [アダプティブフォームの最初のインスタンスのみをキャッシュする可能性があります。] インスタンスで問題が発生しないようにするには、[トラブルシューティング](#only-first-insatnce-of-adptive-forms-is-cached)を参照してください。

### Dispatcher でのキャッシュの有効化

ディスパッチャー上のアダプティブフォームのキャッシュを有効にして設定するには、以下の手順を実行します。

1. 環境のすべてのパブリッシュインスタンスに対して次のURLを開き、環境のパブリッシュインスタンスに対して[フラッシュエージェントを有効にします](https://docs.adobe.com/content/help/ja/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance)。
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [dispatcher.any ファイルに以下を追加します](https://docs.adobe.com/content/help/ja/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files)。

   ```JSON
      /invalidate
      {
      /0000
      {
      /glob "*"
      /type "deny"
      }
      /0001
      {
      # Consider all HTML files stale after an activation.
      /glob "*.html"
      /type "allow"
      }
      /0002
      {
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   上記を追加すると、以下のようになります。

   * アダプティブフォームは、更新されたバージョンのフォームが発行されない限り、キャッシュに残ります。

   * アダプティブフォーム内で参照されている新しいバージョンのリソースが発行されると、影響を受けたアダプティブフォームは自動的に無効化されます。 参照されるリソースの自動無効化には、いくつかの例外があります。例外の回避策については、[トラブルシューティング](#troubleshooting)の節を参照してください。
1. [以下のルール dispatcher.any またはカスタムルールファイルを追加します](https://docs.adobe.com/content/help/ja/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache)。キャッシュをサポートしない URL は除外されます。例えば、インタラクティブ通信などです。

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Don't cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Don't cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Don't cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [「URL パラメーターを無視」リストに以下のパラメーターを追加します](https://docs.adobe.com/content/help/ja/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters)。

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

アダプティブフォームをキャッシュするようにAEM環境が設定されている。 すべてのタイプのアダプティブフォームをキャッシュします。 キャッシュされたページを配信する前に、ページのユーザーアクセス権限を確認する必要がある場合は、[セキュリティで保護されたコンテンツのキャッシュ](https://docs.adobe.com/content/help/ja/experience-manager-dispatcher/using/configuring/permissions-cache.html)を参照してください。

## トラブルシューティング {#troubleshooting}

### 画像やビデオを含むアダプティブフォームの一部が、Dispatcherのキャッシュから自動的に無効化されない {#videos-or-images-not-auto-invalidated}

#### OS クリップボードと内部 AEM クリップボードを使用した     {#issue1}

アセットブラウザーを使用してアダプティブフォームに画像やビデオを選択して追加し、それらの画像やビデオをアセットエディターで編集すると、そのような画像を含むアダプティブフォームはDispatcherのキャッシュから自動的に無効化されません。

#### 解決策 {#Solution1}

画像とビデオを公開した後で、これらのアセットを参照しているアダプティブフォームを明示的に非公開にして公開します。

### アダプティブフォームの最初のインスタンスのみがキャッシュされます {#only-first-instance-of-adaptive-forms-is-cached}

#### OS クリップボードと内部 AEM クリップボードを使用した     {#issue3}

アダプティブフォームのURLにローカリゼーション情報がなく、Configuration Managerの&#x200B;**[!UICONTROL ブラウザーのロケールを使用]**&#x200B;が有効な場合は、ローカライズされたバージョンのアダプティブフォームが提供され、アダプティブフォームの最初のインスタンスのみがキャッシュされ、後続のすべてのユーザーに配信されます。

#### 解決策 {#Solution3}

問題を解決するには、以下の手順を実行します。

1. conf.d/httpd-dispatcher.conf または実行時に読み込むように設定されたその他の設定ファイルを開きます。

1. 以下のコードをファイルに追加して保存します。これはサンプルコードです。環境に合わせて変更してください。

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two character which most likely will be the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
