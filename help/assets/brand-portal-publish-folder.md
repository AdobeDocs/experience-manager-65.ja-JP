---
title: Brand Portal へのフォルダーの公開
description: Brand Portal へのフォルダーの公開および非公開の方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
docset: aem65
feature: Brand Portal
role: User
exl-id: 92a156f0-ce2a-4c83-bd57-0c29efbf784f
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '565'
ht-degree: 100%

---

# Brand Portal へのフォルダーの公開{#publish-folders-to-brand-portal}

Adobe Experience Manager（AEM）Assets の管理者は、アセットやフォルダーを組織の AEM Assets Brand Portal インスタンスに公開（または公開ワークフローを未来の日時で設定）できます。ただし、最初に AEM Assets を Brand Portal と統合する必要があります。詳しくは [AEM Assets と Brand Portal の連携の設定](/help/assets/configure-aem-assets-with-brand-portal.md)を参照してください。

アセットまたはフォルダーを公開すると、Brand Portal のユーザーが使用できるようになります。

その後、AEM Assets でオリジナルのアセットまたはフォルダーに変更を加えても、そのアセットまたはフォルダーを再び公開しない限り変更内容は Brand Portal に反映されません。このため、作業中の変更が Brand Portal に提供されることがありません。管理者が公開した承認済みの変更のみが Brand Portal で提供されます。

## Brand Portal へのフォルダーの公開 {#publish-folders-to-brand-portal-1}

1. AEM Assets のインターフェイスで、目的のフォルダーにマウスポインターを置き、クイックアクションから「**公開**」オプションを選択します。

   あるいは、目的のフォルダーを選択して後述の手順に従います。

   ![publish2bp](assets/publish2bp.png)

1. **フォルダーを今すぐ公開**

   選択したフォルダーを Brand Portal に公開するには、次のいずれかを実行します。

   * ツールバーで「**クイック公開**」を選択します。次に、メニューで「**Brand Portal に公開**」を選択します。

   * ツールバーで「**公開を管理**」を選択します。

   1. **アクション**&#x200B;から「**Brand Portalに公開**」を選択し、**スケジュール**&#x200B;から「**今すぐ**」を選択し、「**次へ**」をクリックします。
   1. 「**範囲**」の選択を確認し、「**Brand Portal に公開**」をクリックします。

   フォルダーが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portal のインターフェイスにログインして、公開されたフォルダーを確認します。

   **フォルダーを後で公開**

   次のように、アセットフォルダーの Brand Portal ワークフローへの公開を、後の日時でスケジュールします。

   1. 公開するアセットまたはフォルダーを選択したら、上部のツールバーから「**公開を管理**」を選択します。
   1. **アクション**&#x200B;から「**Brand Portalに公開**」を選択し、**スケジュール**&#x200B;から「**後で**」を選択します。

      ![publishlaterbp](assets/publishlaterbp.png)

   1. 「**アクティベート日**」を選択して時刻を指定します。「**次へ**」をクリックします。
   1. 「**範囲**」で選択内容を確認します。「**次へ**」をクリックします。
   1. 「**ワークフロー**」でワークフロータイトルを指定します。「**後で公開する**」をクリックします。

      ![manageschedulepub](assets/manageschedulepub.png)

## Brand Portal へのフォルダーの非公開 {#unpublish-folders-from-brand-portal}

AEM オーサーインスタンスから公開を取り消すことで、Brand Portal に公開されているアセットフォルダーを削除できます。元のフォルダーを非公開にすると、Brand Portal ユーザーはそのコピーを使用できなくなります。

Brand Portal へのフォルダーの公開をすぐに取り消すことも、取り消しのスケジュールを未来の日時で設定することもできます。Brand Portal へのアセットフォルダーを非公開にするには、次の手順を実行します。

1. AEM オーサーインスタンス内の AEM Assets インターフェイスで、公開を取り消すフォルダーを選択します。

   ![publish2bp-1](assets/publish2bp.png)

1. ツールバーで「**公開を管理**」をクリックします。

1. **Brand Portal への公開を今すぐ取り消し**

   Brand Portal へのフォルダーの公開をすぐに取り消すには、次のようにします。

   1. ツールバーで「**公開を管理**」を選択します。
   1. **アクション**&#x200B;から「**Brand Portal への公開を取り消し**」を選択し、**スケジュール**&#x200B;から「**今すぐ**」を選択し、「**次へ**」をクリックします。
   1. 「**範囲**」の選択を確認し、「**Brand Portal から非公開**」をクリックします。

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **Brand Portal への公開を後で取り消し**

   Brand Portal へのフォルダーの公開を停止するスケジュールを未来の日時で設定するには、次のようにします。

   1. ツールバーで「**公開を管理**」を選択します。
   1. **アクション**&#x200B;から「**Brand Portal への公開を取り消し**」を選択し、**スケジュール**&#x200B;から「**後で**」を選択します。
   1. 「**アクティベート日**」を選択して時刻を指定します。「**次へ**」をクリックします。
   1. 「**範囲**」で選択内容を確認し、「**次へ**」をクリックします。
   1. 「**ワークフロー**」で&#x200B;**ワークフロータイトル**&#x200B;を指定します。「**後で非公開にする**」をクリックします。

      ![unpublishworkflows](assets/unpublishworkflows.png)

>[!NOTE]
>
>Brand Portal に対してアセットを公開または非公開にする手順は、フォルダーの場合の手順と同様です。
