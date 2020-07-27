---
title: レター PDF プレビューのカスタム透かし
seo-title: レター PDF プレビューのカスタム透かし
description: レター PDF プレビューのカスタム透かしの作成方法について説明します。
seo-description: レター PDF プレビューのカスタム透かしの作成方法について説明します。
uuid: 5adfede3-9b38-4a12-bf14-6d80cfb0a05a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: adc7ec13-0675-4071-9c4c-e238202d9d85
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 57%

---


# レター PDF プレビューのカスタム透かし{#custom-watermark-in-letter-pdf-preview}

## 概要 {#overview}

Create Correspondence UI を使用するエージェントユーザーは、電子メールや印刷などを後処理に送信する最終的形態で表示します。

PDF データの不正使用を防ぐため、プレビューの PDF に透かしを付けることができます。デフォルトのウォーターマークは「プレビュー」で、PDF 全体に表示されます。

To enable the watermark in preview PDF, select the **[!UICONTROL Apply Watermark]** During Preview option in **[!UICONTROL Correspondence Management Configurations]** at https://&#39;[server]:[port]&#39;/system/console/configMgr.

![default-watermark](assets/default-watermark.png)

透かしのテキストと外観をカスタマイズするには、次の手順を実行します。

## Create Correspondence UI で PDF プレビュー内の透かしをカスタマイズする {#customizewatermark-}

1. Go to `https://'[server]:[port]'/[ContextPath]/crx/de` and login as Administrator.
1. In the apps folder, create a folder named **[!UICONTROL previewwatermark]** with path/structure similar to the previewwatermark folder in the libs folder:

   1. Right-click the **previewwatermark** folder at the following path and select **Overlay Node**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/fd/cm/configFiles/previewwatermark

      **オーバーレイの場所：** /apps/

      **ノードタイプを一致：** チェック済み

      >[!NOTE]
      >
      >/libsブランチは変更しないでください。 次の操作を行った場合はこのブランチが変更されるため、各自で加えた変更はすべて失われます。
      >
      >    
      >    
      >    * インスタンス上でのアップグレード
      >    * ホットフィックスの適用
      >    * 機能パックのインストール


   1. 「**OK**」をクリックし、「**すべて保存**」をクリックします。The **[!UICONTROL previewwatermark]** folder is created in the specified path.



1. Copy and paste the ddx file from &quot;/libs/fd/cm/configFiles/previewwatermark&quot; folder to &quot;/apps/fd/cm/configFiles/previewwatermark&quot; folder and click **[!UICONTROL Save All]**.
1. ddx ファイルは /apps/fd/cm/configFiles/previewwatermark/ から必要に応じて変更します。

   ```xml
   <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
    <PDF result="output.pdf">
     <PDF source="input.pdf"/>
           <Watermark opacity="15%" rotation="45">
            <StyledText>
                     <p font-family="Georgia" font-size="70pt" color="black" font-weight="bold">
                         PREVIEW
                    </p>
            </StyledText>
           </Watermark>
    </PDF>
   </DDX>
   ```

   For information on customizing the watermark appearance, text, and alignment, see Adding and removing watermarks and backgrounds in the [Assembler Service and DDX Reference](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) document.

   >[!NOTE]
   >
   >ddx ファイルでは、結果と入力への参照を output.pdf および input.pdf から変化させません。ddx ファイルの名前も変更しません。

1. 「**すべて保存**」をクリックします。

