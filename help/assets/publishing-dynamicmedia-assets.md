---
title: Dynamic Media アセットの公開
description: Dynamic Media アセットの公開方法
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
translation-type: tm+mt
source-git-commit: b8fe3267a808f1a64b78620156826e0b6e3a5676
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 76%

---


# Dynamic Media アセットの公開 {#publishing-dynamic-media-assets}

ダイナミックメディアアセットを公開するには、既にアップロード済みのアセットを選択し、「 **[!UICONTROL 公開]** 」または「 **[!UICONTROL クイック公開]**」をタップします。 ダイナミックメディアアセットが公開されたら、URL経由でWebページに含めたり、ページにコードを埋め込んだりすることができます。

また、ユーザーの介入なしに、アップロードしたアセットを即座に公開することもできます。See [Configuring Dynamic Media - Scene7 mode](config-dms7.md).

カー **[!UICONTROL ド表示で]**、アセット名のすぐ下、アセットが発行されたことを示す日時の左側に、小さなグローブアイコンが表示されます。 **[!UICONTROL リスト表示]**&#x200B;では、公開されたアセットと公開されていないアセットが「**[!UICONTROL 公開]**」列でわかります。

>[!NOTE]
>
>アセットが既に公開されていて、AEM を使用してアセットを別のフォルダーに移動し、その移動先から再公開した場合は、新しく再公開されたアセットに加えて、元の公開済みアセットの場所も使用できる状態のままです。ただし、元の公開済みアセットは AEM からは「消失」しているので、非公開にすることができません。そのため、ベストプラクティスとしては、アセットを別のフォルダーに移動する前に、アセットを非公開にしてください。

ビデオアセットをエンコードした直後に公開する場合は、エンコードが完全に終了していることを確認してください。ビデオのエンコードがまだ完了していない場合は、ビデオ処理ワークフローが実行中であることが通知されます。ビデオのエンコードが完了すると、ビデオレンディションをプレビューできるようになります。その時点で、エラーが発生することなく、安全にビデオを公開できます。

[Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)も参照してください。

See also [Embedding the Dynamic Media Video or Image viewer on a web page](embed-code.md)

>[!NOTE]
>
>* アセットの URL を使用するためには、そのアセットを公開する必要があります。アセットが公開されていない場合、URL をコピーして Web ブラウザーに貼り付けても機能しません。
>* ライブ配信をするには、画像プリセットおよびビューアプリセットをアクティベートして公開する必要があります。
>



一連のアセットを公開する方法について詳しくは、[アセットの公開](managing-assets-touch-ui.md)を参照してください。

## Dynamic Media アセットの HTTP/2 配信 {#http-delivery-of-dynamic-media-assets}

AEM は現在、HTTP/2 上でのすべての Dynamic Media コンテンツ（画像とビデオ）の配信をサポートしています。つまり、画像やビデオの公開済み URL や埋め込みコードは、ホストされるアセットを受け取るアプリケーションとの統合に使用できます。その公開済みアセットは、その後、HTTP/2 プロトコルで配信されます。この配信方法により、ブラウザーとサーバーの通信が向上し、すべての Dynamic Media アセットの応答時間と読み込み時間が短くなります。

詳しくは、[コンテンツの HTTP/2 配信に関する FAQ](/help/sites-administering/scene7-http2faq.md) を参照してください。
