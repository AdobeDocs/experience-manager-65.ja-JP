---
title: セキュアな AEM Forms アプリケーション（iOS 用）の構築
description: Xcode プロジェクトをアーカイブして、iOS用のセキュアなAEM Formsアプリを構築する方法を説明します。 これにより、インストーラー（.ipa ファイル）とプロパティリスト（.plist ファイル）ファイルが作成されます。
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
exl-id: 12cc2027-ae94-40c3-a7d1-553469426114
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 62%

---

# セキュアな AEM Forms アプリケーション（iOS 用）の構築 {#building-a-secure-aem-forms-app-for-ios}

AEM Formsアプリケーションの Xcode プロジェクトをアーカイブして、インストーラー（.ipa ファイル）とプロパティリスト（.plist ファイル）ファイルを構築する必要があります。 プロパティリストファイルには、アプリケーションの名前やホストしているロケーションなど、ホストされているインハウスアプリケーションの設定情報が含まれます。プロパティリストファイルについての詳細は、[About Information Property List Files](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) を参照してください。

1. 次の Web サイトにログインします。

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. アプリ ID を作成します。 アプリ ID を作成する詳しい手順については、 [アプリ ID の作成と設定](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. アプリ用にiOSアプリケーションのバンドル識別子を設定するには、 **[!UICONTROL アプリ ID を設定]**.
1. Web ページの下部にある、**[!UICONTROL Enable for Data Protection]** を選択します。データ保護オプションを指定します。

   「**[!UICONTROL 完了]**」をクリックします。

1. プロビジョニング/配布に移動し、手順 3 で設定したアプリ ID を使用して新しいプロファイルを作成します。
1. プロビジョニングプロファイルをダウンロードして Xcode および iPad に追加します。 
1. Xcode、iOS SDK がインストールされ設定済みの Mac マシンにログインします。
1. Xcode で `AEM Forms.xcodeproj` プロジェクトを開きます。
1. 「**[!UICONTROL TARGETS]**」の「**[!UICONTROL AEM Forms]**」をクリックし、「**[!UICONTROL AEM Forms]**」を選択します。「**[!UICONTROL ビルド設定]**」タブを選択し、「**[!UICONTROL コード署名エンタイトルメント]**」セクションを探して、「エンタイトルメント」ドロップダウンで「**[!UICONTROL LC エンタープライズ]**」オプションを選択します。
1. Xcode 内にある `LC Enterprise.entitlements` ファイルを探して、編集するために開きます。**XCode エンタイトルメント**&#x200B;の下で、プロビジョニングプロファイル内に存在するのものと同じキー値ペアを追加します。
1. Adobe Analytics の **[!UICONTROL ビルド設定]** タブ、クリック **[!UICONTROL すべて]** 次に、「 **[!UICONTROL 組み合わせ]**.
1. 次から： **[!UICONTROL 設定]** リスト、展開 **[!UICONTROL コード署名]**.
1. 「**[!UICONTROL コード署名 ID]**」から、適切な署名を選択します。「**[!UICONTROL デバッグ]**」、「**[!UICONTROL リリース]**」、「**[!UICONTROL 任意の iOS SDK]**」に同じ署名が選択されていることを確認します。
1. 「**[!UICONTROL プロジェクト]**」の「**[!UICONTROL AEM Forms]**」を選択し、「**[!UICONTROL コード署名 ID]**」、「**[!UICONTROL デバッグ]**」、「**[!UICONTROL リリース]**」、「**[!UICONTROL 任意の iOS SDK]**」に対して適切な署名が選択されていることを確認します。
1. AEM Forms アプリケーションを構築し、配布します。AEM Forms アプリケーションを構築および配布する詳細な手順については、[AEM Forms アプリケーション用のインストーラーの構築](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app)を参照してください。
