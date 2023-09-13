---
title: AEM Forms用Adobe Experience Manager(AEM) デスクトップアプリケーション
description: AEM Forms用Adobe Experience Manager(AEM) デスクトップアプリケーション
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
noindex: true
role: Admin
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
source-git-commit: 5af420c8e95fed88a8516cce27b8bbc7d3974e75
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 27%

---

# AEM Forms用Adobe Experience Manager(AEM) デスクトップアプリケーション {#aem-desktop-app-for-aem-forms}

AEM デスクトップアプリケーションにより、Adobe Experience Manager（AEM）のアセットリポジトリと AEM Forms のバイナリファイルを、システム上のネットワークディレクトリにマップすることができます。同期されたアセットとバイナリファイルをエクスプローラーで表示し、様々なアプリを使用して必要に応じてファイルを編集できます。 ファイルの表示に加えて、バイナリファイルの作成、アップロード、削除をおこなうこともできます。 また、ソフトウェアから直接ファイルを開いたり、編集したり、保存したりすることもできます。 例えば、Designer から直接 XDP ファイルを開いて編集することができます。 アセットに対してローカルで加えた変更は、AEM AssetsリポジトリとAEM Formsユーザーインターフェイスに反映されます。

AEMインスタンスからアプリをダウンロードできます。 AEM デスクトップアプリケーションの詳しいダウンロード方法については、[AEM デスクトップアプリケーションのリリースノート](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=ja)を参照してください。

## AEM デスクトップアプリケーションでサポートされる AEM Forms のアセット {#aem-forms-assets-supported-in-aem-desktop-app}

このアプリケーションを使用して、フォームテンプレート (.xdp)、PDFフォーム (.pdf)、ドキュメント (.pdf)、画像、XML スキーマ (.xsd)、スタイルシート (.xfs) のAEM Formsバイナリファイルを同期できます。 その他のすべてのファイル（サポートされていないファイル）が 0 バイトファイルとしてデスクトップアプリケーションに表示されます。 サポートされていないファイルを 0 バイトファイルとして表示すると、AEM Forms Server 上に使用可能なその他のアセットの存在をユーザーが認識できるようになります。

>[!NOTE]
>
>ファイル名には、英数字、ハイフン、アンダースコアのみを含めることができます。

## AEM デスクトップアプリケーションに対して AEM Forms を有効にする {#enable-aem-forms-for-aem-desktop-app}

AEMデスクトップアプリケーションは、Microsoft® Windows では WebDAV プロトコルを使用し、macOS X では SMB1 を使用してAEM Formsサーバーに接続します。 WebDAV または SMB クライアントとのバイナリファイルおよび他のアセットの同期は、デフォルトでは、AEM Formsサーバーで有効になっていません。 AEM Forms for AEMデスクトップアプリケーションを有効にできるように、次の手順を実行します。

1. 管理者として AEM Forms にログインします。
1. オーサーインスタンスで、「![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager／Tools]** ![ハンマー](assets/hammer.png) **[!UICONTROL ／Deployment／Operations／Web Console]**」をクリックしてください。新しいウィンドウに web コンソールが表示されます。
1. Web コンソールウィンドウで、 **[!UICONTROL FormsManager AddOn 設定]** オプション。
1. FormsManager アドオン設定ダイアログで&#x200B;**[!UICONTROL 非同期リソース]**&#x200B;チェックボックスの選択を解除して、**[!UICONTROL 保存]**&#x200B;をクリックしてください。
1. AEM Forms サーバーを再起動します。再起動後、 AEM Forms Server は、AEMデスクトップアプリケーションでコンテンツを受け入れ、共有できるようになります。
1. デスクトップアプリケーションを開き、AEM Forms Server に接続します。

   接続に成功すると、アプリケーションは `content/dam` と `content/dam/formsanddocuments` のフォルダーを作成します。上のフォルダーからローカルフォルダーにファイルを移動するほか、逆に、デスクトップアプリケーションを使用して自動入力されたフォルダー間でコンテンツを移動することもできます。
