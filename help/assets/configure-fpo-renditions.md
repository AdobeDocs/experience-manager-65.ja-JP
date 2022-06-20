---
title: Adobe InDesign 用のプレースメント専用レンディションの生成
description: Experience Manager Assets ワークフローと ImageMagick を使用して、新規および既存アセットの FPO レンディションを生成します。
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 1e4ddd73-a31c-4ddd-94eb-1dac6a4835b3
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 98%

---

# Adobe InDesign 用の配置専用レンディションの生成 {#fpo-renditions}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/configure-fpo-renditions.html?lang=en) |
| AEM 6.5 | この記事 |

Adobe Experience Manager の大きいサイズのアセットを Adobe InDesign ドキュメントに配置する場合、クリエイティブプロフェッショナルは、[アセットを配置](https://helpx.adobe.com/jp/indesign/using/placing-graphics.html)してからかなりの時間待つ必要があります。一方、ユーザーは InDesign の使用をブロックされます。これにより、クリエイティブの流れが中断され、ユーザーエクスペリエンスに悪影響が出ます。そこで、最初に小さいサイズのレンディションを InDesign ドキュメントに一時的に配置できるようになっています。印刷ワークフローや公開ワークフローなど、最終的な出力が必要な場合は、バックグラウンドの一時レンディションが元のフル解像度のアセットに置き換わります。このバックグラウンドでの非同期更新により、設計プロセスが迅速化されて生産性が向上する一方、クリエイティブプロセスが妨げられることはありません。

Adobe Experience Manager（AEM）には、配置専用（FPO）のレンディションが用意されています。これらの FPO レンディションは、ファイルサイズは小さいですが、縦横比は同じです。FPO レンディションがアセットに使用できない場合、Adobe InDesign は元のアセットを代わりに使用します。このフォールバックメカニズムにより、クリエイティブワークフローは中断することなく確実に続行されます。

## FPO レンディションを生成するための取り組み {#approach-to-generate-fpo-renditions}

Experience Manager には、FPO レンディションの生成に使用できる画像処理方法が数多く用意されています。最も一般的な 2 つの方法は、組み込みの Experience Manager ワークフローを使用する方法と ImageMagick を使用する方法です。これらの 2 つの方法を使用して、新しくアップロードしたアセットと Experience Manager に存在するアセットのレンディション生成を設定します。

ImageMagick を使用して、FPO レンディションの生成などの画像処理が可能です。このようなレンディションはダウンサンプルされます。つまり、元の画像の PPI が 72 を超える場合、レンディションのピクセルサイズが比例的に小さくなります。詳しくは、[Experience Manager Assets と連携するための ImageMagick のインストールと設定](best-practices-for-imagemagick.md)を参照してください。

|  | Experience Manager の組み込みワークフローの使用 | ImageMagick ワークフローの使用 | 備考 |
|--- |--- |---|--- |
| 新しいアセットの場合 | FPO レンディションを有効にする（[ヘルプ](#generate-renditions-of-new-assets-using-aem-workflow)） | ImageMagick コマンドラインを Experience Manager ワークフローに追加する（[ヘルプ](#generate-renditions-of-new-assets-using-imagemagick)） | Experience Manager は、アップロードのたびに DAM アセットの更新ワークフローを実行します。 |
| 既存のアセットの場合 | 新しい専用 Experience Manager ワークフローで FPO レンディションを有効にする（[ヘルプ](#generate-renditions-of-existing-assets-using-aem-workflow)） | ImageMagick コマンドラインを新しい専用 Experience Manager ワークフローに追加する（[ヘルプ](#generate-renditions-of-existing-assets-using-imagemagick)） | 既存のアセットの FPO レンディションは、オンデマンドまたは一括で作成できます。 |

>[!CAUTION]
>
>デフォルトのワークフローのコピーを変更することで、レンディションを生成するためのワークフローを作成します。これにより、新しいサービスパックをインストールするなどして Experience Manager が更新された場合に変更が上書きされるのを防ぎます。

## Experience Manager ワークフローを使用した新しいアセットのレンディションの生成 {#generate-renditions-of-new-assets-using-aem-workflow}

次に、レンディションの生成を有効にするための DAM アセットの更新ワークフローモデルの設定手順を示します。

1. **[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;をクリックします。**[!UICONTROL DAM アセットの更新]**&#x200B;モデルを選択して、「**[!UICONTROL 編集]**」をクリックします。

1. **[!UICONTROL サムネールを処理]**&#x200B;ステップを選択して、「**[!UICONTROL 設定]**」をクリックします。

1. 「**[!UICONTROL FPO レンディション]**」タブをクリックします。「**[!UICONTROL FPO レンディション作成を有効にする]**」を選択します。

   ![fpo_rendition_damupdateasset_model](assets/fpo_rendition_damupdateasset_model.png)

1. 必要に応じて、**[!UICONTROL 画質]**&#x200B;を調整したり、「**[!UICONTROL 形式リスト]**」の値を追加または変更したりします。デフォルトでは、FPO レンディションを生成するための MIME タイプのリストは、pjpeg、jpeg、jpg、gif、png、x-png、tiff です。「**[!UICONTROL 完了]**」をクリックします。

   >[!NOTE]
   >
   >レンディションの生成は、ファイルタイプ JPEG、GIF、PNG、TIFF、PSD、BMP でサポートされます。

1. 変更を有効にするには、「**[!UICONTROL 同期]**」をクリックします。

>[!NOTE]
>
>片側が 1280 ピクセルを超える画像は、FPO レンディションのピクセルサイズを保持しません。

## ImageMagick を使用した新しいアセットのレンディションの生成 {#generate-renditions-of-new-assets-using-imagemagick}

Experience Manager では、新しいアセットがアップロードされると、DAM アセットの更新ワークフローが実行されます。ImageMagick を使用して新しくアップロードされたアセットのレンディションを処理するには、ワークフローモデルに新しいコマンドを追加します。

1. **[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;をクリックします。

1. **[!UICONTROL DAM アセットの更新]**&#x200B;モデルを選択して、「**[!UICONTROL 編集]**」をクリックします。

1. 左上隅の「**[!UICONTROL サイドパネルを切り替え]**」をクリックして、コマンドラインステップを検索します。

1. **[!UICONTROL コマンドライン]**&#x200B;ステップをドラッグして、**[!UICONTROL サムネールを処理]**&#x200B;ステップの前に追加します。

1. **[!UICONTROL コマンドライン]**&#x200B;ステップを選択して、「**[!UICONTROL 設定]**」をクリックします。

1. 必要な情報をカスタム&#x200B;**[!UICONTROL タイトル]**&#x200B;および&#x200B;**[!UICONTROL 説明]**&#x200B;として追加します。例えば、FPO レンディション（ImageMagick を利用）です。

1. 「**[!UICONTROL 引数]**」タブで、関連する **[!UICONTROL MIME タイプ]**&#x200B;を追加して、コマンドが適用されるファイル形式のリストを提供します。

   ![imagemagick-mimetype](assets/imagemagick-mimetype.png)

1. 「**[!UICONTROL 引数]**」タブの「**[!UICONTROL コマンド]**」セクションで、FPO レンディションを生成するための関連する ImageMagick コマンドを追加します。

   次のコマンドの例では、JPEG 形式の FPO レンディションを生成し、72 PPI（10％画質設定）でダウンサンプリングを行い、出力をフラット化して複数レイヤーの Adobe Photoshop ファイルを処理します。

   `convert -quality 10% -units PixelsPerInch ${filename} -resample 72 -flatten cq5dam.fpo.jpeg`

1. 変更を有効にするには、「**[!UICONTROL 同期]**」をクリックします。

ImageMagick のコマンドライン機能について詳しくは、[https://imagemagick.org](https://imagemagick.org) を参照してください。

## Experience Manager ワークフローを使用した既存アセットのレンディションの生成 {#generate-renditions-of-existing-assets-using-aem-workflow}

Experience Manager ワークフローを使用して既存アセットの FPO レンディションを生成するには、組み込みの FPO レンディションオプションを使用する専用のワークフローモデルを作成します。

1. **[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;をクリックします。

1. モデルを作成するには、**[!UICONTROL 作成]**／**[!UICONTROL モデルを作成]**&#x200B;をクリックします。

1. 意味のある「**[!UICONTROL タイトル]**」および「**[!UICONTROL 名前]**」を追加します。

1. モデルを選択し、「**[!UICONTROL 編集]**」をクリックします。**[!UICONTROL ページ情報]**／**[!UICONTROL プロパティを開く]**&#x200B;をクリックして、**[!UICONTROL 一時的なワークフロー]**&#x200B;を選択します。これにより、拡張性とパフォーマンスが向上します。

1. 「**[!UICONTROL 保存]**」および「**[!UICONTROL 閉じる]**」をクリックします。

1. 左上隅の「**[!UICONTROL サイドパネルを切り替え]**」をクリックして、「サムネールを処理」ステップを検索します。

1. 「**[!UICONTROL サムネールを処理]**」を選択し、「**[!UICONTROL 設定]**」をクリックします。[Experience Manager ワークフローを使用して、新しいアセットのレンディションを生成するための設定](#generate-renditions-of-new-assets-using-aem-workflow)に従います。

1. 変更を有効にするには、「**[!UICONTROL 同期]**」をクリックします。


## ImageMagick を使用した既存アセットのレンディションの生成 {#generate-renditions-of-existing-assets-using-imagemagick}

ImageMagick 処理機能を使用して既存アセットの FPO レンディションを生成するには、 ImageMagick コマンドラインを使用する専用のワークフローモデルを作成します。

1. [Experience Manager ワークフローを使用して既存アセットのレンディションを生成するための設定](#generate-renditions-of-existing-assets-using-aem-workflow)の節の手順 1 ～ 3 に従います。

1. [ImageMagick を使用して新しいアセットのレンディションを生成するための設定](#generate-renditions-of-new-assets-using-imagemagick)の節の手順 4 ～ 8 に従います。


## FPO レンディションの表示 {#view-fpo-renditions}

ワークフローが完了したら、生成された FPO レンディションを確認できます。Experience ManagerAssets ユーザーインターフェイスで、アセットをクリックして大きいプレビューを開きます。左側のパネルを開き、「レンディション」を選択します。または、プレビューが開いたときに、キーボードショートカット `Alt + 3` を使用します。

「**[!UICONTROL FPO レンディション]**」をクリックして、プレビューを読み込みます。オプションで、レンディションを右クリックしてファイルシステムに保存できます。

![rendition_list](assets/rendition_list.png)


## ヒントと制限事項 {#tips-limitations}

* ImageMagick ベースの設定を使用するには、ImageMagick を Experience Manager と同じマシンにインストールします。
* 多数のアセットまたはリポジトリ全体の FPO レンディションを生成するには、トラフィックの少ない時間帯にワークフローを計画および実行します。 大量のアセットの FPO レンディションを生成するアクティビティはリソースを大量に消費するので、Experience Manager サーバーには十分な処理能力と空きメモリが必要です。
* パフォーマンスと拡張性については、[ImageMagick の微調整](performance-tuning-guidelines.md)を参照してください。
* アセットの一般的なコマンドライン処理については、[アセットを処理するためのコマンドラインハンドラー](media-handlers.md)を参照してください。
