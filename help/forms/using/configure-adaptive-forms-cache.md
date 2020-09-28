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
translation-type: tm+mt
source-git-commit: d5a649337acdc01c58ecc473e7c919e06cbd0188
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 19%

---


# アダプティブフォームのキャッシュの設定 {#configure-adaptive-forms-cache}

キャッシュは、データへのアクセスにかかる時間を短縮し、遅延を削減して I/O 速度を改善するメカニズムです。アダプティブフォームのキャッシュは、アダプティブフォームの HTML コンテンツと JSON の構造のみを保存し、事前入力されたデータは保存しません。これは、クライアントでのアダプティブフォームのレンダリングに要する時間を短縮するのに役立ちます。 これは、アダプティブフォーム専用に設計されています。

## 作成者インスタンスと発行インスタンスでのアダプティブフォームのキャッシュの設定 {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Go to AEM web console configuration manager at `https://[server]:[port]/system/console/configMgr`.
1. 「**[!UICONTROL アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定]**」をクリックして、設定値を編集します。
1. In the [!UICONTROL edit configuration values] dialog, specify the maximum number of forms or documents an instance of the AEM [!DNL Forms] server can cache in the **[!UICONTROL Number of Adaptive Forms]** field. デフォルト値は 100 です。

   >[!NOTE]
   >
   >キャッシュを無効にするには、「アダプティブフォームの数」フィールドの値を **0** に設定します。キャッシュの設定を無効または変更すると、キャッシュがリセットされ、フォームとドキュメントがすべてキャッシュから削除されます。

   ![アダプティブフォームの HTML キャッシュの設定ダイアログ](assets/cache-configuration-edit.png)

1. 「**[!UICONTROL Save]**」をクリックして、 設定を保存します。

環境は、アダプティブフォームおよび関連アセットをキャッシュするように設定されています。


## （オプション）ディスパッチャーでのアダプティブフォームのキャッシュの設定 {#configure-the-cache}

また、パフォーマンスをさらに向上させるために、ディスパッチャーでアダプティブフォームのキャッシングを設定することもできます。

### 前提条件 {#pre-requisites}

* クライアントでのデータの [結合または事前入力を有効にします](prepopulate-adaptive-form-fields.md#prefill-at-client) 。 これは、事前入力されたフォームの各インスタンスの一意のデータをマージするのに役立ちます。
* [すべての発行インスタンスに対してフラッシュエージェントを有効にします](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance)。 これにより、アダプティブフォームのキャッシュパフォーマンスを向上できます。 フラッシュエージェントのデフォルトURLはで `http://[server]:[port]]/etc/replication/agents.publish/flush.html`す。

### ディスパッチャー上のアダプティブフォームのキャッシュに関する考慮事項 {#considerations}

* When using the adaptive forms cache, use the AEM [!DNL Dispatcher] to cache client libraries (CSS and JavaScript) of an adaptive form.
* カスタムコンポーネントの開発時には、開発に使用されるサーバー上でアダプティブフォームのキャッシュを無効にしておく必要があります。
* 拡張子のないURLはキャッシュされません。 例えば、パターンパターンを持つURLはキャッシュされ`/content/forms/[folder-structure]/[form-name].html` 、パターンを持つURLはキャッシュされません `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`。 したがって、URLに拡張子を付けて使用すると、キャッシュの利点を活用できます。
* ローカライズされたアダプティブフォームの考慮事項：
   * URL形式を使用し `http://host:port/content/forms/af/<afName>.<locale>.html` て、アダプティブフォームのローカライズ版をリクエストし、 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [形式を指定したURLに対するブラウザーロケール](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) の使用を無効に `http://host:port/content/forms/af/<adaptivefName>.html`します。
   * URL形式を使用し、Configuration Manager `http://host:port/content/forms/af/<adaptivefName>.html`の「 **** ブラウザーロケールを使用」が無効になっている場合、アダプティブフォームのローカライズされていないバージョンが提供されます。 ローカライズされていない言語は、アダプティブフォームの開発時に使用される言語です。 ブラウザーに設定されているロケール（ブラウザーのロケール）は考慮されず、アダプティブフォームのローカライズされていないバージョンが提供されます。
   * 「URL形式を使用」を選択し、Configuration Manager `http://host:port/content/forms/af/<adaptivefName>.html`で「ブラウザーロケールを **** 使用」を有効にすると、ローカライズ版のアダプティブフォームが提供されます（使用可能な場合）。 ローカライズされたアダプティブフォームの言語は、ブラウザー（ブラウザーのロケール）に設定されたロケールに基づきます。 これにより、アダプティブフォームの最初のインスタンスの [みがキャッシュされる可能性があり]ます。 インスタンスで問題が発生しないようにするには、トラブルシューティングを参照して [ください](#only-first-insatnce-of-adptive-forms-is-cached)。

### ディスパッチャーでのキャッシュの有効化

ディスパッチャー上のアダプティブフォームのキャッシュを有効にし、設定するには、次の手順を実行します。

1. 環境の各発行インスタンスに対して次のURLを開き、複製エージェントを設定します。
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

   * アダプティブフォーム内で参照されている新しいバージョンのリソースが発行されると、影響を受けたアダプティブフォームは自動的に無効になります。 参照先リソースの自動無効化には、いくつかの例外があります。 例外の回避策については、 [トラブルシューティング](#troubleshooting) の節を参照してください。
1. [次追加のルールは、dispatcher.anyまたはカスタムルールファイル](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache)。 キャッシュをサポートしないURLは除外されます。 例えば、Interactive Communicationなどです。

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

AEM環境は、アダプティブフォームをキャッシュするように設定されています。 すべてのタイプのアダプティブフォームをキャッシュします。 キャッシュされたページを配信する前に、ページのユーザーアクセス権限を確認する必要がある場合は、セキュリティで保護されたコンテンツの [キャッシュを参照してください](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/permissions-cache.html)。

## トラブルシューティング {#troubleshooting}

### 画像やビデオを含む一部のアダプティブフォームは、ディスパッチャーのキャッシュから自動的に無効にされません {#videos-or-images-not-auto-invalidated}

#### 問題 {#issue1}

アセットブラウザを介して画像またはビデオを選択してアダプティブフォームに追加し、これらの画像およびビデオをアセットエディターで編集した場合、このような画像を含むアダプティブフォームは、自動的にディスパッチャーキャッシュから無効にされません。

#### 解決策 {#Solution1}

画像とビデオを公開した後、これらのアセットを参照するアダプティブフォームの公開を明示的に取り消し、公開を取り消します。

### コンテンツフラグメントまたはエクスペリエンスフラグメントを含むアダプティブフォームの一部は、ディスパッチャーのキャッシュから自動的に無効化されません {#content-or-experience-fragment-not-auto-invalidated}

#### 問題 {#issue2}

コンテンツフラグメントまたはエクスペリエンスフラグメントをアダプティブフォームに追加し、これらのアセットを個別に編集して発行すると、このようなアセットが含まれるアダプティブフォームは自動的にディスパッチャーキャッシュから無効になりません。

#### 解決策 {#Solution2}

更新されたコンテンツフラグメントまたはエクスペリエンスフラグメントの発行後、これらのアセットを使用するアダプティブフォームの公開を明示的に取り消し、発行します。

### アダプティブフォームの最初のインスタンスのみがキャッシュされます{#only-first-insatnce-of-adptive-forms-is-cached}

#### 問題 {#issue3}

アダプティブフォームURLにローカライゼーション情報がなく、Configuration Managerの「ブラウザーロケールを **** 使用」が有効な場合は、ローカライズされたバージョンのアダプティブフォームが提供され、アダプティブフォームの最初のインスタンスのみがキャッシュされ、後続のすべてのユーザーに配信されます。

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
