---
title: WebDAV アクセス
description: WebDAV を使用して Adobe Experience Manager にアクセスする方法について説明します。
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
exl-id: 891ee66c-e49c-4561-8fef-e6e448a8aa1c
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 100%

---

# WebDAV アクセス{#webdav-access}

KDE を使用して WebDAV を介して AEM に接続するには：

AEM では、WebDAV がサポートされており、WebDAV を使用してリポジトリコンテンツを表示および編集できます。WebDAV を介して接続すると、デスクトップからコンテンツリポジトリに直接アクセスできるようになります。WebDAV 接続を使用してテキストファイルや PDF ファイルをリポジトリに追加すると、自動的にそのファイルの全文インデックスが作成され、通常の検索インターフェイスや標準的な Java™ API を使用して検索できるようになります。

## 一般 {#general}

このドキュメントでは、[各オペレーティングシステムでの詳細な手順](/help/sites-administering/webdav-access.md#connecting-via-webdav)について説明していますが、基本的に、WebDAV プロトコルを使用してリポジトリに接続するには、WebDAV クライアントの接続先を以下の場所に指定します。

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

この URL にオペレーティングシステムレベルで接続した場合には、WebDAV からデフォルトワークスペース（`crx.default`）にアクセスすることになります。ユーザーにとっては簡単ですが、この場合、[WebDAV の URL](/help/sites-administering/webdav-access.md#webdav-urls) を追加で指定してワークスペース名を柔軟に指定することはできません。

AEM ではリポジトリコンテンツが以下のように表示されます。

* タイプ `nt:folder` のノードはフォルダーとして表示されます。`nt:folder` ノード以下のノードがフォルダーコンテンツとして表示されます。

* タイプ `nt:file` のノードはファイルとして表示されます。`nt:file` ノード以下のノードは表示されませんが、ファイルのコンテンツを形成します。

WebDAV を使用してフォルダーやファイルを作成および編集すると、AEM は必要な `nt:folder` および `nt:file` ノードを作成し編集します。WebDAV を使用してコンテンツのインポートとエクスポートを行う場合は、 `nt:file` および `nt:folder` ノードのタイプをできるだけ使用するようにしてください。

>[!NOTE]
>
>WebDAV を設定する前に、[技術要件](/help/sites-deploying/technical-requirements.md#webdav-clients)を確認してください。

## WebDAV の URL {#webdav-urls}

WebDAV サーバーの URL の構造は以下のとおりです。

<table>
 <colgroup>
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
 </colgroup>
 <tbody>
  <tr>
   <td>
    <code>
     <strong>URL Component</strong>
    </code></td>
   <td><code>https://&lt;host&gt;:&lt;port&gt;</code></td>
   <td><code>/&lt;crx-webapp-path&gt;</code></td>
   <td><code>/repository</code></td>
   <td><code>/&lt;workspace&gt;</code></td>
  </tr>
  <tr>
   <td>
    <code>
     <strong>Example</strong>
    </code></td>
   <td><code>http://localhost:4502</code></td>
   <td><code>/crx</code></td>
   <td><code>/repository</code></td>
   <td><code>/crx.default</code></td>
  </tr>
  <tr>
   <td><strong>説明</strong></td>
   <td>AEM を実行しているホストおよびポート</td>
   <td>AEM リポジトリ Web アプリケーションのパス</td>
   <td>WebDAV サーブレットのマッピング先のパス</td>
   <td>ワークスペースの名前</td>
  </tr>
 </tbody>
</table>

パスのワークスペース要素を変更することによって、デフォルト（`crx.default`）以外のワークスペースをマッピングできます。例えば、`staging` というワークスペースをマッピングするには、次の URL を使用します。

```xml
http://localhost:4502/crx/repository/staging
```

## WebDAV を介した接続 {#connecting-via-webdav}

[前述のとおり](/help/sites-administering/webdav-access.md#general)、WebDAV プロトコルを使用してリポジトリに接続する場合は、WebDAV クライアントからリポジトリの場所を参照してください。ただし、クライアントを接続するための手順は OS によって異なり、場合によっては OS の設定が必要になることもあります。

ここでは、次のオペレーティングシステムを接続する方法について説明します。

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

SSL で保護されていない AEM インスタンスに Microsoft® Windows 7（以降）システムを正常に接続するには、保護されていないネットワーク上で基本認証を確立するためのオプションを Windows で明示的に有効にする必要があります。これには、WebClient の Windows レジストリの変更が必要です。

レジストリの更新後、AEM インスタンスをドライブとしてマッピングできます。

#### Windows 7 以降の設定 {#windows-and-greater-configuration}

保護されていないネットワーク上での基本認証を許可するようにレジストリを更新するには：

1. 次のレジストリのサブキーを探します。

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. `BasicAuthLevel` レジストリエントリのサブキーの値を `2` 以上に設定します。

   サブキーが存在しない場合は追加します。

1. レジストリの変更を有効にするには、システムを再起動します。

>[!NOTE]
>
>リポジトリユーザーと同じ資格情報を持つ Windows ユーザーを作成することをお勧めします。そうしないと、権限の競合が発生する可能性があります。

#### Windows 8 の設定 {#windows-configuration}

Windows 8 でも、[Windows 7 以降の場合](/help/sites-administering/webdav-access.md#windows-and-greater-configuration)と同様に、レジストリエントリを変更します。ただし、事前にデスクトップエクスペリエンスを有効にして、レジストリエントリが表示されるようにする必要があります。

デスクトップエクスペリエンスを有効にするには、**サーバーマネージャー**、**機能**、**機能の追加**、**デスクトップエクスペリエンス**&#x200B;の順に開きます。

再起動すると、Windows 7 以降の場合で説明したレジストリエントリが使用可能になります。変更方法は Windows 7 以降の場合と同じです。

#### Windows での接続 {#connecting-in-windows}

Windows 環境で WebDAV を介して AEM に接続するには：

1. **Windows エクスプローラー**&#x200B;または&#x200B;**ファイルエクスプローラー**&#x200B;を開き、「**コンピューター**」または「**PC**」をクリックします。

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. ウィザードを起動するには、「**ネットワークドライブの割り当て**」をクリックします。
1. 割り当ての詳細を入力します。

   * **ドライブ**：使用可能な任意の文字を選択
   * **フォルダー**：`http://localhost:4502`
   * 「**別の資格情報を使用して接続する**」をオン

   「完了」をクリックします。

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >AEM が別のポートにある場合は、4502 の代わりにそのポート番号を使用してください。また、コンテンツリポジトリをローカルマシンで実行していない場合は、`localhost` を該当するサーバー名または IP アドレスに置き換えてください。

1. ユーザー名 `admin` とパスワード `admin` を入力します。あらかじめ設定されている管理者アカウントを使用してテストすることをお勧めします。

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. ウィザードが閉じ、新規に割り当てられたドライブが Windows エクスプローラーまたはファイルエクスプローラーのウィンドウで開きます。

   ![chlimage_1-115](assets/chlimage_1-115a.png)

以上で、WebDAV を介して AEM が Windows のドライブとして割り当てられ、他のドライブと同じように使用できるようになります。

### macOS {#macos}

macOS では、WebDAV を介して接続するために必要な設定手順は特にありません。WebDAV サーバーに接続できます。

1. 任意の **Finder** ウィンドウに移動して&#x200B;**移動**&#x200B;と&#x200B;**サーバへ接続**&#x200B;をクリックするか、**Command + K** キーを押してください。
1. **サーバへ接続**&#x200B;ウィンドウで、AEM の場所を入力します。

   * `http://localhost:4502`

   >[!NOTE]
   >
   >AEM が別のポートにある場合は、4502 の代わりにそのポート番号を使用してください。また、コンテンツリポジトリをローカルマシンで実行していない場合は、`localhost` を該当するサーバー名または IP アドレスに置き換えてください。

1. 認証を要求する画面が表示されたら、ユーザー名に `admin`、パスワードに `admin` と入力してください。あらかじめ設定されている管理者アカウントを使用してテストすることをお勧めします。

以上で、WebDAV を介して AEM に接続され、Mac 上の他のフォルダーと同じように使用できるようになります。

### Linux® {#linux}

Linux® では、WebDAV を介して接続するために必要な設定は特にありませんが、接続を確立するためにいくつかの手順が必要になり、デスクトップ環境によって手順が異なります。

#### GNOME {#gnome}

GNOME を使用して WebDAV を介して AEM に接続するには：

1. Nautilus（ファイルエクスプローラー）で、「**場所**」を選択し、「**サーバーへ接続**」を選択します。
1. **サーバーへ接続**&#x200B;ウィンドウの「サービスのタイプ」で「WebDAV (HTTP)」を選択します。

1. **サーバー**&#x200B;で、`http://localhost:4502/crx/repository/crx.default` と入力します。

   >[!NOTE]
   >
   >AEM が別のポートにある場合は、4502 の代わりにそのポート番号を使用してください。また、コンテンツリポジトリをローカルマシンで実行していない場合は、`localhost` を該当するサーバー名または IP アドレスに置き換えてください。

1. **フォルダー**&#x200B;で、`/dav` と入力します
1. ユーザー名に `admin` と入力します。あらかじめ設定されている管理者アカウントを使用してテストすることをお勧めします。
1. ポートは空白のままにして、接続用の名前を入力します。
1. 「**接続**」をクリックします。パスワードを要求する画面が表示されます。
1. パスワードに `admin` と入力し、**接続**&#x200B;をクリックしてください。

以上で、AEM が GNOME のボリュームとしてマウントされ、他のボリュームと同じように使用できるようになります。

#### KDE {#kde}

1. ネットワークフォルダーウィザードを開きます。
1. **Web フォルダー**（webdav）を選択して「次へ」をクリックしてください。
1. **名前**&#x200B;に接続名を入力します。
1. **ユーザー**&#x200B;に、`admin.` と入力します。アドビでは、事前設定済みの管理者アカウントを使用することをお勧めします。
1. **サーバー**&#x200B;に、`http://localhost:4502/crx/repository/crx.default` と入力します

   >[!NOTE]
   >
   >AEM が別のポートにある場合は、4502 の代わりにそのポート番号を使用してください。また、コンテンツリポジトリをローカルマシンで実行していない場合は、`localhost` を該当するサーバー名または IP アドレスに置き換えてください。

1. **フォルダー**&#x200B;に、`dav` と入力します。

1. 「**保存と接続**」をクリックします。
1. パスワードを要求する画面が表示されたら、パスワードに `admin` と入力し、**接続**&#x200B;をクリックしてください。

以上で、AEM が KDE のボリュームとしてマウントされ、他のボリュームと同じように使用できるようになります。
