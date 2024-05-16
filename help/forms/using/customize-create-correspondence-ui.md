---
title: 通信作成 UI をカスタマイズ
description: AEM Forms 環境でロゴなどの通信ユーザーインターフェイス（UI）をカスタマイズする方法について説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 9593ca2a-7f9e-4487-a1a5-ca44114bff17
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '1099'
ht-degree: 100%

---

# 通信作成 UI のカスタマイズ{#customize-create-correspondence-ui}

## 概要 {#overview}

Correspondence Management を使用すると、ソリューションテンプレートをリブランディングしてブランド価値を高め、組織のブランディング標準に準拠することができます。ユーザーインターフェイスのリブランディングには、組織のロゴの変更が含まれます。ロゴは、通信作成 UI の左上隅に表示されます。

通信作成 UI のロゴを組織のロゴに変更できます。

![通信作成 UI のカスタムアイコン](assets/0_1_introscreenshot.png)

通信作成用 UI に表示されたカスタムアイコン

### 通信作成 UI のロゴの変更 {#changing-the-logo-in-the-create-correspondence-ui}

ロゴ画像を設定するには、次の手順を実行します。

1. [CRX 内で適切なフォルダー構造](#creatingfolderstructure)を作成します。
1. CRX で作成したフォルダーに、[新しいロゴファイルをアップロード](#uploadlogo)します。

1. CRX 上に [CSS をセットアップ](#createcss)し、新しいロゴを参照します。
1. ブラウザーの履歴を消去し、[通信作成 UI を更新](#refreshccrui)します。

## 必要なフォルダー構造の作成 {#creatingfolderstructure}

カスタムロゴ画像とスタイルシートをホストするために、以下の説明に従ってフォルダー構造を作成します。ルートフォルダー /apps を持つ新しいフォルダー構造は、/libs フォルダーの構造に似ています。

カスタマイズする場合は、以下に説明するように、/apps ブランチに並列フォルダー構造を作成します。

`/apps` ブランチ（フォルダー構造）：

* システムに更新がある場合に、ファイルの安全を確保します。アップグレード、機能パックまたはホットフィックスがある場合、`/libs` ブランチが更新されます。`/libs` ブランチに変更内容をホストしていると上書きされてしまいます。
* 現在のシステム／ブランチを乱さないようにします。カスタムファイルの保存用にデフォルトの場所を使用すると、誤って乱してしまう可能性があります。
* AEM がリソースを検索する際に、リソースの優先度を高めます。AEM は、リソースを検索する場合、最初に `/apps` ブランチを検索し、次に `/libs` ブランチを検索するように設定されています。このメカニズムにより、システムはオーバーレイ（および、そこに定義されたカスタマイズ内容）を使用します。

次の手順を実行して、必要なフォルダー構造を `/apps` ブランチに作成します。

1. `https://'[server]:[port]'/[ContextPath]/crx/de` に移動して、管理者としてログインします。
1. apps フォルダー内に、ccrui フォルダーにある css フォルダーと同様のパスと構造を持つ、`css` というフォルダーを作成します。

   css フォルダーの作成手順：

   1. 次のパスにある **css** フォルダーを右クリックし、「**ノードをオーバーレイ**」を選択します。`/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css`

      ![ノードをオーバーレイ](assets/1_overlaynode_css.png)

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス:** `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css`

      **オーバーレイの場所：** `/apps/`

      **ノードタイプを一致させる：**&#x200B;オン

      ![オーバーレイノードのパス](assets/0_1_5ioverlaynodedialog.png)

      >[!NOTE]
      >
      >`/libs` ブランチは変更しないでください。次の操作を行った場合はこのブランチが変更されるため、各自で加えた変更はすべて失われます。
      >
      >    
      >    
      >    * インスタンスをアップグレード
      >    * ホットフィックスの適用
      >    * 機能パックをインストール
      >    
      >

   1. 「**OK**」をクリックします。指定したパスに css フォルダーが作成されます。

1. apps フォルダー内に、ccrui フォルダーにある `imgs` フォルダーと同様のパスと構造を持つ、`imgs` というフォルダーを作成します。

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

カスタムロゴファイルを CRXに アップロードします。ロゴの描画には、標準的な HTML 規則が適用されます。サポートしている画像ファイル形式は、AEM Forms へのアクセスに使用しているブラウザーによって異なります。ただし、JPEG、GIF、および PNG は、すべてのブラウザーでサポートされています。詳しくは、サポートされる画像形式に関するブラウザー固有のドキュメントを参照してください。

* ロゴ画像のデフォルトの大きさは 48 &#42; 48 ピクセルです。画像はこのサイズに近いか、または 48 &#42; 48 ピクセルよりも大きいことを確認してください。
* ロゴ画像の高さが 50 ピクセルを超えている場合、通信作成ユーザーインターフェイスでは、ヘッダーの高さである 50 ピクセルに合わせて画像を縮小表示します。画像を縮小表示する際も、通信作成ユーザーインターフェイスでは画像の縦横比が維持されます。
* 画像が小さい場合、通信作成用ユーザーインターフェイスでは拡大表示されません。そのため、ロゴ画像をきれいに表示するには、高さが少なくとも 48 ピクセルあり、幅も十分にあるファイルを使用することが大切です。

以下の手順を実行して、CRX にカスタムロゴファイルをアップロードします。

1. `https://'[server]:[port]'/[contextpath]/crx/de` にアクセスします。必要に応じて、管理者としてログインします。
1. CRXDE から、次のパスにある **imgs** フォルダーを右クリックし、「**作成」／「ファイルを作成**」を選択します。

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs/`

   ![imgs フォルダ内に新しいノードを作成する](assets/2_contentexplorernewnode.png)

1. 「ファイルを作成」ダイアログで、ファイルの名前「CustomLogo.png」（またはロゴファイルの名前）を入力します。

   ![新規ノードとしての CustomLogo.png](assets/3_contentexplorernewnode_customlogo.png)

1. 「**すべて保存**」をクリックします。

   作成した新しいファイル（ここでは CustomLogo.png）の下に、jcr:content プロパティが表示されます。

1. フォルダー構造内で jcr:content をクリックします。

   jcr:content のプロパティが表示されます。

   ![jcrcontentproperties](assets/jcrcontentproperties.png)

1. **jcr:data** プロパティをダブルクリックします。

   「Edit jcr:data」のダイアログが表示されます。

   次に、newlogo.png フォルダーをクリックし、jcr:content（dim オプション）をダブルクリックして、タイプ nt:resource を設定します。プロパティが表示されていない場合は、まず、名前が「jcr:content」のプロパティを作成します。

1. 「jcr:data の編集」ダイアログで「**参照**」をクリックし、ロゴとして使用する画像ファイルを選択します（ここでは、「CustomLogo.png」）。

   サポートしている画像ファイル形式は、AEM Forms へのアクセスに使用しているブラウザーによって異なります。ただし、JPEG、GIF、および PNG は、すべてのブラウザーでサポートされています。詳しくは、サポートされる画像形式に関するブラウザー固有のドキュメントを参照してください。

   ![カスタムロゴファイルのサンプル](assets/geometrixx-outdoors.png)

   例：CustomLogo.png をカスタムロゴとして使用する

1. 「**すべて保存**」をクリックします。

## UI でロゴをレンダリングするための CSS を作成 {#createcss}

カスタムロゴ画像では、コンテンツコンテキストで追加のスタイルシートを読み込む必要があります。

UI でロゴをレンダリングするためのスタイルシートを作成するには、次の手順を実行します。

1. `https://'[server]:[port]'/[contextpath]/crx/de` にアクセスします。必要に応じて、管理者としてログインします。
1. 次の場所に、customcss.css というファイルを作成します。異なるファイル名は使用できません。

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css/`

   customcss.css ファイルの作成手順：

   1. **css** フォルダーを右クリックし、**作成／ファイルを作成**&#x200B;を選択します。
   1. 新規ファイルダイアログボックスで、CSS の名前を「`customcss.css`」として指定し、「**OK**」をクリックします。異なるファイル名は使用できません。
   1. 次のコードを、新しく作成した css ファイルに追加します。コードの content:url で、CRXDE の imgs フォルダーにアップロードした画像名を指定します。

      ```css
      .logo, .logo:after {
      content:url("../imgs/CustomLogo.png");
      }
      ```

   1. 「**すべて保存**」をクリックします。

## 通信作成 UI を更新してカスタムロゴを表示 {#refreshccrui}

ブラウザーキャッシュをクリアし、ブラウザーで通信作成 UI インスタンスを開いて、カスタムロゴを表示します。

![カスタムロゴを用いて、通信作成用ユーザーインターフェイスを構築する](assets/0_1_introscreenshot-1.png)

通信作成用 UI に表示されたカスタムアイコン
