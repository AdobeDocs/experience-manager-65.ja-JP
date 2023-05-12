---
title: "[!DNL Assets] HTTP API."
description: ' [!DNL Adobe Experience Manager Assets] の HTTP API を使用した、デジタルアセットの作成、読み取り、更新、削除、管理について説明します。'
contentOwner: AG
role: Developer
feature: APIs,Assets HTTP API,Developer Tools
exl-id: 6bc10f4e-a951-49ba-9c71-f568a7f2e40d
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1746'
ht-degree: 97%

---

# [!DNL Assets] HTTP API {#assets-http-api}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets.html?lang=ja) |
| AEM 6.5 | この記事 |

## 概要 {#overview}

[!DNL Assets] HTTP API を使用すれば、デジタルアセット（メタデータ、レンディション、コメントのほか、[!DNL Experience Manager] コンテンツフラグメントを使用した構造化コンテンツも含む）に対して作成、読み取り、更新、削除（CRUD）操作を実行できます。この API は `/api/assets` で公開されており、REST API として実装されています。これには以下が含まれます。 [コンテンツフラグメントのサポート](/help/assets/assets-api-content-fragments.md).

API にアクセスするには：

1. API サービスドキュメント（`https://[hostname]:[port]/api.json`）を開きます。
1. `https://[hostname]:[server]/api/assets.json` への [!DNL Assets] サービスリンクをクリックします。

API の応答は、一部の MIME タイプに対する JSON ファイル、およびすべての MIME タイプに対する応答コードです。JSON 応答はオプションで、PDFファイルなどは使用できない場合があります。 詳細な分析やアクションを行う場合は、応答コードを利用します。

[!UICONTROL オフタイム]の経過後、アセットとそのレンディションは、[!DNL Assets] Web インターフェイスでも HTTP API でも使用できません。[!UICONTROL オンタイム]が未来の場合、または[!UICONTROL オフタイム]が過去の場合、API は 404 エラーメッセージを返します。

>[!CAUTION]
>
>`jcr` 名前空間内で [HTTP API がメタデータのプロパティを更新します](#update-asset-metadata)。ただし、Experience Managerユーザーインターフェイスは、 `dc` 名前空間のメタデータプロパティを更新します。

## コンテンツフラグメント {#content-fragments}

[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)は特殊なタイプのアセットです。テキスト、数値、日付などの構造化データにアクセスするために使用できます。`standard` アセット（画像やドキュメントなど）とはいくつかの違いがあるので、コンテンツフラグメントの処理にはいくつかの追加ルールが適用されます。

詳しくは、[AEM Assets HTTP API でのコンテンツフラグメントのサポート](/help/assets/assets-api-content-fragments.md)を参照してください。

## データモデル {#data-model}

[!DNL Assets] HTTP API は、フォルダーとアセット（標準アセット用）という 2 つの主要要素を公開します。

さらに、コンテンツフラグメント内の構造化コンテンツを記述するカスタムデータモデルの詳細な要素が公開されます。詳しくは、 [コンテンツフラグメントデータモデル](/help/assets/assets-api-content-fragments.md#content-fragments) を参照してください。

### フォルダー {#folders}

フォルダーは、従来のファイルシステムにおけるディレクトリに似ています。これらは、他のフォルダーやアサートのコンテナです。 フォルダーには、以下のコンポーネントがあります。

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

Experience Manager では、アセットに次の要素が含まれています。

* アセットのプロパティとメタデータ
* オリジナルのレンディション（最初にアップロードされたアセット）、サムネール、その他の各種レンディションなど複数のレンディション。追加レンディションは、サイズやビデオエンコーディングの異なる画像や、PDF ファイルまたは [!DNL Adobe InDesign] ファイルから抽出されたページの場合があります。
* コメント（オプション）

コンテンツフラグメントの要素については、[AEM Assets HTTP API でのコンテンツフラグメントのサポート](/help/assets/assets-api-content-fragments.md#content-fragments)を参照してください。

[!DNL Experience Manager] では、フォルダーには次のコンポーネントが含まれています。

* エンティティ：アセットの子はアセットのレンディションです。
* プロパティ
* リンク

[!DNL Assets] HTTP API には、以下の機能が含まれます。

* [フォルダーリストの取得](#retrieve-a-folder-listing)。
* [フォルダーの作成](#create-a-folder)。
* [アセットを作成します](#create-an-asset)。
* [アセットバイナリを更新します](#update-asset-binary)。
* [アセットメタデータの更新](#update-asset-metadata)。
* [アセットレンディションの作成](#create-an-asset-rendition)。
* [アセットレンディションの更新](#update-an-asset-rendition)。
* [アセットコメントの作成](#create-an-asset-comment)。
* [フォルダーまたはアセットのコピー](#copy-a-folder-or-asset)。
* [フォルダーまたはアセットの移動](#move-a-folder-or-asset)。
* [フォルダー、アセットまたはレンディションの削除](#delete-a-folder-asset-or-rendition)。

>[!NOTE]
>
>読みやすいように、以下の例では、すべての cURL 表記法を省略しています。実際には、この表記法は [Resty](https://github.com/micha/resty)（`cURL` 用のスクリプトラッパー）と関連があります。

**前提条件**

* `https://[aem_server]:[port]/system/console/configMgr` にアクセスします。
* **[!UICONTROL Adobe Granite CSRF フィルター]**&#x200B;に移動します。
* プロパティの&#x200B;**[!UICONTROL フィルターメソッド]**&#x200B;に `POST`、`PUT`、`DELETE` が含まれることを確認します。

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

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"jcr:title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"jcr:title=My Folder"`

**応答コード**：応答コードは次のとおりです。

* 201 - CREATED（作成が成功した場合）
* 409 - CONFLICT（フォルダーが既に存在する場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## アセットの作成 {#create-an-asset}

指定されたファイルを指定されたパスに配置して、DAM リポジトリ内にアセットを作成します。ノード名の代わりに「`*`」が指定されている場合、サーブレットはパラメーター名またはファイル名をノード名として使用します。

**パラメーター**：パラメーターは `name` （アセット名）と `file`（ファイルの参照）です。

**リクエスト**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**応答コード**：応答コードは次のとおりです。

* 201 - CREATED（コメントが正常に作成された場合）
* 409 - CONFLICT（アセットが既に存在する場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## アセットバイナリの更新 {#update-asset-binary}

アセットバイナリ（オリジナル名のレンディション）を更新します。「更新」トリガーは、デフォルトのアセット処理ワークフローが設定されている場合に実行します。

**リクエスト**：`PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**応答コード**：応答コードは次のとおりです。

* 200 - OK（アセットが正常に更新された場合）
* 404 - NOT FOUND（指定した URI でアセットが見つからなかったかアクセスできなかった場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

## アセットメタデータの更新 {#update-asset-metadata}

アセットメタデータのプロパティを更新します。`dc:` 名前空間内のプロパティを更新すると、API は `jcr` 名前空間内の同じプロパティをアップデートします。API は 2 つの名前空間内のプロパティを同期させません。

**リクエスト**：`PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**応答コード**：応答コードは次のとおりです。

* 200 - OK（アセットが正常に更新された場合）
* 404 - NOT FOUND（指定した URI でアセットが見つからなかったかアクセスできなかった場合）
* 412 - PRECONDITION FAILED（ルートコレクションが見つからないかアクセスできない場合）
* 500 - INTERNAL SERVER ERROR（他に問題がある場合）

### メタデータの更新を `dc` と `jcr` 名前空間の間で同期する {#sync-metadata-between-namespaces}

API メソッドは、`jcr` 名前空間のメタデータプロパティを更新します。ユーザーインターフェイスを使用しておこなった更新により、 `dc` 名前空間のメタデータプロパティが変更されます。  `dc` と `jcr` 名前空間の間でメタデータ値を同期するには、アセットの編集時に Experience Manager を実行するようにワークフローを作成してワークフローを設定できます。ECMA スクリプトを使用して、必要なメタデータプロパティを同期します。次のサンプルスクリプトは、 `dc:title` と `jcr:title` 間でタイトル文字列を同期します。

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

URL で `/content/dam` を使用しないでください。次に、アセットを移動して既存のアセットを上書きするコマンドの例を示します。

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: https://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
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

*  `jcr` 名前空間では [HTTP API がメタデータのプロパティを更新します](#update-asset-metadata)。ただし、Experience Manager ユーザーインターフェイスは、 `dc` 名前空間のメタデータプロパティを更新します。

* Assets HTTP API は完全なメタデータを返しません。名前空間はハードコードされ、これらの名前空間のみが返されます。完全なメタデータについては、アセットパス `/jcr_content/metadata.json` を参照してください。
