---
title: ' [!DNL Assets] のカスタマイズと拡張'
description: アセット共有とアセットエディターのカスタマイズと拡張をおこなう方法について説明します。これにより、ユーザーに合わせたインターフェイスと一連の機能が提供されます。
contentOwner: AG
role: Developer
feature: Developer Tools
exl-id: 0271c528-23b0-4a3a-b5e8-5baf6cdeecc7
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 40%

---

# [!DNL Assets] のカスタマイズと拡張 {#customizing-and-extending-assets}

Asset Editor は、AdobeEnterprise Manager Web サイトのユーザーがリポジトリ内のデジタルアセットの検索、表示、操作に使用する主なアクセスポイントです。

As an [!DNL Experience Manager] 開発者は、アセットエディターを複数の方法でカスタマイズおよび拡張し、特別にカスタマイズされたインターフェイスと機能のセットをユーザーに提示できます。

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
