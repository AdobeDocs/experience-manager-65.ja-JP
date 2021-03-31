---
title: '[!DNL Assets] HTTP API。'
description: ' [!DNL Adobe Experience Manager Assets] の HTTP API を使用した、デジタルアセットの作成、読み取り、更新、削除、管理について説明します。'
contentOwner: AG
role: デベロッパー
feature: API，アセットHTTP API，開発者ツール
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 79%

---


# [!DNL Assets] HTTP API {#assets-http-api}

## 概要 {#overview}

[!DNL Assets] HTTP APIを使用すると、メタデータ、レンディション、コメントなどのデジタルアセットに対して、[!DNL Experience Manager]コンテンツフラグメントを使用して構造化されたコンテンツと共に、create-read-update-delete(CRUD)操作を実行できます。 この API は `/api/assets` で公開されており、REST API として実装されています。[コンテンツフラグメントをサポート](/help/assets/assets-api-content-fragments.md)しています。

この API にアクセスするには、次の手順を実行します。

1. API サービスドキュメント（`https://[hostname]:[port]/api.json`）を開きます。
1. `https://[hostname]:[server]/api/assets.json`に続く[!DNL Assets]サービスのリンクに従います。

API の応答は、一部の MIME タイプに対する JSON ファイル、およびすべての MIME タイプに対する応答コードです。JSON 応答はオプションであり、PDF ファイルなどでは利用できない場合があります。詳細な分析やアクションをおこなう場合は、応答コードを利用します。

[!UICONTROL オフタイム]の経過後、アセットとそのレンディションは、[!DNL Assets] Web インターフェイスでも HTTP API でも使用できません。[!UICONTROL オンタイム]が未来の場合、または[!UICONTROL オフタイム]が過去の場合、API は 404 エラーメッセージを返します。

>[!CAUTION]
>
>[HTTP APIは、](#update-asset-metadata) 名前空間内のメタデータ `jcr` プロパティを更新します。ただし、Experience Managerユーザーインターフェイスは、`dc`名前空間のメタデータプロパティを更新します。

## コンテンツフラグメント {#content-fragments}

[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)は特殊なタイプのアセットです。テキスト、数値、日付などの構造化データにアクセスするために使用できます。`standard` アセット（画像やドキュメントなど）とはいくつかの違いがあるので、コンテンツフラグメントの処理にはいくつかの追加ルールが適用されます。

詳しくは、[AEM Assets HTTP API でのコンテンツフラグメントのサポート](/help/assets/assets-api-content-fragments.md)を参照してください。

## データモデル {#data-model}

[!DNL Assets] HTTP APIは、（標準アセット用の）フォルダーとアセットの2つの主要な要素を公開します。

さらに、コンテンツフラグメント内の構造化コンテンツを記述するカスタムデータモデルに対する詳細な要素が公開されます。詳しくは、[コンテンツフラグメントのデータモデル](/help/assets/assets-api-content-fragments.md#content-fragments)を参照してください。

### フォルダー {#folders}

フォルダーは、従来のファイルシステムにおけるディレクトリに似ています。フォルダーは、他のフォルダーまたはアセットのコンテナです。フォルダーには、以下のコンポーネントがあります。

**エンティティ**：フォルダーのエンティティはフォルダーの子要素で、フォルダーまたはアセットです。

**プロパティ**：

* `name` はフォルダーの名前です。これは、URL パスの最後のセグメント（拡張子を除く）と同じです。
* `title` は名前の代わりに表示できるフォルダータイトル（オプション）です。

>[!NOTE]
>
>フォルダーまたはアセットの一部のプロパティは、異なるプレフィックスにマップされます。`jcr:title`、`jcr:description`、`jcr:language` の `jcr` プレフィックスは `dc` プレフィックスに置き換えられます。したがって、返された JSON コードで、`dc:title`、`dc:description` にはそれぞれ `jcr:title`、`jcr:description` の値が含まれています。

**リンク**&#x200B;フォルダーは、次の 3 つのリンクを公開します。

* `self`：自分自身へのリンク。
* `parent`：親フォルダーへのリンク。
* `thumbnail`：（オプション）フォルダーのサムネール画像へのリンク。

### Assets {#assets}

Experience Managerでは、アセットに次の要素が含まれます。

* アセットのプロパティとメタデータ
* オリジナルのレンディション（最初にアップロードされたアセット）、サムネール、その他の各種レンディションなど複数のレンディション。追加のレンディションには、様々なサイズの画像、ビデオエンコーディングの画像、PDFまたは[!DNL Adobe InDesign]ファイルから抽出したページなどがあります。
* コメント（オプション）

コンテンツフラグメントの要素については、[AEM Assets HTTP API でのコンテンツフラグメントのサポート](/help/assets/assets-api-content-fragments.md#content-fragments)を参照してください。

[!DNL Experience Manager] では、フォルダーには次のコンポーネントが含まれています。

* エンティティ：アセットの子はアセットのレンディションです。
* プロパティ
* リンク

[!DNL Assets] HTTP APIには次の機能が含まれています。

* [フォルダーのリストの取得](#retrieve-a-folder-listing).
* [フォルダーを作成](#create-a-folder)します。
* [アセットの作成](#create-an-asset).
* [アセットバイナリの更新](#update-asset-binary).
* [アセットメタデータの更新](#update-asset-metadata).
* [アセットレンディションの作成](#create-an-asset-rendition).
* [アセットレンディションの更新](#update-an-asset-rendition).
* [アセットコメントの作成](#create-an-asset-comment).
* [フォルダーまたはアセットのコピー](#copy-a-folder-or-asset).
* [フォルダーまたはアセットの移動](#move-a-folder-or-asset).
* [フォルダー、アセットまたはレンディションの削除](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>読みやすいように、以下の例では、すべての cURL 表記法を省略しています。実際には、この表記法は [Resty](https://github.com/micha/resty)（`cURL` 用のスクリプトラッパー）と関連があります。

**前提条件**

* `https://[aem_server]:[port]/system/console/configMgr` にアクセスします。
* **[!UICONTROL AdobeGranite CSRF Filter]**&#x200B;に移動します。
* **[!UICONTROL フィルターメソッド]**&#x200B;のプロパティに次の内容が含まれていることを確認します。`POST`、`PUT`、`DELETE`。

## フォルダーのリストの取得 {#retrieve-a-folder-listing}

既存のフォルダーとその子エンティティ（サブフォルダーまたはアセット）の Siren 表現を取得します。

**リクエスト**：`GET /api/assets/myFolder.json`

**応答コード**：応答コードは次のとおりです。

* 200 - OK（成功）
* 404 - NOT FOUND（フォルダーが存在しないかアクセスできない）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

**応答**：返されるエンティティのクラスはアセットまたはフォルダーです。含まれるエンティティのプロパティは、各エンティティの完全なプロパティセットのサブセットです。エンティティのすべての表現を取得するために、クライアントは `rel` が `self` となっているリンクで参照される URL のコンテンツを取得する必要があります。

## フォルダーの作成 {#create-a-folder}

指定されたパスに新しい `sling`:`OrderedFolder` を作成します。ノード名の代わりに「`*`」が指定されている場合、サーブレットパラメーター名がノード名として使用されます。リクエストデータとして受け入れられるのは、新しいフォルダーの Siren 表現か、`application/www-form-urlencoded` または `multipart`/`form`-`data` としてエンコードされた名前と値のペアのセットで、HTML フォームから直接フォルダーを作成するのに役立ちます。さらに、フォルダーのプロパティを URL クエリパラメーターとして指定できます。

指定されたパスの親ノードが存在しない場合、API 呼び出しは失敗し、応答コード `500` が返されます。フォルダーが既に存在する場合、呼び出しは応答コード `409` を返します。

**パラメーター**：`name` はフォルダー名です。

**リクエスト**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**応答コード**：応答コードは次のとおりです。

* 201 - CREATED（作成が成功した場合）
* 409 - CONFLICT（フォルダーが既に存在する場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## アセットの作成 {#create-an-asset}

指定されたファイルを指定されたパスに配置し、DAMリポジトリ内にアセットを作成します。 ノード名の代わりに`*`を指定した場合、サーブレットはパラメータ名またはファイル名をノード名として使用します。

**パラメータ**:パラメーターは、アセ `name` ット名とファイル参照 `file` 用のものです。

**リクエスト**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**応答コード**：応答コードは次のとおりです。

* 201 — 作成済み — アセットが正常に作成された場合。
* 409 - CONFLICT — アセットが既に存在する場合。
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## アセットバイナリの更新 {#update-asset-binary}

アセットのバイナリ（オリジナルの名前のレンディション）を更新します。 更新トリガーは、デフォルトのアセット処理ワークフローが設定されている場合、実行するワークフローを指定します。

**リクエスト**：`PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**応答コード**：応答コードは次のとおりです。

* 200 - OK（アセットが正常に更新された場合）
* 404 - NOT FOUND（指定した URI でアセットが見つからなかったかアクセスできなかった場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## アセットメタデータの更新 {#update-asset-metadata}

アセットのメタデータプロパティを更新します。 `dc:` 名前空間内のプロパティを更新すると、API は `jcr` 名前空間内の同じプロパティをアップデートします。API は 2 つの名前空間内のプロパティを同期させません。

**リクエスト**：`PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**応答コード**：応答コードは次のとおりです。

* 200 - OK（アセットが正常に更新された場合）
* 404 - NOT FOUND（指定した URI でアセットが見つからなかったかアクセスできなかった場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

### `dc`と`jcr`名前空間{#sync-metadata-between-namespaces}の間でメタデータを同期

APIメソッドは、`jcr`名前空間のメタデータプロパティを更新します。 ユーザーインターフェイスを使用して行った更新により、`dc`名前空間のメタデータプロパティが変更されます。 メタデータ値を`dc`と`jcr`名前空間の間で同期するには、ワークフローを作成し、アセット編集時にワークフローを実行するようにExperience Managerを設定します。 ECMAスクリプトを使用して、必要なメタデータプロパティを同期します。 次のサンプルスクリプトでは、`dc:title`と`jcr:title`の間でタイトル文字列を同期します。

```javascript
var workflowData = workItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH")
{
 var path = workflowData.getPayload().toString();
 var node = workflowSession.getSession().getItem(path);
 var metadataNode = node.getNode("jcr:content/metadata");
 var jcrcontentNode = node.getNode("jcr:content");
if (jcrcontentNode.hasProperty("jcr:title"))
{
 var jcrTitle = jcrcontentNode.getProperty("jcr:title");
 metadataNode.setProperty("dc:title", jcrTitle.toString());
 metadataNode.save();
}
}
```

## アセットレンディションの作成 {#create-an-asset-rendition}

アセットの新しいアセットレンディションを作成します。リクエストパラメーター名が指定されない場合、ファイル名がレンディション名として使用されます。

**パラメーター**：パラメーターは `name`（レンディションの名前）と `file`（ファイル参照）です。

**リクエスト**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**応答コード**：応答コードは次のとおりです。

* 201 - CREATED（レンディションが正常に作成された場合）
* 404 - NOT FOUND（指定した URI でアセットが見つからなかったかアクセスできなかった場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## アセットレンディションの更新 {#update-an-asset-rendition}

アセットレンディションをそれぞれ新しいバイナリデータで置き換えて更新します。

**リクエスト**：`PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**応答コード**：応答コードは次のとおりです。

* 200 - OK（レンディションが正常に更新された場合）
* 404 - NOT FOUND（指定した URI でアセットが見つからなかったかアクセスできなかった場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## アセットへのコメントの追加 {#create-an-asset-comment}

新しいアセットコメントを作成します。

**パラメーター**：パラメーターは `message`（コメントのメッセージ本文）と `annotationData`（JSON 形式の注釈データ）です。

**リクエスト**：`POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**応答コード**：応答コードは次のとおりです。

* 201 - CREATED（コメントが正常に作成された場合）
* 404 - NOT FOUND（指定した URI でアセットが見つからなかったかアクセスできなかった場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## フォルダーまたはアセットのコピー {#copy-a-folder-or-asset}

指定されたパスに存在するフォルダーまたはアセットを新しい宛先にコピーします。

**リクエストヘッダー**：パラメーターは次のとおりです。

* `X-Destination` - API ソリューション範囲内の、リソースのコピー先となる新しい宛先 URI
* `X-Depth` - `infinity` か `0` のいずれか。`0` を使用すると、リソースとそのプロパティのみがコピーされ、子はコピーされません。
* `X-Overwrite` - 既存の宛先にあるアセットが上書きされないようにするには、`F` を使用します。

**リクエスト**：`COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**応答コード**：応答コードは次のとおりです。

* 201 - CREATED（フォルダーやアセットが既存でない宛先にコピーされた場合）
* 204 - NO CONTENT（フォルダーまたはアセットが既存の宛先にコピーされた場合）
* 412 - PRECONDITION FAILED（リクエストヘッダーが不明な場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## フォルダーまたはアセットの移動 {#move-a-folder-or-asset}

指定されたパスのフォルダーまたはアセットを新しい宛先に移動します。

**リクエストヘッダー**：パラメーターは次のとおりです。

* `X-Destination` - API ソリューション範囲内の、リソースのコピー先となる新しい宛先 URI
* `X-Depth` - `infinity` か `0` のいずれか。`0` を使用すると、リソースとそのプロパティのみがコピーされ、子はコピーされません。
* `X-Overwrite` - 既存のリソースを強制的に削除する場合は `T` を、既存リソースの上書きを防ぐ場合は `F` を使用します。

**リクエスト**：`MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

URLに`/content/dam`を使用しないでください。 アセットを移動し、既存のアセットを上書きするサンプルコマンドは、次のとおりです。

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: http://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
```

**応答コード**：応答コードは次のとおりです。

* 201 - CREATED（フォルダーやアセットが既存でない宛先にコピーされた場合）
* 204 - NO CONTENT（フォルダーまたはアセットが既存の宛先にコピーされた場合）
* 412 - PRECONDITION FAILED（リクエストヘッダーが不明な場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## フォルダー、アセットまたはレンディションの削除 {#delete-a-folder-asset-or-rendition}

指定されたパスのリソース（ツリー）を削除します。

**リクエスト**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**応答コード**：応答コードは次のとおりです。

* 200 - OK（フォルダーが正常に削除された場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## ヒントと制限事項 {#tips-best-practices-limitations}

* [HTTP APIは、](#update-asset-metadata) 名前空間内のメタデータ `jcr` プロパティを更新します。ただし、Experience Managerユーザーインターフェイスは、`dc`名前空間のメタデータプロパティを更新します。

* アセットAPIは、完全なメタデータを返しません。 APIでは、名前空間はハードコードされ、それらのみが返されます。 メタデータ全体が必要な場合は、アセットのパス`/jcr_content/metadata.json`を確認します。
