---
title: ' [!DNL Assets] のカスタマイズと拡張'
description: アセット共有とアセットエディターのカスタマイズと拡張をおこなう方法について説明します。これにより、ユーザーに合わせたインターフェイスと一連の機能が提供されます。
contentOwner: AG
role: Developer
feature: Developer Tools
exl-id: 0271c528-23b0-4a3a-b5e8-5baf6cdeecc7
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 50%

---

# [!DNL Assets] のカスタマイズと拡張 {#customizing-and-extending-assets}

Asset Editor は、AdobeEnterprise Manager Web サイトのユーザーがリポジトリ内のデジタルアセットの検索、表示、操作に使用する主なアクセスポイントです。

[!DNL Experience Manager] の開発者は、アセットエディターを様々な方法でカスタマイズして拡張し、ユーザーに合わせたインターフェイスと一連の機能を提供できます。

以下の領域における機能について、カスタマイズまたは拡張できます。

* [アセットエディターの拡張](asseteditorx.md)
* [アセットの検索機能の拡張](searchx.md)
* [メディアハンドラーとワークフローを使用したアセットの処理](media-handlers.md)
* [アセットとアクティビティストリームの統合](extending-activity-stream.md)
* [アセットのプロキシ開発](proxy.md)
* [ImageMagick 設定のベストプラクティス](best-practices-for-imagemagick.md)

## 外観のカスタマイズ {#customizing-the-look-and-feel}

アセットエディターの外観と操作性に関する以下の特性をカスタマイズできます。

* ロゴ：インターフェイスに独自の組織のロゴを追加できます。
* 色とフォント：インターフェイスで使用する色とフォントを変更できます。
* HTMLコード：より詳細なカスタマイズを行うために、インターフェイスを定義する基になるHTMLコードを変更できます。

## レンディションのカスタマイズ {#customizing-renditions}

[!DNL Experience Manager Assets] の用語では、レンディションとは、アセットが表示されるフォームを指します。一般に、特定のアセットに複数のレンディションが含まれる場合があります。 例えば、フルカラー画像の場合は、元のサイズのレンディションと、縮小されたサイズのレンディション、縮小された後グレースケールに変換されたレンディションがあります。

特定のアセットが使用可能なレンディションは、カスタマイズしたり、新しく作成したりできます。
