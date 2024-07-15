---
title: AEM Forms 用 Adobe Experience Manager (AEM) デスクトップアプリケーション
description: AEM Forms 用 Adobe Experience Manager (AEM) デスクトップアプリケーション
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
noindex: true
role: Admin,User
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 100%

---

# AEM Forms 用 Adobe Experience Manager (AEM) デスクトップアプリケーション {#aem-desktop-app-for-aem-forms}

AEM デスクトップアプリケーションにより、Adobe Experience Manager（AEM）のアセットリポジトリと AEM Forms のバイナリファイルを、システム上のネットワークディレクトリにマップすることができます。同期されたアセットとバイナリファイルをファイルエクスプローラーで表示し、様々なアプリを使用して必要に応じてファイルを編集できます。ファイルの表示に加えて、バイナリファイルの作成、アップロード、削除も行えます。また、ソフトウェアから直接ファイルを開いたり、編集したり、保存したりすることもできます。例えば、Designer から直接 XDP ファイルを開いて編集できます。アセットに対してローカルで加えた変更は、AEM Assets リポジトリと AEM Forms ユーザーインターフェイスに反映されます。

AEM インスタンスからアプリをダウンロードできます。AEM デスクトップアプリケーションの詳しいダウンロード方法については、[AEM デスクトップアプリケーションのリリースノート](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=ja)を参照してください。

## AEM デスクトップアプリケーションでサポートされる AEM Forms のアセット {#aem-forms-assets-supported-in-aem-desktop-app}

このアプリを使用して、フォームテンプレートタイプ (.xdp)、PDFフォームタイプ (.pdf)、ドキュメントタイプ (.pdf)、画像タイプ、XML スキーマタイプ (.xsd)、スタイルシートタイプ (.xfs) の AEM Forms バイナリファイルを同期できます。その他のすべてのファイル（サポートされていないファイル）は、0 バイトファイルとしてアプリに表示されます。サポートされていないファイルを 0 バイトファイルとして表示することにより、AEM Forms サーバー上に使用可能な他のアセットが存在することをユーザーが認識できます。

>[!NOTE]
>
>ファイル名には、英数字、ハイフン、アンダースコアしか使えません。

## AEM デスクトップアプリケーションに対して AEM Forms を有効にする {#enable-aem-forms-for-aem-desktop-app}

AEM デスクトップアプリケーションは、Microsoft® Windowsでは WebDAV プロトコル、MacOS XではSMB1 をそれぞれ使用して、AEM Forms サーバーに接続します。初期状態の AEM Forms サーバーは、バイナリファイルと他のアセットを WebDAV クライアントまたは SMB クライアントと同期するようには設定されていません。AEM デスクトップアプリケーションに対して AEM Forms を有効にするには、以下の手順を実行します。

1. 管理者として AEM Forms にログインします。
1. オーサーインスタンスで、「![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager／Tools]** ![ハンマー](assets/hammer.png) **[!UICONTROL ／Deployment／Operations／Web Console]**」をクリックしてください。新しいウィンドウに web コンソールが表示されます。
1. Web コンソールウィンドウで、「**[!UICONTROL FormsManager アドオン設定]**」オプションを探して選択します。
1. FormsManager アドオン設定ダイアログで「**[!UICONTROL 非同期リソース]**」チェックボックスの選択を解除して、「**[!UICONTROL 保存]**」をクリックします。
1. AEM Forms サーバーを再起動します。再起動が完了すると、AEM Forms サーバーでコンテンツを取得し、そのコンテンツを AEM デスクトップアプリケーションと共有できるようになります。
1. アプリを開き、AEM Formsサーバーに接続します。

   >[!NOTE]
   >
   > 「Ctrl + C」コマンドを使用して SDK を再起動することをお勧めします。 Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。

   接続に成功すると、アプリケーションは `content/dam` と `content/dam/formsanddocuments` のフォルダーを作成します。上記のフォルダーとローカルフォルダーとの間でファイルを移動するだけでなく、アプリを使用して、自動的に作成されたフォルダー間でコンテンツを移動することができます。
