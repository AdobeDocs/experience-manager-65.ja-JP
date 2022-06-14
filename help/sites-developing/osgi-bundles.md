---
title: OSGi バンドル
seo-title: OSGI Bundles
description: OSGi バンドルを管理するためのヒント
seo-description: Tips for managing your OSGi bundles
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
exl-id: e18065c7-75b9-4b37-8294-cf94122a4dcf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 100%

---

# OSGi バンドル{#osgi-bundles}

## セマンティックバージョニングを使用する {#use-semantic-versioning}

セマンティックバージョニング番号付けに関する合意に基づいたベストプラクティスについては、[https://semver.org/](https://semver.org/) を参照してください。

## 厳密に必要な数を超えるクラスおよび jar を OSGi バンドルに埋め込まない {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

共通ライブラリは個別のバンドルに取り出す必要があります。これで、共通ライブラリをバンドル全体で再利用できるようになります。OSGi バンドルに *JAR* をラップするときは、オンラインソースを調べて、誰かが既にこのラップをおこなっていないかどうかを確認してください。既存のバンドルラッパーを探す一般的な場所としては、Apache Felix、Apache Sling、Apache Geronimo、Apache ServiceMix、Eclipse Bundle Recipes および SpringSource Enterprise Bundle Repository があります。

## 最低限必要なバンドルバージョンに依存する {#depend-on-the-lowest-needed-bundle-versions}

POM ファイルのコンパイル時依存関係の場合、常に、必要な API を公開するために最低限必要なバージョンに依存するようにします。このようにすると、下位互換性を高め、以前のリリースに対するバックポート修正が容易になります。

## OSGi バンドルから最小限のパッケージセットをエクスポートする {#export-a-minimal-set-of-packages-from-osgi-bundles}

パッケージのエクスポートが完了したら、すぐに他のユーザーが依存する API を作成しておきます。エクスポート対象を可能な限り少なくし、エクスポートされているものが API であることを確認してください。以前にエクスポートしたものを取得してプライベートにするよりも、プライベートメソッドまたはクラスを取得してパブリックにする方がはるかに簡単です。

実装は、必ず個別の *impl* パッケージに配置する必要があります。デフォルトでは、*maven-bundle-plugin* は、名前に *impl* が含まれていないプロジェクトにあるものをすべてエクスポートします。

## エクスポートしたパッケージごとに必ずセマンティックバージョニングを明示的に定義する {#always-explicitly-define-a-semantic-version-for-each-package-exported}

このようにすることで、API の利用者も新しいバージョンに取り組むことができます。定義の際には、必ずセマンティックバージョニングのベストプラクティスに従ってください。これにより、API の利用者は、新しいバージョンでの変更点がどのようなタイプのものかを知ることができます。

## 公開場所に関するメタタイプ情報を含める {#include-metatype-information-where-exposed}

意味のあるメタタイプ情報を指定することで、Felix コンソールでのサービスおよびコンポーネントが理解しやすくなります。SCR 注釈および属性のリストについては、[https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html) を参照してください。
