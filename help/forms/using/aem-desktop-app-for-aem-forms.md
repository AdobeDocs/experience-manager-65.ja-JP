---
title: AEM forms用AEMデスクトップアプリケーション
seo-title: AEM forms用AEMデスクトップアプリケーション
description: 'null'
seo-description: 'null'
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
translation-type: tm+mt
source-git-commit: 6fa293028332596bb93013119b4339c7721eb536

---


# AEM desktop app for AEM Forms {#aem-desktop-app-for-aem-forms}

AEMデスクトップアプリケーションを使用すると、Adobe Experience Manager(AEM)AssetsリポジトリとAEM Formsバイナリファイルをシステム上のネットワークディレクトリにマップできます。 同期されたアセットとバイナリファイルをファイルエクスプローラーで表示し、各種のアプリケーションを使用してファイルを編集することができます。ファイルを表示するだけでなく、バイナリファイルの作成、アップロード、削除を行うこともできます。また、ソフトウェアから、ファイルのオープン、編集、保存を直接実行することもできます。例えば、Designer で直接 XDP ファイルを開いて編集することができます。アセットに対してローカルで行った変更内容は、AEM アセットリポジトリと AEM Forms の UI に反映されます。

AEM デスクトップアプリケーションは、AEM インスタンスからダウンロードすることができます。For detailed information about downloading the app, see [AEM desktop app Release Notes](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html).

## AEM Forms assets supported in AEM desktop app {#aem-forms-assets-supported-in-aem-desktop-app}

AEM デスクトップアプリケーションを使用して、フォームテンプレートタイプ（.xdp）、PDF フォームタイプ（.pdf）、ドキュメントタイプ（.pdf）、画像タイプ、XML スキーマタイプ（.xsd）、スタイルシートタイプ（.xfs）の AEM Forms バイナリファイルを同期することができます。AEM デスクトップアプリケーションでは、他のすべてのファイル（サポートされていないファイル）は 0 バイトファイルとして表示されます。サポートされていないファイルを 0 バイトファイルとして表示することにより、他の使用可能なアセットが AEM Forms サーバー上に存在することをユーザーに認識させることができます。

>[!NOTE]
>
>ファイル名には、英数字、ハイフン、下線のみを含めることができます。

## Enable AEM Forms for AEM desktop app {#enable-aem-forms-for-aem-desktop-app}

AEMデスクトップアプリケーションは、Microsoft WindowsではWebDAVプロトコルを使用し、Mac OS xではSMB1を使用してAEM Formsサーバーに接続します。 AEM Formsサーバーは、バイナリファイルやその他のアセットをWebDAVまたはSMBクライアントと同期できません。 AEM Forms for AEM Desktop appを有効にするには、次の手順を実行します。

1. 管理者として AEM Forms にログインします。
1. In the author instance, click ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > Tools]** ![hammer](assets/hammer.png) **[!UICONTROL > Deployment > Operations > Web Console]**. をクリックします。新しいウィンドウが Web コンソールに表示されます。
1. Web コンソールウィンドウで、「**[!UICONTROL FormsManager アドオン設定]**」オプションを探して選択します。
1. FormsManager アドオン設定ダイアログで「**[!UICONTROL 非同期リソース]**」チェックボックスの選択を解除して「**[!UICONTROL 保存]**」をクリックします。
1. AEM Forms サーバーを再起動します。再起動後、AEM Formsサーバーは、AEMデスクトップアプリケーションに対するコンテンツの受け入れと共有を有効にします。
1. AEM デスクトップアプリケーションを起動し、AEM Forms サーバーに接続します。

   On successful connection, the app populates the `content/dam` and `content/dam/formsanddocuments` folders. 上記のフォルダーとローカルフォルダーとの間でファイルを移動するだけでなく、AEM デスクトップアプリケーションを使用して、自動的にデータが取り込まれたフォルダー間でコンテンツを移動することができます。

