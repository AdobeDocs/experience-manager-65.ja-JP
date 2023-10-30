---
title: 通信作成用 UI のカスタマイズ
description: AEM Forms環境でロゴなどの通信ユーザーインターフェイス (UI) をカスタマイズする方法を説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 9593ca2a-7f9e-4487-a1a5-ca44114bff17
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 37%

---

# 通信作成 UI のカスタマイズ{#customize-create-correspondence-ui}

## 概要 {#overview}

Correspondence Management を使用すると、ソリューションテンプレートを再ブランディングして、より優れたブランド価値を実現し、組織のブランディング標準に準拠できます。 ユーザーインターフェイスのリブランディングには、組織のロゴの変更が含まれます。ロゴは、通信を作成 UI の左上隅に表示されます。

通信を作成 UI のロゴを組織のロゴと共に変更できます。

![通信作成 UI のカスタムアイコン](assets/0_1_introscreenshot.png)

通信作成用 UI に表示されたカスタムアイコン

### 通信を作成 UI でのロゴの変更 {#changing-the-logo-in-the-create-correspondence-ui}

選択したロゴイメージを設定するには、次の手順を実行します。

1. [CRX 内で適切なフォルダー構造](#creatingfolderstructure)を作成します。
1. [新しいロゴファイルをアップロード](#uploadlogo) を CRX で作成したフォルダーに追加します。

1. CRX 上に [CSS をセットアップ](#createcss)し、新しいロゴを参照します。
1. ブラウザーの履歴を消去し、[通信作成 UI を更新](#refreshccrui)します。

## 必要なフォルダー構造の作成 {#creatingfolderstructure}

カスタムロゴイメージとスタイルシートをホストするためのフォルダー構造を、以下で説明するように作成します。 ルートフォルダー/apps を持つ新しいフォルダー構造は、/libs フォルダーの構造に似ています。

カスタマイズの場合は、以下に説明するように、/apps ブランチに並列フォルダー構造を作成します。

The `/apps` ブランチ（フォルダー構造）:

* システムに更新があった場合に、ファイルを安全に保護します。 アップグレード、機能パック、またはホットフィックスがある場合は、 `/libs` ブランチが更新され、変更を `/libs` 分岐では、上書きされます。
* 現在のシステム/ブランチを乱さないようにします。カスタムファイルの保存にデフォルトの場所を使用すると、誤ってセトル解除する可能性があります。
* AEMでリソースを検索する際に、リソースの優先度を高めるのに役立ちます。 AEMが `/apps` 最初に分岐し、次に `/libs` 分岐を使用して、リソースを検索します。 このメカニズムにより、システムはオーバーレイ（および、そこに定義されたカスタマイズ内容）を使用します。

次の手順を実行して、 `/apps` ブランチ：

1. `https://'[server]:[port]'/[ContextPath]/crx/de` に移動して、管理者でログインします。
1. apps フォルダーに、 `css` （ccrui フォルダー内の）css フォルダーに似たパス/構造を持つ。

   css フォルダーの作成手順：

   1. 次のパスにある **css** フォルダーを右クリックし、「**ノードをオーバーレイ**」を選択します。`/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css`

      ![ノードをオーバーレイ](assets/1_overlaynode_css.png)

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス:** `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css`

      **オーバーレイの場所:** `/apps/`

      **ノードタイプを一致させる：**&#x200B;オン

      ![オーバーレイノードのパス](assets/0_1_5ioverlaynodedialog.png)

      >[!NOTE]
      >
      >次を変更しない： `/libs` 分岐。 このブランチは、次の操作を行うたびに変更される可能性が高いので、加えた変更はすべて失われる可能性があります。
      >
      >    
      >    
      >    * インスタンスでのアップグレード
      >    * ホットフィックスの適用
      >    * 機能パックのインストール
      >    
      >

   1. 「**OK**」をクリックします。指定されたパスに css フォルダーが作成されます。

1. apps フォルダーに、 `imgs` （ccrui フォルダー内の）imgs フォルダーに似たパス/構造を持つ。

   1. 次のパスにある **imgs** フォルダーを右クリックし、「**ノードをオーバーレイ**」を選択します。`/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs`
   1. 「ノードをオーバーレイ」ダイアログに次の値が表示されていることを確認します。

      **パス：**/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs

      **オーバーレイの場所：**/apps/

      **ノードタイプを一致させる**：オン

   1. 「**OK**」をクリックします。

      >[!NOTE]
      >
      >/apps フォルダーに手動でフォルダー構造を作成することもできます。

1. 「**すべて保存**」をクリックして、サーバーに変更を保存します。

## CRX に新しいロゴをアップロード {#uploadlogo}

カスタムロゴファイルを CRX にアップロードします。 ロゴの描画には、標準的な HTML 規則が適用されます。サポートされる画像ファイル形式は、AEM Formsにアクセスするために使用しているブラウザーに応じて異なります。 すべてのブラウザーは、JPEG、GIF、PNG をサポートしています。 詳しくは、サポートされる画像形式に関するブラウザー固有のドキュメントを参照してください。

* ロゴ画像のデフォルトの大きさは 48 &#42; 48 ピクセルです。画像はこのサイズに近いか、または 48 &#42; 48 ピクセルよりも大きいことを確認してください。
* ロゴ画像の高さが 50 px を超える場合、通信を作成ユーザーインターフェイスでは、ヘッダーの高さになるので、画像を最大 50 px まで縮小表示します。 画像を縮小しても、通信を作成ユーザーインターフェイスは画像の縦横比を維持します。
* 画像が小さい場合、通信作成用ユーザーインターフェイスでは拡大表示されません。そのため、ロゴ画像をきれいに表示するには、高さが少なくとも 48 ピクセルあり、幅も十分にあるファイルを使用することが大切です。

以下の手順を実行して、CRX にカスタムロゴファイルをアップロードします。

1. `https://'[server]:[port]'/[contextpath]/crx/de` にアクセスします。必要に応じて、管理者としてログインします。
1. CRXDE から、次のパスにある **imgs** フォルダーを右クリックし、「**作成」／「ファイルを作成**」を選択します。

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs/`

   ![imgs フォルダ内に新しいノードを作成する](assets/2_contentexplorernewnode.png)

1. 「ファイルを作成」ダイアログで、ファイルの名前「CustomLogo.png」（またはロゴファイルの名前）を入力します。

   ![新規ノードとしての CustomLogo.png](assets/3_contentexplorernewnode_customlogo.png)

1. 「**すべて保存**」をクリックします。

   作成した新しいファイル（ここでは CustomLogo.png）の下に、 jcr:content プロパティが表示されます。

1. フォルダー構造で jcr:content をクリックします。

   jcr:content のプロパティが表示されます。

   ![jcrcontentproperties](assets/jcrcontentproperties.png)

1. **jcr:data** プロパティをダブルクリックします。

   「Edit jcr:data」のダイアログが表示されます。

   次に、newlogo.png フォルダーをクリックし、jcr:content (dim option) をダブルクリックして、タイプ nt:resource を設定します。 存在しない場合は、jcr:content という名前のプロパティを作成します。

1. 「jcr:data の編集」ダイアログで「**参照**」をクリックし、ロゴとして使用する画像ファイルを選択します（ここでは、「CustomLogo.png」）。

   サポートされる画像ファイル形式は、AEM Formsにアクセスするために使用しているブラウザーに応じて異なります。 すべてのブラウザーは、JPEG、GIF、PNG をサポートしています。 詳しくは、サポートされる画像形式に関するブラウザー固有のドキュメントを参照してください。

   ![カスタムロゴファイルのサンプル](assets/geometrixx-outdoors.png)

   例：カスタムロゴとして使用する CustomLogo.png

1. 「**すべて保存**」をクリックします。

## UI でロゴをレンダリングするための CSS を作成する {#createcss}

カスタムロゴイメージを使用するには、コンテンツコンテキストに追加のスタイルシートを読み込む必要があります。

UI でロゴをレンダリングするためのスタイルシートを作成するには、次の手順を実行します。

1. `https://'[server]:[port]'/[contextpath]/crx/de` にアクセスします。必要に応じて、管理者としてログインします。
1. 次の場所に、customcss.css というファイルを作成します。異なるファイル名は使用できません。

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css/`

   customcss.css ファイルの作成手順：

   1. を右クリックします。 **css** フォルダーと選択 **作成/ファイルを作成**.
   1. 新規ファイルダイアログボックスで、CSS の名前を「`customcss.css`」として指定し、「**OK**」をクリックします。異なるファイル名は使用できません。
   1. 次のコードを、新しく作成した css ファイルに追加します。 コードの content:url で、CRXDE の imgs フォルダーにアップロードした画像名を指定します。

      ```css
      .logo, .logo:after {
      content:url("../imgs/CustomLogo.png");
      }
      ```

   1. 「**すべて保存**」をクリックします。

## 通信を作成 UI を更新して、カスタムロゴを表示します。 {#refreshccrui}

ブラウザーのキャッシュをクリアし、ブラウザーで通信を作成 UI インスタンスを開いて、カスタムロゴを表示します。

![カスタムロゴを用いて、通信作成用ユーザーインターフェイスを構築する](assets/0_1_introscreenshot-1.png)

通信作成用 UI に表示されたカスタムアイコン
