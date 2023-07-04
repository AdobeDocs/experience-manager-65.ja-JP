---
title: Dynamic Media のビデオ
description: Dynamic Media でのビデオの操作方法（ビデオのエンコーディング、YouTube でのビデオの公開、ビデオレポートの表示のベストプラクティスなど）を説明します。また、ビデオにクローズドキャプション、字幕、チャプターマーカーを追加する方法についても説明します。
mini-toc-levels: 3
uuid: 97f311a3-a227-479a-91bf-fb54ecd1a55d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 1103b849-0042-4e11-b170-38ee81dd0157
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 28cf9e39-cab4-4278-b6c9-e84cc31964db
source-git-commit: a95255594ec03c152cd96df48597ced5fce4b315
workflow-type: tm+mt
source-wordcount: '8066'
ht-degree: 99%

---

# Dynamic Media のビデオ {#video}

ここでは、Dynamic Media でのビデオの操作について説明します。

## クイックスタート：ビデオ {#quick-start-videos}

次のワークフローの手順説明は、Dynamic Media でアダプティブビデオセットをすぐに使い始めることを目的としたものです。各手順に続いて、詳しい説明のあるトピックの見出しへのリンクが記載されています。

>[!IMPORTANT]
>
>Dynamic Media のビデオを操作する前に、Adobe Experience Manager 管理者が Dynamic Media - Scene7 モードまたは Dynamic Media - ハイブリッドモードの Dynamic Media クラウドサービスを既に有効にして設定を完了していることを確認してください。
>
>* 「Dynamic Media - Scene7 モードの設定」の [Dynamic Media クラウドサービスの設定](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)および [Dynamic Media - Scene7 モードのトラブルシューティング](/help/assets/troubleshoot-dms7.md)を参照してください。
>
>* 「Dynamic Media - ハイブリッドモードの設定」の [Dynamic Media クラウドサービスの設定](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services)を参照してください。
>
>Dynamic Media での既知のビデオ再生の問題（*Experience Manager 6.5.9.0 のみ*）：
>
>* 公開済みのビデオを更新する場合は、ビデオを再度公開して配信に変更を反映させる必要があります。
>

1. 次の手順を実行して、**Dynamic Media ビデオをアップロード**&#x200B;します。

   * 独自のビデオエンコーディングプロファイルを作成します。または、Dynamic Media に付属している事前定義済みの&#x200B;_アダプティブビデオエンコーディング_（AVE）プロファイルを使用してもかまいません。

      * [ビデオエンコーディングプロファイルを作成します](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming)。
      * 詳しくは、[ビデオエンコーディングのベストプラクティス](#best-practices-for-encoding-videos)を参照してください。

   * ビデオ処理プロファイルを、プライマリソースビデオのアップロード先となる 1 つ以上のフォルダーに関連付けます。

      * [ビデオプロファイルをフォルダーに適用します](/help/assets/video-profiles.md#applying-a-video-profile-to-folders)。
      * 詳しくは、[処理プロファイルを使用するためのデジタルアセットの整理におけるベストプラクティス](/help/assets/organize-assets.md)を参照してください。
      * 詳しくは、[デジタルアセットの整理](/help/assets/organize-assets.md)を参照してください。

   * フォルダーにプライマリソースビデオをアップロードします。フォルダーにビデオを追加すると、そのフォルダーに割り当てたビデオ処理プロファイルに従ってビデオがエンコードされます。

      * Dynamic Media では、最大長 30 分、最小解像度が 25 x 25 を超える短い形式のビデオが主にサポートされています。
      * 15 GB までのビデオファイルをアップロードできます。
      * [ビデオをアップロードします](/help/assets/managing-video-assets.md#upload-and-preview-video-assets)。
      * 詳しくは、[サポートされる入力ファイル形式](/help/assets/assets-formats.md#supported-multimedia-formats)を参照してください。

   * アセットまたはワークフロー表示から、[ビデオエンコードの進行状況](#monitoring-video-encoding-and-youtube-publishing-progress)を監視します。

1. 次のいずれかの操作を行って、**Dynamic Media ビデオを管理します**。

   * ビデオアセットの整理、参照、検索

      * [デジタルアセットの整理](/help/assets/organize-assets.md)。
詳しくは、[処理プロファイルを使用するためのデジタルアセットの整理におけるベストプラクティス](organize-assets.md)を参照してください。

      * [ビデオアセットを検索](search-assets.md#custompredicates)するか[アセットを検索](/help/assets/search-assets.md)します。

   * ビデオアセットをプレビューして公開します。

      * ソースビデオとビデオのエンコードされたレンディションを、関連するサムネールと共に表示します。
        [ビデオをプレビュー](managing-video-assets.md#upload-and-preview-video-assets)するか[アセットをプレビュー](previewing-assets.md)します。
        [ビデオレンディションを表示](video-renditions.md)
        [ビデオレンディションを管理します](manage-assets.md#managing-renditions)。

      * [ビューアプリセットの管理](managing-viewer-presets.md)
      * [アセットを公開します。](publishing-dynamicmedia-assets.md)

   * ビデオのメタデータを操作します。

      * フレームレート、オーディオおよびビデオのビットレート、コーデックなど、エンコードされたビデオレンディションのプロパティを表示します。
        [ビデオレンディションのプロパティを表示](video-renditions.md)

      * タイトル、説明、タグ、カスタムメタデータフィールドなど、ビデオのプロパティを編集します。
        [ビデオのプロパティを編集します](manage-assets.md#editing-properties)。

      * [デジタルアセットのメタデータの管理](metadata.md)
      * [メタデータスキーマ](metadata-schemas.md)

   * ビデオをレビューおよび承認し、注釈を付け、完全なバージョン管理を維持します。

      * [ビデオの注釈](managing-video-assets.md#annotate-video-assets)または[アセットの注釈](manage-assets.md#annotating)

      * [バージョンを作成します。](manage-assets.md#asset-versioning)
      * [アセットにワークフローを適用](assets-workflow.md)または[アセットでワークフローを開始](manage-assets.md#starting-a-workflow-on-an-asset)を参照

      * [フォルダーのアセットのレビュー](bulk-approval.md)
      * [プロジェクト](../sites-authoring/projects.md)

1. 次のいずれかの操作を行って、**Dynamic Media ビデオを公開します**。

   * Adobe Experience Manager を web コンテンツ管理システムとして使用する場合、web ページにビデオを直接追加できます。

      * [Web ページにビデオを追加します](adding-dynamic-media-assets-to-pages.md)。

   * サードパーティの web コンテンツ管理システムを使用している場合、web ページにビデオをリンクするか、ビデオを埋め込むことができます。

      * URL を使用したビデオの統合：
        [Web アプリケーションに URL をリンクします](linking-urls-to-yourwebapplication.md)。

      * Web ページの埋め込みコードを使用したビデオの統合：
        [Web ページにビデオビューアを埋め込みます](embed-code.md)。

   * [ビデオレポートを生成します](#viewing-video-reports)。

   * [ビデオにキャプションを追加します](#adding-captions-to-video)。

## Dynamic Media でのビデオの操作 {#working-with-video-in-dynamic-media}

Dynamic Media のビデオは、高品質のアダプティブビデオを簡単に公開して、デスクトップ、iOS、Android™、BlackBerry®、Windows などのモバイルデバイスを含む複数の画面にストリーミングするためのエンドツーエンドのソリューションです。アダプティブビデオセットでは、同じビデオを、400 kbps、800 kbps、1000 kbps などの様々なビットレートと形式でエンコードしたバージョンにグループ分けします。デスクトップコンピューターまたはモバイルデバイスによって、利用可能な帯域幅が検出されます。

例えば、iOS モバイルデバイスでは、3G、4G、Wi-Fi などの帯域幅が検出されます。次に、アダプティブビデオセット内の様々なビデオビットレートの中から、適切なエンコード済みビデオが自動的に選択されます。ビデオはデスクトップ、モバイルデバイスまたはタブレットにストリーミングされます。

また、デスクトップまたはモバイルデバイスでネットワークの状態が変化した場合は、ビデオ画質が自動的に動的に切り替わります。また、顧客がデスクトップで全画面表示モードに入ると、アダプティブビデオセットはより高い解像度を使用して顧客の視聴エクスペリエンスを向上させるよう対応します。アダプティブビデオセットを使用すると、Dynamic Media ビデオを複数の画面とデバイスで再生するユーザーにとって最適な再生方法が提供されます。

再生または再生時に選択するエンコード済みビデオの決定に、ビデオプレーヤーが使用するロジックは、次のアルゴリズムに基づきます。

1. ビデオプレーヤーは、プレーヤー自体の「初期ビットレート」に設定されている値に最も近いビットレートで、初期ビデオフラグメントを読み込みます。
1. ビデオプレーヤーは、帯域幅の速度の変化に応じて、次の条件に従って切り替わります。

   1. プレーヤーは、見積もり帯域幅を超えない範囲内で、最も高い帯域幅でのストリームを選択します。
   1. プレーヤーは、使用可能な帯域幅の 80％ほどを見積もります。ただし、使用可能な帯域幅が上昇した場合は、帯域幅を大きく見積もりすぎてすぐに元の帯域幅に戻ることを防ぐために、より控えめな 70％ほどの見積もりとなります。

アルゴリズムの技術情報について詳しくは、[https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp) を参照してください。

単一のビデオとアダプティブビデオセットの管理では、次の機能がサポートされています。

* 多数のサポートされているビデオ形式およびオーディオ形式からビデオをアップロードし、複数の画面で再生できるようにビデオを MP4 H.264 形式にエンコーディングします。事前定義済みのアダプティブビデオセット、1 つのビデオのエンコーディングプリセットを使用するか、独自のエンコーディングをカスタマイズしてビデオの品質とサイズを制御できます。

   * 生成されるアダプティブビデオセットには、MP4 ビデオが含まれます。
   * **メモ**：プライマリビデオ（ソースビデオ）はアダプティブビデオセットには追加されません。

* すべての HTML5 ビデオビューアーでビデオキャプションを追加します。
* ビデオアセットを効率的に管理するための完全なメタデータサポートを使用して、ビデオを整理、参照および検索します。
* Web やデスクトップおよびモバイルデバイス（iPhone、iPad、Android™、BlackBerry®、Windows Phone など）に対してアダプティブビデオセットを配信します。

アダプティブビデオのストリーミングは、各種 iOS プラットフォームでサポートされています。詳しくは、[Dynamic Media ビューアリファレンスガイド](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html?lang=ja#video)を参照してください。

Dynamic Media では、MP4 H.264 ビデオのモバイルビデオ再生がサポートされています。このビデオ形式をサポートする BlackBerry® デバイスについては、[BlackBerry® でサポートされているビデオ形式](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482)のページで確認できます。

このビデオ形式をサポートする Windows デバイスについては、[Windows Phone 8 でサポートされているメディアコーデック](https://learn.microsoft.com/ja-jp/windows/uwp/audio-video-camera/supported-codecs)のページで確認できます。

* 以下を含む Dynamic Media ビデオビューアープリセットを使用して、ビデオを再生します。

   * 単一のビデオビューア。
   * ビデオコンテンツと画像コンテンツの両方を組み合わせた混在メディアビューア。

* 自社ブランドのニーズに合わせてビデオプレーヤーを設定します。
* 単純な URL か埋め込みコードを使用して、ビデオを web サイト、モバイルサイトまたはモバイルアプリケーションに統合します。

<!-- See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample. -->

[Experience Manager Assets 用のビューアおよび Dynamic Media Classic 用のビューア](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html?lang=ja#viewers-aem-assets-dmc)と [Experience Manager Assets 専用のビューア](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html?lang=ja#viewers-for-aem-assets-only)を参照してください。

## ベストプラクティス：HTML5 ビデオビューアの使用 {#best-practice-using-the-html-video-viewer}

Dynamic Media の HTML5 ビデオビューアープリセットは、堅牢なビデオプレーヤーです。このプリセットを使用すれば、HTML5 ビデオ再生に関連する多くの一般的な問題のほか、アダプティブビットレートストリーミング配信の欠如やデスクトップブラウザーの限られたリーチなど、モバイルデバイスに関連する問題を回避することができます。

プレーヤーの設計側では、標準の web 開発ツールでビデオプレーヤーの機能を設計できます。例えば、HTML5 と CSS を使用して、ボタン、コントロールおよびカスタムのポスター画像背景をデザインすることにより、カスタマイズした表示で顧客にリーチすることができます。

ビューアーの再生側では、ブラウザーのビデオ機能が自動的に検出されます。次に、アダプティブビットレートストリーミングとも呼ばれる、HLS（HTTP ライブストリーミング）または DASH（HTTP での動的アダプティブストリーミング）を使用してビデオを提供します。これらの配信方法が使用できない場合は、HTML5 プログレッシブが代わりに使用されます。

単一のプレーヤーにまとめることで、次のようなことができるようになりました。

* HTML5 と CSS を使って再生コンポーネントをデザインする機能
* 埋め込み再生する機能
* ブラウザーの機能に応じて、アダプティブストリーミングとプログレッシブストリーミングを使い分ける

リッチメディアコンテンツの配信範囲をデスクトップユーザーとモバイルユーザーの両方に拡大し、ビデオエクスペリエンスを確実に効率化することができます。

[HTML5 ビューアについて](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html?lang=ja#viewers-for-aem-assets-only)も参照してください。

### HTML5 ビデオビューアを使用した、デスクトップコンピューターおよびモバイルデバイス上でのビデオ再生 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

デスクトップおよびモバイルへのアダプティブビデオストリーミングの場合、ビットレートの切り替えに使用されるビデオは、アダプティブビデオセット内のすべての MP4 ビデオに基づいています。

ビデオ再生は、DASH か HLS、またはプログレッシブビデオダウンロードを使用して行われます。6.0、6.1、6.2 など以前の Experience Manager バージョンでは、ビデオは HTTP 上でストリーミングされました。

DM ゲートウェイサービスの URL が常に HTTPS も使用するので、Experience Manager 6.3 以降ではビデオが HTTPS（DASH または HLS） でストリーミングされるようになりました。このデフォルトの動作はユーザーに影響しません。つまり、ブラウザーでサポートされていない場合を除き、ビデオストリーミングは常に HTTPS 上で行われます（次の表を参照）。したがって、

* HTTPS web サイトが HTTPS ビデオストリーミングに対応している場合は、ストリーミングが適しています。
* HTTP web サイトが HTTPS ビデオストリーミングに対応している場合は、ストリーミングが適しており、web ブラウザーから混合コンテンツに関する問題は発生しません。

DASH は国際標準であり、HLS は Apple の標準です。どちらもアダプティブビデオストリーミングに使用されます。どちらのテクノロジーも、ネットワーク帯域幅の容量に基づいて再生を自動的に調整します。また、HLS では、ビデオの残りがダウンロードされるまで待たなくても、ビデオ内の任意のポイントを「シーク」できます。

プログレッシブビデオは、ユーザーのデスクトップシステムやモバイルデバイスにビデオをダウンロードしてローカルに保存することで配信されます。

デバイス、ブラウザーおよびデスクトップコンピューターやモバイルデバイスでの Dynamic Media ビデオビューアによるビデオの再生方法を次の表に示します。

<table>
 <tbody>
  <tr>
   <td><strong>デバイス</strong></td>
   <td><strong>ブラウザー</strong></td>
   <td><strong>ビデオ再生モード</strong></td>
  </tr>
  <tr>
   <td>デスクトップ</td>
   <td>Internet Explorer 9 および 10</td>
   <td>プログレッシブダウンロード。</td>
  </tr>
  <tr>
   <td>デスクトップ</td>
   <td>Internet Explorer 11+</td>
   <td>Windows 8 および Windows 10 - DASH* または HLS が要求された場合、常に HTTPS の使用を強制します。既知の制約事項：このブラウザーとオペレーティングシステムの組み合わせでは、DASH* または HLS で HTTP は機能しません。<br /> <br />Windows 7 - プログレッシブダウンロード。HTTP プロトコルと HTTPS プロトコルの選択に標準のロジックを使用します。</td>
  </tr>
  <tr>
   <td>デスクトップ</td>
   <td>Firefox 23～44</td>
   <td>プログレッシブダウンロード。</td>
  </tr>
  <tr>
   <td>デスクトップ</td>
   <td>Firefox 45 以降</td>
   <td>DASH* または HLS アダプティブビットレートストリーミング。</td>
  </tr>
  <tr>
   <td>デスクトップ</td>
   <td>Chrome</td>
   <td>DASH* または HLS アダプティブビットレートストリーミング。</td>
  </tr>
  <tr>
   <td>デスクトップ</td>
   <td>Safari（Mac）</td>
   <td>HLS アダプティブビットレートストリーミング。</td>
  </tr>
  <tr>
   <td>モバイル</td>
   <td>Chrome（Android™ 6 以前）</td>
   <td>プログレッシブダウンロード。</td>
  </tr>
  <tr>
   <td>モバイル</td>
   <td>Chrome（Android™ 7 以降）</td>
   <td>DASH* または HLS アダプティブビットレートストリーミング。</td>
  </tr>
  <tr>
   <td>モバイル</td>
   <td>Android™（デフォルトブラウザー）</td>
   <td>プログレッシブダウンロード。</td>
  </tr>
  <tr>
   <td>モバイル</td>
   <td>Safari（iOS）</td>
   <td>HLS アダプティブビットレートストリーミング。</td>
  </tr>
  <tr>
   <td>モバイル</td>
   <td>Chrome（iOS）</td>
   <td>HLS アダプティブビットレートストリーミング。</td>
  </tr>
  <tr>
   <td>モバイル</td>
   <td>BlackBerry®</td>
   <td>DASH* または HLS アダプティブビットレートストリーミング。/td&gt;
  </tr>
 </tbody>
</table>

>[!IMPORTANT]
>
>*ビデオに DASH を使用するには、まずアカウントの Adobe テクニカルサポートが DASH を有効にする必要があります。詳しくは、[アカウントでの DASH の有効化](#enable-dash)を参照してください。

## Dynamic Media ビデオソリューションのアーキテクチャ {#architecture-of-dynamic-media-video-solution}

次の図に、アップロード後、（Dynamic Media Hybrid モードの）DMGateway によってエンコードされ、公開されるビデオのオーサリングワークフローの全体像を示します。

![chlimage_1-427](assets/chlimage_1-427.png)

## ビデオのハイブリッド公開アーキテクチャ {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## ビデオエンコーディングのベストプラクティス {#best-practices-for-encoding-videos}

Dynamic Media を有効にし、ビデオクラウドサービスを設定済みの場合、**Dynamic Media エンコードビデオ**&#x200B;ワークフローがビデオをエンコードします。このワークフローは、ワークフローの処理履歴とエラー情報を取り込みます。Dynamic Media を有効にし、ビデオ Cloud Services を設定してある場合は、ビデオをアップロードすると、**[!UICONTROL Dynamic Media エンコーディングビデオ]**&#x200B;ワークフローが自動的に有効になります（Dynamic Media を使用していない場合は、**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローが有効になります）。

<!-- DEAD The following are best-practice tips for encoding source video files.

For advice about video encoding, see [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en).

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en). -->

### ソースビデオファイル {#source-video-files}

ビデオファイルをエンコードする場合は、可能な限り高品質のソースビデオファイルを使用します。以前にエンコードされたビデオファイルの使用は避けてください。そのようなファイルは既に圧縮済みで、さらにエンコードすると標準を下回る品質のビデオが作成されるからです。

* Dynamic Media では、最大長 30 分、最小解像度が 25 x 25 を超える短い形式のビデオが主にサポートされています。
* 15 GB までのプライマリソースビデオファイルをアップロードできます。

次の表に、ソースビデオファイルのエンコード前の推奨サイズ、縦横比および最小ビットレートを示します。

| サイズ | 縦横比 | 最小ビットレート |
|--- |--- |--- |
| 1,024 x 768 | 4:3 | 4,500 kbps（ほとんどのビデオ） |
| 1,280 x 720 | 16:9 | 3,000～6,000 kbps（ビデオ内のモーションの量に応じて調整） |
| 1,920 x 1,080 | 16:9 | 6,000～8,000 kbps（ビデオ内のモーションの量に応じて調整） |

### ファイルのメタデータの取得 {#obtaining-a-file-s-metadata}

ファイルのメタデータを取得するには、ビデオ編集ツールを使用してメタデータを表示するか、メタデータを取得するために設計されたアプリケーションを使用します。 次に、サードパーティアプリケーションである MediaInfo を使用してビデオファイルのメタデータを取得する手順を示します。

1. [MediaInfo のダウンロードページ](https://mediaarea.net/ja/MediaInfo/Download)に移動します。
1. GUI バージョンのインストーラーを選択してダウンロードし、インストール手順に従って操作します。
1. インストールの完了後、ビデオファイルを右クリックして（Windows のみ）MediaInfo を選択するか、MediaInfo を開いてビデオファイルをアプリケーションにドラッグします。ビデオの幅、高さ、fps を含む、ビデオファイルに関連するすべてのメタデータが表示されます。

### 縦横比 {#aspect-ratio}

プライマリソースビデオファイルのビデオエンコーディングプリセットを選択または作成するときには、プライマリソースビデオファイルと同じ縦横比をプリセットに使用してください。縦横比とは、ビデオの高さに対する幅の比率のことです。

ビデオファイルのアスペクト比を求めるには、ファイルのメタデータを取得し、そのファイルの幅と高さを記録します（前述の「ファイルのメタデータの取得」を参照してください）。さらに、次の式を使用してアスペクト比を計算します。

幅/高さ = 縦横比

次の表に、この式の解を一般的な縦横比に変換した結果を示します。

| 数式の結果 | 縦横比 |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

例えば、幅 1,440、高さ 1,080 のビデオの縦横比は 1,440/1,080、つまり 1.33 になります。このビデオファイルをエンコードするには、縦横比 4:3 のビデオエンコーディングプリセットを選択します。

### ビットレート {#bitrate}

ビットレートとは、1 秒間のビデオ再生を構成するエンコードされたデータの量です。ビットレートは、1 秒あたりのキロビット数（Kbps）の単位で測定します。

>[!NOTE]
>
>すべてのコーデックは非可逆圧縮を使用するので、ビットレートはビデオ画質の最も重要な要素となります。非可逆圧縮では、ビデオファイルを圧縮するほど画質が低下します。したがって、他の特性（解像度、フレームレートおよびコーデック）がすべて等しい場合は、ビットレートが低いほど、圧縮ファイルの品質は低下します。

ビットレートエンコーディングは 2 種類あり、そのどちらかを選択できます。

* **[!UICONTROL 固定ビットレートエンコーディング]**（CBR）- CBR エンコーディングでは、ビットレートまたは 1 秒あたりのビット数が、エンコーディングプロセス全体で同じ数値に維持されます。CBR エンコーディングでは、設定されているデータレートが、ビデオ全体での設定値として使用されます。また、CBR エンコーディングでは、メディアファイルの品質は最適化されませんが、その分、空き容量の節約になります。ビデオ全体に同じようなモーションレベルが含まれている場合は、CBR を使用します。CBR は、ビデオコンテンツのストリーミングに最も一般的に使用されています。[カスタムで追加するビデオエンコーディングパラメーターの使用](/help/assets/video-profiles.md#using-custom-added-video-encoding-parameters)も参照してください。

* **[!UICONTROL 可変ビットレートエンコーディング]**（VBR）- VBR エンコーディングでは、コンプレッサーで必要となるデータに基づいて、設定したデータレートが下限から上限の範囲内で調整されます。つまり、VBR エンコーディングプロセスでは、メディアファイルのビットレートが、そのニーズに応じて動的に増減します。VBR は、CBR よりエンコードに時間がかかりますが、生成されるメディアファイルは最高品質となります。VBR は、ビデオコンテンツの HTTP プログレッシブ配信に最も一般的に使用されます。

VBR と CRB のどちらを使用するべきかVBR と CBR のどちらを選択すべきかと言えば、ほとんどの場合、メディアファイルには VBR を使用することをお勧めします。VBR は、優位性のあるビットレートで CBR より高品質のファイルを生成します。VBR を使用するときは、2 パスエンコーディングを使用し、最大ビットレートをターゲットビデオのビットレートの 1.5 倍に設定してください。

ビデオエンコーディングプリセットを選択するときは、ターゲットエンドユーザーの接続速度を念頭に置いてください。その速度の 80% のデータレートを持つプリセットを選択してください。例えば、ターゲットエンドユーザーの接続速度が 1,000 Kbps の場合、ビデオデータレートが 800 kbps のプリセットが最適です。

次の表に、一般的な接続速度のデータレートを示します。

| 速度（Kbps） | 接続タイプ |
|--- |--- |
| 256 | ダイヤルアップ接続。 |
| 800 | 一般的なモバイル接続。この接続では、3G エクスペリエンス向けに 400～800 の範囲のデータレートがターゲットとなります。 |
| 2,000 | 一般的なブロードバンドデスクトップ接続。この接続では、800～2,000 Kbps の範囲のデータレートがターゲットとなります。大部分のターゲットは、平均 1,200～1,500 Kbps です。 |
| 5,000 | 一般的な高ブロードバンド接続。ほとんどの消費者は、この速度でのビデオ配信を使用できないので、この上限範囲でのエンコーディングはお勧めしません。 |

### 解像度 {#resolution}

**解像度**&#x200B;は、ビデオファイルの高さと幅をピクセル単位で表したものです。ほとんどのソースビデオは、1920 x 1080 などの高解像度で保存されます。ストリーミング用のソースビデオは、比較的低い解像度（640 x 480 以下）に圧縮されます。

解像度とデータレートは、ビデオ画質を決定する統合的な 2 つの要素です。同じビデオ画質を維持するには、ビデオファイルのピクセル数が多いほど（解像度が高いほど）、データレートを高くする必要があります。例えば、320 x 240 の解像度と 640 x 480 の解像度のビデオファイルで、フレームあたりのピクセル数を考えてみましょう。

| 解像度 | フレームあたりピクセル数 |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

640 x 480 ファイルのピクセル数は、フレームあたり 4 倍になります。この 2 つの解像度の例でデータレートを同じにするには、640 x 480 ファイルを 4 倍に圧縮します。これにより、ビデオの画質が低下する可能性があります。そのため、250 kbps のビデオデータレートの場合、320 x 240 の解像度では高画質になりますが、640 x 480 の解像度では高画質になりません。

一般に、高いデータレートを使用するほど、ビデオの画質は良くなり、高い解像度を使用するほど、その画質を維持するために必要になるデータレートも（解像度が低い場合と比較して）増加します。

解像度とデータレートには関連があるので、ビデオをエンコードする際には次の 2 つの方法から選択できます。

* データレートを選択してから、選択したデータレートで美しく表示される最高の解像度でエンコードします。
* 解像度を選択してから、選択した解像度で高品質のビデオを配信するために必要になるデータレートでエンコードします。

プライマリソースビデオファイルのビデオエンコーディングプリセットを選択（または作成）する場合は、次の表を使用して正しい解像度をターゲットにします。

| 解像度 | 高さ（ピクセル） | 画面サイズ |
|--- |--- |--- |
| 240p | 240 | ごく小さな画面 |
| 300p | 300 | 小型の画面（一般にモバイルデバイス用） |
| 360p | 360 | 小型の画面 |
| 480p | 480 | 中型の画面 |
| 720p | 720 | 大型の画面 |
| 1080p | 1080 | 高画質の大型の画面 |

### Fps（1 秒あたりのフレーム数） {#fps-frames-per-second}

米国と日本では、ほとんどのビデオが 29.97 フレーム/秒（fps）で撮影されます。ヨーロッパでは、ほとんどのビデオが 25 fps で撮影されます。映画は 24 fps で撮影されます。

プライマリソースビデオファイルの fps レートに一致するビデオエンコーディングプリセットを選択します。例えば、プライマリソースビデオが 25 fps の場合は、25 fps のエンコーディングプリセットを選択します。デフォルトでは、すべてのカスタムエンコーディングでプライマリソースビデオファイルの fps が使用されます。そのため、ビデオエンコーディングプリセットを作成するときに、fps 設定を明示的に指定する必要はありません。

### ビデオエンコーディングのサイズ {#video-encoding-dimensions}

最適な結果を得るには、ソースビデオがエンコードされたすべてのビデオの整数倍になるようにエンコーディングのサイズを選択します。

この比率を計算するには、ソースの幅をエンコードされた幅で割って、幅の比率を求めます。次に、ソースの高さをエンコードの高さで割って高さの比率を求めます。

結果の比率が整数の場合、ビデオは最適に拡大／縮小されます。結果の比率が整数でない場合は、余ったピクセルのアーティファクトがディスプレイに残るので、ビデオの画質に影響します。この影響は、ビデオにテキストが含まれる場合に特に目立ちます。

例えば、ソースビデオが 1920 x 1080 だとします。次の表では、エンコードされた 3 つのビデオで使用する、最適なエンコード設定を示しています。

| ビデオタイプ | 幅 x 高さ | 幅の比率 | 高さの比率 |
|--- |--- |--- |--- |
| ソース | 1920 x 1080 | 1 | 1 |
| エンコード済み | 960 x 540 | 2 | 2 |
| エンコード済み | 640 x 360 | 3 | 3 |
| エンコード済み | 480 x 270 | 4 | 4 |

### エンコードされたビデオのファイル形式 {#encoded-video-file-format}

Dynamic Media では、MP4 H.264 ビデオエンコーディングプリセットの使用をお勧めします。MP4 ファイルでは H.264 ビデオコーデックが使用されるので、高品質のビデオを圧縮されたファイルサイズで作成できます。

### アカウントでの DASH の有効化 {#enable-dash}

DASH（HTTP での動的アダプティブストリーミング）はビデオストリーミングの国際標準であり、様々なビデオビューアーで広く採用されています。アカウントで DASH が有効になっている場合は、アダプティブビデオストリーミング用に DASH または HLS のいずれかを選択できます。ビューアのプリセットで再生タイプとして「**[!UICONTROL 自動]**」が選択されていると、プレーヤー間の自動切り替えで両方を選択できます。

アカウントで DASH を有効にする場合の主なメリットには、次のようなものがあります。

* アダプティブビットレートストリーミング用に DASH ストリームビデオをパッケージ化できます。この方法では配信の効率が向上します。アダプティブストリーミングにより、顧客に最適な視聴エクスペリエンスが提供されます。
* Dynamic Media プレイヤーでブラウザーに最適化されたストリーミングにより、HLS と DASH のストリーミングを切り替え、最高のサービス品質を確保できます。Safari ブラウザーを使用すると、ビデオプレーヤーが HLS に自動的に切り替わります。
* ビデオビューアプリセットを編集して、優先ストリーミング方式（HLS または DASH）を設定できます。
* 最適化されたビデオエンコーディングにより、DASH 機能を有効にしながら、追加のストレージを使用しなくて済みます。HLS と DASH の両方に対して 1 つのビデオエンコードセットが作成され、ビデオの保存コストが最適化されます。
* 顧客がビデオ配信をアクセスしやすくなります。
* API を使用してストリーミング URL を取得することもできます。

アカウントで DASH を有効にするには、次の 2 つの手順が必要です。

* DASH を使用するように Dynamic Media を設定します。これは、自分で簡単に行えます。
* Experience Manager 6.5 で DASH を使用するように設定します。これは、Adobe カスタマーサポートにケースを作成して送信することにより行います。

**アカウントで DASH を有効にするには**

1. **Dynamic Media の設定** - Experience Manager 6.5 の Dynamic Media で、[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) に移動します。
1. 「**AEM Assets Dynamic Media のビデオの高度なストリーミング**」機能フラグを検索します。
1. DASH を有効（オン）にするには、チェックボックスをオンにします。
1. 「**[!UICONTROL 保存]**」を選択します。
1. **Experience Manager 6.5 の設定** - [Admin Console で新しいサポートケースの作成を開始します。](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)
1. サポートケースを作成するには、手順に従いながら次の情報を入力します。

   * 主要連絡先の氏名、メールアドレス、電話番号。
   * Dynamic Media アカウントの名前。
   * Experience Manager 6.5 で DASH を有効にするように指定します。

1. アドビカスタマーサポートでは、リクエストが送信された順序に基づいて、DASH の順番待ちリストに追加します。
1. リクエストを処理する準備が整った時点で、カスタマーサポートから連絡を差し上げ、DASH を有効にする日付の調整と設定を行います。
1. 完了後、カスタマーサポートから通知があります。
1. 通常通り、[ビデオビューアープリセット](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset)を作成します。

## ビデオレポートの表示 {#viewing-video-reports}

>[!NOTE]
>
>ビデオレポートを使用できるのは、Dynamic Media - ハイブリッドモードを実行している場合のみです。

ビデオレポートは、指定した時間にわたるいくつかの集計指標を表示し、*公開された*&#x200B;個別および集計ビデオが期待通りに実行されていることを監視するのに役立ちます。次の上位指標データは、web サイト全体で公開されているすべてのビデオについて集計されます。

* ビデオ開始
* 完了率
* ビデオの平均視聴時間
* ビデオの合計視聴時間
* 訪問別ビデオ数

すべての&#x200B;*公開済み*&#x200B;ビデオの表も表示されるので、ビデオ開始数の合計に基づいて、web サイトで視聴された上位のビデオを追跡できます。

リストのビデオ名をタップすると、ビデオのオーディエンス保持（ドロップオフ）レポートが折れ線グラフの形式で表示されます。このグラフには、ビデオ再生の特定の時点におけるビュー数が表示されます。ビデオを再生すると、プレーヤーの時間インジケーターと同期して縦棒が表示されていきます。この折れ線グラフが急激に下る箇所は、オーディエンスが関心をなくして再生を終了した時点を示しています。

ビデオが Adobe Experience Manager Dynamic Media 以外でエンコードされた場合、オーディエンス保持（ドロップオフ）グラフおよび表内の再生率データは利用できません。

[Dynamic Media クラウドサービスの設定](/help/assets/config-dynamic.md)も参照してください。

>[!NOTE]
>
>トラッキングとレポートのデータは、Dynamic Media 独自のビデオプレーヤーと、関連するビデオプレーヤープリセットの使用にのみ基づいています。そのため、他のビデオプレーヤーを介して再生されたビデオをトラッキングしてレポートすることはできません。

デフォルトでは、ビデオレポートを最初に開いたときに、今月初めから今月の今日の日付までのビデオデータが表示されます。ただし、このデフォルトの日付範囲を上書きして、独自の日付範囲を指定することができます。次回ビデオレポートを開くと、指定した日付範囲が使用されます。

ビデオレポートの正常動作のために、Dynamic Media Cloud Services の設定時に、レポートスイート ID が自動的に作成されます。そのときに、そのレポートスイート ID がパブリッシュサーバーにプッシュされ、アセットのプレビューの際に URL のコピー機能で使用できるようになります。ただし、この機能を使用するには、公開サーバーが既に設定されている必要があります。パブリッシュサーバーがセットアップされていない場合でも、公開してビデオレポートを確認することはできます。ただし、その際には Dynamic Media クラウド設定に戻って「**[!UICONTROL OK]**」をタップする必要があります。

**ビデオレポートを表示するには：**

1. Experience Manager の左上隅にある Experience Manager ロゴをタップし、左のレールで&#x200B;**[!UICONTROL ツール]**（ハンマーのアイコン）／**[!UICONTROL アセット]**／**[!UICONTROL ビデオレポート]**&#x200B;をタップします。
1. ビデオレポートページで、次のいずれかの操作を行います。

   * 右上付近にある&#x200B;**ビデオレポートを更新**&#x200B;アイコンをタップします。「更新」を使用するのは、レポートの終了日が今日の日付である場合のみです。これにより、前回のレポート実行以降に発生したビデオトラッキングを確認できます。

   * 右上付近にある&#x200B;**日付選択**アイコンをタップします。
ビデオデータを表示する開始日と終了日の範囲を指定し、「**[!UICONTROL レポートを実行]**」をタップします。

   「トップの指標」グループボックスに、サイト全体にわたるすべての&#x200B;*公開済み*&#x200B;ビデオに関する様々な集計値が表示されます。

1. 上位の公開済みビデオの一覧表でビデオ名をタップしてビデオを再生し、そのビデオのオーディエンス維持（ドロップオフ）レポートを確認します。

### Dynamic Media HTML5 ビューア SDK を使用して作成したビデオビューアに基づいたビデオレポートの表示 {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

Dynamic Media で標準提供されているビデオビューアを使用している場合、または標準提供のビデオビューアからカスタムのビューアプリセットを作成した場合は、ビデオレポートを表示するために必要な追加手順はありません。ただし、HTML5 ビューア SDK API から独自のビデオビューアを作成した場合は、次の手順を実行して、ビデオビューアが Dynamic Media のビデオレポートにトラッキングイベントを確実に送信するようにしてください。

独自のビデオビューアを作成するには、[Adobe Dynamic Media ビューアリファレンスガイド](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html?lang=ja)および [HTML5 ビューア SDK API](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) を参照します。

**Dynamic Media HTML5 ビューア SDK を使用して作成したビデオビューアに基づいてビデオレポートを表示するには：**

1. 公開済みのビデオアセットに移動します。
1. アセットのページの左上隅付近にある、ドロップダウンリストで「**[!UICONTROL ビューア]**」を選択します。
1. 任意のビデオビューアのプリセットを選択し、埋め込みコードをコピーします。
1. 埋め込みコード内で、以下を使用して行を見つけます。

   `videoViewer.setParam("config2", "<value>");`

   `config2` パラメーターは、HTML5 ビューアでの追跡を有効にします。また、ビデオレポートの設定情報や、お客様固有の Adobe Analytics 設定を含む、会社固有のプリセットでもあります。

   config2 パラメーターの正しい値は、**[!UICONTROL 埋め込みコード]**&#x200B;のコピー機能と **[!UICONTROL URL]** のコピー機能のどちらでも検索できます。**[!UICONTROL URL]** コピーコマンドから取得した URL 内で探すべきパラメーターは、`&config2=<value>` です。この値はほぼ常に `companypreset` ですが、一部のケースでは `companypreset-1`、`companypreset-2` などとなっていることもあります。

1. カスタムのビデオビューアコードで、次の操作をおこなって、ビューアページに AppMeasurementBridge.jsp を追加します。

   * 最初に、`&preset` パラメーターが必要かどうかを判断します。

     `config2` パラメーターが `companypreset` の場合、`&preset=parameter` は&#x200B;*不要*&#x200B;です。

     `config2` がその他の場合は、プリセットパラメーターを `config2` パラメーターと同じに設定します。例えば、`config2=companypreset-2` の場合、`&param2=companypreset-2` を AppMeasurmentBridge.jsp の URL に追加します。

   * 次に、AppMeasurementBridge.jsp にスクリプトを追加します。

     `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. 次の操作をおこなって、TrackingManager コンポーネントを作成します。

   * `s7sdk.Util.init();` を呼び出した後で、次のコードを追加して、イベントを追跡する TrackingManager インスタンスを作成します。

     `var trackingManager = new s7sdk.TrackingManager();`

   * 以下を行って、TrackingManager にコンポーネントを接続します。

     `s7sdk.Event.SDK_READY` イベントハンドラーで、追跡するコンポーネントを TrackingManager に関連付けます。

     例えば、コンポーネントが `videoPlayer` の場合、

     `trackingManager.attach(videoPlayer);`

     追加して、コンポーネントを trackingManager に関連付けます。ページ上の複数のビューアを追跡するには、複数のトラッキングマネージャーコンポーネントを使用します。

   * 次のコードを追加して、AppMeasurementBridge オブジェクトを作成します。

     ```
     var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
     ```

   * 次のコードを追加して、トラッキング関数を追加します。

     ```
     trackingManager.setCallback(appMeasurementBridge.track, 
      appMeasurementBridge);
     ```

   appMeasurementBridge オブジェクトには組み込みのトラッキング関数があります。ただし、複数のトラッキングシステムやその他の機能をサポートするために、独自のトラッキング関数を作成することもできます。

<!--    For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

## ビデオへのキャプションまたはサブタイトルの追加 {#adding-captions-to-video}

クローズドキャプションを 1 つのビデオまたはアダプティブビデオセットに追加することにより、ビデオの配信先をグローバルマーケットまで拡大できます。クローズドキャプションを追加すると、音声をダビングする必要も、異なる言語ごとにネイティブスピーカーの音声を使って再録音する必要もなくなります。ビデオは、録画された言語で再生されます。様々な言語を使う人々が音声を理解できるように、外国語の字幕が表示されます。

クローズドキャプションは、耳の不自由な方にもご利用いただけるため、アクセシビリティの向上にもつながります。

>[!NOTE]
>
>使用するビデオプレーヤーがキャプションの表示に対応する必要があります。

[Dynamic Media のアクセシビリティ](/help/assets/accessibility-dm.md)も参照してください。

Dynamic Media では、キャプションファイルを JSON（JavaScript Object Notation）形式に変換します。このように変換できるので、JSON テキストを、ビデオの完全なトランスクリプトとして表示せずに Web ページに埋め込むことができます。この後、検索エンジンがコンテンツをクロールしてインデックスを作成します。これにより、ビデオを見つけやすくなるとともに、ビデオコンテンツについての追加情報を顧客に提供することができます。

URL で JSON 機能を使用する方法について詳しくは、*Dynamic Media 画像サービングおよびレンダリング API ヘルプ*&#x200B;の[静的コンテンツ（画像以外）の提供](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html?lang=ja#image-serving-api)を参照してください。

**ビデオにキャプションまたはサブタイトルを追加するには:**

1. サードパーティのアプリケーションまたはサービスを使用して、ビデオのキャプションやサブタイトルのファイルを作成します。

   作成するファイルは、WebVTT（Web ビデオテキストトラック）標準に従っている必要があります。キャプションファイル名の拡張子は .vtt です。WebVTT キャプション標準をよく確認してください。

   [WebVTT：Web Video Text Tracks 形式（英語）](https://w3c.github.io/webvtt/)を参照してください。

   Dynamic Media 以外でキャプションやサブタイトルのファイルの作成に使用できる、無料および有料のツールやサービスが用意されています。例えば、スタイル設定なしの単純なビデオキャプションファイルを作成するには、次に示すキャプションの作成および編集用の無償オンラインツールを使用できます。

   [WebVTT Caption Maker](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   良い結果を得るためには、このツールを Explorer 9 以上、Google Chrome、または Safari で使用してください。

   ツールの「**[!UICONTROL ビデオファイルの URL を入力]**」フィールドにビデオファイルの URL をコピーして貼り付け、「**[!UICONTROL 読み込み]**」をクリックします。[アセットの URL の取得](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)を参照して、ビデオファイルそのものの URL を取得し、それを「**[!UICONTROL ビデオファイルの URL を入力]**」フィールドに貼り付けてください。その後、Internet Explorer、Chrome、または Safari で、ビデオを再生できます。

   ここで、サイトの画面に表示される指示に従って、WebVTT ファイルを作成して保存します。完了したら、キャプションファイルの内容をコピーしてプレーンテキストエディターに貼り付け、`.vtt` のファイル拡張子で保存します。

   >[!NOTE]
   >
   >複数言語のビデオサブタイトルを用意してグローバル対応する場合、WebVTT 標準の規定により、サポート対象の言語ごとに個別の .vtt ファイルを作成して呼び出す必要があります。

   一般に、キャプションの VTT ファイルにはビデオファイルと同じ名前を付け、名前の末尾に言語ロケール（-EN、-FR、-DE、-JA など）を追加します。そうしておくと、既存の web コンテンツ管理システムを使用してビデオの URL を自動的に生成する際に役立ちます。

1. Experience Manager で、WebVTT キャプションファイルを DAM にアップロードします。
1. アップロードしたキャプションファイルを関連付ける、*公開済み*&#x200B;ビデオアセットに移動します。

   URL をコピーするには、その&#x200B;*前に*&#x200B;アセットを&#x200B;*公開*&#x200B;しておく必要があります。

   [アセットの公開](/help/assets/publishing-dynamicmedia-assets.md)を参照してください。

1. 次のいずれかの操作を行います。

   * ポップアップビデオビューアエクスペリエンスの場合、「**[!UICONTROL URL]**」をタップします。URL ダイアログボックスで、URL を選択してクリップボードにコピーし、その URL を単純なテキストエディターに貼り付けます。コピーしたビデオの URL を次の構文で追加します。

     `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

     キャプションパスの末尾にある `,1` に注意します。パスの `.vtt` ファイル名拡張子の直後で、ビデオプレーヤーバーのクローズドキャプションボタンの有効（オン）と無効（オフ）を任意に切り替えることができます。それには、それぞれ `,1` または `,0` を設定します。

   * 埋め込みビデオビューアエクスペリエンスの場合、「**[!UICONTROL 埋め込みコード]**」をタップします。埋め込みコードダイアログボックスで、埋め込みコードを選択してクリップボードにコピーし、そのコードを単純なテキストエディターに貼り付けます。コピーした埋め込みコードを次の構文で追加します。

     `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

     キャプションパスの末尾にある `,1` に注意します。パスの `.vtt` ファイル名拡張子の直後で、ビデオプレーヤーバーのクローズドキャプションボタンの有効（オン）と無効（オフ）を任意に切り替えることができます。それには、それぞれ `,1` または `,0` を設定します。

## ビデオへのチャプターマーカーの追加 {#adding-chapter-markers-to-video}

1 つのビデオまたはアダプティブビデオセットにチャプターマーカーを追加すると、長編ビデオの視聴と操作が簡単になります。ユーザーがビデオを再生する際、ビデオタイムライン（別名：ビデオスクラバー）のチャプターマーカーをクリックすると、関心のあるシーンに簡単に移動できます。または、新しいコンテンツ、デモおよびチュートリアルに即座にジャンプすることができます。

>[!NOTE]
>
>ビデオプレーヤーが、チャプターマーカーの使用をサポートしている必要があります。Dynamic Media ビデオプレーヤーは、チャプターマーカーをサポートしていますが、サードパーティのビデオプレーヤーは、チャプターマーカーをサポートしているとは限りません。

必要であれば、ビデオビューアプリセットを使用するのではなく、チャプター機能を備えた独自のカスタムビデオビューアを作成して、ブランディングできます。チャプターナビゲーション機能を備えた独自の HTML5 ビューアを作成する方法については、Adobe HTML5 Viewer SDK API ドキュメントで `s7sdk.video.VideoPlayer` クラスと `s7sdk.video.VideoScrubber` クラスの説明の「Customizing Behavior Using Modifiers」節を参照してください。[HTML5 Viewer SDK API](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) ドキュメントを参照してください。

<!-- If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

ビデオのチャプターリストを作成する方法は、キャプションを作成する方法とほとんど同じです。つまり、WebVTT ファイルを作成します。ただし、WebVTT キャプションファイルも使用する場合は、このファイルを WebVTT ファイルと分けておく必要があります。キャプションとチャプターを 1 つの WebVTT ファイルにまとめることはできません。

チャプターナビゲーション機能を備えた WebVTT ファイルを作成する際に使用するフォーマットの例として、次のサンプルを使用できます。

### ビデオチャプターナビゲーション機能を備えた WebVTT ファイル {#webvtt-file-with-video-chapter-navigation}

```xml
WEBVTT
Chapter 1
00:00.000 --> 01:04.364
The bicycle store behind it all.
Chapter 2
01:04.364 --> 02:00.944
Creative Cloud.
Chapter 3
02:00.944 --> 03:02.937
Ease of management for a working solution.
Chapter 4
03:02.937 --> 03:35.000
Cost-efficient access to rapidly evolving technology.
```

上記の例では、`Chapter 1` はキュー識別子で、オプションです。`00:00:000 --> 01:04:364` のキュー時間は、チャプターの開始時間と終了時間を、`00:00:000` という形式で指定しています。最後の 3 桁はミリ秒で、`000` のまま残しておくこともできます。`The bicycle store behind it all` のチャプタータイトルは、チャプターの内容を示す実際の説明です。ビデオのタイムラインのビジュアルキューポイントにマウスポインターを合わせると、キュー識別子、開始キュー時間およびチャプタータイトルが、ビデオプレーヤーのポップアップに表示されます。

HTML5 ビデオビューアを使用するので、作成するチャプターファイルが WebVTT（Web Video Text Tracks）標準に準拠していることを確認してください。チャプターファイルの拡張子は `.vtt` です。WebVTT キャプション標準をよく確認してください。

 詳しくは、[WebVTT: The Web Video Text Tracks Format](https://w3c.github.io/webvtt/) を参照してください。

**ビデオチャプターナビゲーションを追加するには：**

1. この `.vtt` ファイルを UTF8 エンコーディングで保存して、チャプタータイトルテキストの文字レンディションに関する問題を回避します。

   一般に、チャプター VTT ファイルの名前には、ビデオファイルと同じ名前を付けて、名前の末尾にチャプターを追加します。そうしておくと、既存の web コンテンツ管理システムを使用してビデオの URL を自動的に生成する際に役立ちます。
1. Experience Manager で、WebVTT チャプターファイルをアップロードします。

   [アセットのアップロード](/help/assets/manage-assets.md#uploading-assets)を参照してください。

1. 次のいずれかの操作を行います。

   <table>
     <tbody>
      <tr>
       <td>ポップアップビデオビューアエクスペリエンスの場合</td>
       <td>
       <ol>
       <li>アップロードしたチャプターファイルを関連付ける、<i>公開済み</i>ビデオアセットに移動します。URL をコピーするには、その<i>前に</i>アセットを<i>公開</i>しておく必要があります。<a href="/help/assets/publishing-dynamicmedia-assets.md">アセットの公開</a>を参照してください。</li>
       <li>ドロップダウンメニューで「<strong>ビューア</strong>」をクリックまたはタップします。</li>
       <li>左側のレールで、ビデオビューアプリセット名をタップまたはクリックします。ビデオのプレビューが別のページで開きます。</li>
       <li>左側のレールの下部にある「<strong>URL</strong>」をクリックします。</li>
       <li>URL ダイアログボックスで、URL を選択してクリップボードにコピーし、その URL を単純なテキストエディターに貼り付けます。</li>
       <li>ビデオのコピー済み URL を次の構文で追加すると、チャプターファイルのコピー済み URL に関連付けることができます。<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>埋め込みビデオビューアエクスペリエンスの場合<br /> </td>
       <td>
       <ol>
       <li>アップロードしたチャプターファイルを関連付ける、<i>公開済み</i>ビデオアセットに移動します。URL をコピーするには、その<i>前に</i>アセットを<i>公開</i>しておく必要があります。<a href="/help/assets/publishing-dynamicmedia-assets.md">アセットの公開</a>を参照してください。</li>
       <li>ドロップダウンメニューで「<strong>ビューア</strong>」をクリックまたはタップします。</li>
       <li>左側のレールで、ビデオビューアプリセット名をタップまたはクリックします。ビデオのプレビューが別のページで開きます。</li>
       <li>左側のレールの下部にある「<strong>埋め込み</strong>」をクリックします。</li>
       <li>埋め込みコードダイアログボックスで、コード全体を選択してクリップボードにコピーし、そのコードを単純なテキストエディターに貼り付けます。</li>
       <li>ビデオの埋め込みコードを次の構文で追加して、チャプターファイルのコピー済み URL に関連付けることができます。<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt&gt;"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

## Dynamic Media - Scene7 モードのビデオサムネールについて {#about-video-thumbnails-in-dynamic-media-scene-mode}

ビデオサムネールは、ビデオフレームまたは画像アセットの縮小バージョンで、顧客向けのビデオを表すものです。サムネールは、顧客がビデオを選択するよう促すのに役立ちます。

Experience Manager 内のすべてのビデオには、サムネールを関連付ける必要があります。サムネールを置き換えずに削除することはできません。デフォルトでは、Experience Manager にビデオをアップロードすると、最初のフレームがサムネールとして使用されます。例えば、ブランド設定やビジュアル検索用にサムネールをカスタマイズできます。ビデオのサムネールをカスタマイズするには、ビデオを再生して、使用するフレームで一時停止します。あるいは、Digital Asset Manager に既にアップロードして&#x200B;*公開*&#x200B;している画像アセットを選択できます。

ビデオから選択したカスタムビデオサムネール画像は抽出されず、別個のアセットとして DAM に保存されます。ただし、既存の画像アセットから選択したカスタムビデオサムネイルは JCR に保存されます。選択したアセットのパスは、次のサンプルパスのように、ビデオアセットのノードに保存されます。

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

ビデオのサムネiルをカスタマイズする機能は、ビデオがあるフォルダーにビデオプロファイルを適用した後でのみ使用できます。

「[Dynamic Media - ハイブリッドモード のビデオサムネイルについて](#about-video-thumbnails-in-dynamic-media-hybrid-mode)」も参照してください。

### カスタムビデオサムネールの追加 {#adding-a-custom-video-thumbnail}

これらの手順は、「Dynamicmedia_Scene7」モードで動作している Dynamic Media にのみ適用されます。

**カスタムビデオサムネールを追加するには：**

1. 次の作業が完了していることを確認してください。

   * ビデオアセット用のフォルダーの作成。
   * [ビデオプロファイルをフォルダーに適用します](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).。

   * [フォルダーへのビデオのアップロード](/help/assets/managing-video-assets.md#upload-and-preview-video-assets)。

1. サムネイル画像を変更するアップロード済みビデオアセットに移動します。
1. **[!UICONTROL リスト表示]**&#x200B;または&#x200B;**[!UICONTROL カード表示]**&#x200B;のいずれかのアセット選択モードで、ビデオアセットをタップします。
1. ツールバーで、「**[!UICONTROL プロパティ]**」アイコン（中に「i」がある円）をタップします。
1. ビデオのプロパティページで、「**[!UICONTROL サムネイルを変更]**」をタップします。
1. 「サムネイルを変更」ページで以下のいずれかを行います。

   * ビデオのフレームを新しいサムネイルとして使用するには：

      * ツールバーで「**[!UICONTROL ビデオからフレームを選択]**」をタップします。
      * 「再生」ボタンをタップし、ビデオの新しいサムネールとしてキャプチャするフレームの「一時停止」ボタンをタップします。

   * 画像アセットを新しいサムネールとして使用するには：

      * ツールバーで、「**[!UICONTROL アセットからサムネイルを選択]**」をタップします。
      * 「**[!UICONTROL サムネールを選択]**」をタップします。
      * 使用を希望する、以前にアップロードおよび公開された画像アセットに移動します。アセットは、ビデオのサムネール画像として機能するように自動的にサイズ変更されます。
      * 画像アセットを選択し、「**[!UICONTROL 選択]**」をタップします。

1. 「サムネイルを変更」ページで、「**[!UICONTROL 変更を保存]**」をタップします。
1. ビデオのプロパティページで、右上隅にある「**[!UICONTROL 保存して閉じる]**」をタップします。

## Dynamic Media - ハイブリッドモード のビデオサムネイルについて {#about-video-thumbnails-in-dynamic-media-hybrid-mode}

Dynamic Media で自動的に生成された 10 個のサムネイル画像の中から 1 つを選択して、ビデオに追加できます。選択したサムネールは、Experience Manager Sites、Experience Manager Mobile または Experience Manager Screens のオーサリング環境で Dynamic Media コンポーネントとともにビデオアセットを使用するときに、ビデオプレーヤーに表示されます。このサムネールは、ビデオの内容を最も適切に表し、かつユーザーが再生ボタンをクリックしたくなるような静的画像として提供されます。

Dynamic Media では、ビデオの合計時間に基づいて 10 個（デフォルト）のサムネール画像がキャプチャされます。画像は、1%、11%、21%、31%、41%、51%、61%、71%、81% および 91% でビデオにキャプチャされます。10 個のサムネイルが保持されるので、後で別のサムネールを選択する場合にシリーズを再生成する必要はありません。10 個のサムネール画像をプレビューし、ビデオで使用する画像を選択します。デフォルトに変更する場合は、CRXDE Lite を使用して、サムネール画像が生成される時間間隔を設定できます。例えば、ビデオから均等に配置された 4 つのサムネイル画像のみを生成する場合は、間隔を 24%、49%、74%、99%に設定できます。

ビデオのアップロード後、web サイトにビデオを公開する前に、いつでもビデオサムネiルを追加できるのが理想です。

Dynamic Media で生成されたサムネイルを使用する代わりに、ビデオを表すカスタムサムネイルをアップロードすることもできます。例えば、ビデオのタイトル、人目を引くオープニング画像、またはビデオからキャプチャした特定の画像を含むカスタムサムネール画像を作成できます。アップロードするカスタムビデオサムネール画像は、最大解像度が 1280 x 720 ピクセル（最小幅 640 ピクセル）で、2 MB を超えないようにしてください。

また、[Dynamic Media - Scene7 モードのビデオサムネールについて](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)も参照してください。

### ビデオサムネールの追加 {#adding-a-video-thumbnail}

これらの手順は、ハイブリッドモードで動作している Dynamic Media にのみ適用されます。

**ビデオサムネールを追加するには：**

1. ビデオサムネールを追加する、アップロード済みビデオアセットに移動します。
1. リスト表示またはカード表示のアセット選択モードで、ビデオアセットをタップします。
1. ツールバーで、「**[!UICONTROL プロパティを表示]**」アイコン（中に「i」がある円）をタップします。
1. ビデオのプロパティページで、「**[!UICONTROL サムネイルを変更]**」をタップします。
1. サムネールの変更ページのツールバーで、「**[!UICONTROL フレームを選択]**」をタップします。

   デフォルトの時間間隔またはカスタマイズした時間間隔に基づき、Dynamic Media によって一連のサムネール画像がビデオから生成されます。

1. 生成されたサムネイル画像をプレビューし、ビデオに追加する画像を選択します。
1. 「**[!UICONTROL 変更を保存]**」をタップします。

   ビデオのサムネイル画像が更新され、選択したサムネールが使用されます。後でサムネール画像を変更する場合は、「**[!UICONTROL サムネールを変更]**」ページに戻って新しいサムネイルを選択します。

   新しいデフォルトの時間間隔を設定した場合、または新しいビデオをアップロードして既存のビデオを置き換えた場合は、Dynamic Media によってサムネールを再生成します。

   詳しくは、[ビデオサムネールが生成されるデフォルトの時間間隔の設定](#configuring-the-default-time-interval-that-video-thumbnails-are-generated)を参照してください。

#### ビデオサムネールが生成されるデフォルトの時間間隔の設定 {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

新しいデフォルトの時間間隔を設定して保存すると、今後アップロードするビデオにのみに変更が自動的に適用されます。以前にアップロードしたビデオには、新しいデフォルトは自動的に適用されません。既存のビデオの場合は、サムネールを再生成する必要があります。

詳しくは、[ビデオサムネールの追加](#adding-a-video-thumbnail)を参照してください。

**ビデオサムネールが生成されるデフォルトの時間間隔を設定するには：**

1. Experience Manager で、**[!UICONTROL ツール]**／**[!UICONTROL 一般]**／**[!UICONTROL CRXDE Lite]** をタップします。

1. CRXDE Lite ページの左側にあるディレクトリパネルで、`o etc/dam/imageserver/configuration/jcr:content/settings.` に移動します。

   このディレクトリパネルが表示されない場合は、「ホーム」タブの左側にある >> アイコンをタップします。

1. 右下のパネルにある「プロパティ」タブで、「`thumbnailtime`」をダブルタップします。
1. **[!UICONTROL thumbnailtime を編集]**&#x200B;ダイアログボックスで、テキストフィールドに間隔値を割合で入力します。

   * 1 つ以上の間隔値フィールドを追加するには、プラス記号（+）アイコンをタップします。このアイコンは、ダイアログボックスの下部までスクロールしないと表示されない場合があります。
   * リストから間隔値フィールドを削除するには、そのフィールドの右側にあるマイナス記号（-）アイコンをタップします。
   * 間隔値の順序を変更するには、上向き矢印アイコンと下向き矢印アイコンをタップします。

1. 「**[!UICONTROL OK]**」をタップして、「プロパティ」タブに戻ります。
1. CRXDE Lite ページの左上隅にある「**[!UICONTROL すべて保存]**」をタップした後、左上隅の「ホームに戻る」アイコンをタップして Experience Manager に戻ります。

   詳しくは、[ビデオサムネールの追加](#adding-a-video-thumbnail)を参照してください。

### カスタムビデオサムネールの追加 {#adding-a-custom-video-thumbnail-1}

これらの手順は、ハイブリッドモードで動作している Dynamic Media にのみ適用されます。

**カスタムビデオサムネールを追加するには：**

1. カスタムビデオサムネールを追加するアップロード済みビデオアセットに移動します。
1. リスト表示またはカード表示のアセット選択モードで、ビデオアセットをタップします。
1. ツールバーで、「**[!UICONTROL プロパティを表示]**」アイコン（中に「i」がある円）をタップします。
1. ビデオのプロパティページで、「**[!UICONTROL サムネールを変更]**」をタップします。
1. サムネールの変更ページのツールバーで、「**[!UICONTROL 新しいサムネールをアップロード]**」をタップします。
1. 使用するサムネール画像に移動してその画像を選択し、「**[!UICONTROL 開く]**」をタップして Experience Manager への画像のアップロードを開始します。アップロード後は、必ず画像を公開してください。
1. 画像のアップロードと公開が完了したら、サムネールの変更ページで「**[!UICONTROL 変更を保存]**」をタップします。

   カスタムサムネールがビデオに追加されます。

## Dynamic Media アセットの Dynamic Media URL の変更 {#manifest-urls}

Dynamic Media で処理したビデオは標準のビューアで使用できますが、直接マニフェスト URL にアクセスして独自のカスタムビューアで再生して使用することもできます。次に、ビデオのマニフェスト URL を取得する API を示します。

### getVideoManifestURI API について

`getVideoManifestURI`API は c`q-scene7-api:com.day.cq.dam.scene7.api` を通じて公開され、次のマニフェスト URL を生成するために使用できます。

```java
/**   
* Returns the manifest url for videos 
* @param resource video resource 
* @param manifestType type of video streaming manifest being requested 
* @param onlyIfPublished return a manifest only if the video is published 
* @return the manifest url for videos 
* 
* @throws Exception 
*/
@Nullable 
String getVideoManifestURI(Resource resource, ManifestType manifestType, boolean onlyIfPublished) throws Exception;
```

#### getVideoManifestURI API パラメーター

この API では、次の 3 つのパラメーターを取り込みます。

| パラメーター | 説明 |
| --- | --- |
| `resource` | Dynamic Media が取り込んだビデオに対応するリソース。 |
| `manifestType` | `ManifestType.DASH` または `ManifestType.HLS` のいずれか |
| `onlyIfPublished` | マニフェスト URI が公開され、配信層で使用できる場合にのみ生成される場合に、True に設定します。 |

上記のメソッドを使用してビデオのマニフェスト URL を取得するには、[ビデオエンコーディングプロファイル](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming)を「ビデオのアップロード」フォルダーに追加します。Dynamic Media は、フォルダーに割り当てられたビデオエンコーディングファイルで見つかったエンコーディングに基づいて、これらのビデオを処理します。これで、上記の API を呼び出して、アップロードされたビデオのマニフェスト URL を取得できます。

### エラーシナリオ

エラーがある場合、API は null を返します。例外は、Experience Manager エラーログに記録されます。ログに記録されるこれらのエラーは、すべて `Could not generate Video Manifest URI` で始まります。次のシナリオでは、このようなエラーが発生する可能性があります。

* `IllegalArgumentException` は、次のいずれかに関してログに記録されます。

   * 渡された `resource` パラメーターが null である。
   * 渡された `resource` パラメーターがビデオではない。
   * 渡された `manifestType` パラメーターが null である。
   * `onlyIfPublished` パラメーターは true として渡されたものの、ビデオが公開されていない。
   * Dynamic Media のアダプティブビデオセットを使用してビデオが取り込まれていない。

* `IOException` は、Dynamic Media への接続で問題が発生した場合にログに記録されます。
* 渡された `manifestType` パラメーターが `ManifestType.DASH` であり、ビデオが DASH 形式で処理されていない場合、`UnsupportedOperationException` がログに記録されます。

以下は、*HTTPWhiteBoard* 仕様で記述されたサーブレットを使用した上記の API の例です。コード構文の各タブを選択します。

>[!BEGINTABS]

>[!TAB pom.xml への依存関係の追加]

+++**pom.xml への依存関係の追加**

```java
dependency> 
     <groupId>com.day.cq.dam</groupId> 
     <artifactId>cq-scene7-api</artifactId> 
     <version>5.12.64</version> 
     <scope>provided</scope> 
</dependency> 
```

+++

>[!TAB サンプルサーブレット]

+++**サンプルサーブレット**

```java
@Component
        service = Servlet.class 
) 
@HttpWhiteboardServletPattern(value = ManifestServlet.SERVLET_PATTERN) 
@HttpWhiteboardContextSelect(value = Constants.SERVLET_CONTEXT_SELECTOR) 
public class ManifestServlet extends HttpServlet { 

   private static final Logger LOGGER = LoggerFactory.getLogger(ManifestServlet.class); 

   private final ObjectMapper objectMapper; 

    @Reference 
    private Scene7Service scene7Service; 

   public static final String SERVLET_PATTERN = Constants.VIDEO_API_PREFIX + "/manifestUrl"; 

   public ManifestServlet() {
         this.objectMapper = new ObjectMapper(); 
         objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL); 
   }

   @Override 

   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        final ResourceResolver resolver = getResourceResolver(request); 
        String assetPath = request.getParameter("assetPath"); 
        String manifest = request.getParameter("manifestType"); 
        String onlyIfPublished = request.getParameter("onlyIfPublished"); 
        Resource resource = resolver.getResource(assetPath); 
        response.setCharacterEncoding(StandardCharsets.UTF_8.toString()); 
        response.setContentType("application/json"); 
        if(resource == null) { 
            LOGGER.info("could not retrieve the resource from JCR"); 
            error("could not retrieve the resource from JCR", response); 
            return; 
        }

        String manifestUri = null; 

        try{ 
            ManifestType manifestType =  ManifestType.DASH; 
            if(manifest != null) { 
                manifestType = ManifestType.valueOf(manifest); 
            } 
            manifestUri = scene7Service.getVideoManifestURI(resource, manifestType, onlyIfPublished != null); 
            objectMapper.writeValue(response.getWriter(), new ManifestUrl(manifestUri)); 
            response.setContentType("application/json"); 
        } catch (Exception e) { 
            LOGGER.error(e.getMessage(), e); 
            error(String.format("Unable to get the manifest url for %s. %s", assetPath, e.getMessage()), response); 
        } 
    } 

    private ResourceResolver getResourceResolver(HttpServletRequest request) { 
        Object rr = request.getAttribute(AuthenticationSupport.REQUEST_ATTRIBUTE_RESOLVER); 
        if (!(rr instanceof ResourceResolver)) { 
            throw new IllegalStateException( 
                    "The request does not seem to have been created via Apache Sling's authentication mechanism."); 
        } else { 
            return (ResourceResolver) rr; 
        } 
    } 

    private void error(String errorMessage, HttpServletResponse response) throws IOException { 
        ManifestUrl errorManifest = new ManifestUrl(null); 
        errorManifest.setErrorMessage(errorMessage); 
        response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR); 
        objectMapper.writeValue(response.getWriter(), errorManifest); 
    } 
} 
```

+++

>[!TAB サーブレットの応答クラス]

+++**サーブレットの応答クラス**

```java
public class ManifestUrl extends VideoResponse { 
     String manifestUrl; 
     public ManifestUrl(String manifestUrl) { 
         this.manifestUrl = manifestUrl; 
     } 
     public String getManifestUrl() { 
         return manifestUrl; 
     } 
} 

public abstract class VideoResponse { 
     String errorString; 

     public String getErrorString() { 
         return errorString; 
     } 

     public void setErrorMessage(String errorString) { 
         this.errorString = errorString; 
     } 
} 
```

+++

>[!TAB サーブレットで参照される定数ファイル]

+++**サーブレットで参照される定数ファイル**

```java
public final class Constants { 

     private Constants() { 
     } 

     public static final String VIDEO_API_PREFIX = "/dynamicmedia/video"; 
     public static final String SERVLET_CONTEXT_SELECTOR = "(" + HttpWhiteboardConstants.HTTP_WHITEBOARD_CONTEXT_NAME + "=" + 
             DMSampleApiHttpContext.CONTEXT_NAME + ")"; 

 } 
```

+++

>[!TAB ServletContext]

+++**ServletContext**

`servletContext` を使用して上記のサーブレットをマウントします。以下は `servletContext` の例です。

```java
public class DMSampleApiHttpContext extends ServletContextHelper { 

 public static final String CONTEXT_NAME = "com.adobe.dmSample"; 
 public static final String CONTEXT_PATH = "/dmSample"; 

 private final MimeTypeService mimeTypeService; 

 private final AuthenticationSupport authenticationSupport; 

 /** 
  * Constructs a new context that will use the given dependencies. 
  * 
  * @param mimeTypeService Used when providing mime type of requests. 
  * @param authenticationSupport Used to authenticate requests with sling. 
  */ 
 @Activate 
 public DMSampleApiHttpContext(@Reference final MimeTypeService mimeTypeService, 
                               @Reference final AuthenticationSupport authenticationSupport) { 
     this.mimeTypeService = mimeTypeService; 
     this.authenticationSupport = authenticationSupport; 
 } 

 // ---------- HttpContext interface ---------------------------------------- 
 /** 
  * Returns the MIME type as resolved by the <code>MimeTypeService</code> or 
  * <code>null</code> if the service is not available. 
  */ 
 @Override 
 public String getMimeType(String name) { 
     MimeTypeService mtservice = mimeTypeService; 
     if (mtservice != null) { 
         return mtservice.getMimeType(name); 
     } 
     return null; 
 } 

 /** 
  * Returns the real context path that is used to mount this context. 
  * @param req servlet request 
  * @return the context path 
  */ 
 public static String getRealContextPath(HttpServletRequest req) { 
     final String path = req.getContextPath(); 
     if (path.equals(CONTEXT_PATH)) { 
         return ""; 
     } 
     return path.substring(CONTEXT_PATH.length()); 
 } 

 /** 
  * Returns a request wrapper that transforms the context path back to the original one 
  * @param req request 
  * @return the request wrapper 
  */ 
 public static HttpServletRequest createContextPathAdapterRequest(HttpServletRequest req) { 
     return new HttpServletRequestWrapper(req) { 

         @Override 
         public String getContextPath() { 
             return getRealContextPath((HttpServletRequest) getRequest()); 
         } 

     }; 

 } 

 /** 
  * Always returns <code>null</code> because resources are all provided 
  * through individual endpoint implementations. 
  */ 
 @Override 
 public URL getResource(String name) { 
     return null; 
 } 

 /** 
  * Tries to authenticate the request using the 
  * <code>SlingAuthenticator</code>. If the authenticator or the Repository 
  * is missing this method returns <code>false</code> and sends a 503/SERVICE 
  * UNAVAILABLE status back to the client. 
  */ 
 @Override 
 public boolean handleSecurity(HttpServletRequest request, 
                               HttpServletResponse response) throws IOException { 

     final AuthenticationSupport authenticator = this.authenticationSupport; 
     if (authenticator != null) { 
         return authenticator.handleSecurity(createContextPathAdapterRequest(request), response); 
     } 

     // send 503/SERVICE UNAVAILABLE, flush to ensure delivery 
     response.sendError(HttpServletResponse.SC_SERVICE_UNAVAILABLE, 
             "AuthenticationSupport service missing. Cannot authenticate request."); 
     response.flushBuffer(); 

     // terminate this request now 
     return false; 
 } 
}
```

+++

>[!ENDTABS]

### サンプルサーブレットの使用

このサーブレットを呼び出すには、`/dmSample/dynamicmedia/video/manifestUrl` で `GET` 操作を実行します。次のクエリパラメーターが渡されます。

| クエリパラメーター | 説明 |
| --- | --- |
| `assetPath` | 必須です。ビデオのパス。`manifestUrl` が生成されます。 |
| `manifestType` | オプション。パラメーターは DASH または HLS です。渡されない場合は、デフォルトで DASH に設定されます。 |
| `onlyIfPublished` | オプション。渡された場合、ビデオが公開された場合にのみ `manifestUrl` が返されます。 |

この例では、次の設定を考えます。

* 会社は `samplecompany` です。
* オーサリングインスタンスは `http://sample-aem-author.com` です。
* フォルダー `/content/dam/video-example` には、ビデオエンコーディングプロファイルが適用されています。
* ビデオ `scenery.mp4` がフォルダー `/content/dam/video-example` にアップロードされています。

サーブレットは、次の方法で呼び出すことができます。

| タイプ | 説明 |
| :--- | --- |
| HLS | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=HLS&assetPath=/content/dam/video-example/scenery.mp4`<br><br>DASH 配信が有効な場合：<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8?packagedStreaming=true"}`<br><br>DASH 配信が無効な場合：<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8"}` |
| DASH | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scenery.mp4`<br><br>DASH 配信が有効な場合：<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.mpd"}`<br><br>DASH 配信が無効な場合：<br>`{}` |
| エラー：アセットのパスが正しくありません | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scennnnnnery.mp4`<br><br>`{"errorString":"could not retrieve the resource from JCR"}` |


