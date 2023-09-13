---
title: アダプティブフォームのキャッシュの設定
description: アダプティブフォームのキャッシュは、アダプティブフォームとアダプティブドキュメント用に特別に設計されています。 クライアント上でのアダプティブフォームまたはドキュメントのレンダリングに要する時間を短縮する目的で、アダプティブフォームおよびアダプティブドキュメントをキャッシュします。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin
exl-id: 153986f0-b6ff-4278-8bb6-70c320a4e539
source-git-commit: 5af420c8e95fed88a8516cce27b8bbc7d3974e75
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 54%

---

# アダプティブフォームのキャッシュの設定 {#configure-adaptive-forms-cache}

キャッシュは、データへのアクセスにかかる時間を短縮し、遅延を削減して I／O 速度を改善するメカニズムです。アダプティブフォームのキャッシュには、アダプティブフォームのHTMLコンテンツと JSON 構造のみが保存されます。事前入力されたデータは保存されません。 これにより、クライアントサイドのアダプティブフォームのレンダリングの時間を短縮します。特にアダプティブフォーム向けに設計されています。

## オーサーインスタンスおよびパブリッシュインスタンスでのアダプティブフォームのキャッシュの設定 {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. `https://[server]:[port]/system/console/configMgr` の AEM Web コンソール設定マネージャーに移動します。
1. 「**[!UICONTROL アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定]**」をクリックして、設定値を編集します。
1. Adobe Analytics の [!UICONTROL 設定値の編集] ダイアログを開き、AEMの 1 つのインスタンスのフォームまたはドキュメントの最大数を指定します [!DNL Forms] サーバーが **[!UICONTROL アダプティブFormsの数]** フィールドに入力します。 デフォルト値は 100 です。

   >[!NOTE]
   >
   >キャッシュを無効にするには、「アダプティブフォームの数」フィールドの値を **0** に設定します。キャッシュ設定を無効にしたり変更したりすると、キャッシュがリセットされ、すべてのフォームとドキュメントがキャッシュから削除されます。

   ![アダプティブフォームの HTML キャッシュの設定ダイアログ](assets/cache-configuration-edit.png)

1. 「**[!UICONTROL 保存]**」をクリックして、設定を保存します。

環境は、アダプティブフォームと関連アセットのキャッシュを使用するように設定されています。


## （オプション）Dispatcher でのアダプティブフォームのキャッシュの設定 {#configure-the-cache}

また、パフォーマンスを向上させるために、Dispatcher でアダプティブフォームのキャッシュを設定することもできます。

### 前提条件 {#pre-requisites}

* を有効にします。 [クライアントでのデータの結合または事前入力](prepopulate-adaptive-form-fields.md#prefill-at-client) オプション。 これは、事前入力されたフォームの各インスタンスの一意のデータを結合するのに役立ちます。

### Dispatcher 上のアダプティブフォームをキャッシュする際の考慮事項 {#considerations}

* アダプティブフォームのキャッシュを使用する場合、AEM [!DNL Dispatcher] を使用してアダプティブフォームのクライアントライブラリ（CSS および JavaScript）をキャッシュしてください。
* カスタムコンポーネントの開発時には、開発に使用されるサーバー上でアダプティブフォームのキャッシュを無効にしておく必要があります。
* 拡張子のない URL はキャッシュされません。例えば、次のパターンを含む URL `/content/forms/[folder-structure]/[form-name].html` はキャッシュされ、パターンを持つ URL はキャッシュによって無視されます `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. そのため、キャッシュのメリットを活用するには、拡張機能と共に URL を使用してください。
* ローカライズされたアダプティブフォームの考慮事項：
   * `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>` の代わりに `http://host:port/content/forms/af/<afName>.<locale>.html` の URL 形式を使用して、アダプティブフォームのローカライズ版をリクエストします。
   * [ 形式の URL に対するブラウザーロケール](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) `http://host:port/content/forms/af/<adaptivefName>.html` の使用を無効にします。
   * URL 形式 `http://host:port/content/forms/af/<adaptivefName>.html` を使用し、設定マネージャーで&#x200B;**[!UICONTROL ブラウザーロケールを使用]**&#x200B;が無効になっている場合、アダプティブフォームの非ローカライズ版が提供されます。非ローカライズ言語とは、アダプティブフォームの開発時に使用される言語です。ブラウザーに対して設定されたロケール（ブラウザーのロケール）は考慮されず、アダプティブフォームの非ローカライズバージョンが提供されます。
   * URL 形式 `http://host:port/content/forms/af/<adaptivefName>.html` を使用し、設定マネージャーで&#x200B;**[!UICONTROL ブラウザーロケールを使用]**&#x200B;が有効になっている場合、アダプティブフォームのローカライズ版が提供されます（利用可能な場合）。ローカライズされたアダプティブフォームの言語は、ブラウザーに設定されたロケール（ブラウザーロケール）に基づきます。それは次のようになります。 [アダプティブフォームの最初のインスタンスのみをキャッシュする]. インスタンスで問題が発生しないようにするには、[トラブルシューティング](#only-first-insatnce-of-adptive-forms-is-cached)を参照してください。

### Dispatcher でのキャッシュの有効化

Dispatcher 上でアダプティブフォームのキャッシュを有効にして設定するには、以下の手順を実行します。

1. 環境のすべてのパブリッシュインスタンスに対して次の URL を開き、 [お使いの環境のパブリッシュインスタンス用のフラッシュエージェントを有効にする](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=ja#invalidating-dispatcher-cache-from-a-publishing-instance):
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [dispatcher.any ファイルに以下を追加します](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#automatically-invalidating-cached-files)。

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

   * アダプティブフォームは、更新されたバージョンのフォームが公開されない限り、キャッシュに残ります。

   * アダプティブフォーム内で参照されている新しいバージョンのリソースが公開されると、影響を受けるアダプティブフォームは自動的に無効化されます。 参照されるリソースの自動無効化には、いくつかの例外があります。例外の回避策については、 [トラブルシューティング](#troubleshooting) 」セクションに入力します。
1. [以下のルール dispatcher.any またはカスタムルールファイルを追加します](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#specifying-the-documents-to-cache)。キャッシュをサポートしない URL は除外されます。例えば、インタラクティブ通信などです。

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

1. [「URL パラメーターを無視」リストに以下のパラメーターを追加します](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#ignoring-url-parameters)。

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

AEM 環境は、アダプティブフォームをキャッシュするように設定されています。すべてのタイプのアダプティブフォームをキャッシュします。キャッシュされたページを配信する前に、ページのユーザーアクセス権限を確認する必要がある場合は、 [セキュリティで保護されたコンテンツのキャッシュ](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=ja).

## トラブルシューティング {#troubleshooting}

### 画像やビデオを含む一部のアダプティブフォームは、Dispatcher のキャッシュから自動的に無効化されません {#videos-or-images-not-auto-invalidated}

#### 問題 {#issue1}

アセットブラウザーを使用して画像やビデオを選択してアダプティブフォームに追加し、それらの画像やビデオを Assets エディターで編集すると、そのような画像を含むアダプティブフォームは Dispatcher のキャッシュから自動的に無効化されません。

#### 解決策 {#Solution1}

画像とビデオを公開した後、これらのアセットを参照するアダプティブフォームを明示的に非公開にしてから公開してください。

### アダプティブフォームの最初のインスタンスのみがキャッシュされます {#only-first-instance-of-adaptive-forms-is-cached}

#### 問題 {#issue3}

アダプティブフォームの URL にローカリゼーション情報がない場合、および **[!UICONTROL ブラウザーのロケールを使用]** configuration manager を有効にすると、アダプティブフォームのローカライズ版が提供されます。 アダプティブフォームの最初のインスタンスのみがキャッシュされ、後続のすべてのユーザーに配信されます。

#### 解決策 {#Solution3}

次の手順を実行して問題を解決します。

1. conf.d/httpd-dispatcher.conf または実行時に読み込むように設定されたその他の設定ファイルを開きます。

1. 次のコードをファイルに追加して保存します。これはサンプルコードです。環境に合わせて変更してください。

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
