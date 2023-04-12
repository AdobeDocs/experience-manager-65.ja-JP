---
title: WebDAV アクセス
seo-title: WebDAV Access
description: AEMでの WebDAV アクセスについて説明します。
seo-description: Learn about WebDAV access in AEM.
uuid: b0ecaa5d-5454-42df-8453-404ece734c32
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 1eaf7afe-a181-45df-8766-bd564b1ad22a
exl-id: 891ee66c-e49c-4561-8fef-e6e448a8aa1c
source-git-commit: e05f6cd7cf17f4420176cf76f28cb469bcee4a0a
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 49%

---

# WebDAV アクセス{#webdav-access}

KDE で WebDAV 経由でAEMに接続するには：

AEMでは、リポジトリのコンテンツを表示および編集できる WebDAV をサポートしています。 WebDAV を使用して接続すると、デスクトップからコンテンツリポジトリに直接アクセスできます。 WebDAV 接続を通じてリポジトリに追加されるテキストおよびPDFファイルは、自動的にフルテキストインデックスが作成され、標準の検索インターフェイスおよび標準の Java™ API を使用して検索できます。

## 一般 {#general}

[オペレーティングシステムごとの詳細な手順](/help/sites-administering/webdav-access.md#connecting-via-webdav) はこのドキュメントに含まれていますが、基本的には WebDAV プロトコルを使用してリポジトリに接続する場合、WebDAV クライアントで次の場所を指すようにします。

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
>WebDAV を設定する前に、 [技術要件](/help/sites-deploying/technical-requirements.md#webdav-clients).

## WebDAV URL {#webdav-urls}

WebDAV サーバーの URL の構造は次のとおりです。

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

[前述のとおり](/help/sites-administering/webdav-access.md#general)、WebDAV プロトコルを使用してリポジトリに接続する場合は、WebDAV クライアントからリポジトリの場所を参照してください。ただし、OS によっては、クライアントとの接続に伴う手順が異なり、OS の設定が必要になる場合があります。

次のオペレーティングシステムの接続方法に関する手順が記載されています。

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

Microsoft® Windows 7 以降のシステムを、SSL で保護されていないAEMインスタンスに正常に接続するには、セキュリティで保護されていないネットワークを介して基本認証を確立するオプションを Windows で明示的に有効にする必要があります。 この機能を使用するには、WebClient の Windows レジストリを変更する必要があります。

レジストリが更新されると、AEMインスタンスをドライブとしてマッピングできます。

#### Windows 7 以降の設定 {#windows-and-greater-configuration}

セキュリティで保護されていないネットワークを介した基本認証を許可するようにレジストリを更新するには、次の手順に従います。

1. 次のレジストリサブキーを探します。

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. `BasicAuthLevel` レジストリエントリのサブキーの値を `2` 以上に設定します。

   存在しない場合は、サブキーを追加します。

1. レジストリの変更を有効にするには、システムを再起動します。

>[!NOTE]
>
>Adobeでは、リポジトリユーザーと同じ資格情報を持つ Windows ユーザーを作成することをお勧めします。作成しない場合は、権限の競合が発生する場合があります。

#### Windows 8 の設定 {#windows-configuration}

Windows 8 の場合、レジストリエントリを変更します。 [Windows 7 以降の場合の説明](/help/sites-administering/webdav-access.md#windows-and-greater-configuration). ただし、このタスクを実行する前に、レジストリエントリを表示するためにデスクトップエクスペリエンスを有効にする必要があります。

デスクトップエクスペリエンスを有効にするには、**サーバーマネージャー**、**機能**、**機能の追加**、**デスクトップエクスペリエンス**&#x200B;の順に開きます。

再起動後、Windows 7 以降に関するレジストリエントリを使用できます。 Windows 7 以降の場合の説明に従って変更します。

#### Windows での接続 {#connecting-in-windows}

Windows 環境で WebDAV 経由でAEMに接続するには：

1. 開く **Windows エクスプローラ** または **エクスプローラ** をクリックし、 **コンピュータ** または **この PC**.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. ウィザードを起動するには、 **ネットワークドライブをマッピング**.
1. マッピングの詳細を入力します。

   * **ドライブ**:使用可能な任意のレターを選択
   * **フォルダー**：`http://localhost:4502`
   * チェック **別の資格情報を使用して接続**

   完了をクリックします。

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >AEMが別のポートにある場合は、4502 ではなくそのポート番号を使用します。 また、コンテンツリポジトリをローカルマシンで実行していない場合は、`localhost` を該当するサーバー名または IP アドレスに置き換えてください。

1. ユーザー名 `admin` とパスワード `admin` を入力します。あらかじめ設定されている管理者アカウントを使用してテストすることをお勧めします。

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. ウィザードが閉じ、新しくマッピングしたドライブが Windows エクスプローラまたはエクスプローラウィンドウで開きます。

   ![chlimage_1-115](assets/chlimage_1-115a.png)

AEMは WebDAV を介してドライブとしてマッピングされ、他のドライブとして使用できるようになりました。

### macOS {#macos}

macOSで WebDAV を介して接続するために必要な設定手順はありません。 WebDAV サーバーに接続できます。

1. 任意の **Finder** ウィンドウに移動して&#x200B;**移動**&#x200B;と&#x200B;**サーバへ接続**&#x200B;をクリックするか、**Command + K** キーを押してください。
1. **サーバへ接続**&#x200B;ウィンドウで、AEM の場所を入力します。

   * `http://localhost:4502`
   >[!NOTE]
   >
   >AEMが別のポートにある場合は、4502 ではなくそのポート番号を使用します。 また、コンテンツリポジトリをローカルマシンで実行していない場合は、`localhost` を該当するサーバー名または IP アドレスに置き換えてください。

1. 認証を要求する画面が表示されたら、ユーザー名に `admin`、パスワードに `admin` と入力してください。あらかじめ設定されている管理者アカウントを使用してテストすることをお勧めします。

macOSは WebDAV を介してAEMに接続し、Mac上の他のフォルダーとして使用できます。

### Linux® {#linux}

Linux®で WebDAV を介して接続する場合は、設定は必要ありませんが、接続を確立する手順はデスクトップ環境によって異なります。

#### GNOME {#gnome}

GNOME で WebDAV 経由でAEMに接続するには：

1. Nautilus （ファイルエクスプローラ）で、 **場所** を選択し、 **サーバーに接続**.
1. **サーバーへ接続**&#x200B;ウィンドウの「サービスのタイプ」で「WebDAV (HTTP)」を選択します。

1. **サーバー**&#x200B;で、`http://localhost:4502/crx/repository/crx.default` と入力します。

   >[!NOTE]
   >
   >AEMが別のポートにある場合は、4502 ではなくそのポート番号を使用します。 また、コンテンツリポジトリをローカルマシンで実行していない場合は、`localhost` を該当するサーバー名または IP アドレスに置き換えてください。

1. **フォルダー**&#x200B;で、`/dav` と入力します
1. ユーザー名に `admin` と入力します。あらかじめ設定されている管理者アカウントを使用してテストすることをお勧めします。
1. ポートは空白のままにして、接続用の名前を入力します。
1. **接続**&#x200B;をクリックします。パスワードを要求する画面が表示されます。
1. パスワードに `admin` と入力し、**接続**&#x200B;をクリックしてください。

以上で、AEM が GNOME のボリュームとしてマウントされ、他のボリュームと同じように使用できるようになります。

#### KDE {#kde}

1. [ ネットワークフォルダ ] ウィザードを開きます。
1. **Web フォルダー**（webdav）を選択して「次へ」をクリックしてください。
1. **名前**&#x200B;に接続名を入力します。
1. **ユーザー**&#x200B;に、`admin.` と入力します。アドビでは、事前設定済みの管理者アカウントを使用することをお勧めします。
1. **サーバー**&#x200B;に、`http://localhost:4502/crx/repository/crx.default` と入力します

   >[!NOTE]
   >
   >AEMが別のポートにある場合は、4502 ではなくそのポート番号を使用します。 また、コンテンツリポジトリをローカルマシンで実行していない場合は、`localhost` を該当するサーバー名または IP アドレスに置き換えてください。

1. **フォルダー**&#x200B;に、`dav` と入力します。

1. 「**保存と接続**」をクリックします。
1. パスワードを要求する画面が表示されたら、パスワードに `admin` と入力し、**接続**&#x200B;をクリックしてください。

以上で、AEM が KDE のボリュームとしてマウントされ、他のボリュームと同じように使用できるようになります。
