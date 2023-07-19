---
title: Workspace に表示されるカテゴリの管理
seo-title: Managing the categories displayed in Workspace
description: Workspace では、ユーザーが開始できるプロセスは、左側のナビゲーションウィンドウのカテゴリに表示されます。 Workspace に表示されるこれらのカテゴリを管理する方法について説明します。
seo-description: In Workspace, the processes that a user can start are displayed in categories in the left navigation pane. Learn how you can manage these categories displayed in Workspace.
uuid: c2a275f5-872e-467f-9f07-4b130631e8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0d1536a2-10ac-4031-bd7f-264b02d0d75f
exl-id: 62621fe9-f69f-4bc0-aecc-d7bcc3064516
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 9%

---

# Workspace に表示されるカテゴリの管理 {#managing-the-categories-displayed-in-workspace}

Workspace では、ユーザーが開始できるプロセスは、左側のナビゲーションウィンドウのカテゴリに表示されます。 カテゴリは管理コンソールで設定できます。また、プロセスデザイナーが Workbench で設定することもできます。 プロセスデザイナーは、プロセスを作成する際にカテゴリに割り当てます。

カテゴリ名を指定する場合は、Workspace ナビゲーションウィンドウに正しく表示されるように作成します。 デフォルトでは、左側のナビゲーションパネルの幅は、210 ピクセル（約 24 文字）に固定されています。 指定したカテゴリ名が長すぎて、左側のナビゲーションウィンドウの固定幅に収まらない場合は、切り捨てられます。 フルネームは、マウスポインタをその上に置いたときにのみ表示されます。 切り捨てられるカテゴリ名を避けるようにしてください。 次の例は、に適合するカテゴリ名と切り捨てられるカテゴリ名を示しています。

**サイズに合うカテゴリ名：** Attendance &amp; Leave

**切り捨てられるカテゴリ名：** Attendance &amp; Leave（米国）

Workspace では、通常、カテゴリ内のプロセスは、「Start Process」ページにカードとして表示されます。 一般に、1 つのカテゴリに対して 6 つのカードを画面に表示してから、残りのカードを表示するためにスクロールする必要があります。 スクロールを使用するとプロセスを見つけるのが難しくなるので、各カテゴリを 6 つのプロセスに制限するか、解像度に応じて、スクロールせずに画面に表示できるプロセスの数を制限することを検討してください。

MySQL をAEM forms データベースとして使用している場合、管理コンソールでは、拡張文字の使用だけで異なる 2 つのカテゴリ名を区別することはできません。 例えば、「abcde」という名前のカテゴリと「âbcdè」という名前のカテゴリを作成した場合、これらは同じと見なされます。

## カテゴリを追加 {#add-a-category}

1. 管理コンソールで、サービス/アプリケーションおよびサービス/カテゴリの管理をクリックします。
1. 「追加」をクリックします。サブカテゴリを追加する場合は、カテゴリを選択し、[ 追加 ] をクリックします。
1. [ 名前 ] ボックスにカテゴリの名前を入力し、[ 説明 ] ボックスにカテゴリの説明を入力します。
1. 「追加」をクリックします。カテゴリがカテゴリ管理ページに表示されます。

   ***注意&#x200B;**：カテゴリを作成するときは、最大 5 階層まで追加できます。*

## カテゴリの編集 {#edit-a-category}

1. 管理コンソールで、サービス/アプリケーションおよびサービス/カテゴリの管理をクリックします。
1. 編集するカテゴリを選択し、「編集」をクリックします。 または、カテゴリをダブルクリックして編集することもできます。
1. [ 名前 ] ボックスでカテゴリの名前を編集します。

## カテゴリの削除 {#remove-a-category}

削除できるのは、使用されていないカテゴリだけです。

1. 管理コンソールで、サービス/アプリケーションおよびサービス/カテゴリの管理をクリックします。
1. カテゴリの管理ページで、削除するカテゴリのチェックボックスを選択し、「削除」をクリックします。 カテゴリが表示されなくなりました。
