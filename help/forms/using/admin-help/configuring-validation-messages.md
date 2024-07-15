---
title: 検証メッセージの設定
description: 検証メッセージの表示方法と、web ブラウザーに返すフォームを基準に位置を指定する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 14314383-5228-4904-98c1-586f48a1142c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 100%

---

# 検証メッセージの設定 {#configuring-validation-messages}

HTML としてレンダリングされるフォームの場合、発生したフォーム検証エラーがユーザーに対して表示されます。検証メッセージの表示方法をカスタマイズできます。検証メッセージを表示する場所に応じて、フォーム内のメッセージの位置とフレーム境界線のサイズも制御できます。

## 検証メッセージの表示方法の指定 {#specify-how-validation-messages-are-displayed}

1. 管理コンソールで、サービス／Forms をクリックします。
1. 「検証結果」の「レポート」リストで次のいずれかのオプションを選択します。

   **メッセージボックス：**&#x200B;検証メッセージを別のダイアログボックスに表示します。

   **フレーム：**&#x200B;検証メッセージを同じウィンドウのフレーム内に表示します。

   **フレームなし：**&#x200B;検証メッセージを同じウィンドウ内に表示します。これがデフォルト値です。

   **API 経由（データ）：**&#x200B;検証メッセージをデータと共に API 経由で返します。検証メッセージは画面に表示されません。

   **API 経由（フォーム）：**&#x200B;検証メッセージをフォームと共に API 経由で返します。検証メッセージは画面に表示されません。

   **なし：**&#x200B;検証メッセージを表示しません。

1. 「保存」をクリックします。

## Web ブラウザーに返すフォームを基準にした検証メッセージの位置の指定 {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

「レポート」を「フレーム」または「フレームなし」に設定するとき、検証メッセージの位置を指定できます。

1. 「検証結果」の「位置」リストで次のいずれかのオプションを選択します。

   **左：**&#x200B;検証メッセージを web ブラウザーの左側に表示します。

   **右：**&#x200B;検証メッセージを web ブラウザーの右側に表示します。

   **上：**&#x200B;検証メッセージを web ブラウザーの一番上に表示します。これがデフォルト値です。

   **下：**&#x200B;検証メッセージを web ブラウザーの一番下に表示します。

1. 「保存」をクリックします。

## フレーム境界線のサイズの指定 {#specify-the-frame-border-size}

「レポート」を「フレーム」に設定するとき、フレーム境界線のサイズを指定できます。

1. 「検証結果」の「境界線のサイズ」ボックスにフレーム境界線のサイズをピクセル単位で入力します。

   境界線のサイズは 0 以上である必要があります。デフォルト値は 1 です。

1. 「保存」をクリックします。
