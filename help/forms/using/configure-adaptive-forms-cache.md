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
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 21%

---


# アダプティブフォームのキャッシュの設定 {#configure-adaptive-forms-cache}

キャッシュは、データへのアクセスにかかる時間を短縮し、遅延を削減して I/O 速度を改善するメカニズムです。アダプティブフォームのキャッシュは、アダプティブフォームの HTML コンテンツと JSON の構造のみを保存し、事前入力されたデータは保存しません。これは、クライアントでのアダプティブフォームのレンダリングに要する時間を短縮するのに役立ちます。 これは、アダプティブフォーム専用に設計されています。

## 作成者インスタンスと発行インスタンスでアダプティブフォームのキャッシュを設定{#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. `https://[server]:[port]/system/console/configMgr`のAEM Web Console Configuration Managerに移動します。
1. 「**[!UICONTROL アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定]**」をクリックして、設定値を編集します。
1. [!UICONTROL 設定値の編集]ダイアログで、AEM [!DNL Forms]サーバーのインスタンスがキャッシュできるフォームまたはドキュメントの最大数を&#x200B;**[!UICONTROL アダプティブFormsの数]**&#x200B;フィールドに指定します。 デフォルト値は 100 です。

   >[!NOTE]
   >
   >キャッシュを無効にするには、「アダプティブフォームの数」フィールドの値を **0** に設定します。キャッシュの設定を無効または変更すると、キャッシュがリセットされ、フォームとドキュメントがすべてキャッシュから削除されます。

   ![アダプティブフォームの HTML キャッシュの設定ダイアログ](assets/cache-configuration-edit.png)

1. 「**[!UICONTROL Save]**」をクリックして、 設定を保存します。

環境は、アダプティブフォームおよび関連アセットをキャッシュするように設定されています。


## （オプション）ディスパッチャーでアダプティブフォームのキャッシュを設定{#configure-the-cache}

また、パフォーマンスをさらに向上させるために、ディスパッチャーでアダプティブフォームのキャッシングを設定することもできます。

### 前提条件 {#pre-requisites}

* [クライアント](prepopulate-adaptive-form-fields.md#prefill-at-client)でのデータの結合または事前入力を有効にします。 これは、事前入力されたフォームの各インスタンスの一意のデータをマージするのに役立ちます。

### ディスパッチャー{#considerations}上のアダプティブフォームをキャッシュする際の考慮点

* アダプティブフォームのキャッシュを使用する場合は、AEM [!DNL Dispatcher]を使用してアダプティブフォームのクライアントライブラリ（CSSおよびJavaScript）をキャッシュします。
* カスタムコンポーネントの開発時には、開発に使用されるサーバー上でアダプティブフォームのキャッシュを無効にしておく必要があります。
* 拡張子のないURLはキャッシュされません。 例えば、パターンパターン`/content/forms/[folder-structure]/[form-name].html`のURLはキャッシュされ、パターン`/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`のURLはキャッシュされません。 したがって、URLに拡張子を付けて使用すると、キャッシュの利点を活用できます。
* ローカライズされたアダプティブフォームの考慮事項：
   * `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`の代わりに、URL形式`http://host:port/content/forms/af/<afName>.<locale>.html`を使用してアダプティブフォームのローカライズ版をリクエストする
   * [形式を指定したURLに対するブラウザー](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) ロケールの使用を無効に `http://host:port/content/forms/af/<adaptivefName>.html`します。
   * URL形式`http://host:port/content/forms/af/<adaptivefName>.html`を使用し、Configuration Managerで&#x200B;**[!UICONTROL 「ブラウザーロケールを使用」]**&#x200B;が無効になると、ローカライズされていないバージョンのアダプティブフォームが提供されます。 ローカライズされていない言語は、アダプティブフォームの開発時に使用される言語です。 ブラウザーに設定されているロケール（ブラウザーのロケール）は考慮されず、アダプティブフォームのローカライズされていないバージョンが提供されます。
   * URL形式`http://host:port/content/forms/af/<adaptivefName>.html`を使用し、Configuration Managerで「**[!UICONTROL ブラウザーロケールを使用]**」が有効な場合、ローカライズ版のアダプティブフォームが提供されます（使用可能な場合）。 ローカライズされたアダプティブフォームの言語は、ブラウザー（ブラウザーのロケール）に設定されたロケールに基づきます。 [アダプティブフォーム]の最初のインスタンスのみをキャッシュする原因になる場合があります。 インスタンスで問題が発生しないようにするには、[トラブルシューティング](#only-first-insatnce-of-adptive-forms-is-cached)を参照してください。

### ディスパッチャーでのキャッシュの有効化

ディスパッチャー上のアダプティブフォームのキャッシュを有効にし、設定するには、次の手順を実行します。

1. 自分の環境の各パブリッシュインスタンスに対して次のURLを開き、[環境のパブリッシュインスタンスに対してフラッシュエージェントを有効にします](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance)。
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [dispatcher.anyフ追加ァイルに対して次の操作を行います](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files)。

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

   上記の

   * アダプティブフォームは、更新されたバージョンのフォームが発行されない限り、キャッシュに残ります。

   * アダプティブフォーム内で参照されている新しいバージョンのリソースが発行されると、影響を受けたアダプティブフォームは自動的に無効になります。 参照先リソースの自動無効化には、いくつかの例外があります。 例外の回避策については、[トラブルシューティング](#troubleshooting)の節を参照してください。
1. [次追加のルールは、dispatcher.anyまたはカスタムルールファイル](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache)。キャッシュをサポートしないURLは除外されます。 例えば、Interactive Communicationなどです。

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

1. [「追加ignore URL parameters」リストーに対する次のパラメーター](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters)。

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

AEM環境は、アダプティブフォームをキャッシュするように設定されています。 すべてのタイプのアダプティブフォームをキャッシュします。 キャッシュされたページを配信する前に、ページのユーザーアクセス権限を確認する必要がある場合は、[セキュリティで保護されたコンテンツのキャッシュ](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/permissions-cache.html)を参照してください。

## トラブルシューティング {#troubleshooting}

### 画像やビデオを含む一部のアダプティブフォームは、ディスパッチャーキャッシュ{#videos-or-images-not-auto-invalidated}から自動的に無効にされません

#### OS クリップボードと内部 AEM クリップボードを使用した    {#issue1}

アセットブラウザを介して画像またはビデオを選択してアダプティブフォームに追加し、これらの画像およびビデオをアセットエディターで編集した場合、このような画像を含むアダプティブフォームは、自動的にディスパッチャーキャッシュから無効にされません。

#### 解決策 {#Solution1}

画像とビデオを公開した後、これらのアセットを参照するアダプティブフォームの公開を明示的に取り消し、公開を取り消します。

### アダプティブフォームの最初のインスタンスのみがキャッシュ{#only-first-instance-of-adaptive-forms-is-cached}

#### OS クリップボードと内部 AEM クリップボードを使用した    {#issue3}

アダプティブフォームURLにローカライゼーション情報がなく、Configuration Managerの&#x200B;**[!UICONTROL ブラウザーロケールを使用]**&#x200B;が有効な場合、アダプティブフォームのローカライズ版が提供され、アダプティブフォームの最初のインスタンスのみがキャッシュされ、後続のすべてのユーザーに配信されます。

#### 解決策 {#Solution3}

問題を解決するには、次の手順を実行してください。

1. conf.d/httpd-dispatcher.confまたは実行時に読み込むように設定されたその他の設定ファイルを開きます。

1. 次追加のコードをファイルに保存します。 これはサンプルコードで、環境に合わせて変更します。

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
