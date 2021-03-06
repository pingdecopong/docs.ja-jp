---
title: '方法: Visual C# の機能を使用して Office 相互運用オブジェクトにアクセスする (C# プログラミング ガイド)'
ms.date: 07/20/2015
helpviewer_keywords:
- optional parameters [C#], Office programming
- named and optional arguments [C#], Office programming
- dynamic [C#], Office programming
- optional arguments [C#], Office programming
- named arguments [C#], Office programming
- Office programming [C#]
ms.assetid: 041b25c2-3512-4e0f-a4ea-ceb2999e4d5e
ms.openlocfilehash: 4e2599f34e80f70a36d6f497f908887aa6853121
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33338745"
---
# <a name="how-to-access-office-interop-objects-by-using-visual-c-features-c-programming-guide"></a>方法: Visual C# の機能を使用して Office 相互運用オブジェクトにアクセスする (C# プログラミング ガイド)
Visual C# には、Office API オブジェクトへのアクセスを容易にする機能があります。 新機能は、名前付き引数と省略可能な引数、`dynamic` と呼ばれる新しい型、値パラメーターの場合と同様に COM メソッドの参照パラメーターに引数を渡す機能などです。  
  
 このトピックでは、新機能を使用して、Microsoft Office Excel ワークシートを作成および表示するコードを記述します。 その後、Excel ワークシートにリンクされているアイコンを含む Office Word 文書を追加するコードを記述します。  
  
 このチュートリアルを実行するには、Microsoft Office Excel 2007 と Microsoft Office Word 2007 またはそれ以降のバージョンがコンピューターにインストールされている必要があります。  
  
 [!INCLUDE[windowsver](~/includes/windowsver-md.md)] よりも前のオペレーティング システムを使用している場合は、[!INCLUDE[dnprdnlong](~/includes/dnprdnlong-md.md)] がインストールされていることを確認します。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-a-new-console-application"></a>新しいコンソール アプリケーションを作成するには  
  
1.  Visual Studio を起動します。  
  
2.  **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
3.  **[インストールされたテンプレート]** ペインで、**[Visual C#]** を展開し、**[Windows]** をクリックします。  
  
4.  **[新しいプロジェクト]** ダイアログ ボックスの上部で、**.NET Framework 4** (またはそれ以降のバージョン) がターゲット フレームワークとして選択されていることを確認します。  
  
5.  **[テンプレート]** ペインの **[コンソール アプリケーション]** をクリックします。  
  
6.  **[名前]** フィールドに、プロジェクトの名前を入力します。  
  
7.  **[OK]** をクリックします。  
  
     **ソリューション エクスプローラー**に新しいプロジェクトが表示されます。  
  
### <a name="to-add-references"></a>参照を追加するには  
  
1.  **ソリューション エクスプローラー**で、プロジェクトの名前を右クリックし、**[参照の追加]** をクリックします。 **[参照の追加]** ダイアログ ボックスが表示されます。  
  
2.  **[アセンブリ]** ページの **[コンポーネント名]** 一覧で **[Microsoft.Office.Interop.Word]** を選択し、Ctrl キーを押しながら **[Microsoft.Office.Interop.Excel]** を選択します。  アセンブリが表示されない場合は、アセンブリがインストールされ、表示されることの確認が必要になることがあります (「[方法: Office のプライマリ相互運用機能アセンブリをインストールする](/visualstudio/vsto/how-to-install-office-primary-interop-assemblies)」を参照)。  
  
3.  **[OK]** をクリックします。  
  
### <a name="to-add-necessary-using-directives"></a>ディレクティブを使用して必要なものを追加するには  
  
1.  **ソリューション エクスプローラー**で、**Program.cs** ファイルを右クリックし、**[コードの表示]** をクリックします。  
  
2.  次の `using` ディレクティブをコード ファイルの先頭に追加します。  
  
     [!code-csharp[csProgGuideOfficeHowTo#1](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_1.cs)]  
  
### <a name="to-create-a-list-of-bank-accounts"></a>銀行口座の一覧を作成するには  
  
1.  次のクラス定義を **Program.cs** の `Program` クラスの下に貼り付けます。  
  
     [!code-csharp[csProgGuideOfficeHowTo#2](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_2.cs)]  
  
2.  次のコードを `Main` メソッドに追加して、2 つの口座を含む `bankAccounts` 一覧を作成します。  
  
     [!code-csharp[csProgGuideOfficeHowTo#3](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_3.cs)]  
  
### <a name="to-declare-a-method-that-exports-account-information-to-excel"></a>口座情報を Excel にエクスポートするメソッドを宣言するには  
  
1.  次のメソッドを `Program` クラスに追加して、Excel ワークシートを設定します。  
  
     [Add](https://msdn.microsoft.com/library/microsoft.office.interop.excel.workbooks.add.aspx) メソッドには、特定のテンプレートを指定する省略可能なパラメーターがあります。 [!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] の新機能であるオプションのパラメーターでは、パラメーターの既定値を使用する場合は、そのパラメーターの引数を省略することができます。 次のコードで引数が渡されないため、`Add` は、既定のテンプレートを使用して、新しいブックを作成します。 以前のバージョンの C# では、同等のステートメントには、プレースホルダーの引数 `ExcelApp.Workbooks.Add(Type.Missing)` が必要です。  
  
     [!code-csharp[csProgGuideOfficeHowTo#4](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_4.cs)]  
  
2.  次のコードを `DisplayInExcel` の末尾に追加します。 このコードでは、ワークシートの最初の行の最初の 2 つの列に値が挿入されます。  
  
     [!code-csharp[csProgGuideOfficeHowTo#5](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_5.cs)]  
  
3.  次のコードを `DisplayInExcel` の末尾に追加します。 `foreach` ループでは、ワークシートの連続した行の最初の 2 つの列に口座の一覧の情報が配置されます。  
  
     [!code-csharp[csProgGuideOfficeHowTo#7](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_6.cs)]  
  
4.  次のコードを `DisplayInExcel` の末尾に追加して、コンテンツに合わせて列の幅を調整します。  
  
     [!code-csharp[csProgGuideOfficeHowTo#13](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_7.cs)]  
  
     C# の以前のバージョンでは、`ExcelApp.Columns[1]` が `Object` を返し、`AutoFit` が Excel [Range](https://msdn.microsoft.com/library/microsoft.office.interop.excel.range.aspx) メソッドであるため、これらの操作の明示的なキャストが必要です。 次の行にキャストを示します。  
  
     [!code-csharp[csProgGuideOfficeHowTo#14](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_8.cs)]  
  
     [!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] 以降のバージョンでは、アセンブリが [/link](../../../csharp/language-reference/compiler-options/link-compiler-option.md) コンパイラ オプションで参照される場合、または同等に、Excel の **[相互運用機能型の埋め込み]** プロパティが true に設定されている場合は、返される `Object` が `dynamic` に自動的に変換されます。 このプロパティの既定値は true です。  
  
### <a name="to-run-the-project"></a>プロジェクトを実行するには  
  
1.  `Main` の末尾に次の行を追加します。  
  
     [!code-csharp[csProgGuideOfficeHowTo#8](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_9.cs)]  
  
2.  Ctrl キーを押しながら、F5 キーを押します。  
  
     2 つの口座からのデータを含む Excel ワークシートが表示されます。  
  
### <a name="to-add-a-word-document"></a>Word 文書を追加するには  
  
1.  [!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] およびそれ以降のバージョンで Office プログラミングを強化するその他の方法を説明するために、次のコードでは、Word アプリケーションを開き、Excel ワークシートにリンクするアイコンを作成します。  
  
     この手順の後半で提供されている `CreateIconInWordDoc` メソッドを `Program` クラスに貼り付けます。 [Add](https://msdn.microsoft.com/library/microsoft.office.interop.word.documents.add.aspx) メソッドと [PasteSpecial](https://msdn.microsoft.com/library/microsoft.office.interop.word.selection.pastespecial.aspx) メソッドの呼び出しに伴う複雑さが、`CreateIconInWordDoc` の名前付き引数と省略可能な引数によって軽減されます。 これらの呼び出しによって、[!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] で導入された、参照パラメーターを持つ COM メソッドの呼び出しを簡略化する 2 つの他の新しい機能が組み込まれます。 第一に、値パラメーターの場合と同様に参照パラメーターに引数を渡すことができます。 つまり、参照パラメーターごとに変数を作成することなく値を直接渡すことができます。 コンパイラは引数の値を保持する一時変数を生成し、呼び出しから戻るときに変数を破棄します。 第二に、引数リスト内の `ref` キーワードを省略できます。  
  
     `Add` メソッドには 4 つの参照パラメーターがあり、これらはすべてオプションです。 [!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] 以降のバージョンでは、既定値を使用する場合は、任意またはすべてのパラメーターの引数を省略できます。 [!INCLUDE[csharp_orcas_long](~/includes/csharp-orcas-long-md.md)] 以前のバージョンでは、各パラメーターの引数を提供する必要があり、パラメーターが参照パラメーターであるため、引数は変数である必要があります。  
  
     `PasteSpecial` メソッドは、クリップボードの内容を挿入します。 このメソッドには 7 つの参照パラメーターがあり、これらはすべてオプションです。 次のコードでは、クリップボードの内容のソースへのリンクを作成する `Link` とリンクをアイコンとして表示する `DisplayAsIcon` の 2 つの参照パラメーターの引数を指定します。 [!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] では、これら 2 つに名前付き引数を使用して、その他を省略できます。 これらは参照パラメーターですが、`ref` キーワードを使用したり、引数として渡す変数を作成したりする必要はありません。 値は直接渡すことができます。 [!INCLUDE[csharp_orcas_long](~/includes/csharp-orcas-long-md.md)] 以前のバージョンでは、各参照パラメーターに変数引数を渡す必要があります。  
  
     [!code-csharp[csProgGuideOfficeHowTo#9](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_10.cs)]  
  
     [!INCLUDE[csharp_orcas_long](~/includes/csharp-orcas-long-md.md)] 以前のバージョンの言語では、次のより複雑なコードが必要です。  
  
     [!code-csharp[csProgGuideOfficeHowTo#10](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_11.cs)]  
  
2.  次のステートメントを `Main` の末尾に追加します。  
  
     [!code-csharp[csProgGuideOfficeHowTo#11](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_12.cs)]  
  
3.  次のステートメントを `DisplayInExcel` の末尾に追加します。 `Copy` メソッドはクリップボードにワークシートを追加します。  
  
     [!code-csharp[csProgGuideOfficeHowTo#12](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_13.cs)]  
  
4.  Ctrl キーを押しながら、F5 キーを押します。  
  
     アイコンを含む Word 文書が表示されます。 ワークシートを前面に表示するアイコンをダブルクリックします。  
  
### <a name="to-set-the-embed-interop-types-property"></a>[相互運用機能型の埋め込み] プロパティを設定するには  
  
1.  実行時に、プライマリ相互運用機能アセンブリ (PIA) を必要としない COM 型を呼び出すときに、追加の拡張が可能です。 PIA への依存関係を削除することによって、バージョンに依存しない、より簡単な展開が実現されます。 PIA を使用しないプログラミングのメリットの詳細については、「[チュートリアル: マネージ アセンブリからの型の埋め込み](http://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21)」を参照してください。  
  
     また、`dynamic` ではなく `Object` 型を使用して、COM メソッドに必要とされ、COM メソッドによって返される型を簡単に表現できるため、プログラミングがより簡単になります。 型が `dynamic` の変数は、明示的なキャストが不要になる実行時まで評価されません。 詳細については、「[dynamic 型の使用](../../../csharp/programming-guide/types/using-type-dynamic.md)」を参照してください。  
  
     [!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] の既定の動作では、PIA を使用せずに型情報を埋め込みます。 この既定のため、前の例のいくつかは、明示的なキャストが必要ないために簡素化されます。 たとえば、`worksheet` での `DisplayInExcel` の宣言は、`Excel._Worksheet workSheet = excelApp.ActiveSheet` ではなく `Excel._Worksheet workSheet = (Excel.Worksheet)excelApp.ActiveSheet` と記述されます。 同じメソッドの `AutoFit` への呼び出しでも、既定値を使用せずに明示的なキャストが必要になります。これは、`ExcelApp.Columns[1]` が `Object` を返し、`AutoFit` が Excel のメソッドであるためです。 次のコードはキャストを示しています。  
  
     [!code-csharp[csProgGuideOfficeHowTo#14](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_8.cs)]  
  
2.  既定値を変更し、型情報を埋め込むのではなく PIA を使用するには、**ソリューション エクスプ ローラー**で **[参照設定]** ノードを展開し、**[Microsoft.Office.Interop.Excel]** または **[Microsoft.Office.Interop.Word]** を選択します。  
  
3.  **[プロパティ]** ウィンドウが表示されない場合は、**F4** キーを押します。  
  
4.  プロパティの一覧で **[相互運用機能型の埋め込み]** を見つけて、値を **[False]** に変更します。 同様に、コマンド プロンプトで [/link](../../../csharp/language-reference/compiler-options/link-compiler-option.md) の代わりに [/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md) コンパイラ オプションを使用してコンパイルすることができます。  
  
### <a name="to-add-additional-formatting-to-the-table"></a>テーブルに追加の書式設定を追加するには  
  
1.  `AutoFit` の `DisplayInExcel` への 2 つの呼び出しを次のステートメントに置き換えます。  
  
     [!code-csharp[csProgGuideOfficeHowTo#15](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_14.cs)]  
  
     [AutoFormat](https://msdn.microsoft.com/library/microsoft.office.interop.excel.range.autoformat.aspx) メソッドには、7 つの値パラメーターがあり、これらはすべて省略可能です。 名前付き引数と省略可能な引数を使用すると、一部またはすべてのパラメーターに引数を指定することができます。引数を指定しないこともできます。 前のステートメントでは、1 つのパラメーター `Format` にのみ引数が指定されています。 `Format` はパラメーター リストの最初のパラメーターであるため、パラメーター名を指定する必要はありません。 ただし、次のコードに示すように、パラメーター名が含まれている場合、ステートメントがわかりやすい場合があります。  
  
     [!code-csharp[csProgGuideOfficeHowTo#16](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_15.cs)]  
  
2.  Ctrl + F5 キーを押して結果を表示します。 その他の形式は、[XlRangeAutoFormat](https://msdn.microsoft.com/library/microsoft.office.interop.excel.xlrangeautoformat.aspx) 列挙型のページに掲載されています。  
  
3.  手順 1 のステートメントと [!INCLUDE[csharp_orcas_long](~/includes/csharp-orcas-long-md.md)] 以前のバージョンで必要な引数が示されている次のコードを比較します。  
  
     [!code-csharp[csProgGuideOfficeHowTo#17](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_16.cs)]  
  
## <a name="example"></a>例  
 コード例全体を次に示します。  
  
 [!code-csharp[csProgGuideOfficeHowTo#18](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-access-office-onterop-objects_17.cs)]  
  
## <a name="see-also"></a>参照  
 <xref:System.Type.Missing?displayProperty=nameWithType>  
 [dynamic](../../../csharp/language-reference/keywords/dynamic.md)  
 [dynamic 型の使用](../../../csharp/programming-guide/types/using-type-dynamic.md)  
 [名前付き引数と省略可能な引数](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)  
 [方法: Office プログラミングで名前付き引数と省略可能な引数を使用する](../../../csharp/programming-guide/classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)
