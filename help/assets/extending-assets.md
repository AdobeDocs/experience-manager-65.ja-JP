---
title: ' [!DNL Assets] のカスタマイズと拡張'
description: アセット共有とアセットエディターのカスタマイズと拡張をおこなう方法について説明します。これにより、ユーザーに合わせたインターフェイスと一連の機能が提供されます。
contentOwner: AG
role: Developer
feature: Developer Tools
exl-id: 0271c528-23b0-4a3a-b5e8-5baf6cdeecc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '253'
ht-degree: 100%

---

# [!DNL Assets] のカスタマイズと拡張 {#customizing-and-extending-assets}

アセットエディターは、Adobe Enterprise Manager の web サイトのユーザーがリポジトリー内のデジタルアセットを検索、表示および操作するために使用する主要なアクセスポイントです。

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

* ロゴ：組織の独自のロゴをインターフェイスに追加できます。
* 色およびフォント：インターフェイスで使用される色およびフォントを変更できます。
* HTML コード：より完全にカスタマイズするために、インターフェイス定義の基盤となる HTML コードを変更できます。

## レンディションのカスタマイズ {#customizing-renditions}

[!DNL Experience Manager Assets] の用語では、レンディションとは、アセットが表示されるフォームを指します。通常、特定のアセットは、複数のレンディションを持つ場合があります。例えば、フルカラー画像は、1 つのレンディションをオリジナルのサイズで保持し、別のレンディションを縮小サイズで、さらに別のレンディションを縮小されグレースケールに変換された状態で保持している場合があります。

特定のアセットを利用できるレンディションは、カスタマイズできます。また、新しいレンディションを作成することもできます。
