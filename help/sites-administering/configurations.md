---
title: 設定と設定ブラウザー
description: AEM 設定と、AEM でのワークスペース設定の管理方法について理解します。
exl-id: 1be5849b-748c-48e8-afa8-35a9026c27b3
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: ht
source-wordcount: '1472'
ht-degree: 100%

---

# 設定と設定ブラウザー {#configuration-browser}

AEM 設定は、AEM の設定を管理し、ワークスペースとして機能します。

## 設定とは  {#what-is-a-configuration}

設定には、2 つの異なる観点があります。

* [管理者](#configurations-administrator)は、設定グループを定義および管理するために、AEM 内のワークスペースとして AEM の設定を使用します。
* [デベロッパー](#configurations-developer)は、AEM の設定を保持および参照するための設定を実装する基本的な設定メカニズムを使用します。

まとめ：管理者の観点からの設定とは、AEM で設定を管理するワークスペースの作成方法を指します。一方、デベロッパーは、AEM がリポジトリー内でこれらの設定を使用および管理する方法を理解する必要があります。

設定は、上記の観点に関係なく、AEM で 2 つの主な目的を果たします。

* 設定により、特定のユーザーグループに対して特定の機能が有効になります。
* 設定によって、これらの機能のアクセス権が定義されます。

## 管理者にとっての設定 {#configurations-administrator}

AEM 管理者と作成者は、設定をワークスペースとして見なすことができます。ワークスペースを使用すると、機能にアクセス権を実装することで、組織の目的のために設定グループや関連するコンテンツを収集できます。

設定は、AEM 内の多くの異なる機能に対して作成できます。

* [クラウド設定](/help/sites-administering/configurations.md)
* [ContextHub セグメント](/help/sites-administering/segmentation.md)
* [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)
* [編集可能なテンプレート](/help/sites-authoring/templates.md)

### 例 {#administrator-example}

例えば、管理者は編集可能なテンプレートの 2 つの設定を作成できます。

* WKND-General
* WKND-Magazine

WKND-General の設定を使用して一般的なページテンプレートを作成し、WKND-Magazine の設定で雑誌専用のテンプレートを作成できます。

WKND-General を WKND サイトのすべてのコンテンツに関連付けることができますが、WKND-Magazine は、雑誌サイトにのみ関連付けられます。

これににより、次のことができます。

* 見開きのページを作成する際、コンテンツ作成者は一般テンプレート（WKND-General）または見開きテンプレート（WKND-Magazine）から選択できます。
* 見開き以外のサイトの別の部分に対してページを作成する場合は、一般テンプレート（WKND-General）のみを選択できます。

編集可能なテンプレートだけでなく、クラウド設定、ContextHub セグメント、コンテンツフラグメントモデルに対しても同様の設定が可能です。

### 設定ブラウザーの使用 {#using-configuration-browser}

設定ブラウザーを使用すると、管理者は AEM 設定に対するアクセス権を簡単に作成、管理、設定できます。

>[!NOTE]
>
>ユーザーに `admin` 権限がある場合にのみ、設定ブラウザーを使用して設定を作成できます。アクセス権を設定に割り当てたり、設定を変更したりする場合には、管理者権限も必要です。

#### 設定の作成 {#creating-a-configuration}

設定ブラウザーを使用すると、AEM で設定を簡単に作成できます。

1. AEM as a Cloud Service にログインし、メインメニューで&#x200B;**ツール**／**一般**／**設定ブラウザー**&#x200B;を選択します。
1. 「**作成**」をクリックします。
1. 設定に&#x200B;**タイトル**&#x200B;と&#x200B;**名前**&#x200B;を指定します。

   ![設定の作成](assets/configuration-create.png)

   * **タイトル**&#x200B;は内容がわかるように付けます。
   * **名前**&#x200B;はリポジトリ内のノード名になります。
      * タイトルに基づいて自動的に生成され、[AEM の命名規則](/help/sites-developing/naming-conventions.md)に従って調整されます。
      * 必要に応じて調整できます。
1. 許可する設定のタイプを確認します。
   * [クラウド設定](/help/sites-administering/configurations.md)
   * [ContextHub セグメント](/help/sites-administering/segmentation.md)
   * [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)
   * [編集可能なテンプレート](/help/sites-authoring/templates.md)
1. 「**作成**」をクリックします。

>[!TIP]
>
>設定は入れ子にできます。

#### 設定とそのアクセス権の編集 {#access-rights}

設定をワークスペースと考える場合、これらの設定にアクセス権を設定して、それらのワークスペースにアクセスできるユーザーとアクセスできないユーザーを指定することができます。

1. AEM as a Cloud Service にログインし、メインメニューで&#x200B;**ツール**／**一般**／**設定ブラウザー**&#x200B;を選択します。
1. 変更する設定を選択し、ツールバーの「**プロパティ**」をクリックします。
1. 設定に追加する機能を選択します。

   >[!NOTE]
   >
   >設定の作成後は、機能の選択を解除することはできません。

1. 「**有効な権限**」ボタンを使用すると、役割の一覧と、現在設定されている設定に対する権限が表示されます。
   ![有効な権限ウィンドウ](assets/configuration-effective-permissions.png)
1. 新しい権限を割り当てるには、**新しい権限の追加**&#x200B;セクションの「**ユーザーまたはグループを選択**」フィールドにユーザーまたはグループ名を入力します。
   * 「**ユーザーまたはグループを選択**」フィールドは、既存のユーザーと役割に基づいて自動入力されます。
1. オートコンプリートの結果から適切なユーザーまたは役割を選択します。
   * 複数のユーザーまたは役割を選択できます。
1. 選択したユーザーまたは役割に必要なアクセスオプションを確認し、「**追加**」をクリックします。
   ![設定へのアクセス権の追加](assets/configuration-edit.png)
1. 手順を繰り返して、ユーザーまたは役割を選択し、必要に応じて追加のアクセス権を割り当てます。
1. 完了したら、「**保存して閉じる**」を選択します。

## デベロッパーにとっての設定 {#configurations-developer}

デベロッパーは、AEM as a Cloud Service と設定との連携、および設定の処理方法を知ることが重要です。

### 設定とコンテンツの分離 {#separation-of-config-and-content}

管理者とユーザーは、設定を、異なる設定やコンテンツを管理するための[ワークスペースと考る](#configurations-administrator)かもしれませんが、AEM では設定とコンテンツはリポジトリー内で別々に保存および管理されることを理解しておくことが重要です。

* `/content` はすべてのコンテンツのホームページです。
* `/conf` はすべての設定のホームです。

コンテンツは `cq:conf` プロパティを介して関連する設定を参照します。AEM は、コンテンツとそのコンテキスト依存の `cq:conf` プロパティに基づいて検索を実行し、適切な設定を見つけます。

### 例 {#developer-example}

この例では、DAM 設定に関心のあるアプリケーションコードがあるとします。

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

すべての設定参照の開始点はコンテンツリソースで、`/content` の下にあります。これは、ページ、ページ内のコンポーネント、アセット、または DAM フォルダーの場合がありますが、この状況で適用される適切な設定を探している実際のコンテンツです。

`Conf` オブジェクトを用意したら、関心のある特定の設定項目を取得できます。ここでは、`imageserver` に関連する設定の集まりである `dam/imageserver` となります。`getItem` を呼び出すと `ValueMap` が返されます。次に、`bgkcolor` 文字列プロパティを読み取り、プロパティ（または設定項目全体）が存在しない場合に備えて、デフォルト値の「FFFFFF」を指定します。

次に、対応する JCR コンテンツを見てみましょう。

```text
/content/dam/wknd
    + jcr:content
      - cq:conf = "/conf/wknd"
    + image.png [dam:Asset]

/conf/wkns
    + settings
      + dam
        + imageserver [cq:Page]
          + jcr:content
            - bgkcolor = "FF0000"
```

この例では、WKND 固有の DAM フォルダーと、このフォルダーに対応する設定があると仮定します。このフォルダー `/content/dam/wknd` から始めると、サブツリーに適用する設定を参照する `cq:conf` という名前の文字列プロパティがあることがわかります。このプロパティは、アセットフォルダーまたはアセットページの `jcr:content` で設定されます。これらの `conf` リンクは明示的なので、CRXDE 内のコンテンツを見るだけで簡単にリンク先を追うことができます。

`/conf` の中に入り、参照をたどると `/conf/wknd` ノードがあるのがわかります。これは設定です。そのルックアップは、アプリケーションコードに対して透過的です。この例のコードは、専用の参照を持たないので、`Conf` オブジェクトの背後に隠れています。どの設定が適用されるかは、JCR コンテンツを介して制御されます。

設定には、固定名の `settings` ノードが含まれ、その中には、この場合に必要な実際の項目（`dam/imageserver` など）が含まれています。このような項目は「設定ドキュメント」と考えることができ、実際のコンテンツを保持する `jcr:content` を含む `cq:Page` で表されます。

最後に、サンプルコードに必要なプロパティ `bgkcolor` を確認できます。`getItem` から返される `ValueMap` は、ページの `jcr:content` ノードに基づいています。

### 設定の解決 {#configuration-resolution}

上記の基本的な例は、1 つの設定を示しています。ただし、デフォルトのグローバル設定、ブランドごとに異なる設定、場合によってはサブプロジェクトに固有の設定など、様々な設定が必要な場合が多くあります。

これをサポートするために、AEM での設定の参照には、継承とフォールバックのメカニズムが次の環境設定で備わっています。

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * `cq:conf` から `/content` のどこかで参照された特定の設定
   * 階層は任意であり、サイト設定と同様にデザインできます。階層はアプリケーションコードには知らされません。
   * 設定の権限を持つユーザーが実行時に変更可能
1. `/conf/<siteconfig>/<parentconfig>`
   * 代替構成設定のために親をトラバース
   * 設定の権限を持つユーザーが実行時に変更可能
1. `/conf/<siteconfig>`
   * 代替構成設定のために親をトラバース
   * 設定の権限を持つユーザーが実行時に変更可能
1. `/conf/global`
   * システムのグローバル設定
   * インストールのグローバルデフォルト
   * `admin` の役割によって設定
   * 設定の権限を持つユーザーが実行時に変更可能
1. `/apps`
   * アプリケーションのデフォルト
   * アプリケーションのデプロイメントで固定
   * 実行時は読み取り専用
1. `/libs`
   * AEM 製品のデフォルト
   * アドビによってのみ変更可能、プロジェクトへのアクセス許可なし
   * アプリケーションのデプロイメントで固定
   * 実行時は読み取り専用

### 設定の使用 {#using-configurations}

AEM の設定は、Sling コンテキスト対応設定に基づいています。Sling バンドルには、コンテキスト対応設定の取得に使用できるサービス API が用意されています。コンテキスト対応設定とは、[前の例で説明したように](#developer-example)、コンテンツリソースまたはリソースツリーに関連する設定です。

コンテキスト対応設定、例、使用方法の詳細については、[Sling のドキュメント](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)を参照してください。

### ConfMgr Web コンソール {#confmgr-web-console}

デバッグおよびテストの目的で、`https://<host>:<port>/system/console/conf` には **ConfMgr** Web コンソールがあり、特定のパス／項目の設定を表示することができます。

![ConfMgr](assets/configuration-confmgr.png)

以下を提供するだけです。

* **コンテンツのパス**
* **項目**
* **ユーザー**

解決された設定を確認し、その設定を解決するサンプルコードを受け取るには、「**解決**」を選択します。

### コンテキスト対応設定の Web コンソール {#context-aware-web-console}

デバッグおよびテストの目的で、`https://<host>:<port>/system/console/slingcaconfig` に&#x200B;**コンテキスト対応設定の** Web コンソールがあり、リポジトリー内のコンテキスト対応設定にクエリを実行し、そのプロパティを表示できます。

![コンテキスト対応設定の Web コンソール](assets/configuration-context-aware-console.png)

以下を提供するだけです。

* **コンテンツのパス**
* **設定名**

選択した設定に関連付けられたコンテキストパスとプロパティを取得するには、「**解決**」を選択します。
