---
title: コンテンツフラグメント - 設定ブラウザー
description: 設定ブラウザーで特定のコンテンツフラグメント機能を有効にして、Adobe Experience Managerの強力なヘッドレス配信機能を使用する方法を説明します。
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
source-git-commit: 2810e34f642f4643fa4dc24b31a57a68e9194e39
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 47%

---

# コンテンツフラグメント - 設定ブラウザー{#content-fragments-configuration-browser}

設定ブラウザーで特定のコンテンツフラグメント機能を有効にして、Adobe Experience Manager(AEM) の強力なヘッドレス配信機能を使用する方法を説明します。

## インスタンスに対するコンテンツフラグメント機能の有効化 {#enable-content-fragment-functionality-instance}

コンテンツフラグメントを使用する前に、 **設定ブラウザー** を有効にするには、次の手順を実行します。

* **コンテンツフラグメントモデル** - 必須
* **GraphQL の永続的なクエリ** - オプション

>[!CAUTION]
>
>**コンテンツフラグメントモデル**&#x200B;を有効にしない場合：
>
>* の **作成** オプションは、モデルの作成には使用できません。
>* できません [Sites 設定を選択して関連するエンドポイントを作成します](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint).

コンテンツフラグメント機能を有効にするには、次の操作を行う必要があります。

* 設定ブラウザーを使用してコンテンツフラグメント機能の使用を有効にする
* アセットフォルダーへの設定の適用

### 設定ブラウザーでコンテンツフラグメント機能を有効にする {#enable-content-fragment-functionality-in-configuration-browser}

宛先 [特定のコンテンツフラグメント機能の使用](#creating-a-content-fragment-model)、 **必須** 最初に **設定ブラウザー**:

>[!NOTE]
>
>詳しくは、 [設定ブラウザ：](/help/sites-administering/configurations.md#using-configuration-browser).

1. **ツール**／**一般**&#x200B;に移動し、**設定ブラウザー**&#x200B;を開きます。

1. 「**作成**」を使用してダイアログを開き、次の操作を行います。

   1. 「**タイトル**」を指定します。
   1. 使用できるようにするには、以下を選択します。
      * **コンテンツフラグメントモデル**
      * **GraphQL の永続的なクエリ**

      ![設定の定義](assets/cfm-conf-01.png)

1. 「**作成**」を選択して、定義を保存します。

<!-- 1. Select the location appropriate to your website. -->

### アセットフォルダーへの設定の適用 {#apply-the-configuration-to-your-assets-folder}

「**グローバル**」がコンテンツフラグメント機能に対して有効になっている場合、設定はすべてのアセットフォルダーに適用されます。

他の設定（グローバルを除く）を同等の Assets フォルダーで使用するには、接続を定義する必要があります。 そのためには、適切なフォルダーの「**フォルダーのプロパティ**」の「**クラウドサービス**」タブで「**設定**」を適切に選択します。

![設定の適用](assets/cfm-conf-02.png)
