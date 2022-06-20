---
title: アセットのダウンロード
description: ' [!DNL Adobe Experience Manager]  からアセットをダウンロードする方法とダウンロード機能を有効または無効にする方法について説明します。'
contentOwner: AG
role: User
feature: Asset Management,Asset Distribution
exl-id: 6bda9e52-5a6e-446e-99c7-96793482c190
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 97%

---

# [!DNL Adobe Experience Manager] からのアセットのダウンロード  {#download-assets-from-aem}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/download-assets-from-aem.html?lang=en) |
| AEM 6.5 | この記事 |
| AEM 6.4 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/download-assets-from-aem.html?lang=en) |

静的レンディションおよび動的レンディションを含むアセットをダウンロードできます。または、アセットへのリンクを含む電子メールを [!DNL Adobe Experience Manager Assets] から直接送信できます。ダウンロードされたアセットは、ZIP ファイルにバンドルされています。書き出しジョブ用に圧縮する ZIP ファイルの最大サイズは 1 GB です。書き出しジョブあたり、最大で 500 個のアセットの合計を指定できます。

>[!NOTE]
>
>`/var/dam/share` の場所に読み取り権限を持つユーザーは電子メールメッセージで共有されるダウンロードリンクにアクセスできます。
>
>`/var/dam/jobs/download` の場所に読み取り権限を持つユーザーはアセットをダウンロードできます。
>
>画像セット、スピンセット、混在メディアセット、カルーセルセットの各アセットタイプはダウンロードできません。

<!--
OLD content of the above NOTE, changed wrt CQDOC-18661.
>The email recipients must be members of the `dam-users` group to access the ZIP download link in the email message.
>
-->

**アセットをダウンロードするには、次の手順に従います。**

1. 左上隅のロゴをクリックします。 左側のパネルで「**[!UICONTROL ナビゲーション]**」をクリックします。
1. [!UICONTROL ナビゲーション]ページで、**[!UICONTROL アセット]**／**[!UICONTROL ファイル]**&#x200B;をクリックします。
1. ダウンロードするアセットを含むフォルダーに移動します。
1. フォルダーを選択するか、フォルダー内の 1 つ以上のアセットを選択します。
1. ツールバーの「**[!UICONTROL ダウンロード]**」をクリックします。
1. ダウンロードダイアログボックスで、目的のダウンロードオプションを選択します。

   | エクスポートまたはダウンロードのオプション | 説明 |
   |---|---|
   | **[!UICONTROL アセットごとに別のフォルダーを作成]** | このオプションを選択すると、ダウンロードした各アセット（アセットの親フォルダーの下にネストされた子フォルダー内のアセットを含む）が、ローカルコンピューター上の 1 つのフォルダーに含まれます。このオプションを選択しない場合、デフォルトでは、フォルダー階層は無視され、すべてのアセットがローカルコンピューターの 1 つのフォルダーにダウンロードされます。 |
   | **[!UICONTROL 電子メール]** | ユーザーに電子メール通知が送信されます。次の場所にある標準の電子メールテンプレートを利用できます。<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> デプロイメント時にカスタマイズしたテンプレートは、次の場所で利用できます。 <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>テナント固有のカスタムテンプレートは、次の場所に保存できます。<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL アセット]** | レンディションを含めずに、元の形式でアセットをダウンロードする場合に、このオプションを選択します。<br>元のアセットにサブアセットがある場合は、サブアセットオプションを使用できます。 |
   | **[!UICONTROL レンディション]** | レンディションは、アセットのバイナリ表現です。アセットは、（アップロードされたファイルの）一次表現を持ちます。アセットは任意の数の追加の表現を持つことができます。<br>このオプションを選択すると、ダウンロードするレンディションを選択できます。使用できるレンディションは、選択したアセットによって異なります。アセットにレンディションがある場合は、レンディションオプションを使用できます。 |
   | **[!UICONTROL スマート切り抜き]** | このオプションを選択すると、選択したアセットのすべてのスマート切り抜きレンディションが AEM 内からダウンロードされます。スマート切り抜きレンディションを含む zip ファイルが作成され、ローカルコンピューターにダウンロードされます。 |
   | **[!UICONTROL 動的レンディション]** | 一連の代替レンディションをリアルタイムで生成するには、このオプションを選択します。また、このオプションを選択すると、動的に作成するレンディションを[画像プリセット](image-presets.md)リストから選択します。<br>さらに、サイズ、測定単位、形式、カラースペース、解像度および、画像の反転用などのオプションの画像修飾子を選択できます。このオプションは、[!DNL Dynamic Media] を有効にしている場合にのみ使用できます。 |

1. ダイアログボックスで、「**[!UICONTROL ダウンロード]**」をクリックします。

ダウンロードするフォルダーを選択すると、そのフォルダーの下位のアセットの階層全体がダウンロードされます。ダウンロードする各アセット（親フォルダーの下にネストされている子フォルダーのアセットを含む）を個々のフォルダーに格納するには、「**[!UICONTROL アセットごとに別のフォルダーを作成]**」を選択します。

## アセットダウンロードサーブレットの有効化 {#enable-asset-download-servlet}

[!DNL Experience Manager] のデフォルトサーブレットを使用すると、認証されたユーザーは、表示可能なアセットの ZIP ファイルを作成するために任意のサイズの同時ダウンロード要求を発行することができますが、その結果、サーバーやネットワークに過剰な負荷をかけるおそれがあります。この機能で生じる可能性がある DoS リスクを軽減するために、パブリッシュインスタンスに対しては、`AssetDownloadServlet` OSGi コンポーネントがデフォルトで無効になっています。

例えば Asset Share Commons やポータルのような実装などを使用する場合に DAM からアセットをダウンロードできるようにするには、OSGi 設定を通じてサーブレットを手動で有効にします。日常的なダウンロードの要件に影響を与えない範囲で、許容ダウンロードサイズをできるだけ小さく設定することをお勧めします。この値を大きくすれば、パフォーマンスに影響を与える可能性があります。

1. 次のように、パブリッシュ実行モードを対象とする命名規則（`config.publish`）でフォルダーを作成します：`/apps/<your-app-name>/config.publish`。実行モードの設定プロパティを定義するには、 [実行モード](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode)を参照してください。
1. config フォルダーに、`nt:file` タイプのファイル `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` を作成します。
1. `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` に以下を入力します。ダウンロードの最大サイズ（バイト単位）を `asset.download.prezip.maxcontentsize` の値として設定します。以下のサンプルでは、ZIP ダウンロードの最大サイズを 100 KB を超えないように設定しています。

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

デフォルトでは、`GET` のファイルダウンロード要求に対して、[!DNL Experience Manager] では、ZIP アーカイブのダウンロードサイズに対して 50 MB の制限が適用されます。 `POST` のリクエストまたはユーザーインターフェイスから開始されるダウンロードは、この制限の影響を受けません。

## アセットダウンロードサーブレットの無効化 {#disable-asset-download-servlet}

 パブリッシュインスタンスの `Asset Download Servlet` を無効にするには、アセットダウンロード要求をすべてブロックするように Dispatcher 設定を更新します。[!DNL Experience Manager]サーブレットは、OSGi コンソールから手動で直接無効にすることもできます。

1. Dispatcher 設定を通じてアセットダウンロード要求をブロックするには、`dispatcher.any` 設定を編集し、[フィルターセクション](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#defining-a-filter)にルールを追加します。`/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. パブリッシュインスタンスで OSGi コンポーネントを無効にするには、`http://[aem_server]:[port]/system/console/components` で OSGi コンソール にアクセスします。`com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` を探して、「**[!UICONTROL 無効にする]**」をクリックします。

>[!MORELIKETHIS]
>
>* [Brand Portal からのアセットのダウンロード](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html?lang=ja)
>* [DRM で保護されたアセットのダウンロード](drm.md)。
>* [Windows／Mac OS デスクトップで Experience Manager デスクトップアプリケーションを使用したアセットのダウンロード](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja#download-assets)。
>* [サポートされている Adobe Creative Cloud アプリ内から Adobe Asset Link を使用したアセットのダウンロード](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html)。

