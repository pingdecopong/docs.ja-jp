---
title: ".NET Compiler Platform SDK セマンティック モデルの使用"
description: "この概要は、コードのセマンティック モデルを理解して操作するために使用する型を理解するためのものです。"
author: billwagner
ms.author: wiwagn
ms.date: 10/15/2017
ms.topic: conceptual
ms.prod: .net
ms.devlang: devlang-csharp
ms.custom: mvc
ms.openlocfilehash: 28366093c516f5367d82c0bdfc53749e764361ef
ms.sourcegitcommit: d095094e942eedf09530ea5636fbaf9029853027
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2017
---
# <a name="work-with-semantics"></a>セマンティクスの使用

[構文ツリー](work-with-syntax.md)は、ソース コードの字句および構文構造を表します。 ソースのすべての宣言とロジックを説明するにはこの情報だけで十分ですが、参照内容を識別するには十分ではありません。 名前は以下を表す場合があります。

- 型
- フィールド
- メソッド
- ローカル変数

これらはそれぞれ一意に異なりますが、実際に識別子が指しているものを判別するには、多くの場合、言語規則をよく理解する必要があります。 

ソース コードで表されるプログラム要素がいくつかあります。プログラムは、以前にコンパイルされ、アセンブリ ファイルにパッケージ化されたライブラリを参照することもできます。 アセンブリで使用できるソース コードはありません (したがって、構文ノードやツリーもありません) が、プログラムは引き続き、その内部の要素を参照することができます。

これらのタスクには、**セマンティック モデル**が必要です。

ソース コードの構文モデルだけでなく、セマンティック モデルでも言語規則がカプセル化されます。これにより、参照される正しいプログラム要素と識別子を簡単に一致させることができます。

## <a name="compilation"></a>コンパイル

コンパイルは、C# または Visual Basic プログラムのコンパイルに必要なすべてを表します。これには、アセンブリ参照、コンパイラ オプション、ソース ファイルがすべて含まれます。 

この情報はすべて 1 か所にあるため、ソース コードに含まれる要素を詳細に説明することができます。 コンパイルでは、宣言される型、メンバー、または変数をそれぞれシンボルとして表します。 コンパイルにはさまざまなメソッドが含まれています。これらは、ソース コードで宣言されているか、アセンブリからメタデータとしてインポートされたシンボルを見つけて関連付けるのに役立ちます。

構文ツリーと同じように、コンパイルは不変です。 作成したコンパイルを自分自身で変更することも、共有する可能性のある他のユーザーが変更することもできません。 ただし、既存のコンパイルから新しいコンパイルを作成することはできます。その際に、変更を指定します。 たとえば、追加のソース ファイルまたはアセンブリ参照が含まれる場合があることを除き、既存のコンパイルとあらゆる点で同じコンパイルを作成できます。

## <a name="symbols"></a>シンボル

シンボルは、ソース コードで宣言されたか、メタデータとしてアセンブリからインポートされた異なる要素を表します。 すべての名前空間、型、メソッド、プロパティ、フィールド、イベント、パラメーター、またはローカル変数はシンボルで表されます。 

<xref:Microsoft.CodeAnalysis.Compilation> 型のさまざまなメソッドとプロパティは、シンボルを見つけるのに役立ちます。 たとえば、共通のメタデータ名で宣言された型のシンボルを見つけることができます。 グローバル名前空間をルートとするシンボルのツリーとしてシンボル テーブル全体にアクセスすることもできます。

シンボルには、他の参照シンボルなど、ソースまたはメタデータからコンパイラが判別した追加情報も含まれます。 各種類のシンボルは <xref:Microsoft.CodeAnalysis.ISymbol> から派生した個別のインターフェイスによって表され、それぞれ独自のメソッドとプロパティで、コンパイラが収集した情報が詳細に示されます。 これらのプロパティの多くは、他のシンボルを直接参照します。 たとえば、<xref:Microsoft.CodeAnalysis.IMethodSymbol.ReturnType?displayProperty=nameWithType> プロパティは、メソッドの宣言で参照される実際の型のシンボルを示します。

シンボルは、ソース コードとメタデータ間の名前空間、型、メンバーの共通表現を示します。 たとえば、ソース コードで宣言されたメソッドと、メタデータからインポートされたメソッドは両方とも、同じプロパティを持つ <xref:Microsoft.CodeAnalysis.IMethodSymbol> で表されます。

シンボルは <xref:System.Reflection> API で表される CLR 型システムと概念が似ていますが、型だけでなく、モデル化を行うという点で優れています。 名前空間、ローカル変数、ラベルはすべてシンボルです。 また、シンボルは、CLR 概念ではなく、言語概念を表します。 重複するものが多くありますが、意味のある違いも多くあります。 たとえば、C# または Visual Basic の反復子メソッドは単一のシンボルです。 ただし、反復子メソッドが CLR メタデータに変換された場合、それは 1 つの型および複数のメソッドとなります。

## <a name="semantic-model"></a>セマンティック モデル

セマンティック モデルは、1 つのソース ファイルに対するすべてのセマンティック情報を表します。 これを使用して以下を検出できます。 

* ソース内の特定の場所で参照されているシンボル。
* 任意の式の結果の型。
* エラーや警告など、すべての診断情報。
* ソース領域内外への変数のフロー状態。
* より予測的な質問に対する回答。