---
title: ビデオレンディション
description: ビデオレンディション
uuid: a02f9ec1-30d9-4cbb-8746-8391ac614f0a
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 1601b473-7227-4a56-bb7c-289de2987e4b
exl-id: a644558e-5be9-4ba2-b560-fc300497fbdf
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: ht
source-wordcount: '221'
ht-degree: 100%

---

# ビデオレンディション {#video-renditions}

Adobe Experience Manager Assets では、様々な形式（OGG、FLV など）のビデオアセット用のビデオレンディションが生成されます。

Experience Manager Assets では、メディアアセットの静的レンディションと動的レンディション（DM エンコードされたレンディション）がサポートされています。

静的レンディションは、FFMPEG（システムパスにインストールされ、使用できるもの）を使用してネイティブに生成され、コンテンツリポジトリに保存されます。

DM エンコードされたレンディションは、プロキシサーバーに保存され、実行時に提供されます。

Experience Manager Assets では、クライアントサイドでこのようなレンディションの再生がサポートされています。

特定のビデオアセットのレンディションを表示するには、アセットのページを開いて、グローバルナビゲーションアイコンを選択します。次に、リストから「**[!UICONTROL レンディション]**」を選択します。

![chlimage_1-478](assets/chlimage_1-478.png)

ビデオレンディションのリストは、**[!UICONTROL レンディション]**&#x200B;パネルに表示されます。

![chlimage_1-479](assets/chlimage_1-479.png)

DM エンコードされたレンディションのプロキシサーバーを設定するには、[Dynamic Media クラウドサービスを設定します](config-dynamic.md)。

必要なパラメーターを指定してビデオレンディションを生成するには、[対応するビデオプロファイルを作成](video-profiles.md)します。

プロキシサーバーを設定し、ビデオプロファイルを作成したら、このビデオプリセットを処理プロファイルに追加して、その処理プロファイルをフォルダーに適用することができます。

>[!NOTE]
>
>Microsoft® Internet Explorer 11 では、OGG および WAV ファイルのオーディオは再生できません。拡張子が OGG または WAV のアセットの詳細ページに、エラー `Invalid Source` が表示されます。
>
>MS® Edge および iPad では、OGG ファイルは再生されず、サポートされていない形式というエラーが発生します。
