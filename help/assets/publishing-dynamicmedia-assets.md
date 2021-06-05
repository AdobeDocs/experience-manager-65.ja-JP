---
title: Dynamic Media アセットの公開
description: Dynamic Media Assetsの公開方法
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
role: Business Practitioner, Administrator
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: 公開
source-git-commit: 1349d9929fc64ad46fc91f0d189bab54cca9de81
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 50%

---

# Dynamic Media アセットの公開 {#publishing-dynamic-media-assets}

Dynamic Media アセットを公開するには、既にアップロード済みのアセットを選択し、「**[!UICONTROL 公開]**」または「**[!UICONTROL クイック公開]**」をタップします。Dynamic Mediaアセットを公開したら、URLを使用してWebページに含めたり、ページにコードを埋め込んだりできます。

また、ユーザーの介入なしに、アップロードしたアセットを即座に公開することもできます。 [Dynamic Media - Scene7モード](config-dms7.md)の設定を参照してください。
または、フォルダーレベルで**[!UICONTROL 選択的公開]**&#x200B;を使用して、相互に排他的なアセットをDynamic MediaまたはAdobe Experience Managerに選択的に公開することもできます。 [Dynamic Mediaでの選択的公開の操作](/help/assets/selective-publishing.md)を参照してください。

**[!UICONTROL カード表示]**&#x200B;で、アセット名のすぐ下、アセットが発行されたことを示す日時の左側に、小さな地球アイコンが表示されます。**[!UICONTROL リスト表示]**&#x200B;では、公開されたアセットと公開されていないアセットが「**[!UICONTROL 公開]**」列でわかります。

>[!NOTE]
>
>アセットが既に公開されている場合は、「Experience Manager」を使用してアセットを別のフォルダーに移動し、新しい場所から再公開します。 新しく再公開したアセットとともに、最初に公開したアセットの場所も引き続き使用できます。ただし、最初に公開したアセットは Experience Manager からは「消失」しているので、非公開にすることができません。そのため、ベストプラクティスとしては、アセットを別のフォルダーに移動する前に、アセットを非公開にしてください。

ビデオアセットをエンコードした後すぐに公開する場合は、エンコードがおこなわれていることを確認します。 ビデオがエンコードされている間、システムはビデオ処理ワークフローが進行中であることを知らせます。 ビデオのエンコーディングが完了すると、ビデオレンディションをプレビューできます。 その時点で、公開エラーが発生することなく、安全にビデオを公開できます。

[Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)も参照してください。

[WebページへのDynamic Mediaビデオビューアまたは画像ビューアの埋め込み](embed-code.md)も参照してください。

>[!NOTE]
>
>* アセットの URL を使用するためには、そのアセットを公開する必要があります。アセットが公開されていない場合、URLのコピーおよびWebブラウザーへの貼り付けは機能しません。
>* ライブ配信をするには、画像プリセットおよびビューアプリセットをアクティベートして公開する必要があります。

>



セットまたはアセットの公開について詳しくは、[アセットの公開](manage-assets.md)を参照してください。

## Dynamic Media アセットの HTTP/2 配信 {#http-delivery-of-dynamic-media-assets}

Experience Managerは、HTTP/2を介したすべてのDynamic Mediaコンテンツ（画像とビデオ）の配信をサポートするようになりました。 つまり、画像やビデオの公開済み URL や埋め込みコードは、ホストされるアセットを受け取るアプリケーションとの統合に使用できます。その公開済みアセットは、その後、HTTP/2 プロトコルで配信されます。この配信方法により、ブラウザーとサーバーの通信が向上し、すべての Dynamic Media アセットの応答時間と読み込み時間が短くなります。

詳しくは、[HTTP/2配信のコンテンツに関するよくある質問](/help/sites-administering/scene7-http2faq.md)を参照してください。
