---
title: 早期導入者とプレリリース機能を統合するための機能切り替えを有効にします
description: 機能の切り替えは、管理者がランタイム環境で新機能を有効にできる、AEMの機能です。
feature: Adaptive Forms, Foundation Components
role: User, Developer
hidefromtoc: true
exl-id: 08815c2b-23b3-4545-a3ab-ba47ba1c3c55
source-git-commit: 9b28ab12422743cd7849d2761aef9916ec6710f5
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---

# Adobe Experience Manager（AEM） 6.5 の機能の切り替え{#enable-feature-toggle-aem-forms-65}

機能の切り替えはAEMの機能で、管理者が特定の機能を動的に有効または無効にできるようにするものです。 この機能は、大規模なデプロイメントやコードベースの変更を必要とせずに **早期導入者機能** および **プレリリース機能** を管理する場合に特に役立ちます。 これにより、AEM環境でアクセスできる機能を柔軟に制御できます。

## AEM 6.5 設定で機能の切り替えを使用する理由

AEM 6.5 設定で作業している場合、機能は次のヘルプを切り替えます。

* 実験的な機能を安全にテストする

* 新しいコンポーネントを段階的にロールアウトする。

* 複数の環境で単一のコードベースを維持する。

* 導入とアップグレードの際のリスクを軽減

## 前提条件

AEM 6.5 設定で機能の切り替えを有効にする前に、次を確認します。

* ユーザーは `forms-users` グループのメンバーです。

* `http://<author-instance-url>:portnumber/system/console/bundles` に移動し、**（com.adobe.granite.toggle.impl.dev-1.1.2.jar）** バンドルが存在するかどうかを確認します。 存在しない場合は [ リンクからバンドルをダウンロード ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/com.adobe.granite.toggle.impl.dev-1.1.2%20.jar)。

  ![ 機能切り替え ](/help/forms/using/assets/feature-toggle-6.5.png)

## 機能切替スイッチの有効化 {#enable-feature-toggle-65}

早期導入者または新機能の機能の切り替えは、次の手順に従って **0}AEM web コンソールを使用して設定できます。**

1. AEM Forms インスタンスにログインします。
2. `http://<author-instance-url>:portnumber/system/console/configMgr` に移動します。
3. Configuration Manager で **Adobe Granite Dynamic Toggle Provider** を検索します。
4. アイコン ![ 鉛筆アイコン ](assets/illustratorcc_penciltool_cur_edit_2_17.png) をクリックします。
5. 「[!UICONTROL  有効な切り替え ]」セクションで、「![ 鉛筆アイコン ](assets/aem6forms_add.png)」をクリックします。
6. 以下の画像に示すように、機能の機能切り替え ID を追加します。
   ![ 追加と切り替え ](assets/add_toggle_number_forms.png)

   >[!NOTE]
   >
   >機能の切り替え ID は、早期導入者機能に固有のドキュメントで確認できます。

7. 「保存」をクリックします。

## 機能切り替えを無効にする {#disable-feature-toggle-65}

切り替えが有効になっている機能の機能の切り替えを無効にするには、次の手順に従います。

1. AEM Forms インスタンスにログインします。
2. `http://<author-instance-url>:portnumber/system/console/configMgr` に移動します。
3. Configuration Manager で **Adobe Granite Dynamic Toggle Provider** を検索します。
4. アイコン ![ 鉛筆アイコン ](assets/illustratorcc_penciltool_cur_edit_2_17.png) をクリックします。
5. 「[!UICONTROL  無効な切り替え ]」セクションで、「![ 鉛筆アイコン ](assets/aem6forms_add.png)」をクリックします。
6. 無効にする機能のトグル番号を追加します。
   ![ 切り替えを削除 ](assets/remove_toggle_feature_forms.png)
7. 「保存」をクリックします。

## 技術的な考慮事項

機能の切り替えは環境に固有で、実行時に管理されるので、サーバーを再起動する必要はありません。 ただし、一部の機能では、変更を反映するために、関連するページの更新やキャッシュのクリアが必要になる場合があります。
`http://<author-instance-url>:4502/etc.clientlibs/toggles.json` を使用して、環境の機能切り替えによって有効になった機能のリストにアクセスできます。
