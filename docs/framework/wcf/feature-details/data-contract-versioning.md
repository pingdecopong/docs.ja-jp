---
title: データ コントラクトのバージョン管理
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- versioning [WCF], data contracts
- versioning [WCF]
- data contracts [WCF], versioning
ms.assetid: 4a0700cb-5f5f-4137-8705-3a3ecf06461f
ms.openlocfilehash: 1ba51c51f30293e05dee17f9cf78cc049e1c751f
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33496287"
---
# <a name="data-contract-versioning"></a>データ コントラクトのバージョン管理
アプリケーションの進化に伴って、サービスが使用するデータ コントラクトを変更することが必要になる場合があります。 ここでは、データ コントラクトをバージョン管理する方法について説明します。 データ コントラクトのバージョン管理のメカニズムについても説明します。 完全な概要および規範的なバージョン管理ガイドでは、「[ベスト プラクティス: データ コントラクトのバージョン管理](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md)です。  
  
## <a name="breaking-vs-nonbreaking-changes"></a>互換性に影響する変更と影響しない変更  
 データ コントラクトへの変更には、互換性に影響するものと影響しないものとがあります。 互換性に影響しない方法でデータ コントラクトを変更すると、古いバージョンのコントラクトを使用するアプリケーションは新しいバージョンを使用するアプリケーションと通信できます。また、新しいバージョンを使用するアプリケーションも古いバージョンを使用するアプリケーションと通信できます。 一方、互換性に影響する変更では、一方向または双方向で通信できなくなります。  
  
 型を変更してもその送受信方法に影響しない場合は、互換性に影響しない変更と呼びます。 このような変更では、データ コントラクトは変更されず、基になる型のみが変更されます。 たとえば、フィールドの名前を変更した後で <xref:System.Runtime.Serialization.DataMemberAttribute.Name%2A> の <xref:System.Runtime.Serialization.DataMemberAttribute> プロパティを以前のバージョン名に設定すれば、互換性に影響しません。 次のコードに、バージョン 1 のデータ コントラクトを示します。  
  
 [!code-csharp[C_DataContractVersioning#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractversioning/cs/source.cs#1)]
 [!code-vb[C_DataContractVersioning#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractversioning/vb/source.vb#1)]  
  
 互換性に影響しない変更を次のコードに示します。  
  
 [!code-csharp[C_DataContractVersioning#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractversioning/cs/source.cs#2)]
 [!code-vb[C_DataContractVersioning#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractversioning/vb/source.vb#2)]  
  
 変更によっては、送信されるデータを変更しても、必ずしも互換性に影響しない場合もあります。 次の変更は常に互換性に影響します。  
  
-   データ コントラクトの <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> 値または <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A> 値の変更。  
  
-   <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> の <xref:System.Runtime.Serialization.DataMemberAttribute> プロパティを使用したデータ メンバーの順序の変更。  
  
-   データ メンバーの名前の変更。  
  
-   データ メンバーのデータ コントラクトの変更  (たとえば、データ メンバーの型を整数型から文字列型に変更したり、"Customer" という名前のデータ コントラクトを持つ型を "Person" という名前のデータ コントラクトを持つ型に変更したりするなど)。  
  
 以下のような変更も考えられます。  
  
## <a name="adding-and-removing-data-members"></a>データ メンバーの追加と削除  
 厳密なスキーマ検証 (古いスキーマに基づく新しいインスタンスの検証) が必要ではない限り、多くの場合、データ メンバーの追加または削除は互換性に影響する変更ではありません。  
  
 追加のフィールドを持つ型が、そのフィールドを持たない型に逆シリアル化された場合、追加のフィールドにある情報は無視されます  (の場合もあります; ラウンド トリップのための詳細については格納されているを参照してください[上位互換性のあるデータ コントラクト](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md))。  
  
 一部のフィールドが足りない型が、追加のフィールドを持つ型に逆シリアル化された場合、追加のフィールドは既定値 (通常はゼロまたは `null`) のままになります  (既定値が変更可能性があります詳細については、次を参照してください。[バージョン トレラントなシリアル化コールバック](../../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md)。)。  
  
 たとえば、クライアントで `CarV1` クラスを使用し、サービスで `CarV2` クラスを使用することも、サービスで `CarV1` クラスを使用し、クライアントで `CarV2` クラスを使用することもできます。  
  
 [!code-csharp[C_DataContractVersioning#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractversioning/cs/source.cs#3)]
 [!code-vb[C_DataContractVersioning#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractversioning/vb/source.vb#3)]  
  
 バージョン 2 のエンドポイントからバージョン 1 のエンドポイントに正常にデータを送信できます。 `Car` データ コントラクトのバージョン 2 をシリアル化すると、次のような XML が生成されます。  
  
```xml  
<Car>  
    <Model>Porsche</Model>  
    <HorsePower>300</HorsePower>  
</Car>  
```  
  
 バージョン 1 の逆シリアル化エンジンでは、`HorsePower` フィールドに一致するデータ メンバーを見つけられないため、データは破棄されます。  
  
 また、バージョン 1 のエンドポイントからバージョン 2 のエンドポイントにデータを送信することもできます。 `Car` データ コントラクトのバージョン 1 をシリアル化すると、次のような XML が生成されます。  
  
```xml  
<Car>  
    <Model>Porsche</Model>  
</Car>  
```  
  
 受信 XML に一致するデータがないため、バージョン 2 のデシリアライザーでは `HorsePower` フィールドを何に設定するのか判別できません。 そのため、このフィールドには既定値である 0 が設定されます。  
  
## <a name="required-data-members"></a>必須データ メンバー  
 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> の <xref:System.Runtime.Serialization.DataMemberAttribute> プロパティを `true` に設定すると、データ メンバーを必須のデータ メンバーとしてマークできます。 逆シリアル化中に必須データがない場合、データ メンバーは既定値に設定されず、代わりに例外がスローされます。  
  
 必須のデータ メンバーの追加は、互換性に影響する変更です。 つまり、新しい型を古い型のエンドポイントに送信することはできますが、その逆はできなくなります。 以前のバージョンで必須としてマークされていたデータ メンバーを削除することも、互換性に影響する変更です。  
  
 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> プロパティの値を `true` から `false` に変更することは互換性に影響しませんが、`false` から `true` に変更すると、これよりも以前のいずれかのバージョンの型にこのデータ メンバーが存在していない場合、互換性に影響することがあります。  
  
> [!NOTE]
>  <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> プロパティが `true` に設定されていても、受信データは NULL またはゼロの場合があるので、型ではこの可能性を処理できるようにしておく必要があります。 不適切な受信データに対するセキュリティ保護メカニズムとして <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> を使用しないでください。  
  
## <a name="omitted-default-values"></a>既定値の省略  
 (推奨されません) 可能であればを設定する、 `EmitDefaultValue` 、DataMemberAttribute 属性をプロパティ`false`」の説明に従って、[データ メンバーの既定値](../../../../docs/framework/wcf/feature-details/data-member-default-values.md)です。 このプロパティが `false` に設定されている場合、データ メンバーが既定値 (通常 NULL またはゼロ) に設定されていても、そのデータ メンバーは出力されません。 これにより、次の 2 つの点で、異なるバージョンの必須データ メンバーの互換性が失われます。  
  
-   あるバージョンで必須になっているデータ メンバーを持つデータ コントラクトは、データ メンバーの `EmitDefaultValue` が `false` に設定されている別のバージョンから既定 (NULL またはゼロ) のデータを受信できません。  
  
-   `EmitDefaultValue` が `false` に設定されている必須データ メンバーは、既定値 (NULL またはゼロ) をシリアル化で使用できませんが、逆シリアル化ではこのような値を受信できます。 これによりラウンド トリップの問題が発生します (データを読み取ることはできますが、書き込むことができません)。 そのため、あるバージョンにおいて `IsRequired` が `true` であり、`EmitDefaultValue` が `false` である場合、どのバージョンのデータ コントラクトにおいてもラウンド トリップを発生させる値を生成できるように、これ以外のすべてのバージョンに同じ組み合わせを適用する必要があります。  
  
## <a name="schema-considerations"></a>スキーマの考慮事項  
 データ コントラクト型用に生成されるスキーマの詳細については、次を参照してください。[データ コントラクト スキーマの参照](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)です。  
  
 データ コントラクト型には、バージョン管理に対応の WCF スキーマを生成します。 つまり、あるバージョンの型からエクスポートされたスキーマには、そのバージョンに存在するデータ メンバーのみが含まれます。 <xref:System.Runtime.Serialization.IExtensibleDataObject> インターフェイスを実装しても、型のスキーマは変更されません。  
  
 データ メンバーは、既定でオプション要素としてスキーマにエクスポートされます。 つまり、`minOccurs` (XML 属性) の値は 0 に設定されています。 `minOccurs` を 1 に設定した場合、必須データ メンバーがエクスポートされます。  
  
 スキーマを厳密に遵守する必要がある場合、互換性に影響しないと思われる変更の多くが、実際には互換性に影響します。 前述の例では、`CarV1` 要素だけを持つ `Model` インスタンスは、`CarV2` スキーマ (`Model` と `Horsepower` の 2 つの要素を持ちますが、いずれも省略可能です) に対して有効です。 しかし、この逆は真ではありません。つまり、`CarV2` インスタンスは `CarV1` スキーマに対して検証が失敗します。  
  
 ラウンド トリップにもいくつかの考慮事項があります。 詳細については、「スキーマの考慮事項」セクションを参照してください。[上位互換性のあるデータ コントラクト](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)です。  
  
### <a name="other-permitted-changes"></a>許可されるその他の変更  
 <xref:System.Runtime.Serialization.IExtensibleDataObject> インターフェイスの実装は、互換性に影響しない変更です。 ただし、<xref:System.Runtime.Serialization.IExtensibleDataObject> が実装されていた型のバージョンより前のバージョンでは、ラウンド トリップはサポートされていません。 詳細については、「[上位互換性のあるデータ コントラクト](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)」を参照してください。  
  
## <a name="enumerations"></a>列挙  
 列挙体メンバーの追加や削除は、互換性に影響する変更です。 `EnumMemberAtttribute` 属性を使用して古いバージョンのコントラクト名を保持しない限り、列挙体メンバーの名前の変更は互換性に影響します。 詳細については、次を参照してください。[データ コントラクトの列挙型](../../../../docs/framework/wcf/feature-details/enumeration-types-in-data-contracts.md)です。  
  
## <a name="collections"></a>コレクション  
 コレクション型の大半はデータ コントラクト モデル内で交換可能であるため、多くの場合、コレクションの変更は互換性に影響しません。 ただし、カスタマイズされていないコレクションからカスタマイズされたコレクションへの変更またはその逆の変更は、互換性に影響する変更です。 また、コレクションのカスタマイズ設定の変更 (データ コントラクトの名前と名前空間の変更、要素名、キー要素名、および値要素名の反復) も互換性に影響します。 コレクションのカスタマイズの詳細については、次を参照してください。[データ コントラクトのコレクション型](../../../../docs/framework/wcf/feature-details/collection-types-in-data-contracts.md)です。  
また、コレクションの内容のデータ コントラクトの変更 (整数のリストから文字列のリストへの変更など) は互換性に影響する変更です。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Runtime.Serialization.DataMemberAttribute.Name%2A>  
 <xref:System.Runtime.Serialization.DataMemberAttribute>  
 <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A>  
 <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>  
 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A>  
 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A>  
 <xref:System.Runtime.Serialization.SerializationException>  
 <xref:System.Runtime.Serialization.IExtensibleDataObject>  
 [バージョン トレラントなシリアル化コールバック](../../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md)  
 [ベスト プラクティス: データ コントラクトのバージョン管理](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md)  
 [データ コントラクトの使用](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)  
 [データ コントラクトの等価性](../../../../docs/framework/wcf/feature-details/data-contract-equivalence.md)  
 [上位互換性のあるデータ コントラクト](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)
