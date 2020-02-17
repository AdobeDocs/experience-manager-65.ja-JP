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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 命名規則 {#naming-conventions}

## Java パッケージ名内のハイフン {#hyphens-in-java-package-name}

Java クラスの場所を作成する際には、パッケージ名がリポジトリフォルダーの場所のパッケージ名と一致しており、パス内のハイフンが適切にエスケープされている必要がある点に注意してください。

AEM の開発では、リポジトリ項目の名前にハイフンを使用することが推奨されていますが、Java パッケージ名でハイフンを使用することはできません。

The underlying CRX platform must be able to distinguish between an actual underscore &#39;_&#39; and a hyphen &#39;-&#39;. Thus, in JCR, the hyphen must be replaced with its unicode value (u002d) and escaped with an underscore &#39;_&#39;.

例えば、リポジトリパスが/apps/my-example/component/info/Info.java **の場合**、パッケージ名は `java package apps.my_002dexample.component.info;`

Notice that an underscore must similarly be escaped, such that `_` becomes `_005f`.
