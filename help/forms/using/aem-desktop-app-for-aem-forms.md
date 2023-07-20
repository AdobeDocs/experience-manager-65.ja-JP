---
title: AEM Forms用Adobe Experience Manager(AEM) デスクトップアプリケーション
description: AEM Forms用Adobe Experience Manager(AEM) デスクトップアプリケーション
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
noindex: true
role: Admin
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 50%

---

# AEM Forms用Adobe Experience Manager(AEM) デスクトップアプリケーション {#aem-desktop-app-for-aem-forms}

AEM デスクトップアプリケーションにより、Adobe Experience Manager（AEM）のアセットリポジトリと AEM Forms のバイナリファイルを、システム上のネットワークディレクトリにマップすることができます。同期されたアセットとバイナリファイルをエクスプローラーで表示し、様々なアプリを使用して必要に応じてファイルを編集できます。 ファイルの表示に加えて、バイナリファイルの作成、アップロード、削除をおこなうこともできます。 また、ソフトウェアから直接ファイルを開いたり、編集したり、保存したりすることもできます。 例えば、Designer から直接 XDP ファイルを開いて編集することができます。 アセットに対してローカルで加えた変更は、AEM AssetsリポジトリとAEM Forms UI に反映されます。

AEMインスタンスからアプリをダウンロードできます。 AEM デスクトップアプリケーションの詳しいダウンロード方法については、[AEM デスクトップアプリケーションのリリースノート](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=ja)を参照してください。

## AEM デスクトップアプリケーションでサポートされる AEM Forms のアセット {#aem-forms-assets-supported-in-aem-desktop-app}

このアプリケーションを使用して、フォームテンプレート (.xdp)、PDFフォーム (.pdf)、ドキュメント (.pdf)、画像、XML スキーマ (.xsd)、スタイルシート (.xfs) のAEM Formsバイナリファイルを同期できます。 その他のすべてのファイル（サポートされていないファイル）が 0 バイトファイルとしてデスクトップアプリケーションに表示されます。 サポートされていないファイルを 0 バイトファイルとして表示すると、AEM Formsサーバー上で使用可能なその他のアセットの存在をユーザーが認識できます。

>[!NOTE]
>
>ファイル名には、英数字、ハイフン、アンダースコアのみを含めることができます。

## AEM デスクトップアプリケーションに対して AEM Forms を有効にする {#enable-aem-forms-for-aem-desktop-app}

AEM デスクトップアプリケーションは、Microsoft Windows で WebDAV プロトコル、Mac OS X で SMB1 をそれぞれ使用して、AEM Forms サーバーに接続します。初期状態の AEM Forms サーバーは、バイナリファイルと他のアセットを WebDAV クライアントまたは SMB クライアントと同期するようには設定されていません。AEM デスクトップアプリケーションに対して AEM Forms を有効にするには、以下の手順を実行します。

1. 管理者として AEM Forms にログインします。
1. オーサーインスタンスで、「![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager／Tools]** ![ハンマー](assets/hammer.png) **[!UICONTROL ／Deployment／Operations／Web Console]**」をクリックしてください。新しいウィンドウに web コンソールが表示されます。
1. Web コンソールウィンドウで、**[!UICONTROL FormsManager アドオン設定]**&#x200B;オプションを探して選択してください。
1. FormsManager アドオン設定ダイアログで&#x200B;**[!UICONTROL 非同期リソース]**&#x200B;チェックボックスの選択を解除して、**[!UICONTROL 保存]**&#x200B;をクリックしてください。
1. AEM Forms サーバーを再起動します。再起動が完了すると、AEM Forms サーバーでコンテンツを取得し、そのコンテンツを AEM デスクトップアプリケーションと共有できるようになります。
1. AEM デスクトップアプリケーションを開き、AEM Forms サーバーに接続してください。

   接続に成功すると、アプリケーションは `content/dam` と `content/dam/formsanddocuments` のフォルダーを作成します。上のフォルダーからローカルフォルダーにファイルを移動するほか、逆に、デスクトップアプリケーションを使用して自動入力されたフォルダー間でコンテンツを移動することもできます。
