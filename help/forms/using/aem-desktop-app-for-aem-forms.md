---
title: AEM Forms の AEM デスクトップアプリケーション
seo-title: AEM desktop app for AEM Forms
description: AEM Forms の AEM デスクトップアプリケーション
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
role: Admin
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 100%

---

# AEM Forms の AEM デスクトップアプリケーション {#aem-desktop-app-for-aem-forms}

AEM デスクトップアプリケーションにより、Adobe Experience Manager（AEM）のアセットリポジトリと AEM Forms のバイナリファイルを、システム上のネットワークディレクトリにマップすることができます。同期されたアセットとバイナリファイルをファイルエクスプローラーで表示し、各種のアプリケーションを使用してファイルを編集することができます。ファイルを表示するだけでなく、バイナリファイルの作成、アップロード、削除を行うこともできます。また、ソフトウェアから、ファイルのオープン、編集、保存を直接実行することもできます。例えば、Designer で直接 XDP ファイルを開いて編集することができます。アセットに対してローカルで行った変更内容は、AEM アセットリポジトリと AEM Forms の UI に反映されます。

AEM デスクトップアプリケーションは、AEM インスタンスからダウンロードすることができます。AEM デスクトップアプリケーションの詳しいダウンロード方法については、[AEM デスクトップアプリケーションのリリースノート](https://helpx.adobe.com/jp/experience-manager/desktop-app/release-notes.html)を参照してください。

## AEM デスクトップアプリケーションでサポートされる AEM Forms のアセット {#aem-forms-assets-supported-in-aem-desktop-app}

AEM デスクトップアプリケーションを使用して、フォームテンプレートタイプ（.xdp）、PDF フォームタイプ（.pdf）、ドキュメントタイプ（.pdf）、画像タイプ、XML スキーマタイプ（.xsd）、スタイルシートタイプ（.xfs）の AEM Forms バイナリファイルを同期することができます。AEM デスクトップアプリケーションでは、他のすべてのファイル（サポートされていないファイル）は 0 バイトファイルとして表示されます。サポートされていないファイルを 0 バイトファイルとして表示することにより、他の使用可能なアセットが AEM Forms サーバー上に存在することをユーザーに認識させることができます。

>[!NOTE]
>
>ファイル名には、英数字、ハイフン、下線のみを含めることができます。

## AEM デスクトップアプリケーションに対して AEM Forms を有効にする {#enable-aem-forms-for-aem-desktop-app}

AEM デスクトップアプリケーションは、Microsoft Windows で WebDAV プロトコル、Mac OS X で SMB1 をそれぞれ使用して、AEM Forms サーバーに接続します。初期状態の AEM Forms サーバーは、バイナリファイルと他のアセットを WebDAV クライアントまたは SMB クライアントと同期するようには設定されていません。AEM デスクトップアプリケーションに対して AEM Forms を有効にするには、以下の手順を実行します。

1. 管理者として AEM Forms にログインします。
1. オーサーインスタンスで、「![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager／Tools]** ![ハンマー](assets/hammer.png) **[!UICONTROL ／Deployment／Operations／Web Console]**」をクリックしてください。新しいウィンドウに web コンソールが表示されます。
1. Web コンソールウィンドウで、**[!UICONTROL FormsManager アドオン設定]**&#x200B;オプションを探して選択してください。
1. FormsManager アドオン設定ダイアログで&#x200B;**[!UICONTROL 非同期リソース]**&#x200B;チェックボックスの選択を解除して、**[!UICONTROL 保存]**&#x200B;をクリックしてください。
1. AEM Forms サーバーを再起動します。再起動が完了すると、AEM Forms サーバーでコンテンツを取得し、そのコンテンツを AEM デスクトップアプリケーションと共有できるようになります。
1. AEM デスクトップアプリケーションを開き、AEM Forms サーバーに接続してください。

   接続に成功すると、アプリケーションは `content/dam` と `content/dam/formsanddocuments` のフォルダーを作成します。上記のフォルダーとローカルフォルダーとの間でファイルを移動するだけでなく、AEM デスクトップアプリケーションを使用して、自動的に作成されたフォルダー間でコンテンツを移動することができます。
