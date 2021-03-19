---
title: AEM Forms用AEMデスクトップアプリケーション
seo-title: AEM Forms用AEMデスクトップアプリケーション
description: AEM Forms用AEMデスクトップアプリケーション
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 57%

---


# AEM Forms用AEMデスクトップアプリケーション{#aem-desktop-app-for-aem-forms}

AEMデスクトップアプリでは、Adobe Experience Manager(AEM)アセットリポジトリとAEM Formsバイナリファイルを、システム上のネットワークディレクトリにマップできます。 同期されたアセットとバイナリファイルをファイルエクスプローラーで表示し、各種のアプリケーションを使用してファイルを編集することができます。ファイルを表示するだけでなく、バイナリファイルの作成、アップロード、削除を行うこともできます。また、ソフトウェアから、ファイルのオープン、編集、保存を直接実行することもできます。例えば、Designer で直接 XDP ファイルを開いて編集することができます。アセットに対してローカルで行った変更内容は、AEM アセットリポジトリと AEM Forms の UI に反映されます。

AEM デスクトップアプリケーションは、AEM インスタンスからダウンロードすることができます。アプリのダウンロードについて詳しくは、[AEMデスクトップアプリのリリースノート](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html)を参照してください。

## AEM desktop app {#aem-forms-assets-supported-in-aem-desktop-app}でサポートされるAEM Formsアセット

AEM デスクトップアプリケーションを使用して、フォームテンプレートタイプ（.xdp）、PDF フォームタイプ（.pdf）、ドキュメントタイプ（.pdf）、画像タイプ、XML スキーマタイプ（.xsd）、スタイルシートタイプ（.xfs）の AEM Forms バイナリファイルを同期することができます。AEM デスクトップアプリケーションでは、他のすべてのファイル（サポートされていないファイル）は 0 バイトファイルとして表示されます。サポートされていないファイルを 0 バイトファイルとして表示することにより、他の使用可能なアセットが AEM Forms サーバー上に存在することをユーザーに認識させることができます。

>[!NOTE]
>
>ファイル名には、英数字、ハイフン、下線のみを含めることができます。

## AEMデスクトップアプリ用AEM Formsを有効にする{#enable-aem-forms-for-aem-desktop-app}

AEMデスクトップアプリは、Microsoft WindowsではWebDAVプロトコルを使用し、Mac OS XではSMB1を使用してAEM Formsサーバーに接続します。 初期設定では、AEM Formsサーバーは、バイナリファイルや他のアセットをWebDAVまたはSMBクライアントと同期できません。 次の手順を実行して、AEMデスクトップアプリ用AEM Formsを有効にします。

1. 管理者として AEM Forms にログインします。
1. オーサーインスタンスで、![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager/ツール]** ![ハンマー](assets/hammer.png) **[!UICONTROL 展開/操作/Webコンソール]**&#x200B;をクリックします。 をクリックします。新しいウィンドウが Web コンソールに表示されます。
1. Web コンソールウィンドウで、「**[!UICONTROL FormsManager アドオン設定]**」オプションを探して選択します。
1. FormsManager アドオン設定ダイアログで「**[!UICONTROL 非同期リソース]**」チェックボックスの選択を解除して「**[!UICONTROL 保存]**」をクリックします。
1. AEM Forms サーバーを再起動します。再起動後、AEM FormsサーバーはAEMデスクトップアプリケーションでコンテンツを受け入れ、共有できます。
1. AEM デスクトップアプリケーションを起動し、AEM Forms サーバーに接続します。

   接続に成功すると、アプリは`content/dam`フォルダーと`content/dam/formsanddocuments`フォルダーにデータを入力します。 上記のフォルダーとローカルフォルダーとの間でファイルを移動するだけでなく、AEM デスクトップアプリケーションを使用して、自動的にデータが取り込まれたフォルダー間でコンテンツを移動することができます。

