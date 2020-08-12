---
title: ダイナミックメディアを使用したCDNキャッシュの無効化
description: コンテンツ配信ネットワーク（CDN）にキャッシュされたコンテンツを無効にすることで、Dynamic Media で配信されるアセットをすばやく更新できます。キャッシュが期限切れになるのを待つ必要はありません。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 9e67e252348f471c052f6c3e88aea61d7a309241
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 16%

---


# ダイナミックメディアを使用したCDNキャッシュの無効化 {#invalidating-cdn-cache-for-dm-assets}

Dynamic Mediaアセットは、顧客との配信を高速化するために、CDN(コンテンツ配信ネットワーク)によってキャッシュされます。 ただし、これらのアセットを更新する場合は、その変更をWebサイトに即座に反映させることができます。 CDNキャッシュの削除または無効化を行うと、ダイナミックメディアによって配信されるアセットをすばやく更新できます。 TTL(Time To Live)値（デフォルトは10時間）を使用してキャッシュの有効期限が切れるのを待つ代わりに、ダイナミックメディア内から要求を送信し、キャッシュの有効期限をすぐに切れるようにすることができます。

>[!IMPORTANT]
>
>これらの手順は、AEM 6.5のダイナミックメディア —Scene7モード、Service Pack 6以降にのみ適用されます。 <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

ダイナミックメディアの [キャッシュの概要も参照してください](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)。

**ダイナミックメディアアセット用のCDNキャッシュコンテンツを無効にするには：**

1. AEM 6.5.6以降では、 **[!UICONTROL ツール/アセット/CDNの無効化をタップします。]**

   ![CDN検証機能](/help/assets/assets-dm/cdn-invalidation-path.png)

1. CDN無効化ページで、目的のオプションを設定します。

   | オプション | 説明 |
   | --- | --- |
   | **[!UICONTROL CDN でアセット関連の画像プリセットを無効化します]** | このオプションを選択すると、MIMEタイプと、キャッシュの無効化に関連付けられた画像プリセットに関係なく、1つ以上のダイナミックメディアアセットを選択できます。<br>アセットを含む1つ以上のフォルダーを選択できますが、Adobeはこの方法を推奨しません。 代わりに、個々のアセットファイルを選択する必要があります。<br>次の手順に進みます。 |
   | **[!UICONTROL テンプレートに基づく無効化]** | このオプションをチェックすると、以前に作成したダイナミックメディアアセットと無効化テンプレートを選択できます。 このオプションは、 |
   | **[!UICONTROL アセットを追加]** | ブラー |
   | **[!UICONTROL URL を追加]** | キャッシュを無効にするダイナミックメディアアセットに、完全なURLパスを手動で追加します。 |

1. 
1. Tap **[!UICONTROL Next.]**
1. 
