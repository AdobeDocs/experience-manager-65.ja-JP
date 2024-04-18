---
title: OSGi バンドル
description: Adobe Experience Manager で OSGi バンドルを管理するためのいくつかのヒントについて説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: e18065c7-75b9-4b37-8294-cf94122a4dcf
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 100%

---

# OSGi バンドル{#osgi-bundles}

## セマンティックバージョニングを使用する {#use-semantic-versioning}

セマンティックバージョニング番号付けに関する合意に基づいたベストプラクティスについては、[https://semver.org/](https://semver.org/) を参照してください。

## 厳密に必要な数を超えるクラスおよび jar を OSGi バンドルに埋め込まないようにする {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

共通ライブラリは個別のバンドルに分割する必要があります。これで、共通ライブラリをバンドル全体で再利用できるようになります。OSGi バンドルに *JAR* をラップするときは、オンラインソースを調べて、他のユーザーが既にこのラップを行っていないかどうかを確認してください。既存のバンドルラッパーを探す一般的な場所としては、Apache Felix、Apache Sling、Apache Geronimo、Apache ServiceMix、Eclipse Bundle Recipes および SpringSource Enterprise Bundle Repository があります。

## 最低限必要なバンドルバージョンに依存する {#depend-on-the-lowest-needed-bundle-versions}

POM ファイルのコンパイル時の依存関係については、常に、必要な API を公開するために最低限必要なバージョンに依存するようにします。このようにすると、下位互換性を高め、以前のリリースに対するバックポート修正が容易になります。

## OSGi バンドルから最小限のパッケージセットを書き出す {#export-a-minimal-set-of-packages-from-osgi-bundles}

パッケージを書き出すと、他のパッケージが依存する API が作成されます。エクスポート対象を可能な限り少なくし、エクスポートされているものが API であることを確認してください。以前にエクスポートしたものを取得してプライベートにするよりも、プライベートメソッドまたはクラスを取得してパブリックにする方がはるかに簡単です。

実装は、常に個別の *impl* パッケージに配置してください。デフォルトでは、*maven-bundle-plugin* は、プロジェクト内の名前に *impl* が含まれていないものをすべて書き出します。

## 書き出したパッケージごとに必ずセマンティックバージョニングを明示的に定義する {#always-explicitly-define-a-semantic-version-for-each-package-exported}

このようにすることで、API の利用者も新しいバージョンの変更点を把握することができます。定義の際には、必ずセマンティックバージョニングのベストプラクティスに従ってください。これにより、API の利用者は、新しいバージョンでの変更点がどのようなタイプのものかを知ることができます。

## 公開場所に関するメタタイプ情報を含める {#include-metatype-information-where-exposed}

意味のあるメタタイプ情報を指定することで、Felix コンソールでのサービスおよびコンポーネントが理解しやすくなります。SCR 注釈および属性のリストについては、[https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html) を参照してください。
