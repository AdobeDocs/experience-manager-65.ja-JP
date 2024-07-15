---
title: Dynamic Media アセットの公開
description: ビデオや画像などの Dynamic Media アセットを公開する方法について説明します。このようなアセットの HTTP/2 配信についても説明します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: Publishing
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 100%

---

# Dynamic Media アセットの公開 {#publishing-dynamic-media-assets}

Dynamic Media アセットを公開するには、既にアップロード済みのアセットを選択し、「**[!UICONTROL 公開]**」または「**[!UICONTROL クイック公開]**」をタップします。Dynamic Media アセットを公開すると、URL を経由して、または web ページにコードを埋め込むことで、web ページに含めることができます。

また、ユーザーの介入なしに、アップロードしたアセットを即座に公開することもできます。[Dynamic Media - Scene7 モードの設定](config-dms7.md)を参照してください。
または、フォルダーレベルで「**[!UICONTROL 選択的公開]**」を使用して、相互に排他的なアセットを Dynamic Media または Adobe Experience Manager に選択的に公開することもできます。詳しくは、[Dynamic Media での選択的公開の操作](/help/assets/selective-publishing.md)を参照してください。

**[!UICONTROL カード表示]**&#x200B;で、アセット名のすぐ下、アセットが発行されたことを示す日時の左側に、小さな地球アイコンが表示されます。**[!UICONTROL リスト表示]**&#x200B;では、公開されたアセットと公開されていないアセットが「**[!UICONTROL 公開]**」列でわかります。

>[!NOTE]
>
>アセットが公開済みの場合は、Experience Manager を使用してアセットを別のフォルダーに移動し、その新しい場所から再公開します。新しく再公開したアセットとともに、最初に公開したアセットの場所も引き続き使用できます。ただし、最初に公開したアセットは Experience Manager からは「消失」しているので、非公開にすることができません。そのため、ベストプラクティスとしては、アセットを別のフォルダーに移動する前に、アセットを非公開にしてください。

ビデオアセットをエンコードした直後に公開する場合は、エンコードが完了していることを確認してください。ビデオがエンコード中の間は、ビデオ処理ワークフローが実行中であることが示されます。ビデオのエンコードが完了すると、ビデオレンディションをプレビューできます。その時点で、公開エラーが発生することなく、安全にビデオを公開できます。

[Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)も参照してください。

[Web ページへの Dynamic Media ビデオビューアまたは画像ビューアの埋め込み](embed-code.md)も参照してください。

>[!NOTE]
>
>* アセットの URL を使用するには、そのアセットを公開する必要があります。アセットが公開されていない場合、URL をコピーして Web ブラウザーに貼り付けても機能しません。
>* ライブ配信をするには、画像プリセットおよびビューアプリセットをアクティベートして公開する必要があります。
>

セットまたはアセットの公開について詳しくは、[アセットの公開](manage-assets.md)を参照してください。

## Dynamic Media アセットの HTTP/2 配信 {#http-delivery-of-dynamic-media-assets}

Experience Manager では、HTTP/2 上でのすべての Dynamic Media コンテンツ（画像とビデオ）の配信をサポートするようになりました。つまり、画像やビデオの公開済み URL または埋め込みコードを、ホストされているアセットを受け入れる任意のアプリケーションと統合できるようになります。その公開済みアセットは、HTTP/2 プロトコルを使用して配信されます。この配信方法により、ブラウザーとサーバーの通信が向上し、すべての Dynamic Media アセットの応答時間と読み込み時間が短くなります。

詳しくは、[コンテンツの HTTP/2 配信に関するよくある質問](/help/sites-administering/scene7-http2faq.md)を参照してください。
