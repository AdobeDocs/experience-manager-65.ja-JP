---
title: デジタルアセットをチェックインし、編集用にチェックアウトする
description: 編集のためにアセットをチェックアウトし、変更が完了した後にアセットをチェックインする方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 60%

---


# Experience Manager DAMのチェックインおよびチェックアウトファイル {#check-in-and-check-out-files-in-assets}

Adobe Experience Manager Assetsを使用すると、変更を完了した後、アセットを編集用にチェックアウトし、再度チェックインできます。 アセットをチェックアウトした後は、その人だけがアセットを編集、注釈、公開、移動、削除できるようになります。アセットのチェックアウトでアセットにロックがかかることになります。他のユーザーは、アセットを再度アセットにチェックインするまで、アセットに対してこれらの操作を実行できません。 ただし、ロックされたアセットのメタデータは変更することができます。

アセットをチェックイン／チェックアウトするには、アセットへの書き込み権限が必要です。

この機能は、複数のユーザーが複数のチームにわたるワークフローの編集で共同作業をする際、ある作成者が変更した内容を他のユーザーが書き換えてしまう事態を防ぐのに役立ちます。

## アセットのチェックアウト {#checking-out-assets}

1. Assets の UI でチェックアウトしたいアセットを選択します。チェックアウトしたいアセットは複数選択することもできます。
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

1. インター [!DNL Assets] フェイスから編集済みのアセットを選択し、ツールバーの「 **[!UICONTROL チェックイン]** 」をクリックします。 変更されたアセットは Assets にチェックインされ、他のユーザーが編集できるようになります。

## Forced check in {#forced-check-in}

管理者は他のユーザーがチェックアウトしたアセットをチェックインできます。

1. 管理者として Assets にログインします。
1. Assets UI で他のユーザーにチェックアウトされているアセットを 1 つ以上選択します。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. ツールバーで、「ロックを **[!UICONTROL 解除]**」をクリックします。 アセットはチェックインされ、他のユーザーが編集できるようになります。

>[!MORELIKETHIS]
>
>* [Experience Managerデスクトップアプリケーションのチェックインとチェックアウトについて理解する](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [アセットのチェックインとチェックアウトについて理解するためのビデオチュートリアル](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/collaboration/checkin-checkout-technical-video-understand.html)

