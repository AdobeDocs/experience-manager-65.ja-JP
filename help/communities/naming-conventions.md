---
title: 命名規則
seo-title: 命名規則
description: Java パッケージ名内のハイフン
seo-description: Java パッケージ名内のハイフン
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 54%

---

# 命名規則 {#naming-conventions}

## Java パッケージ名内のハイフン {#hyphens-in-java-package-name}

Java クラスの場所を作成する際には、パッケージ名がリポジトリフォルダーの場所のパッケージ名と一致しており、パス内のハイフンが適切にエスケープされている必要がある点に注意してください。

AEM の開発では、リポジトリ項目の名前にハイフンを使用することが推奨されていますが、Java パッケージ名でハイフンを使用することはできません。

基になるCRXプラットフォームでは、実際のアンダースコア`_ `とハイフン`-`を区別できる必要があります。 したがって、JCRでは、ハイフンをそのUnicode値(u002d)に置き換え、アンダースコア`_`でエスケープする必要があります。

例えば、リポジトリパスが&#x200B;**/apps/my-example/component/info/Info.java**&#x200B;の場合、パッケージ名は`java package apps.my_002dexample.component.info;`にする必要があります。

アンダースコアも同様にエスケープする必要があり、`_`が`_005f`になることに注意してください。
