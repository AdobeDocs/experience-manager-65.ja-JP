---
title: セキュアな AEM Forms アプリケーション（iOS 用）の構築
seo-title: セキュアな AEM Forms アプリケーション（iOS 用）の構築
description: セキュアな AEM Forms アプリケーションを構築する手順
seo-description: セキュアな AEM Forms アプリケーションを構築する手順
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0

---


# セキュアな AEM Forms アプリケーション（iOS 用）の構築 {#building-a-secure-aem-forms-app-for-ios}

AEM Forms アプリケーション用 Xcode プロジェクトをアーカイブして、インストーラー（.ipa ファイル）とプロパティリストファイル（.plist ファイル）を構築する必要があります。プロパティリストファイルには、アプリケーションの名前やホストしているロケーションなど、ホストされているインハウスアプリケーションの設定情報が含まれます。 プロパティリストファイルについての詳細は、[About Information Property List Files](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)を参照してください。

1. 次の Web サイトにログインします。

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. アプリケーション ID を作成します。アプリケーション ID を作成する詳細な手順については、[アプリケーション ID の作成と設定](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html)を参照してください。
1. アプリケーションのご使用の iOS アプリケーションのためのバンドル識別子を設定するには、**[!UICONTROL アプリケーション ID の設定]**&#x200B;をクリックします。
1. Web ページの下部にある、**[!UICONTROL Enable for Data Protection]** を選択します。 data protection オプションを指定します。

   「**[!UICONTROL 完了]**」をクリックします。

1. プロビジョニング／配布に行き、手順 3 で設定したアプリケーション ID を使って新しいプロファイルを作成します。
1. プロビジョニングプロファイルをダウンロードして Xcode および iPad に追加します。 
1. Xcode、iOS SDK がインストールおよび設定済みの Mac マシンにログインします。
1. Xcode で `AEM Forms.xcodeproj` プロジェクトを開きます。
1. 「**[!UICONTROL TARGETS]**」の「**[!UICONTROL AEM Forms]**」をクリックし、**[!UICONTROL AEM Forms]**」を選択します。Select the **[!UICONTROL Build Settings]** tab, locate the **[!UICONTROL Code Signing Entitlement]** section and in the Entitlements dropdown, select the **[!UICONTROL LC Enterprise]** option.
1. Xcode 内にある `LC Enterprise.entitlements` ファイルを探して、編集するために開きます。Under the **XCode entitlements**, add the same key-value pair as present in your provisioning profile.
1. 「**[!UICONTROL Build Settings]**」タブで、「**[!UICONTROL All]**」をクリックし、「**[!UICONTROL Combined]**」をクリックします。
1. 「**[!UICONTROL Settings]**」リストで、「**[!UICONTROL Code Signing]**」を展開します。
1. 「**[!UICONTROL Code Signing Identity]**」から、適切な署名を選択します。「**[!UICONTROL Debug]**」、「**[!UICONTROL Release]**」、「**[!UICONTROL Any iOS SDK]**」に同じ署名が選択されていることを確認します。
1. Under **[!UICONTROL PROJECT]**, select **[!UICONTROL AEM Forms]** and ensure that the appropriate signature is selected for **[!UICONTROL Code Signing Identity]**, **[!UICONTROL Debug]**, **[!UICONTROL Release]** and **[!UICONTROL Any iOS SDK]**.
1. AEM Forms アプリケーションを構築し、配布します。AEM Forms Workspace アプリケーションを構築・配信する詳細な手順については、[AEM Forms アプリケーション用のインストーラーの構築](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app)を参照してください。
