---
title: アセットをチェックインして編集用にチェックアウトする
description: 編集のためにアセットをチェックアウトし、変更が完了した後にアセットをチェックインする方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 117208c634613559bb13556e12f094add70006e2
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 49%

---


# Check-in and check-out files in [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] では、編集のためにアセットをチェックアウトし、変更終了後にアセットをチェックインすることができます。アセットをチェックアウトした後は、その人だけがアセットを編集、注釈、公開、移動、削除できるようになります。アセットのチェックアウトでアセットにロックがかかることになります。Other users cannot perform any of these operations on the asset until you check the asset back in to [!DNL Assets]. ただし、ロックされたアセットのメタデータは変更することができます。

アセットをチェックイン／チェックアウトするには、アセットへの書き込み権限が必要です。

この機能は、複数のユーザーが複数のチームにわたるワークフローの編集で共同作業をする際、ある作成者が変更した内容を他のユーザーが書き換えてしまう事態を防ぐのに役立ちます。

## アセットのチェックアウト {#checking-out-assets}

1. From the [!DNL Assets] user interface, select the asset you want to check out. チェックアウトしたいアセットは複数選択することもできます。
1. ツールバーで、「 **[!UICONTROL Checkout]**」をクリックします。
「 **[!UICONTROL チェックアウト]** 」( **[!UICONTROL Checkout]**)オプションは「チェックイン」(Checkin)に切り替わります。
チェックアウトしたアセットを他のユーザーが編集できるかを確認するには、別のユーザーとしてログインします。チェックアウトしたアセットのサムネールにロック記号が表示されます。

   ![chlimage_1-471](assets/chlimage_1-471.png)

   アセットを選択します。アセットを編集、注釈、公開または削除するためのオプションがツールバーに一切表示されないことを確認します。

   ![chlimage_1-472](assets/chlimage_1-472.png)

   You can click **[!UICONTROL View Properties]** to edit the metadata for the locked asset.

1. 「 **[!UICONTROL 編集]** 」をクリックして、アセットを編集モードで開きます。

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. アセットを編集して、変更内容を保存します。例えば、画像を切り抜いて保存します。

   ![chlimage_1-474](assets/chlimage_1-474.png)

   アセットに注釈を付けたり公開したりすることもできます。

1. インター [!DNL Assets] フェイスから編集済みのアセットを選択し、ツールバーの「 **[!UICONTROL チェックイン]** 」をクリックします。 The modified asset is checked in to [!DNL Assets] and is available to other users for editing.

## Forced check in {#forced-check-in}

管理者は他のユーザーがチェックアウトしたアセットをチェックインできます。

1. Log in to [!DNL Assets] as an administrator.
1. From the [!DNL Assets] user interface select one or more assets that have been checked out by other users.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. ツールバーで、「ロックを **[!UICONTROL 解除]**」をクリックします。 アセットはチェックインされ、他のユーザーが編集できるようになります。

## ベストプラクティスと制限事項 {#tips-limitations}

* チェックアウトされたアセットファイルが含まれる *フォルダ* を削除できます。 フォルダーを削除する前に、デジタルアセットがユーザーによってチェックアウトされていないことを確認します。

>[!MORELIKETHIS]
>
>* [Experience Managerのデスクトップアプリケーションでのチェックインとチェックアウトについて理解する](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [アセットのチェックインとチェックアウトについて理解するためのビデオチュートリアル](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

