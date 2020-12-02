---
title: カスタマイズと拡張 [!DNL Assets]
description: アセット共有とアセットエディターをカスタマイズおよび拡張する方法について説明します。これにより、ユーザーに合わせたインターフェイスと一連の機能が提供されます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 52%

---


# [!DNL Assets] {#customizing-and-extending-assets}のカスタマイズと拡張

アセットエディタは、AdobeEnterprise Manager Webサイトのユーザーがリポジトリ内のデジタルアセットを検索、表示、操作する際に使用する、主要なアクセスポイントです。

[!DNL Experience Manager]開発者は、アセットエディタを様々な方法でカスタマイズおよび拡張でき、カスタマイズされたインターフェイスと機能のセットをユーザに提供できます。

以下の領域における機能について、カスタマイズまたは拡張できます。

* [アセットエディタの拡張](asseteditorx.md)
* [アセット検索の拡張](searchx.md)
* [メディアハンドラーとワークフローを使用したアセットの処理](media-handlers.md)
* [アセットとアクティビティストリームの統合](extending-activity-stream.md)
* [アセットプロキシの開発](proxy.md)
* [ImageMagickを設定するためのベストプラクティス](best-practices-for-imagemagick.md)

## 外観のカスタマイズ{#customizing-the-look-and-feel}

アセットエディタのルック&amp;フィールの次の要素はカスタマイズ可能です。

* ロゴ：組織の独自のロゴをインターフェイスに追加できます。
* 色およびフォント：インターフェイスで使用される色およびフォントを変更できます。
* HTML コード：より完全にカスタマイズするために、インターフェイス定義の基盤となる HTML コードを変更できます。

## レンディションのカスタマイズ{#customizing-renditions}

[!DNL Experience Manager Assets]の用語では、レンディションとはアセットが表示されるフォームです。 通常、特定のアセットは、複数のレンディションを持つ場合があります。例えば、フルカラー画像は、1 つのレンディションをオリジナルのサイズで保持し、別のレンディションを縮小サイズで、さらに別のレンディションを縮小されグレースケールに変換された状態で保持している場合があります。

特定のアセットを利用できるレンディションは、カスタマイズできます。また、新しいレンディションを作成することもできます。
