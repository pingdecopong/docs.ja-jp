---
title: 接続文字列ビルダー
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8434b608-c4d3-43d3-8ae3-6d8c6b726759
ms.openlocfilehash: 01bbf726ffa8d1c595b1ef53df420431bf28560f
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32758478"
---
# <a name="connection-string-builders"></a>接続文字列ビルダー
[!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] の以前のバージョンでは、コンパイル時に文字列の値を連結した接続文字列のチェックが行われなかったために、実行時に不正なキーワードによる <xref:System.ArgumentException> が発生していました。 接続文字列のキーワードの構文は [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] のデータ プロバイダーごとに異なるため、有効な接続文字列を手動で作成するのが難しいという問題がありました。 この問題に対処するため、[!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 2.0 では、各 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] データ プロバイダー用の新しい接続文字列ビルダーが導入されました。 各データ プロバイダーは、<xref:System.Data.Common.DbConnectionStringBuilder> から継承した、厳密に型指定された接続文字列ビルダー クラスを提供しています。 次の表は、各 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] データ プロバイダーおよび対応する接続文字列ビルダー クラスの一覧です。  
  
|プロバイダー|ConnectionStringBuilder クラス|  
|--------------|-----------------------------------|  
|<xref:System.Data.SqlClient>|<xref:System.Data.SqlClient.SqlConnectionStringBuilder?displayProperty=nameWithType>|  
|<xref:System.Data.OleDb>|<xref:System.Data.OleDb.OleDbConnectionStringBuilder?displayProperty=nameWithType>|  
|<xref:System.Data.Odbc>|<xref:System.Data.Odbc.OdbcConnectionStringBuilder?displayProperty=nameWithType>|  
|<xref:System.Data.OracleClient>|<xref:System.Data.OracleClient.OracleConnectionStringBuilder?displayProperty=nameWithType>|  
  
## <a name="connection-string-injection-attacks"></a>接続文字列のインジェクション攻撃  
 ユーザー入力から文字列を動的に連結することによって接続文字列を構築している場合、接続文字列のインジェクション攻撃を受ける可能性があります。 文字列の検証や悪意のある文字のエスケープを怠ると、機密データなど、サーバー上のリソースへのアクセスを攻撃者に許してしまうことも考えられます。 たとえば、セミコロンに続けて値を追加するだけでも攻撃が成立します。 接続文字列は "後勝ち" のアルゴリズムで解析されるため、悪質な入力データによって本来の値が置き換えられます。  
  
 接続文字列ビルダー クラスは推測に頼った作業を排除し、構文エラーやセキュリティ上の脆弱性を防ぐことを目的に設計されています。 このクラスには、各データ プロバイダーによってサポートされた既知のキーと値のペアに対応するプロパティおよびメソッドが存在します。 それぞれのクラスは、あらかじめ決められた一連のシノニムを管理しており、特定のシノニムを対応する既知のキー名に変換することができます。 有効なキーと値のペアに対してチェックが実行され、無効なペアが見つかると例外がスローされます。 また、挿入された値は安全な方法で処理されます。  
  
 次の例を実行すると、<xref:System.Data.SqlClient.SqlConnectionStringBuilder> の設定に対して挿入された余分な値が、`Initial Catalog` によってどのように処理されるかを確認できます。  
  
```vb  
Dim builder As New System.Data.SqlClient.SqlConnectionStringBuilder  
builder("Data Source") = "(local)"  
builder("Integrated Security") = True  
builder("Initial Catalog") = "AdventureWorks;NewValue=Bad"  
Console.WriteLine(builder.ConnectionString)  
```  
  
```csharp  
System.Data.SqlClient.SqlConnectionStringBuilder builder =  
  new System.Data.SqlClient.SqlConnectionStringBuilder();  
builder["Data Source"] = "(local)";  
builder["integrated Security"] = true;  
builder["Initial Catalog"] = "AdventureWorks;NewValue=Bad";  
Console.WriteLine(builder.ConnectionString);  
```  
  
 出力結果を見ると、挿入された値が <xref:System.Data.SqlClient.SqlConnectionStringBuilder> によって適切に処理されていることがわかります。二重引用符内の余分な値は、新しいキーと値のペアとして接続文字列に追加されるのではなくエスケープされています。  
  
```  
data source=(local);Integrated Security=True;  
initial catalog="AdventureWorks;NewValue=Bad"  
```  
  
## <a name="building-connection-strings-from-configuration-files"></a>構成ファイルからの接続文字列の作成  
 接続文字列の特定の要素があらかじめわかっている場合、接続文字列を構成ファイルに格納しておき、それを実行時に取得することによって完全な接続文字列を作成できます。 たとえば、サーバー名は不明でも、データベースの名前はあらかじめ把握できる場合があります。 または、ユーザーに名前とパスワードだけを実行時に指定してもらい、それ以外の値を接続文字列に挿入できないようにしたい場合もあります。  
  
 接続文字列ビルダーには、<xref:System.String> を引数として受け取るオーバーロード コンストラクターがあります。この引数に対して接続文字列を部分的に指定しておき、それ以外の部分をユーザー入力で補完することも可能です。 部分的な接続文字列は構成ファイルに保存し、実行時に取得できます。  
  
> [!NOTE]
>  構成ファイルへのプログラム アクセスは <xref:System.Configuration> 名前空間によって実現できます。Web アプリケーションの場合は <xref:System.Web.Configuration.WebConfigurationManager> を、Windows アプリケーションの場合は <xref:System.Configuration.ConfigurationManager> を使用します。 接続文字列と構成ファイルの操作の詳細については、次を参照してください。[接続文字列と構成ファイル](../../../../docs/framework/data/adonet/connection-strings-and-configuration-files.md)です。  
  
### <a name="example"></a>例  
 この例では、接続文字列の一部を構成ファイルから取得し、<xref:System.Data.SqlClient.SqlConnectionStringBuilder.DataSource%2A> の <xref:System.Data.SqlClient.SqlConnectionStringBuilder.UserID%2A> プロパティ、<xref:System.Data.SqlClient.SqlConnectionStringBuilder.Password%2A> プロパティ、および <xref:System.Data.SqlClient.SqlConnectionStringBuilder> プロパティを設定することによって接続文字列全体を作成します。 構成ファイルは次のように定義されています。  
  
```xml  
<connectionStrings>  
  <clear/>  
  <add name="partialConnectString"   
    connectionString="Initial Catalog=Northwind;"  
    providerName="System.Data.SqlClient" />  
</connectionStrings>  
```  
  
> [!NOTE]
>  このコードを実行するには、プロジェクトで `System.Configuration.dll` を参照設定する必要があります。  
  
 [!code-csharp[DataWorks SqlConnectionStringBuilder.UserNamePwd#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlConnectionStringBuilder.UserNamePwd/CS/source.cs#1)]
 [!code-vb[DataWorks SqlConnectionStringBuilder.UserNamePwd#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlConnectionStringBuilder.UserNamePwd/VB/source.vb#1)]  
  
## <a name="see-also"></a>関連項目  
 [接続文字列](../../../../docs/framework/data/adonet/connection-strings.md)  
 [プライバシーとデータ セキュリティ](../../../../docs/framework/data/adonet/privacy-and-data-security.md)  
 [ADO.NET のマネージ プロバイダーと DataSet デベロッパー センター](http://go.microsoft.com/fwlink/?LinkId=217917)
