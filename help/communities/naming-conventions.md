---
title: Java パッケージ名の命名規則
description: Java パッケージ名でのハイフン
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 1%

---

# 命名規則 {#naming-conventions}

## Java パッケージ名でのハイフン {#hyphens-in-java-package-name}

Java クラスの場所を作成する場合、パッケージ名は、リポジトリフォルダーの場所と一致し、パス内のハイフンが適切にエスケープされる必要があります。

AEMの開発では、リポジトリ項目の名前にハイフンを使用することが推奨されますが、ハイフンは Java パッケージ名内では無効です。

基になる CRX プラットフォームは、実際のアンダースコアを区別できる必要があります `_ `とハイフン `-`. したがって、JCR では、ハイフンをその Unicode 値 (u002d) に置き換え、アンダースコアでエスケープする必要があります `_`.

例えば、リポジトリのパスが **/apps/my-example/component/info/Info.java**、パッケージ名は `java package apps.my_002dexample.component.info;`

アンダースコアも同様にエスケープする必要があり、次のようにします。 `_` 次に `_005f`.
