---
title: コンテンツフラグメントのヘッドレス作成のクイック開始ガイド
description: AEM のコンテンツフラグメントを使用して、ページに依存しないヘッドレス配信用コンテンツを設計、作成、キュレーションおよび使用する方法を説明します。
exl-id: 5787204d-bcce-447e-b98c-2bc1c0d744c3
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: a02b73a7-bdfc-4225-bdfd-69f7891ab55e
    internal-label: GraphQL
  - id: d781bc8f-52af-43f6-84d0-b73e59a130d5
    internal-label: Persisted queries
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 100%
---
# コンテンツフラグメントのヘッドレス作成のクイック開始ガイド {#creating-content-fragments}

AEM のコンテンツフラグメントを使用して、ページに依存しないヘッドレス配信用コンテンツを設計、作成、キュレーションおよび使用する方法を説明します。

## コンテンツフラグメントとは {#what-are-content-fragments}

コンテンツフラグメントを保存できる[アセットフォルダーを作成したので](create-assets-folder.md)、フラグメントを作成できるようになります。

コンテンツフラグメントを使用すると、ページに依存しないコンテンツの設計、作成、キュレーションおよび公開が可能になります。 複数の場所や複数のチャネルで使用可能なコンテンツを用意できるようになります。

コンテンツフラグメントには構造化コンテンツが含まれ、JSON 形式で配信できます。

## コンテンツフラグメントの作成方法 {#how-to-create-a-content-fragment}

コンテンツ作成者は、作成したコンテンツを表す任意の数のコンテンツフラグメントを作成します。 これが AEM での主なタスクとなります。 この「はじめる前に」ガイドの目的上、1 つだけ作成します。

1. AEM にログインし、メインメニューから、**ナビゲーション／アセット**&#x200B;を選択します。
1. 以前に作成した [ フォルダーに移動します。](create-assets-folder.md)
1. **作成／コンテンツフラグメント**&#x200B;をクリックします。
1. コンテンツフラグメントの作成は、2 つの手順でウィザードとして表示されます。 まず、コンテンツフラグメントの作成に使用するモデルを選択し、「**次へ**」をクリックします。
   * 使用できるモデルは、コンテンツフラグメントを作成する&#x200B;[**アセットフォルダーに対して定義した**&#x200B;クラウド設定](create-assets-folder.md)によって異なります。
   * `We could not find any models` というメッセージが表示された場合は、アセットフォルダーの設定を確認してください。

   ![コンテンツフラグメントモデルを選択](assets/content-fragment-model-select.png)
1. 必要に応じて、「**タイトル**」、「**説明**」、「**タグ**」を指定し、「**作成**」をクリックします。

   ![コンテンツフラグメントを作成](assets/content-fragment-create.png)
1. 確認ウィンドウで「**開く**」をクリックします。

   ![作成されたコンテンツフラグメントの確認](assets/content-fragment-confirmation.png)
1. コンテンツフラグメントエディターで、コンテンツフラグメントの詳細を指定します。

   ![コンテンツフラグメントエディター](assets/content-fragment-edit.png)
1. 「**保存**」または「**保存して閉じる**」をクリックします。

コンテンツフラグメントは他のコンテンツフラグメントを参照でき、必要に応じてネストされたコンテンツ構造を作成できます。

コンテンツフラグメントは、AEM 内の他のアセットを参照することもできます。 参照するコンテンツフラグメントを作成する前に、[これらのアセットを AEM に保存する必要があります](/help/assets/manage-assets.md)。

## 次の手順 {#next-steps}

コンテンツフラグメントを作成したら、「はじめる前に」ガイドの最後の部分に進み、[コンテンツフラグメントにアクセスして配信するための API リクエストを作成](create-api-request.md)できます。

>[!TIP]
>
>コンテンツフラグメントの管理について詳しくは、[コンテンツフラグメントのドキュメント](/help/assets/content-fragments/content-fragments.md)を参照してください。
