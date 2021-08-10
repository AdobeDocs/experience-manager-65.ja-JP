---
title: ビデオレンディション
description: ビデオレンディション
uuid: a02f9ec1-30d9-4cbb-8746-8391ac614f0a
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 1601b473-7227-4a56-bb7c-289de2987e4b
exl-id: a644558e-5be9-4ba2-b560-fc300497fbdf
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 39%

---

# ビデオレンディション {#video-renditions}

Adobe Experience Manager Assetsは、OGG、FLVなど、様々な形式のビデオアセット用のビデオレンディションを生成します。

Experience Managerアセットは、メディアアセットの静的レンディションと動的レンディション（DMエンコードされたレンディション）をサポートします。

静的レンディションは、FFMPEG（システムパスにインストールされ、使用できるもの）を使用してネイティブに生成され、コンテンツリポジトリに保存されます。

DM エンコードされたレンディションは、プロキシサーバーに保存され、実行時に提供されます。

Experience Managerアセットは、クライアント側でのこれらのレンディションの再生をサポートします。

特定のビデオアセットのレンディションを表示するには、そのアセットのページを開き、グローバルナビゲーションアイコンを選択します。 次に、リストから「**[!UICONTROL レンディション]**」を選択します。

![chlimage_1-478](assets/chlimage_1-478.png)

ビデオレンディションのリストが&#x200B;**[!UICONTROL レンディション]**&#x200B;パネルに表示されます。

![chlimage_1-479](assets/chlimage_1-479.png)

DMエンコードされたレンディションのプロキシサーバーを設定するには、[Dynamic Media Cloudサービス](config-dynamic.md)を設定します。

必要なパラメーターを指定してビデオレンディションを生成するには、[対応するビデオプロファイルを作成](video-profiles.md)します。

プロキシサーバーを設定し、ビデオプロファイルを作成したら、このビデオプリセットを処理プロファイルに追加して、その処理プロファイルをフォルダーに適用することができます。

>[!NOTE]
>
>Microsoft® Internet Explorer 11のOGGおよびWAVファイルでは、オーディオ再生は機能しません。 拡張子がOGGまたはWAVのアセットの場合、アセットの詳細ページにエラー`Invalid Source`が表示されます。
>
>MS® EdgeおよびiPadでは、OGGファイルは再生されず、サポートされていない形式のエラーが発生します。
