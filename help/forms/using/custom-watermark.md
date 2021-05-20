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
feature: Correspondence Management
exl-id: 7d90fade-1ca4-41d8-bbf9-45490465784a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 58%

---

# レター PDF プレビューのカスタム透かし{#custom-watermark-in-letter-pdf-preview}

## 概要 {#overview}

Create Correspondence UI を使用するエージェントユーザーは、電子メールや印刷などを後処理に送信する最終的形態で表示します。

PDF データの不正使用を防ぐため、プレビューの PDF に透かしを付けることができます。デフォルトのウォーターマークは「プレビュー」で、PDF 全体に表示されます。

PDFのプレビューで透かしを有効にするには、https://&#39;[server]:[port]&#39;/system/console/configMgrにある「**[!UICONTROL Apply Watermark]** During Preview」オプションを選択します。**[!UICONTROL Correspondence Management Configuration&lt;a3/]**

![default-watermark](assets/default-watermark.png)

透かしのテキストと外観をカスタマイズするには、次の手順を実行します。

## Create Correspondence UI で PDF プレビュー内の透かしをカスタマイズする  {#customizewatermark-}

1. `https://'[server]:[port]'/[ContextPath]/crx/de`に移動し、管理者としてログインします。
1. appsフォルダーに、**[!UICONTROL previewwatermark]**&#x200B;という名前のフォルダーを作成します。このフォルダーのパスや構造は、libsフォルダー内のpreviewwatermarkフォルダーと同じです。

   1. 次のパスにある&#x200B;**previewwatermark**&#x200B;フォルダーを右クリックし、「**ノードをオーバーレイ**」を選択します。

      `/libs/fd/cm/configFiles/previewwatermark`

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/fd/cm/configFiles/previewwatermark

      **オーバーレイの場所：** /apps/

      **ノードタイプを一致させる：** オン

      >[!NOTE]
      >
      >/libsブランチでは変更を加えないでください。 次の操作を行った場合はこのブランチが変更されるため、各自で加えた変更はすべて失われます。
      >
      >    
      >    
      >    * インスタンス上でのアップグレード
      >    * ホットフィックスの適用
      >    * 機能パックのインストール


   1. 「**OK**」をクリックし、「**すべて保存**」をクリックします。**[!UICONTROL previewwatermark]**&#x200B;フォルダが指定されたパスに作成されます。



1. 「/libs/fd/cm/configFiles/previewwatermark」フォルダーのddxファイルを「/apps/fd/cm/configFiles/previewwatermark」フォルダーにコピー&amp;ペーストし、「**[!UICONTROL すべて保存]**」をクリックします。
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

   透かしの外観、テキスト、配置のカスタマイズについて詳しくは、『[AssemblerサービスとDDXリファレンス](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf)』ドキュメントの透かしと背景の追加と削除を参照してください。

   >[!NOTE]
   >
   >ddx ファイルでは、結果と入力への参照を output.pdf および input.pdf から変化させません。ddx ファイルの名前も変更しません。

1. 「**すべて保存**」をクリックします。
