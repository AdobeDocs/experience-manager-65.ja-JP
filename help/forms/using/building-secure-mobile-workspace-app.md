---
title: セキュアな AEM Forms アプリケーション（iOS 用）の構築
description: Xcode プロジェクトをアーカイブして、セキュアな AEM Forms アプリケーション（iOS 用）を構築する方法について説明します。これにより、インストーラー（.ipa ファイル）とプロパティリスト（.plist ファイル）ファイルが作成されます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 12cc2027-ae94-40c3-a7d1-553469426114
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '360'
ht-degree: 100%

---

# セキュアな AEM Forms アプリケーション（iOS 用）の構築 {#building-a-secure-aem-forms-app-for-ios}

AEM Forms アプリケーション用 Xcode プロジェクトをアーカイブして、インストーラー（.ipa ファイル）とプロパティリストファイル（.plist ファイル）を構築する必要があります。プロパティリストファイルには、アプリケーションの名前やホストしているロケーションなど、ホストされているインハウスアプリケーションの設定情報が含まれます。プロパティリストファイルについての詳細は、[About Information Property List Files](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) を参照してください。

1. 次の Web サイトにログインします。

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. アプリケーション ID を作成します。アプリケーション ID を作成する詳細な手順については、[アプリケーション ID の作成と設定](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html)を参照してください。
1. ご使用のアプリケーションの iOS アプリケーション用バンドル識別子を設定するには、**[!UICONTROL アプリケーション ID の設定]**&#x200B;をクリックします。
1. Web ページの下部にある、**[!UICONTROL Enable for Data Protection]** を選択します。data protection オプションを指定します。

   「**[!UICONTROL 完了]**」をクリックします。

1. プロビジョニング／配布に移動し、手順 3 で設定したアプリケーション ID を使って新しいプロファイルを作成します。
1. プロビジョニングプロファイルをダウンロードして Xcode および iPad に追加します。 
1. Xcode、iOS SDK がインストールされ設定済みの Mac マシンにログインします。
1. Xcode で `AEM Forms.xcodeproj` プロジェクトを開きます。
1. 「**[!UICONTROL TARGETS]**」の「**[!UICONTROL AEM Forms]**」をクリックし、「**[!UICONTROL AEM Forms]**」を選択します。「**[!UICONTROL ビルド設定]**」タブを選択し、「**[!UICONTROL コード署名エンタイトルメント]**」セクションを探して、「エンタイトルメント」ドロップダウンで「**[!UICONTROL LC エンタープライズ]**」オプションを選択します。
1. Xcode 内にある `LC Enterprise.entitlements` ファイルを探して、編集するために開きます。**XCode エンタイトルメント**&#x200B;の下で、プロビジョニングプロファイル内に存在するのものと同じキー値ペアを追加します。
1. 「**[!UICONTROL ビルド設定]**」タブで、「**[!UICONTROL すべて]**」をクリックし、「**[!UICONTROL 結合]**」をクリックします。
1. 「**[!UICONTROL 設定]**」リストで、「**[!UICONTROL コード署名]**」を展開します。
1. 「**[!UICONTROL コード署名 ID]**」から、適切な署名を選択します。「**[!UICONTROL デバッグ]**」、「**[!UICONTROL リリース]**」、「**[!UICONTROL 任意の iOS SDK]**」に同じ署名が選択されていることを確認します。
1. 「**[!UICONTROL プロジェクト]**」の「**[!UICONTROL AEM Forms]**」を選択し、「**[!UICONTROL コード署名 ID]**」、「**[!UICONTROL デバッグ]**」、「**[!UICONTROL リリース]**」、「**[!UICONTROL 任意の iOS SDK]**」に対して適切な署名が選択されていることを確認します。
1. AEM Forms アプリケーションを構築し、配布します。AEM Forms アプリケーションを構築および配布する詳細な手順については、[AEM Forms アプリケーション用のインストーラーの構築](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app)を参照してください。
