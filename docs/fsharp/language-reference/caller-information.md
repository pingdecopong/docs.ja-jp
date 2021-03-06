---
title: 呼び出し元情報 (f#)
description: 呼び出し元情報引数属性を使用して、メソッドから呼び出し元情報を取得する方法について説明します。
ms.date: 04/25/2017
ms.openlocfilehash: 6fd80213cdaf2c4662fd4c2ed9eaf8949e397efe
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33564802"
---
# <a name="caller-information"></a>呼び出し元情報

呼び出し元情報の属性を使用すると、メソッドへの呼び出し元に関する情報を取得できます。 ソース コードのファイル パス、ソース コードの行番号、および呼び出し元のメンバー名を取得できます。 この情報は、トレース、デバッグ、および診断ツールの作成に役立ちます。

この情報を取得するには、省略可能なパラメーターに適用される属性を使用します。各パラメーターには既定値があります。 次の表に、呼び出し元情報属性で定義されている、 [System.Runtime.CompilerServices](/dotnet/api/system.runtime.compilerservices)名前空間。

|属性|説明|型|
|---------|-----------|----|
|[CallerFilePath](/dotnet/api/system.runtime.compilerservices.callerfilepathattribute)|呼び出し元を含むソース ファイルのフル パスです。 これは、コンパイル時のファイル パスです。|`String`
|[CallerLineNumber](/dotnet/api/system.runtime.compilerservices.callerlinenumberattribute)|メソッドが呼び出されたソース ファイルの行番号。|`Integer`|
|[CallerMemberName](/dotnet/api/system.runtime.compilerservices.callermembernameattribute)|呼び出し元のメソッド名またはプロパティ名。 このトピックの「メンバー名を参照してください。|`String`|

## <a name="example"></a>例

次の例では、これらの属性を呼び出し元のトレースを使用する方法を示します。

```fsharp
open System.Diagnostics
open System.Runtime.CompilerServices

type Tracer() =
    member __.DoTrace(msg: string,
                      [<CallerMemberName>] ?memberName: string,
                      [<CallerFilePath>] ?path: string
                      [<CallerLineNumber>] ?line: int) =
        Trace.WriteLine(sprintf "Message: %s" message)
        match (memberName, path, line) with
        | Some m, Some p, Some l ->
            Trace.WriteLine(sprintf "Member name: %s" m)
            Trace.WriteLine(sprintf "Source file path: %s" p)
            Trace.WriteLine(sprintf "Source line number: %d" l)
        | _,_,_ -> ()
```

## <a name="remarks"></a>コメント

呼び出し元情報属性は、省略可能なパラメーターにのみ適用できます。 省略可能な各パラメーターの明示的な値を指定する必要があります。 呼び出し元情報属性では、呼び出し元情報属性で修飾された各省略可能なパラメーターの適切な値の書き込みにコンパイラがあります。

呼び出し元情報の値は、コンパイル時に中間言語 (IL) 内にリテラルとして出力されます。 結果とは異なり、 [StackTrace](/dotnet/api/system.diagnostics.stacktrace)難読化によるプロパティの例外、結果の影響を受けません。

省略可能な引数を明示的に指定して、呼び出し元情報を制御したり、非表示にしたりできます。

## <a name="member-names"></a>メンバー名

使用することができます、 [ `CallerMemberName` ](/dotnet/api/system.runtime.compilerservices.callermembernameattribute)属性とメンバーの名前を指定しない場合に、`String`呼び出されたメソッドに渡す引数。 この手法を使用すると、名前の変更リファクタリング変更されない問題を回避する、`String`値。 この利点は、次のタスクで役立ちます。

* トレース ルーチンと診断ルーチンの使用。
* 実装する、 [INotifyPropertyChanged](/dotnet/api/system.componentmodel.inotifypropertychanged)インターフェイスのデータをバインドするときにします。 このインターフェイスを使用すると、オブジェクトのプロパティが、プロパティが変更されたことをデータ バインド コントロールに通知できます。これによって、このコントロールは、更新された情報を表示できます。 なし、 [ `CallerMemberName` ](/dotnet/api/system.runtime.compilerservices.callermembernameattribute)属性、リテラルとしてプロパティ名を指定する必要があります。

次の表は、メンバー CallerMemberName 属性を使用するときに返される名を示します。

|呼び出しは、次のものの中で発生します。|メンバー名の結果|
|-------------------|------------------|
|メソッド、プロパティ、またはイベント|呼び出しが発生したメソッド、プロパティ、またはイベントの名前。|
|コンストラクター|文字列「.ctor」|
|静的コンストラクター|文字列「.cctor」|
|デストラクターです。|文字列「Finalize」|
|ユーザー定義の演算子または変換|生成されたメンバー名 (「op_Addition」など)。|
|Attribute コンストラクター|属性が適用されるメンバーの名前。 属性がメンバー内の要素 (パラメーター、戻り値、ジェネリック型パラメーターなど) である場合、この結果は、その要素に関連付けられているメンバーの名前になります。|
|含んでいないメンバー (型に適用されているアセンブリ レベルや属性など)|省略可能なパラメーターの既定値。|

## <a name="see-also"></a>関連項目
 [属性](attributes.md)  
 [名前付き引数](parameters-and-arguments.md#named-arguments)  
 [省略可能なパラメーター](parameters-and-arguments.md#optional-parameters)  
